---
title: Administrar datos de Experience Platform mediante Python y SQLAlchemy
description: Aprenda a utilizar SQLAlchemy para administrar los datos de Experience Platform mediante Python en lugar de SQL.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Administrar datos de Experience Platform mediante [!DNL Python] y [!DNL SQLAlchemy]

Aprenda a utilizar SQLAlchemy para obtener una mayor flexibilidad en la administración de los datos de Adobe Experience Platform. Para aquellos que no están tan familiarizados con SQL, SQLAlchemy puede mejorar en gran medida el tiempo de desarrollo al trabajar con bases de datos relacionales. Este documento proporciona instrucciones y ejemplos para conectar [!DNL SQLAlchemy] al servicio de consultas y comenzar a usar Python para interactuar con las bases de datos.

[!DNL SQLAlchemy] es un Object Relational Mapper (ORM) y una biblioteca de código [!DNL Python] que puede transferir datos almacenados en una base de datos SQL a objetos [!DNL Python]. A continuación, puede realizar operaciones de CRUD en datos mantenidos dentro del lago de datos de Experience Platform mediante el código [!DNL Python]. Esto elimina la necesidad de administrar datos usando solo PSQL.

## Introducción

Para adquirir las credenciales necesarias para conectar [!DNL SQLAlchemy] a Experience Platform, debe tener acceso al área de trabajo Consultas en la interfaz de usuario de Experience Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso al área de trabajo Consultas.

## Credenciales de [!DNL Query Service] {#credentials}

Para encontrar sus credenciales, inicie sesión en la interfaz de usuario de Experience Platform y seleccione **[!UICONTROL Consultas]** en el panel de navegación izquierdo, seguido de **[!UICONTROL Credenciales]**. Para obtener instrucciones completas sobre cómo encontrar sus credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md).

![Se ha resaltado la ficha Credenciales con credenciales que caducan para el servicio de consultas.](../images/use-cases/credentials.png)

Aunque el puerto 80 es el puerto recomendado para una conexión al servicio de consultas, también puede utilizar el puerto 5432.

>[!IMPORTANT]
>
>Si utiliza credenciales que caducan (como se ve en la imagen anterior) para conectarse al servicio de consultas, la duración de la sesión de la conexión caducará después del período de tiempo establecido definido en la configuración de la organización. De forma predeterminada, este periodo es de 24 horas. Consulte la documentación para aprender a [conectar un cliente con credenciales que no caducan](../ui/credentials.md#non-expiring-credentials) o a [cambiar la duración de la sesión de las credenciales que caducan](../ui/credentials.md#expiring-credentials).

Una vez que tenga acceso a sus credenciales de QS, abra el editor [!DNL Python] que haya elegido.

### Almacenar credenciales en [!DNL Python] {#store-credentials}

En el editor [!DNL Python], importe la biblioteca `urllib.parse.quote` y guarde cada variable de credencial como un parámetro. El módulo `urllib.parse` proporciona una interfaz estándar para dividir las cadenas de URL en componentes. La función quote reemplaza los caracteres especiales de la cadena URL para que los datos sean seguros para su uso como componentes URL. A continuación se muestra un ejemplo del código requerido:

>[!TIP]
>
>Use las comillas triples de [!DNL Python] para escribir la cadena de contraseña de varias líneas.

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
>La contraseña que proporcione para conectar [!DNL SQLAlchemy] a Experience Platform caducará si usa credenciales que caduquen. Consulte la [sección de credenciales](#credentials) para obtener más información.

### Crear una instancia de motor [#create-engine]

Una vez creadas las variables, importe la función `create_engine` y cree una cadena para compilar y dar formato a las credenciales del servicio de consulta en SQLAlchemy. A continuación, se utiliza la función `create_engine` para construir una instancia de motor.

>[!NOTE]
>
>`create_engine` devuelve una instancia de un motor. Sin embargo, no abre la conexión al Servicio de consultas hasta que se llama a una consulta que requiere una conexión.

SSL debe estar habilitado al acceder a Experience Platform mediante clientes de terceros. Como parte del motor, use `connect_args` para escribir argumentos de palabras clave adicionales. Se recomienda establecer el modo SSL en `require`. Consulte la [documentación sobre los modos SSL](../clients/ssl-modes.md) para obtener más información sobre los valores aceptados.

El ejemplo siguiente muestra el código [!DNL Python] necesario para inicializar un motor y una cadena de conexión.

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
>La contraseña que proporcione para conectar [!DNL SQLAlchemy] a Experience Platform caducará si usa credenciales que caduquen. Consulte la [sección de credenciales](#credentials) para obtener más información.

Ya está listo para consultar los datos de Experience Platform mediante [!DNL Python]. El ejemplo que se muestra a continuación devuelve una matriz de nombres de tabla del servicio de consultas.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
