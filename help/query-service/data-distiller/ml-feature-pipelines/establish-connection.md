---
title: Conexión a Data Distiller desde un Jupyter Notebook
description: Aprenda a conectarse a Data Distiller desde un Jupyter Notebook.
exl-id: e6238b00-aaeb-40c0-a90f-9aebb1a1c421
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Conexión a Data Distiller desde un Jupyter Notebook

Para enriquecer las canalizaciones de aprendizaje automático con datos de experiencia del cliente de alto valor, primero debe conectarse a Data Distiller desde [!DNL Jupyter Notebooks]. Este documento describe los pasos para conectarse a Data Distiller desde un bloc de notas de [!DNL Python] en su entorno de aprendizaje automático.

## Introducción

En esta guía se da por hecho que está familiarizado con los blocs de notas [!DNL Python] interactivos y tiene acceso a un entorno de bloc de notas. El bloc de notas puede alojarse en un entorno de aprendizaje automático basado en la nube o localmente con [[!DNL Jupyter Notebook]](https://jupyter.org/).

### Obtener credenciales de conexión {#obtain-credentials}

Para conectarse a Data Distiller y otros servicios de Adobe Experience Platform, necesita una credencial de la API de Experience Platform. Alguien con acceso de desarrollador en Experience Platform puede crear las credenciales de la API en [Adobe Developer Console](https://developer.adobe.com/console/home). Se recomienda crear una credencial de la API Oauth2 específicamente para flujos de trabajo de ciencia de datos y hacer que un administrador del sistema de Adobe de su organización asigne la credencial a una función con los permisos adecuados.

Consulte [Autenticar y acceder a las API de Experience Platform](../../../landing/api-authentication.md) para obtener instrucciones detalladas sobre cómo crear una credencial de API y obtener los permisos necesarios.

Los permisos recomendados para la ciencia de datos incluyen:

- Zonas protegidas que se utilizarán para la ciencia de datos (normalmente `prod`)
- Modelado de datos: [!UICONTROL Administrar esquemas]
- Administración de datos: [!UICONTROL Administrar conjuntos de datos]
- Ingesta de datos: [!UICONTROL Ver orígenes]
- Destinos: [!UICONTROL Administrar y activar destinos de conjuntos de datos]
- Servicio de consultas: [!UICONTROL Administrar consultas]

De forma predeterminada, una función (y las credenciales de la API asignadas a esa función) no pueden acceder a los datos etiquetados. Sujeto a las políticas de gobernanza de datos de la organización, un administrador del sistema puede otorgar a la función acceso a ciertos datos etiquetados que se consideren adecuados para el uso de la ciencia de datos. Los clientes de Experience Platform son responsables de administrar correctamente el acceso a las etiquetas y las políticas para cumplir con las regulaciones y políticas organizativas relevantes.

### Almacenar credenciales en un archivo de configuración independiente {#store-credentials}

Para mantener las credenciales seguras, se recomienda evitar escribir información de credenciales directamente en el código. En su lugar, mantenga la información de las credenciales en un archivo de configuración independiente y lea los valores necesarios para conectarse a Experience Platform y a Data Distiller.

Por ejemplo, puede crear un archivo llamado `config.ini` e incluir la siguiente información (junto con cualquier otra información, como los ID de conjuntos de datos, que sería útil guardar entre sesiones):

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

En el bloc de notas, puede leer la información de credenciales en la memoria mediante el paquete `configParser` de la biblioteca estándar [!DNL Python]:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

A continuación, puede hacer referencia a los valores de credencial dentro del código de la siguiente manera:

```python
org_id = config.get('Credential', 'ims_org_id')
```

## Instalación de la biblioteca de App Python {#install-python-library}

[aepp](https://github.com/adobe/aepp/tree/main) es una biblioteca de código abierto [!DNL Python] administrada por Adobe que proporciona funciones para conectarse a Data Distiller y enviar consultas, como realizar solicitudes a otros servicios de Experience Platform. A su vez, la biblioteca `aepp` se basa en el paquete del adaptador de base de datos PostgreSQL `psycopg2` para consultas interactivas de Data Distiller. Es posible conectarse a Data Distiller y consultar los conjuntos de datos de Experience Platform solo con `psycopg2`, pero `aepp` proporciona una mayor comodidad y funcionalidad adicional para realizar solicitudes a todos los servicios de API de Experience Platform.

Para instalar o actualizar `aepp` y `psycopg2` en su entorno, puede usar el comando mágico `%pip` en su bloc de notas:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

A continuación, puede configurar la biblioteca `aepp` con sus credenciales mediante el siguiente código:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## Creación de una conexión con Data Distiller {#create-connection}

Una vez que `aepp` se haya configurado con sus credenciales, puede usar el siguiente código para crear una conexión con Data Distiller e iniciar una sesión interactiva de la siguiente manera:

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

A continuación, puede consultar los conjuntos de datos en la zona protegida de Experience Platform. Dado el ID de un conjunto de datos que desea consultar, puede recuperar el nombre de tabla correspondiente del servicio de catálogo y ejecutar consultas en la tabla:

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Conéctese a un único conjunto de datos para obtener un rendimiento de consulta más rápido {#connect-to-single-dataset}

De forma predeterminada, la conexión de Data Distiller se conecta a todos los conjuntos de datos de la zona protegida. Para consultas más rápidas y un uso de recursos reducido, puede conectarse a un conjunto de datos específico de interés. Para ello, cambie `dbname` en el objeto de conexión de Data Distiller a `{sandbox}:{table_name}`:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Pasos siguientes

Al leer este documento, ha aprendido a conectarse a Data Distiller desde un bloc de notas de [!DNL Python] en su entorno de aprendizaje automático. El siguiente paso para crear canalizaciones de características de Experience Platform para alimentar modelos personalizados en su entorno de aprendizaje automático es [explorar y analizar sus conjuntos de datos](./exploratory-analysis.md).
