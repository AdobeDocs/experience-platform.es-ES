---
title: Conexión de Jupyter Notebook al servicio de consultas
description: Aprenda a conectar Jupyter Notebook con el servicio de consultas de Adobe Experience Platform.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# Conectar [!DNL Jupyter Notebook] al servicio de consultas

Este documento describe los pasos necesarios para conectar [!DNL Jupyter Notebook] con Adobe Experience Platform Query Service.

## Introducción

Esta guía requiere que ya tenga acceso a [!DNL Jupyter Notebook] y que esté familiarizado con su interfaz. Para descargar [!DNL Jupyter Notebook] o más información, consulte la [documentación oficial [!DNL Jupyter Notebook] 3&rbrace;.](https://jupyter.org/)

Para adquirir las credenciales necesarias para conectar [!DNL Jupyter Notebook] a Experience Platform, debe tener acceso al área de trabajo [!UICONTROL Consultas] en la interfaz de usuario de Experience Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso al área de trabajo [!UICONTROL Consultas].

>[!TIP]
>
>[!DNL Anaconda Navigator] es una interfaz gráfica de usuario (GUI) de escritorio que proporciona una forma más sencilla de instalar e iniciar programas comunes de [!DNL Python] como [!DNL Jupyter Notebook]. También ayuda a administrar paquetes, entornos y canales sin utilizar comandos de la línea de comandos.
>Siga el proceso de instalación guiada en su sitio web para [instalar su versión preferida de la aplicación](https://docs.anaconda.com/anaconda/install/).
>En la pantalla de inicio de Anaconda Navigator, seleccione **[!DNL Jupyter Notebook]** de la lista de aplicaciones compatibles para iniciar el programa.
>Encontrará más información en la [documentación oficial de Anaconda](https://docs.anaconda.com/anaconda/navigator/).

La documentación oficial de Jupyter proporciona instrucciones para [ejecutar el bloc de notas desde la interfaz de línea de comandos](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

Después de abrir una nueva aplicación web [!DNL Jupyter Notebook], seleccione el menú desplegable **[!DNL New]** de la interfaz de usuario, seguido de **[!DNL Python 3]** para crear un nuevo bloc de notas. Aparece el editor [!DNL Notebook].

En la primera línea del editor [!DNL Notebook], escriba el siguiente valor: `pip install psycopg2-binary` y seleccione **[!DNL Run]** en la barra de comandos. Aparece un mensaje de éxito debajo de la línea de entrada.

>[!IMPORTANT]
>
>Como parte de este proceso para formar una conexión, debe seleccionar **[!DNL Run]** para ejecutar cada línea de código.

A continuación, importe un adaptador de base de datos [!DNL PostgreSQL] para [!DNL Python]. Introduzca el valor: `import psycopg2` y seleccione **[!DNL Run]**. No hay ningún mensaje de éxito para este proceso. Si no hay ningún mensaje de error, continúe con el paso siguiente.

Ahora debe proporcionar sus credenciales de Adobe Experience Platform al escribir el valor: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Sus credenciales de conexión se encuentran en la sección [!UICONTROL Consultas], en la ficha [!UICONTROL Credenciales] de la interfaz de usuario de Experience Platform. Consulte la documentación sobre cómo [encontrar las credenciales de su organización](../ui/credentials.md) para obtener instrucciones detalladas.

Se recomienda el uso de credenciales que no caducan al utilizar clientes de terceros para ahorrar el esfuerzo de escribir repetidamente sus detalles. Consulte la documentación para obtener instrucciones sobre [cómo generar y utilizar credenciales que no caduquen](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Al copiar credenciales desde la interfaz de usuario de Experience Platform, no es necesario aplicar un formato adicional a las credenciales. Se pueden indicar en una línea, con un solo espacio entre las propiedades y los valores. Las credenciales están entre comillas y **no** separadas por comas.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Su instancia de [!DNL Jupyter Notebook] ahora está conectada al servicio de consultas.

## Ejemplo de ejecución de consultas

Ahora que ha conectado [!DNL Jupyter Notebook] al servicio de consultas, puede realizar consultas en los conjuntos de datos usando las entradas de [!DNL Notebook]. El siguiente ejemplo utiliza una consulta simple para mostrar el proceso.

Introduzca los siguientes valores:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

A continuación, llame al parámetro (`data` en el ejemplo anterior) para mostrar los resultados de la consulta en una respuesta sin formato.

Para dar un formato más legible a los resultados en lenguaje natural, utilice los siguientes comandos:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Estos comandos no generan un mensaje de éxito. Si no hay ningún mensaje de error, puede utilizar una función para generar los resultados de la consulta SQL en formato de tabla.

Escriba y ejecute la función `df.head()` para ver los resultados de la consulta tabularizada.

## Pasos siguientes

Ahora que se ha conectado con el servicio de consultas, puede usar [!DNL Jupyter Notebook] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de ejecución de consultas](../best-practices/writing-queries.md).
