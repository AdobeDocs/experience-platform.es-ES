---
title: Coincidencia aproximada en el servicio de consultas
description: Aprenda a hacer una coincidencia en los datos de Experience Platform que combina los resultados de varios conjuntos de datos haciendo coincidir aproximadamente una cadena de su elección.
exl-id: ec1e2dda-9b80-44a4-9fd5-863c45bc74a7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Coincidencia aproximada en el servicio de consultas

Utilice una coincidencia &quot;difusa&quot; en los datos de Adobe Experience Platform para devolver las coincidencias aproximadas más probables sin necesidad de buscar cadenas con caracteres idénticos. Esto permite una búsqueda de datos mucho más flexible y hace que sus datos sean más accesibles al ahorrar tiempo y esfuerzo.

En lugar de intentar reformatear las cadenas de búsqueda para que coincidan, la coincidencia aproximada analiza la proporción de similitud entre dos secuencias y devuelve el porcentaje de similitud. [[!DNL FuzzyWuzzy]](https://pypi.org/project/fuzzywuzzy/) se recomienda para este proceso ya que sus funciones son más adecuadas para ayudar a hacer coincidir cadenas en situaciones más complejas en comparación con [!DNL regex] o [!DNL difflib].

El ejemplo proporcionado en este caso de uso se centra en la coincidencia de atributos similares de una búsqueda de habitación de hotel en dos conjuntos de datos de agencias de viajes diferentes. El documento muestra cómo hacer coincidir cadenas por su grado de similitud con grandes fuentes de datos independientes. En este ejemplo, la coincidencia aproximada compara los resultados de búsqueda de las características de una habitación de las agencias de viajes Luma y Acme.

## Introducción {#getting-started}

Como parte de este proceso requiere que forme un modelo de aprendizaje automático, en este documento se da por hecho que tiene conocimientos prácticos de uno o más entornos de aprendizaje automático.

Este ejemplo utiliza [!DNL Python] y el entorno de desarrollo [!DNL Jupyter Notebook]. Aunque hay muchas opciones disponibles, se recomienda [!DNL Jupyter Notebook] porque es una aplicación web de código abierto con requisitos de cálculo bajos. Se puede descargar desde [el sitio oficial de Jupyter](https://jupyter.org/).

Antes de empezar, debe importar las bibliotecas necesarias. [!DNL FuzzyWuzzy] es una biblioteca [!DNL Python] de código abierto creada sobre la biblioteca [!DNL difflib] y que se usa para hacer coincidir cadenas. Utiliza [!DNL Levenshtein Distance] para calcular las diferencias entre secuencias y patrones. [!DNL FuzzyWuzzy] tiene los siguientes requisitos:

- [!DNL Python] 2.4 (o superior)
- [!DNL Python-Levenshtein]

Desde la línea de comandos, use el siguiente comando para instalar [!DNL FuzzyWuzzy]:

```console
pip install fuzzywuzzy
```

O use el siguiente comando para instalar también [!DNL Python-Levenshtein]:

```console
pip install fuzzywuzzy[speedup]
```

Encontrará más información técnica sobre [!DNL Fuzzywuzzy] en su [documentación oficial](https://pypi.org/project/fuzzywuzzy/).

### Conectar con el servicio de consultas

Debe conectar el modelo de aprendizaje automático al servicio de consultas proporcionando sus credenciales de conexión. Se pueden proporcionar credenciales que caduquen y que no caduquen. Consulte la [guía de credenciales](../ui/credentials.md) para obtener más información sobre cómo adquirir las credenciales necesarias. Si usa [!DNL Jupyter Notebook], lea la guía completa sobre [cómo conectarse al servicio de consultas](../clients/jupyter-notebook.md).

Además, asegúrese de importar el paquete [!DNL numpy] en su entorno [!DNL Python] para habilitar el álgebra lineal.

```python
import numpy as np
```

Los comandos siguientes son necesarios para conectarse al servicio de consultas desde [!DNL Jupyter Notebook]:

```python
import psycopg2
conn = psycopg2.connect('''
sslmode=require
host=<YOUR_ORGANIZATION_ID>
port=80
dbname=prod:all
user=<YOUR_ADOBE_ID_TO_CONNECT_TO_QUERY_SERVICE>
password=<YOUR_QUERY_SERVICE_PASSWORD>
''')
cur = conn.cursor()
```

Su instancia de [!DNL Jupyter Notebook] ahora está conectada al servicio de consultas. Si la conexión se realiza correctamente, no aparecerá ningún mensaje. Si la conexión falla, se mostrará un error.

### Extraer datos del conjunto de datos de Luma {#luma-dataset}

Los datos para el análisis se extraen del primer conjunto de datos con los siguientes comandos. Para ser breves, los ejemplos se han limitado a los 10 primeros resultados de la columna.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Seleccione **Output** para mostrar la matriz devuelta.

+++Output

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Extraer datos del conjunto de datos de Acme {#acme-dataset}

Los datos para el análisis ahora se extraen del segundo conjunto de datos con los siguientes comandos. De nuevo, para ser breves, los ejemplos se han limitado a los 10 primeros resultados de la columna.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Seleccione **Output** para mostrar la matriz devuelta.

+++Output

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Crear una función de puntuación parcial {#fuzzy-scoring}

A continuación, debe importar `fuzz` de la biblioteca FuzzyWuzzy y ejecutar una comparación de proporción parcial de las cadenas. La función de proporción parcial permite realizar la coincidencia de subcadenas. Toma la cadena más corta y la hace coincidir con todas las subcadenas que tienen la misma longitud. La función devuelve un porcentaje de similitud de hasta el 100 %. Por ejemplo, la función de proporción parcial compararía las siguientes cadenas &quot;Habitación de lujo&quot;, &quot;1 cama King&quot; y &quot;Habitación King Deluxe&quot;, y devolvería una puntuación de similitud del 69 %.

En el caso de uso de coincidencia de habitación de hotel, esto se realiza mediante los siguientes comandos:

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

A continuación, importe `cdist` desde la biblioteca [!DNL SciPy] para calcular la distancia entre cada par en las dos colecciones de entradas. Esto calcula las puntuaciones entre todos los pares de habitaciones de hotel proporcionados por cada una de las agencias de viajes.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Cree asignaciones entre las dos columnas mediante la puntuación de combinación aproximada

Ahora que las columnas se han clasificado según la distancia, puede indexar los pares y conservar solo las coincidencias que tengan una puntuación mayor que un determinado porcentaje. En este ejemplo sólo se conservan los pares que coincidan con una puntuación del 70% o superior.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

Los resultados se pueden mostrar con el siguiente comando. Para que sea más breve, los resultados están limitados a diez filas.

```python
matched_pairs[:10]
```

Seleccione **Output** para ver los resultados.

+++Output

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio')]
```

+++

Los resultados se comparan utilizando SQL con el siguiente comando:

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## Aplicar las asignaciones para realizar una unión aproximada en el servicio de consultas {#mappings-for-query-service}

A continuación, los pares coincidentes de alta puntuación se unen mediante SQL para crear un nuevo conjunto de datos.

```python
:
cur.execute('''
SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{}
'''.format(matching_sql)) 
[r for r in cur]
```

Seleccione **Output** para ver los resultados de esta unión.

+++Output

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio'),
 ('Deluxe Suite', 'Deluxe Suite'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Business King Room'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds',
  'Business Double Room With Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Deluxe Double Room'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Deluxe Suite, 1 Bedroom', 'Deluxe Suite'),
 ('City Room, City View', 'Room With City View'),
 ('City Room, City View', 'Queen Room With City View'),
 ('City Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Club Room, Premium 2 Queen Beds', 'Club Premium Two Queen'),
 ('Club Room, Premium 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, Lake View', 'Deluxe King Or Queen Room with Lake View'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('Deluxe Suite, 1 King Bed, Non Smoking, Kitchen', 'Deluxe Suite'),
 ('Junior Suite, 1 King Bed, Accessible (Roll-in Shower)', 'Junior Suite'),
 ('Regency Club, Mountain View', 'Regency Club Ocean View'),
 ('Regency Club, Mountain View', 'Regency Club Mountain View'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Room, Partial Ocean View', 'Room With Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View With Two Double Beds'),
 ('Room, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, Partial Ocean View', 'Waikiki Tower Partial Ocean View'),
 ('Premium Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Grand Corner King Room, 1 King Bed', 'Grand Corner King Room'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, 1 King Bed, Non Smoking', 'Deluxe Room - One King Bed'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Accessible Partial Ocean View With Two Double Beds'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Partial Ocean View Room'),
 ('Room, Ocean View ', 'Room With Ocean View'),
 ('Room, Ocean View ', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View ', 'Standard Room With Ocean View'),
 ('Signature Suite, 1 Bedroom', 'Signature King'),
 ('Room, 2 Queen Beds (Waikiki View)',
  'Queen Room With Two Queen Beds and Waikiki View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean View'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean Front View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('High-Floor Premium Room, 1 King Bed', 'High-Floor Premium King Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Junior Suite'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Deluxe King Suite With Sofa Bed'),
 ('Deluxe Room, City View', 'Queen Room With City View'),
 ('Deluxe Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, 1 Queen Bed, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Room, Ocean View', 'Room With Ocean View'),
 ('Room, Ocean View', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Partial Ocean View Room'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Standard Room, Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Regency Club, Ocean View',
  'Accessible Club Ocean View Suite With One King Bed'),
 ('Regency Club, Ocean View', 'Regency Club Ocean View'),
 ('Regency Club, Ocean View', 'Regency Club Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Ocean View'),
 ('Room, 1 Queen Bed', 'Deluxe Room - Two Queen Beds'),
 ('Double Room', 'Luxury Double Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Queen Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Business Double Room With Two Double Beds'),
 ('Double Room', 'Deluxe Double Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Twin Room', 'High-Floor Premium King Room'),
 ('Premier Twin Room', 'Premier King Room'),
 ('Premier Twin Room', 'Premier Queen Room With Two Queen Beds'),
 ('Premier Twin Room', 'Premium King Room With Free Wi-Fi'),
 ('Premium Room, 1 Queen Bed', 'Premium Two Queen'),
 ('Premium Room, 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, 1 Queen Bed (High Floor)', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, Garden View',
  'Queen Room With Two Queen Beds and Garden View'),
 ('Signature Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Signature Room, 2 Queen Beds', 'Signature Two Queen'),
 ('Standard Room, Ocean View', 'Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean Front View')]
```

+++

### Guardar resultados de coincidencias aproximadas en Experience Platform {#save-to-platform}

Por último, los resultados de la coincidencia aproximada se pueden guardar como un conjunto de datos para su uso en Adobe Experience Platform mediante SQL.

```python
cur.execute(''' 
Create table luma_acme_join
AS
(SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{})
'''.format(matching_sql))
```
