---
keywords: Experience Platform;inicio;temas populares;esquema crm;crm;CRM;salesforce;Salesforce
solution: Experience Platform
title: Información general sobre el conector de origen de Salesforce
description: Obtenga información sobre cómo conectar Salesforce a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---

# [!DNL Salesforce] conector

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform proporciona asistencia para la ingesta de datos desde un sistema CRM de terceros. La compatibilidad con proveedores CRM incluye [!DNL Salesforce].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Asignación de campos desde [!DNL Salesforce] a XDM

Para establecer una conexión de origen entre [!DNL Salesforce] y Platform, la [!DNL Salesforce] Los campos de datos de origen deben asignarse a sus campos XDM de destino adecuados antes de introducirse en Platform.

Consulte lo siguiente para obtener información detallada sobre las reglas de asignación de campos entre [!DNL Salesforce] conjuntos de datos y Platform:

- [Contactos](../adobe-applications/mapping/salesforce.md#contact)
- [Posibles clientes](../adobe-applications/mapping/salesforce.md#lead)
- [Cuentas](../adobe-applications/mapping/salesforce.md#account)
- [Oportunidades](../adobe-applications/mapping/salesforce.md#opportunity)
- [Funciones de contacto de oportunidad](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campañas](../adobe-applications/mapping/salesforce.md#campaign)
- [Miembros de campaña](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relación de contacto de cuenta](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Configure las variables [!DNL Salesforce] utilidad de generación automática de esquemas y áreas de nombres

Para usar la variable [!DNL Salesforce] origen como parte de [!DNL B2B-CDP], primero debe configurar un [!DNL Postman] para generar automáticamente su [!DNL Salesforce] espacios de nombres y esquemas. La siguiente documentación proporciona información adicional sobre la configuración de [!DNL Postman] utilidad:

- Puede descargar la colección y el entorno de la utilidad de generación automática de esquemas y áreas de nombres desde esta [Repositorio de GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obtener información sobre el uso de las API de Platform, incluidos detalles sobre cómo recopilar valores para los encabezados necesarios y leer llamadas de API de ejemplo, consulte la guía sobre [introducción a las API de Platform](../../../landing/api-guide.md).
- Para obtener información sobre cómo generar sus credenciales para las API de Platform, consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md).
- Para obtener información sobre cómo configurar [!DNL Postman] para las API de Platform, consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md).

Con una consola para desarrolladores de Platform y [!DNL Postman] configurado, ahora puede empezar a aplicar los valores de entorno adecuados a su [!DNL Postman] entorno.

La siguiente tabla contiene valores de ejemplo, así como información adicional sobre cómo rellenar el [!DNL Postman] entorno:

| Variable | Descripción | Ejemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Un identificador único utilizado para generar su `{ACCESS_TOKEN}`. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | El token web JSON (JWT) es una credencial de autenticación utilizada para generar su {ACCESS_TOKEN}. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo generar su `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Identificador único utilizado para autenticar llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | El token de autorización necesario para completar las llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | El `global` contiene todas las clases, grupos de campos de esquema, tipos de datos y esquemas proporcionados por el Adobe estándar y el socio de Experience Platform. Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en `global`. | `global` |
| `PRIVATE_KEY` | Una credencial utilizada para autenticar su [!DNL Postman] a las API de Experience Platform. Consulte el tutorial sobre la configuración de la consola de desarrollador y [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar su {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Credencial utilizada para integrarse en el Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | El sistema de Identity Management (IMS) proporciona el marco para la autenticación en los servicios de Adobe. Con respecto a [!DNL Marketo], este valor es fijo y siempre se establece en: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Una entidad corporativa que puede poseer o licenciar productos y servicios y permitir el acceso a sus miembros. Consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar su `{ORG_ID}` información. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nombre de la partición de zona protegida virtual que está utilizando. | `prod` |
| `TENANT_ID` | ID que se utiliza para garantizar que los recursos que crea tengan un espacio de nombres correcto y estén contenidos en su organización IMS. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | El extremo URL al que realiza llamadas de API. Este valor es fijo y siempre se establece en: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | El ID único de su [!DNL Marketo] cuenta. Consulte el tutorial sobre [autenticación de su [!DNL Marketo] instancia](../adobe-applications/marketo/marketo-auth.md) para obtener información sobre cómo recuperar su `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | El ID de organización de su [!DNL Salesforce] cuenta. Consulte lo siguiente [[!DNL Salesforce] guía](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) para obtener más información sobre cómo adquirir su [!DNL Salesforce] ID de organización. | `00D4W000000FgYJUA0` |
| `has_abm` | Un valor booleano que indica si está suscrito a [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Un valor booleano que indica si está suscrito a [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Ejecución de scripts

Con su [!DNL Postman] configuración de la colección y el entorno, ahora puede ejecutar la secuencia de comandos a través del [!DNL Postman] interfaz.

En el [!DNL Postman] , seleccione la carpeta raíz de la utilidad auto-generator y, a continuación, seleccione **[!DNL Run]** desde el encabezado superior.

![carpeta-raíz](../../images/tutorials/create/salesforce/root-folder.png)

El [!DNL Runner] aparece la interfaz de. Desde aquí, asegúrese de que todas las casillas de verificación estén seleccionadas y, a continuación, seleccione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Una solicitud correcta crea los espacios de nombres y esquemas B2B según las especificaciones beta.

## Connect [!DNL Salesforce] a Platform mediante API

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Salesforce] Vaya a Platform mediante las API o la interfaz de usuario de:

- [Creación de una conexión base de Salesforce mediante la API de Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para una fuente CRM mediante la API de Flow Service](../../tutorials/api/collect/crm.md)

## Connect [!DNL Salesforce] a Platform mediante la IU

- [Crear una conexión de origen de Salesforce en la interfaz de usuario](../../tutorials/ui/create/crm/salesforce.md)
- [Crear un flujo de datos para una conexión CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
