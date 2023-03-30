---
title: Coincidencia aproximada en el servicio de consulta
description: Obtenga información sobre cómo realizar una coincidencia en los datos de Platform que combina resultados de varios conjuntos de datos al hacer coincidir aproximadamente una cadena de su elección.
source-git-commit: a3a4ca4179610348eba73cf1239861265d2bf887
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 0%

---

# Coincidencia borrosa

Utilice una coincidencia &quot;difusa&quot; en los datos de Platform para devolver las coincidencias más probables y aproximadas sin necesidad de buscar cadenas con caracteres idénticos. Esto permite una búsqueda mucho más flexible de los datos y hace que sean más accesibles ahorrando tiempo y esfuerzo.

En lugar de intentar cambiar el formato de las cadenas de búsqueda para que coincidan, la coincidencia difusa analiza la proporción de similitud entre dos secuencias y devuelve el porcentaje de similitud. [!DNL FuzzyWuzzy] se recomienda para este proceso, ya que sus funciones son más adecuadas para ayudar a hacer coincidir cadenas en situaciones más complejas en comparación con [!DNL regex] o [!DNL difflib].

El ejemplo proporcionado en este caso de uso se centra en la coincidencia de atributos similares de una búsqueda de habitaciones de hotel en dos conjuntos de datos de agencias de viajes diferentes. El documento muestra cómo hacer coincidir cadenas por su grado de similitud con fuentes de datos independientes de gran tamaño. En este ejemplo, la coincidencia difusa compara los resultados de búsqueda para las características de una habitación de las agencias de viajes Luma y Acme.

## Primeros pasos {#getting-started}

Como parte de este proceso requiere que imparta un modelo de aprendizaje automático, este documento asume un conocimiento práctico de uno o más entornos de aprendizaje automático.

Este ejemplo utiliza [!DNL Python] y [!DNL Jupyter Notebook] entorno de desarrollo. Aunque hay muchas opciones disponibles, [!DNL Jupyter Notebook] se recomienda porque es una aplicación web de código abierto que tiene bajos requisitos de cálculo. Puede [descargado del sitio oficial de Jupyter](https://jupyter.org/).

Antes de comenzar, debe importar las bibliotecas necesarias. [!DNL FuzzyWuzzy] es de código abierto [!DNL Python] biblioteca creada sobre [!DNL difflib] biblioteca y se usa para buscar coincidencias con cadenas. Utiliza [!DNL Levenshtein Distance] para calcular las diferencias entre secuencias y patrones. [!DNL FuzzyWuzzy] tiene los siguientes requisitos:

- [!DNL Python] 2.4 (o superior)
- [!DNL Python-Levenshtein]

Desde la línea de comandos, utilice el siguiente comando para instalar [!DNL FuzzyWuzzy]:

```console
pip install fuzzywuzzy
```

O utilice el siguiente comando para instalar [!DNL Python-Levenshtein] también:

```console
pip install fuzzywuzzy[speedup]
```

Más información técnica sobre [!DNL Fuzzywuzzy] se puede encontrar en su [documentación oficial](https://pypi.org/project/fuzzywuzzy/).

### Conectar con el servicio de consulta

Debe conectar el modelo de aprendizaje automático con el servicio de consulta proporcionando las credenciales de conexión. Se pueden proporcionar credenciales que caducan y que no caducan. Consulte la [guía de credenciales](../ui/credentials.md) para obtener más información sobre cómo adquirir las credenciales necesarias. Si está utilizando [!DNL Jupyter Notebook], consulte la guía completa de [cómo conectarse al servicio de consulta](../clients/jupyter-notebook.md).

Además, asegúrese de importar la variable [!DNL numpy] paquete en su [!DNL Python] para habilitar álgebra lineal.

```python
import numpy as np
```

Los siguientes comandos son necesarios para conectarse al servicio de consulta desde [!DNL Jupyter Notebook]:

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

Su [!DNL Jupyter Notebook] La instancia de ahora está conectada al servicio de consulta. Si la conexión se realiza correctamente, no aparecerá ningún mensaje. Si la conexión falla, se mostrará un error.

### Dibujar datos desde el conjunto de datos de Luma {#luma-dataset}

Los datos para el análisis se extraen del primer conjunto de datos con los siguientes comandos. Para abreviar, los ejemplos se han limitado a los primeros 10 resultados de la columna .

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Select **Salida** para mostrar la matriz devuelta.

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

### Dibujar datos desde el conjunto de datos Acme {#acme-dataset}

Los datos para el análisis ahora se extraen del segundo conjunto de datos con los siguientes comandos. Una vez más, los ejemplos se han limitado a los 10 primeros resultados de la columna, con carácter abreviado.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Select **Salida** para mostrar la matriz devuelta.

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

### Crear una función de puntuación difusa {#fuzzy-scoring}

A continuación, debe importar `fuzz` de la biblioteca FuzzyWuzzy y ejecute una comparación de proporción parcial de las cadenas. La función de relación parcial permite realizar correspondencias de subcadenas. Toma la cadena más corta y la hace coincidir con todas las subcadenas de la misma longitud. La función devuelve una proporción de similitud de porcentaje de hasta el 100%. Por ejemplo, la función de relación parcial compararía las siguientes cadenas: &quot;Habitación Deluxe&quot;, &quot;1 cama King&quot; y &quot;Habitación Deluxe King&quot; y devolvería una puntuación de similitud del 69%.

En el caso de uso de coincidencia en la sala del hotel, esto se realiza utilizando los siguientes comandos:

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

A continuación, importe `cdist` de la variable [!DNL SciPy] biblioteca para calcular la distancia entre cada par en las dos colecciones de entradas. Esto calcula la puntuación entre todas las parejas de habitaciones de hotel proporcionadas por cada una de las agencias de viajes.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Crear asignaciones entre las dos columnas utilizando la puntuación de unión confusa

Ahora que las columnas se han clasificado en función de la distancia, puede indexar los pares y conservar solo las coincidencias que tengan una puntuación superior a un determinado porcentaje. Este ejemplo solo conserva pares que coinciden con una puntuación del 70 % o superior.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

Los resultados se pueden mostrar con el siguiente comando. Para la brevedad, los resultados están limitados a diez filas.

```python
matched_pairs[:10]
```

Select **Salida** para ver los resultados.

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

## Aplique las asignaciones para realizar una unión confusa en el servicio de consulta {#mappings-for-query-service}

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

Select **Salida** para ver los resultados de esta unión.

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

### Guardar resultados de coincidencia confusos en Platform {#save-to-platform}

Finalmente, los resultados de la coincidencia difusa se pueden guardar como un conjunto de datos para usar en Adobe Experience Platform mediante SQL.

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


