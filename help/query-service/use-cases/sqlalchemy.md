---
title: Administrar datos de plataforma mediante Python y SQLAlchemy
description: Aprenda a utilizar SQLAlchemy para administrar los datos de Platform mediante Python en lugar de SQL.
source-git-commit: 6b7de4236982181eaac2aa37d525604cba31198e
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Administración de datos de Platform mediante [!DNL Python] y [!DNL SQLAlchemy]

Aprenda a utilizar SQLAlchemy para una buena flexibilidad en la administración de sus datos de Adobe Experience Platform. Para aquellos que no están tan familiarizados con SQL, SQLAlchemy puede mejorar considerablemente el tiempo de desarrollo al trabajar con bases de datos relacionales. Este documento proporciona instrucciones y ejemplos para conectar [!DNL SQLAlchemy] a Servicio de consultas y comience a utilizar Python para interactuar con sus bases de datos.

[!DNL SQLAlchemy] es un asignador relacional de objetos (ORM) y un [!DNL Python] biblioteca de código que puede transferir datos almacenados en una base de datos SQL a [!DNL Python] objetos. A continuación, puede realizar operaciones CRUD en datos que se mantienen dentro del lago de datos de Platform mediante [!DNL Python] código. Esto elimina la necesidad de administrar los datos utilizando solo PSQL.

## Primeros pasos

Para adquirir las credenciales necesarias para la conexión [!DNL SQLAlchemy] para Experience Platform, debe tener acceso al espacio de trabajo Consultas en la interfaz de usuario de Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso al espacio de trabajo Consultas .

## [!DNL Query Service] credenciales {#credentials}

Para encontrar sus credenciales, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde la navegación izquierda, seguido de **[!UICONTROL Credenciales]**. Para obtener instrucciones completas sobre cómo encontrar sus credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md).

![La ficha Credencial con credenciales con fecha de expiración para el servicio de consulta está resaltada.](../images/use-cases/credentials.png)

Aunque el puerto 80 es el puerto recomendado para una conexión con el servicio de consulta, también puede utilizar el puerto 5432.

>[!IMPORTANT]
>
>Si utiliza credenciales que caducan (como se muestra en la imagen anterior) para conectarse al servicio de consulta, la duración de la sesión de la conexión caducará después del período de tiempo establecido definido en la configuración de su organización. De forma predeterminada, este periodo es de 24 horas. Consulte la documentación para aprender a [conectar un cliente con credenciales que no caducan](../ui/credentials.md#non-expiring-credentials)o cómo [cambiar la duración de la sesión para sus credenciales de caducidad](../ui/credentials.md#expiring-credentials).

Una vez que tenga acceso a sus credenciales de QS, abra su [!DNL Python] editor elegido.

### Almacenar credenciales en [!DNL Python] {#store-credentials}

En [!DNL Python] editor, importe el `urllib.parse.quote` y guarde cada variable de credencial como parámetro. La variable `urllib.parse` proporciona una interfaz estándar para dividir cadenas URL en componentes. La función de comillas reemplaza caracteres especiales en la cadena URL para que los datos sean seguros para su uso como componentes URL. A continuación se muestra un ejemplo del código requerido:

>[!TIP]
>
>Uso [!DNL Python]Las comillas triples de para introducir su cadena de contraseña de líneas múltiples.

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
>La contraseña que proporciona para conectarse [!DNL SQLAlchemy] a Experience Platform caducará si utiliza credenciales que caducan. Consulte la [sección de credenciales](#credentials) para obtener más información.

### Creación de una instancia de motor [#create-engine]

Una vez creadas las variables, importe la variable `create_engine` y cree una cadena para compilar y dar formato a sus credenciales del servicio de consulta en SQLAlchemy. La variable `create_engine` a continuación se utiliza para construir una instancia de motor.

>[!NOTE]
>
>`create_engine`devuelve una instancia de un motor. Sin embargo, no abre la conexión con el servicio de consulta hasta que se realice una consulta que requiera una conexión.

SSL debe estar habilitado al acceder a Platform mediante clientes de terceros. Como parte del motor, utilice el `connect_args` para introducir argumentos de palabra clave adicionales. Se recomienda configurar el modo SSL en `require`. Consulte la [Documentación de modos SSL](../clients/ssl-modes.md) para obtener más información sobre los valores aceptados.

El ejemplo siguiente muestra la variable [!DNL Python] código necesario para inicializar un motor y una cadena de conexión.

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
>La contraseña que proporciona para conectarse [!DNL SQLAlchemy] a Experience Platform caducará si utiliza credenciales que caducan. Consulte la [sección de credenciales](#credentials) para obtener más información.

Ya está listo para consultar los datos de Platform mediante [!DNL Python]. El ejemplo que se muestra a continuación devuelve una matriz de nombres de tabla de Query Service.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
