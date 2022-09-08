---
title: Conectar el bloc de notas de Jupyter al servicio de consultas
description: Aprenda a conectar Jupyter Notebook con el servicio de consulta de Adobe Experience Platform.
source-git-commit: f910deca43ac49d3a3452b8dbafda20ffdf3bf48
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Connect [!DNL Jupyter Notebook] al servicio de consultas

Este documento cubre los pasos necesarios para conectar [!DNL Jupyter Notebook] con el servicio de consulta de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere que ya tenga acceso a [!DNL Jupyter Notebook] y están familiarizados con su interfaz. Para descargar [!DNL Jupyter Notebook] o para obtener más información, consulte la [oficial [!DNL Jupyter Notebook] documentación](https://jupyter.org/).

Para adquirir las credenciales necesarias para la conexión [!DNL Jupyter Notebook] al Experience Platform, debe tener acceso al [!UICONTROL Consultas] en la interfaz de usuario de Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso al [!UICONTROL Consultas] espacio de trabajo.

>[!TIP]
>
>[!DNL Anaconda Navigator] es una interfaz gráfica de usuario (GUI) de escritorio que proporciona una manera más fácil de instalar e iniciar [!DNL Python] programas como [!DNL Jupyter Notebook]. También ayuda a administrar paquetes, entornos y canales sin utilizar comandos de línea de comandos.
>Puede [instalar la versión preferida de la aplicación](https://docs.anaconda.com/anaconda/install/) de su sitio web.
>Siga el proceso de instalación guiada. En la pantalla de inicio del Navegador de Anaconda, seleccione **[!DNL Jupyter Notebook]** de la lista de aplicaciones compatibles para iniciar el programa.
>![La variable [!DNL Anaconda Navigator] pantalla de inicio con [!DNL Jupyter Notebook] resaltado.](../images/clients/jupyter-notebook/anaconda-navigator-home.png)
>Puede encontrar más información en su [documentación oficial](https://docs.anaconda.com/anaconda/navigator/).

## Launch [!DNL Jupyter Notebook]

Una vez que haya abierto una nueva [!DNL Jupyter Notebook] aplicación web, seleccione **[!DNL New]** desplegable seguido de **[!DNL Python 3]** para crear un nuevo bloc de notas. La variable [!DNL Notebook] aparece como editor.

![La variable [!DNL Jupiter Notebook] Ficha Archivo con el [!DNL New dropdown] y [!DNL Python] 3 resaltados.](../images/clients/jupyter-notebook/new-notebook.png)

En la primera línea del [!DNL Notebook] , introduzca el siguiente valor: `pip install psycopg2-binary` y seleccione **[!DNL Run]** en la barra de comandos. Aparece un mensaje de éxito debajo de la línea de entrada.

>[!IMPORTANT]
>
>Como parte de este proceso para formar una conexión, debe seleccionar **[!DNL Run]** para ejecutar cada línea de código.

![La variable [!DNL Notebook] IU con el comando de bibliotecas de instalación resaltado.](../images/clients/jupyter-notebook/install-library.png)

A continuación, importe un [!DNL PostgreSQL] adaptador de base de datos para [!DNL Python]. Introduzca el valor: `import psycopg2`y seleccione **[!DNL Run]**. No hay ningún mensaje de éxito para este proceso. Si no hay ningún mensaje de error, continúe con el siguiente paso.

![La variable [!DNL Notebook] IU con el código de controlador de la base de datos de importación resaltado.](../images/clients/jupyter-notebook/import-dbdriver.png)

Ahora debe proporcionar sus credenciales de Adobe Experience Platform introduciendo el valor : `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Las credenciales de conexión se pueden encontrar en la sección [!UICONTROL Consultas] en la sección [!UICONTROL Credenciales] de la interfaz de usuario de Platform. Consulte la documentación sobre cómo [buscar las credenciales de la organización](../ui/credentials.md) para obtener instrucciones detalladas.

Se recomienda el uso de credenciales que no caduquen cuando se utilicen clientes de terceros para ahorrar el esfuerzo de introducir los detalles repetidamente. Consulte la documentación para obtener instrucciones sobre [cómo generar y utilizar credenciales que no caduquen](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Al copiar credenciales de la interfaz de usuario de Platform, asegúrese de que no haya ningún formato adicional para las credenciales. Todas deben estar en una línea, con un solo espacio entre las propiedades y los valores. Las credenciales están entre comillas y **not** separados por comas.

![La variable [!DNL Notebook] IU con las credenciales de conexión resaltadas.](../images/clients/jupyter-notebook/provide-credentials.png)

Su [!DNL Jupyter Notebook] La instancia de ahora está conectada al servicio de consulta.

## Ejemplo de ejecución de consultas

Ahora que se ha conectado [!DNL Jupyter Notebook] al servicio de consulta, puede realizar consultas en sus conjuntos de datos mediante el uso de su [!DNL Notebook] entradas. El siguiente ejemplo utiliza una consulta simple para demostrar el proceso.

Introduzca los siguientes valores:

```console
cur = conn.cursor()
cur.execute('''{YOUR_QUERY_HERE}''')
data = [r for r in cur]
```

A continuación, llame al parámetro (`data` en el ejemplo anterior) para mostrar los resultados de la consulta en una respuesta sin formato.

![La variable [!DNL Notebook] IU con comandos para devolver y mostrar resultados SQL en el bloc de notas.](../images/clients/jupyter-notebook/example-query.png)

Para dar formato a los resultados de una forma más legible, utilice los siguientes comandos:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`

Estos comandos no generan un mensaje de éxito. Si no hay ningún mensaje de error, puede utilizar una función para obtener los resultados de la consulta SQL en formato de tabla.

![Los comandos necesarios para dar formato a los resultados SQL.](../images/clients/jupyter-notebook/format-results-commands.png)

Introduzca y ejecute el `df.head()` para ver los resultados de la consulta tabularizada.

![Resultados tabularizados de la consulta SQL en [!DNL Jupyter Notebook].](../images/clients/jupyter-notebook/format-results-output.png)

## Pasos siguientes

Ahora que se ha conectado con el servicio de consulta, puede utilizar [!DNL Jupyter Notebook] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de consultas en ejecución](../best-practices/writing-queries.md).
