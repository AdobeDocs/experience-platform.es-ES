---
title: Información general sobre el conector Salesforce Source
description: Obtenga información sobre cómo conectar Salesforce a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 719f1bca20d5118de14ebe324675bb0aab6161e8
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 1%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>Ahora puede usar el origen [!DNL Salesforce] al ejecutar Adobe Experience Platform en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde un sistema CRM de terceros. La compatibilidad con proveedores CRM incluye [!DNL Salesforce].

## Configurar el origen de [!DNL Salesforce] para Experience Platform en Azure {#azure}

Siga los pasos a continuación para aprender a configurar su cuenta de [!DNL Salesforce] para Experience Platform en Azure.

### LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

### Asignación de campos de [!DNL Salesforce] a XDM

Para establecer una conexión de origen entre [!DNL Salesforce] y Platform, los campos de datos de origen de [!DNL Salesforce] deben asignarse a sus campos XDM de destino adecuados antes de introducirse en Platform.

Consulte lo siguiente para obtener información detallada sobre las reglas de asignación de campos entre [!DNL Salesforce] conjuntos de datos y Platform:

- [Contactos](../adobe-applications/mapping/salesforce.md#contact)
- [Posibles clientes](../adobe-applications/mapping/salesforce.md#lead)
- [Cuentas](../adobe-applications/mapping/salesforce.md#account)
- [Oportunidades](../adobe-applications/mapping/salesforce.md#opportunity)
- [Funciones de contacto de oportunidad](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campañas](../adobe-applications/mapping/salesforce.md#campaign)
- [Miembros de la campaña](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relación de contacto de cuenta](../adobe-applications/mapping/salesforce.md#account-contact-relation)

### Configurar el espacio de nombres [!DNL Salesforce] y la utilidad de generación automática de esquemas

Para usar el origen [!DNL Salesforce] como parte de [!DNL B2B-CDP], primero debe configurar una utilidad [!DNL Postman] para generar automáticamente los esquemas y áreas de nombres de [!DNL Salesforce]. La siguiente documentación proporciona información adicional sobre la configuración de la utilidad [!DNL Postman]:

- Puede descargar la colección de utilidades de generación automática de esquemas y áreas de nombres desde este [repositorio de GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obtener información sobre el uso de las API de Platform, incluidos detalles sobre cómo recopilar valores para los encabezados necesarios y leer llamadas de API de ejemplo, consulte la guía sobre [introducción a las API de Platform](../../../landing/api-guide.md).
- Para obtener información sobre cómo generar las credenciales de las API de Platform, consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md).
- Para obtener información sobre cómo configurar [!DNL Postman] para las API de Platform, consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md).

Con una consola de desarrollador de Platform y [!DNL Postman] configuradas, ahora puede empezar a aplicar los valores de entorno apropiados a su entorno [!DNL Postman].

+++Ver la guía de tabla de variables

La siguiente tabla contiene valores de ejemplo, así como información adicional sobre cómo rellenar el entorno [!DNL Postman]:

| Variable | Descripción | Ejemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Un identificador único usado para generar su `{ACCESS_TOKEN}`. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | El token web JSON (JWT) es una credencial de autenticación utilizada para generar su {ACCESS_TOKEN}. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo generar su `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Identificador único utilizado para autenticar llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | El token de autorización necesario para completar las llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | El contenedor `global` contiene todas las clases, los grupos de campos de esquema, los tipos de datos y los esquemas proporcionados por los socios estándar de Adobe y Experience Platform. Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en `global`. | `global` |
| `PRIVATE_KEY` | Credencial utilizada para autenticar la instancia de [!DNL Postman] en las API de Experience Platform. Consulte el tutorial sobre la configuración de la consola de desarrolladores y [configuración de la consola de desarrolladores y [!DNL Postman]](../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar su {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Credencial utilizada para integrarse en Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | El sistema de Identity Management (IMS) proporciona el marco para la autenticación en los servicios de Adobe. Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Una entidad corporativa que puede poseer o licenciar productos y servicios y permitir el acceso a sus miembros. Consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar la información de `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nombre de la partición de zona protegida virtual que está utilizando. | `prod` |
| `TENANT_ID` | ID que se utiliza para garantizar que los recursos que crea tengan un espacio de nombres correcto y estén contenidos en su organización. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | El extremo URL al que realiza llamadas de API. Este valor es fijo y siempre se establece en: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | Identificador exclusivo de su cuenta de [!DNL Marketo]. Vea el tutorial sobre [autenticación de su [!DNL Marketo] instancia](../adobe-applications/marketo/marketo-auth.md) para obtener información sobre cómo recuperar su `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | Identificador de organización de su cuenta de [!DNL Salesforce]. Consulte la siguiente [[!DNL Salesforce] guía](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) para obtener más información sobre cómo adquirir su ID de organización [!DNL Salesforce]. | `00D4W000000FgYJUA0` |
| `has_abm` | Un valor booleano que indica si está suscrito a [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Un valor booleano que indica si está suscrito a [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

+++

### Ejecutar los scripts

Con la colección y el entorno [!DNL Postman] configurados, ahora puede ejecutar el script a través de la interfaz [!DNL Postman].

En la interfaz [!DNL Postman], seleccione la carpeta raíz de la utilidad autogenerador y, a continuación, seleccione **[!DNL Run]** en el encabezado superior.

![carpeta raíz](../../images/tutorials/create/salesforce/root-folder.png)

Aparecerá la interfaz [!DNL Runner]. Aquí, asegúrese de que todas las casillas de verificación estén seleccionadas y luego seleccione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Una solicitud correcta crea los espacios de nombres y esquemas B2B según las especificaciones beta.

## Configurar el origen de [!DNL Salesforce] para Experience Platform en Amazon Web Service {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Siga los pasos a continuación para aprender a configurar su cuenta de [!DNL Salesforce] para Experience Platform en Amazon Web Service (AWS).

### Requisitos previos

Para conectar tu cuenta de [!DNL Salesforce] a Experience Platform en una región de AWS, debes tener lo siguiente:

- Una cuenta de [!DNL Salesforce] con acceso a API.
- Un [!DNL Salesforce Connected App] que puede usar para habilitar el flujo de OAuth JWT_BEARER.
- Los permisos necesarios en [!DNL Salesforce] para tener acceso a los datos.

### LISTA DE PERMITIDOS de direcciones IP para la conexión en AWS

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar las fuentes a Experience Platform en AWS. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform en AWS](../../ip-address-allow-list.md).

### Crear un(a) [!DNL Salesforce Connected App]

En primer lugar, utilice lo siguiente para crear un certificado/par clave de archivos PEM.

```shell
openssl req -newkey rsa:4096 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem  
```

1. En el panel [!DNL Salesforce], seleccione la configuración (![El icono de configuración.](/help/images/icons/settings.png)) y después seleccione **[!DNL Setup]**.
2. Vaya a [!DNL App Manager] y seleccione **[!DNL New Connection App]**.
3. Asigne un nombre a la aplicación y permita que el resto de los campos se rellenen automáticamente.
4. Habilite la casilla para [!DNL Enable OAuth Settings].
5. Establecer una URL de devolución de llamada. Dado que esto no se usará para JWT, puede usar `https://localhost`.
6. Habilite la casilla para [!DNL Use Digital Signatures].
7. Cargue el archivo cert.pem creado anteriormente.

#### Añadir los permisos necesarios

Añada los siguientes permisos:

1. Administración de datos de usuario mediante API
2. Acceso a permisos personalizados (custom_permissions)
3. Acceso al servicio de URL de identidad (ID, perfil, correo electrónico, dirección, teléfono)
4. Acceso a identificadores únicos (openid)
5. Realizar solicitudes en cualquier momento (refresh_token, offline_access)

Una vez agregados los permisos, asegúrese de habilitar la casilla para **[!DNL Issue JSON Web Token (JWT)-based access tokens for named user]**.

A continuación, seleccione **[!DNL Save]**, **[!DNL Continue]** y luego **[!DNL Manage Customer Details]**. Utilice el panel de detalles del consumidor para recuperar lo siguiente:

- **Clave de consumidor**: Más adelante utilizará esta clave de consumidor como ID de cliente al autenticar su cuenta de [!DNL Salesforce] en Experience Platform.
- **Secreto de consumidor**: Más adelante utilizará este secreto de consumidor como ID de cliente al autenticar su cuenta de [!DNL Salesforce] en Experience Platform.

### Autorizar al usuario [!DNL Salesforce] a la aplicación conectada

Siga los pasos a continuación para obtener autorización para utilizar la aplicación conectada:

1. Vaya a **[!DNL Manage Connected Apps]**.
2. Seleccione **[!DNL Edit]**.
3. Configure **[!DNL Permitted Users]** como **[!DNL Admin approved users are pre-authorized]** y luego seleccione **[!DNL Save]**.
4. Vaya a **[!DNL Settings]> [!DNL Manage Users] >[!DNL Profiles]**.
5. Edite el perfil asociado al usuario.
6. Vaya a **[!DNL Connected App Access]** y, a continuación, seleccione la aplicación que creó en un paso anterior.

### Generar token de portador JWT

Siga los pasos a continuación para generar su token de portador JWT.

#### Convertir par clave en pkcs12

Para generar el token de portador de JWT, primero debe utilizar el siguiente comando para convertir el certificado/par de claves al formato pkcs12. Durante este paso, también debe **establecer una contraseña de exportación** cuando se le solicite.

```shell
openssl pkcs12 -export -in cert.pem -inkey key.pem -name jwtcert >jwtcert.p12
```

#### Crear un repositorio de claves Java basado en pkcs12

A continuación, utilice el siguiente comando para crear un repositorio de claves java basado en el pkcs12 que acaba de generar. Durante este paso, también debe especificar **establecer una contraseña de almacén de claves de destino** cuando se le solicite. Además, debe proporcionar la contraseña de exportación anterior como contraseña del almacén de claves de origen.

```shell
keytool -importkeystore -srckeystore jwtcert.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -alias jwtcert
```

#### Confirme que keystroke.jks incluye un alias jwtcert

A continuación, use el comando follow para confirmar que su `keystroke.jks` incluye un alias `jwtcert`. Durante este paso, se le pedirá que proporcione la contraseña del almacén de claves de destino generada en el paso anterior.

```shell
keytool -keystore keystore.jks -list
```

#### Generar token firmado

Finalmente, utilice el ejemplo JWTE de clase java a continuación para generar el token firmado.

```java
package org.example;
 
import org.apache.commons.codec.binary.Base64;
 
import java.io.*;
import java.security.*;
import java.text.MessageFormat;
 
public class Main {
 
    public static void main(String[] args) {
 
        String header = "{\"alg\":\"RS256\"}";
        String claimTemplate = "'{'\"iss\": \"{0}\", \"sub\": \"{1}\", \"aud\": \"{2}\", \"exp\": \"{3}\"'}'";
 
        try {
            StringBuffer token = new StringBuffer();
 
            //Encode the JWT Header and add it to our string to sign
            token.append(Base64.encodeBase64URLSafeString(header.getBytes("UTF-8")));
 
            //Separate with a period
            token.append(".");
 
            //Create the JWT Claims Object
            String[] claimArray = new String[5];
            claimArray[0] = "{CLIENT_ID}";
            claimArray[1] = "{AUTHORIZED_SALESFORCE_USERNAME}";
            claimArray[2] = "{SALESFORCE_LOGIN_URL}";
            claimArray[3] = Long.toString((System.currentTimeMillis() / 1000) + 2629746*4);
            MessageFormat claims;
            claims = new MessageFormat(claimTemplate);
            String payload = claims.format(claimArray);
 
            //Add the encoded claims object
            token.append(Base64.encodeBase64URLSafeString(payload.getBytes("UTF-8")));
 
            //Load the private key from a keystore
            KeyStore keystore = KeyStore.getInstance("JKS");
            keystore.load(new FileInputStream("path/to/keystore"), "keystorepassword".toCharArray());
            PrivateKey privateKey = (PrivateKey) keystore.getKey("jwtcert", "privatekeypassword".toCharArray());
 
            //Sign the JWT Header + "." + JWT Claims Object
            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(token.toString().getBytes("UTF-8"));
            String signedPayload = Base64.encodeBase64URLSafeString(signature.sign());
 
            //Separate with a period
            token.append(".");
 
            //Add the encoded signature
            token.append(signedPayload);
 
            System.out.println(token.toString());
 
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

| Propiedad | Configuraciones  |
| --- | --- |
| `claimArray[0]` | Actualice `claimArray[0]` con su ID de cliente. |
| `claimArray[1]` | Actualice `claimArray[1]` con el nombre de usuario [!DNL Salesforce] autorizado para la aplicación. |
| `claimArray[2]` | Actualice `claimArray[2]` con la URL de inicio de sesión de [!DNL Salesforce]. |
| `claimArray[3]` | Actualice `claimArray[3]` con una fecha de caducidad formateada en milisegundos desde la hora epoch. Por ejemplo `3660624000000` es 31-12-2085. |
| `/path/to/keystore` | Reemplazar `/path/to/keystore` por la ruta correcta de su keystore.jks |
| `keystorepassword` | Reemplace `keystorepassword` por su contraseña de almacén de claves de destino. |
| `privatekeypassword` | Reemplace `privatekeypassword` por su contraseña de almacén de claves de origen. |

## Pasos siguientes

Una vez que haya completado la configuración de los requisitos previos de su cuenta de [!DNL Salesforce], puede continuar con la conexión de su cuenta de [!DNL Salesforce] a Experience Platform e introducir los datos de CRM. Lea la documentación siguiente para obtener más información:

### Conectar [!DNL Salesforce] a Platform mediante API

La siguiente documentación proporciona información sobre cómo conectar [!DNL Salesforce] a Platform mediante API o la interfaz de usuario:

- [Conexión de Salesforce a Experience Platform mediante la API de Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para una fuente CRM mediante la API de Flow Service](../../tutorials/api/collect/crm.md)

### Conectar [!DNL Salesforce] a Platform mediante la interfaz de usuario

- [Crear una conexión de origen de Salesforce en la interfaz de usuario](../../tutorials/ui/create/crm/salesforce.md)
- [Crear un flujo de datos para una conexión CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)