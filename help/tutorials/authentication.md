---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Autentificación y acceso a las API de la plataforma de experiencias
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

---


# Autenticar y acceder a las API de la plataforma de experiencia

Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de realizar llamadas a las API de la plataforma de experiencia.

## Autenticar para realizar llamadas de API

Para mantener la seguridad de sus aplicaciones y usuarios, todas las solicitudes a las API de Adobe I/O deben autenticarse y autorizarse mediante estándares como OAuth y JSON Web Tokens (JWT). El JWT se utiliza junto con la información específica del cliente para generar su token de acceso personal.

Este tutorial trata los pasos de la autenticación mediante la creación de un token de acceso que se describe en el siguiente diagrama de flujo:
![](images/authentication/authentication-flowchart.png)

## Requisitos previos

Para realizar correctamente llamadas a las API de la plataforma de experiencia, necesita lo siguiente:

* Una organización de IMS con acceso a Adobe Experience Platform
* Una cuenta de Adobe ID registrada
* Un administrador de Admin Console para agregarle como **desarrollador** y un **usuario** para un producto.

Las siguientes secciones explican los pasos para crear un Adobe ID y convertirse en desarrollador y usuario de una organización.

### Creación de un Adobe ID

Si no dispone de un Adobe ID, puede crearlo siguiendo estos pasos:

1. Vaya a la consola de E/S de [Adobe](https://console.adobe.io)
2. Haga clic en **crear una cuenta nueva**
3. Completar el proceso de registro


### Conviértase en desarrollador y usuario de la plataforma de experiencia para una organización

Antes de crear integraciones en Adobe I/O, la cuenta debe tener permisos de desarrollador para un producto en una organización de IMS. Encontrará información detallada sobre las cuentas de desarrollador en Admin Console en el documento [de](https://helpx.adobe.com/enterprise/using/manage-developers.html) asistencia para la administración de desarrolladores.

**Obtener acceso de desarrollador**

Póngase en contacto con un administrador de la Consola de administración de su organización para agregarle como desarrollador de uno de los productos de su organización mediante la Consola de [administración](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

El administrador debe asignarle como desarrollador al menos un perfil de producto para continuar.

![](images/authentication/add-developer.png)

Una vez que se le asigne como desarrollador, tendrá privilegios de acceso para crear integraciones en [Adobe I/O](https://console.adobe.io/). Estas integraciones son una canalización de aplicaciones y servicios externos a la API de Adobe.

**Obtener acceso de usuario**

El administrador de Admin Console también debe agregarle al producto como usuario.

![](images/authentication/assign-users.png)

De forma similar al proceso de adición de un desarrollador, el administrador debe asignarle al menos un perfil de producto para continuar.

![](images/authentication/assign-user-details.png)


## Configuración única

Los siguientes pasos sólo tendrán que realizarse una vez:

* Iniciar sesión en la consola de Adobe I/O
* Crear integración
* Copiar valores de acceso descendentes

Una vez que tenga los valores de integración y acceso, podrá reutilizarlos para la autenticación en el futuro. Cada paso se describe en detalle a continuación.

### Inicio de sesión en la consola de Adobe I/O

Vaya a [Adobe I/O Console](https://console.adobe.io/) e inicie sesión con su Adobe ID.

Una vez que haya iniciado sesión, haga clic en la ficha **Integraciones** en la parte superior de la pantalla. Una integración es una cuenta de servicio creada para la organización de IMS seleccionada. Sólo puede realizar llamadas para la organización de IMS en la que se crea la integración.

>[!NOTE]
>Si su cuenta está asociada con varias organizaciones, el menú desplegable en la parte superior derecha de la pantalla le permite cambiar fácilmente entre ellas.

### Crear integración

En la página **Integraciones** , haga clic en **Nueva integración** para inicio del proceso. El proceso consta de tres pasos:
* Elija el tipo de integración
* Elija con qué servicio de Adobe desea integrar
* Añadir detalles de integración, clave pública y perfil del producto

![](images/authentication/integrations.png)

#### Elija el tipo de integración

La siguiente pantalla le preguntará si desea acceder a una API o recibir eventos en tiempo real próximos. Seleccione **Acceder a una API** y, a continuación, **Continuar**.

![](images/authentication/create-new-integration.png)

#### Elija con qué servicio de Adobe desea integrar

Si su cuenta está asociada con varias organizaciones de IMS, puede cambiar entre ellas mediante el menú desplegable en la parte superior derecha. Seleccione **Taller** y API **de plataforma de** experiencia en **Adobe Experience Platform** para acceder a las API.

![](images/authentication/integration-select-service.png)

Haga clic en **Continuar** para pasar a la siguiente sección.

#### Añadir detalles de integración, clave pública y perfil del producto

La siguiente pantalla le solicita que rellene los detalles de la integración, introduzca el certificado de clave pública y seleccione un perfil de producto.

![](images/authentication/integration-details.png)

Primero, introduzca los detalles de la integración. A continuación, seleccione un perfil de producto. Los perfiles de productos otorgan acceso granular a un grupo de funciones pertenecientes al servicio seleccionado en pasos anteriores.

Para la sección de certificados, debe generar un certificado:

**Para plataformas MacOS y Linux:**

Abra la línea de comandos y ejecute el siguiente comando:

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**Para plataformas Windows:**

1. Descargar un cliente openssl para generar certificados públicos (por ejemplo, cliente [Openssl windows](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip))

1. Extraiga la carpeta y cópiela en la ubicación C:/libs/.

1. Abra el símbolo del sistema de la línea de comandos y ejecute los siguientes comandos:

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

Recibirá una respuesta similar a la siguiente, que le indicará que introduzca información sobre usted:

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

Después de introducir la información, se generan dos archivos: `certificate_pub.crt` y `private.key`.

>[!NOTE]
>`certificate_pub.crt` caducará en 365 días. Puede alargar el período cambiando el valor de `days` en el comando `openssl` anterior, pero la rotación periódica de las credenciales es una buena práctica de seguridad.

El `private.key` será utilizado para generar nuestro JWT en la sección posterior.

El `certificate_pub.crt` se utiliza para crear una clave de API. Vuelva a la consola de Adobe I/O y haga clic en **Seleccionar un archivo** para cargar el `certificate_pub.crt` archivo.

Haga clic en **Crear integración** para completar el proceso.

### Copiar valores de acceso

Después de crear la integración, puede realizar la vista de sus detalles. Haga clic en **Recuperar secreto** de cliente y su pantalla tendrá un aspecto similar a este:

![](images/authentication/access-values.png)

Copie los valores para `{API KEY}`, `{IMS ORG}` que es el identificador de organización, y `{CLIENT SECRET}` como se usarán en el paso siguiente.

## Autenticación para cada sesión

El paso final es generar el `{ACCESS_TOKEN}` que se utilizará para autenticar las llamadas de API. El token de acceso debe incluirse en el encabezado de autorización de cada llamada de API que realice a Adobe Experience Platform. Los Tokenes de acceso caducan pasados 24 horas, tras las cuales deben generarse nuevos tokens para continuar utilizando las API.

### Crear JWT

En la página de detalles de la integración en la consola de Adobe I/O, vaya a la ficha **JWT** :

![](images/authentication/generate-jwt.png)

La página le solicita que introduzca el `private.key` que ha creado en la sección anterior. Abra la línea de comandos para vista del contenido del `private.key` archivo:

```shell
cat private.key
```

El resultado tendrá este aspecto:

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

Copie toda la salida y péguela en el campo de texto y, a continuación, haga clic en **Generar JWT**. Copie el JWT generado para el siguiente paso.

![](images/authentication/generated-jwt.png)

### Generar token de acceso

Puede generar un token de acceso mediante un comando cURL. Si no tiene cURL instalada, puede instalarla mediante `npm install curl`. Puede leer más sobre cURL [aquí](https://curl.haxx.se/)

Una vez que cURL esté instalado, tendrá que intercambiar los campos del siguiente comando con los suyos propios `{API_KEY}`, `{CLIENT_SECRET}`y `{JWT_TOKEN}`:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

Si tiene éxito, el resultado tendrá este aspecto:

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

El token de acceso es el valor debajo de la `access_token` clave. Este token de acceso `expires_in` 86399947 milisegundos (24 horas). Después, tendrá que generar un nuevo token de acceso siguiendo los mismos pasos anteriores.

Ya está listo para realizar solicitudes de API en Adobe Experience Platform.

### Código de acceso de prueba

Para comprobar si el token de acceso es válido, puede intentar realizar la siguiente llamada de API. Esta llamada lista todas las clases dentro del `global` contenedor:

>[!NOTE]
>`{API_KEY}` y `{IMS_ORG}` consulte los valores generados anteriormente.

**Solicitud**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


Si su respuesta es similar a la que se muestra a continuación, `access_token` es válida y funciona. (Esta respuesta se ha truncado para el espacio).

**Respuesta**

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Usar Postman para autenticación JWT y llamadas de API

[Postman](https://www.getpostman.com/) es una herramienta popular para trabajar con las API de RESTful. En este [medio](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) se describe cómo configurar el postman para que realice automáticamente la autenticación JWT y la utilice para consumir las API de Adobe Experience Platform.