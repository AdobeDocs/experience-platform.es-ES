---
title: Administrar datos de plataforma mediante Python y SQLAlchemy
description: Aprenda a utilizar SQLAlchemy para administrar los datos de la plataforma mediante Python en lugar de SQL.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Administrar datos de Platform mediante [!DNL Python] y [!DNL SQLAlchemy]

Aprenda a utilizar SQLAlchemy para una buena flexibilidad en la administración de los datos de Adobe Experience Platform. Para aquellos que no están tan familiarizados con SQL, SQLAlchemy puede mejorar en gran medida el tiempo de desarrollo al trabajar con bases de datos relacionales. Este documento proporciona instrucciones y ejemplos para conectarse [!DNL SQLAlchemy] Haga clic en Servicio de consultas y empiece a utilizar Python para interactuar con sus bases de datos.

[!DNL SQLAlchemy] es un asignador relacional de objetos (ORM) y un [!DNL Python] biblioteca de códigos que puede transferir datos almacenados en una base de datos SQL a [!DNL Python] objetos. A continuación, puede realizar operaciones de CRUD en los datos almacenados dentro del lago de datos de Platform mediante [!DNL Python] código. Esto elimina la necesidad de administrar datos usando solo PSQL.

## Primeros pasos

Para adquirir las credenciales necesarias para la conexión [!DNL SQLAlchemy] Para acceder al Experience Platform, debe tener acceso al espacio de trabajo Consultas en la interfaz de usuario de Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso al área de trabajo Consultas.

## [!DNL Query Service] credenciales {#credentials}

Para encontrar sus credenciales, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde el panel de navegación izquierdo, seguido de **[!UICONTROL Credenciales]**. Para obtener instrucciones completas sobre cómo encontrar sus credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md).

![Se resaltó la pestaña Credencial con las credenciales que caducan para el servicio de consultas.](../images/use-cases/credentials.png)

Aunque el puerto 80 es el puerto recomendado para una conexión al servicio de consultas, también puede utilizar el puerto 5432.

>[!IMPORTANT]
>
>Si utiliza credenciales que caducan (como se ve en la imagen anterior) para conectarse al servicio de consultas, la duración de la sesión de la conexión caducará después del período de tiempo establecido definido en la configuración de la organización. De forma predeterminada, este periodo es de 24 horas. Consulte la documentación para obtener información sobre cómo [conectar un cliente con credenciales que no caduquen](../ui/credentials.md#non-expiring-credentials), o cómo [cambiar la duración de la sesión de las credenciales que caducan](../ui/credentials.md#expiring-credentials).

Una vez que tenga acceso a sus credenciales de QS, abra su [!DNL Python] editor de su elección.

### Almacenar credenciales en [!DNL Python] {#store-credentials}

En su [!DNL Python] editor, importe `urllib.parse.quote` y guarde cada variable de credencial como un parámetro. El `urllib.parse` El módulo proporciona una interfaz estándar para desglosar cadenas de URL en componentes. La función quote reemplaza los caracteres especiales de la cadena URL para que los datos sean seguros para su uso como componentes URL. A continuación se muestra un ejemplo del código requerido:

>[!TIP]
>
>Uso [!DNL Python]Comillas triples para introducir la cadena de contraseña de varias líneas.

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>La contraseña que proporcione para conectarse [!DNL SQLAlchemy] El Experience Platform de a caducará si usa credenciales que caducan. Consulte la [sección credenciales](#credentials) para obtener más información.

### Creación de una instancia de motor [#create-engine]

Una vez creadas las variables, importe `create_engine` y cree una cadena para compilar y dar formato a las credenciales del servicio de consultas en SQLAlchemy. El `create_engine` a continuación, se utiliza la función para construir una instancia de motor.

>[!NOTE]
>
>`create_engine`devuelve una instancia de un motor. Sin embargo, no abre la conexión al Servicio de consultas hasta que se llama a una consulta que requiere una conexión.

SSL debe estar habilitado al acceder a Platform mediante clientes de terceros. Como parte del motor, utilice el `connect_args` para introducir argumentos de palabra clave adicionales. Se recomienda establecer el modo SSL en `require`. Consulte la [Documentación de modos SSL](../clients/ssl-modes.md) para obtener más información sobre los valores aceptados.

El ejemplo siguiente muestra el [!DNL Python] código necesario para inicializar un motor y una cadena de conexión.

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>La contraseña que proporcione para conectarse [!DNL SQLAlchemy] El Experience Platform de a caducará si usa credenciales que caducan. Consulte la [sección credenciales](#credentials) para obtener más información.

Ya está listo para consultar los datos de Platform mediante [!DNL Python]. El ejemplo que se muestra a continuación devuelve una matriz de nombres de tabla del servicio de consultas.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
