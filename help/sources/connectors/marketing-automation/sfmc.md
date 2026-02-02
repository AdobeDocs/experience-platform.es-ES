---
title: Información general sobre Salesforce Marketing Cloud (V2) Source
description: Obtenga información sobre cómo conectar Salesforce Marketing Cloud (V2) a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2025-02-02T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Resumen de origen de [!DNL Salesforce Marketing Cloud] (V2)

>[!IMPORTANT]
>
>El origen [[!DNL Salesforce Marketing Cloud] (V1)](salesforce-marketing-cloud.md) original quedó obsoleto en enero de 2026. No hay migraciones disponibles para este origen obsoleto y debe volver a implementar los datos usando el nuevo origen [!DNL Salesforce Marketing Cloud] (V2).

La integración entre Adobe [Real-Time CDP](../../../rtcdp/overview.md) y [!DNL Salesforce Marketing Cloud] está diseñada para aprovechar las extensiones de datos debido a la flexibilidad y el control que proporcionan. A diferencia de las tablas de sistema estándar (vistas de datos y objetos integrados), que se limitan a campos predefinidos y sirven principalmente para el seguimiento de nivel de sistema, puede utilizar las extensiones de datos para definir campos personalizados, organizar una amplia variedad de datos específicos de la empresa y adaptar las estructuras de datos para satisfacer requisitos únicos.

Debido a este nivel de personalización y escalabilidad, la integración entre Real-Time CDP y [!DNL Salesforce Marketing Cloud] depende de las extensiones de datos en lugar de las tablas de sistema estándar. Este enfoque ofrece una base más flexible, escalable e integrada para administrar los datos, lo que garantiza que se ajusten a sus objetivos comerciales

Puede usar el origen [!DNL Salesforce Marketing Cloud] para conectar su cuenta de [!DNL Salesforce Marketing Cloud] a Real-Time CDP y Adobe Experience Platform. Lea la documentación siguiente para aprender a empezar.

## Ejemplos de casos de uso {#use-case-examples}

### Personalización de campañas de correo electrónico con datos de contacto

Una marca minorista quiere personalizar las campañas de correo electrónico en función de las etapas del ciclo vital del cliente (por ejemplo, cliente nuevo, comprador habitual, cliente fiel). Para ello, crean una extensión de datos de contacto para almacenar información clave del cliente, como el nombre, el correo electrónico, la fase del ciclo vital y el comportamiento de compra. Estos datos se incorporan a continuación en Experience Platform para una segmentación y un direccionamiento más profundos.

Al ingerir los datos de la extensión de datos de contacto en Experience Platform, la marca puede segmentar a los clientes en función de su fase de ciclo de vida y del comportamiento de compra. Por ejemplo, pueden enviar una oferta de bienvenida a nuevos clientes, un incentivo por fidelidad a compradores habituales o incluso volver a atraer a clientes inactivos con ofertas específicas. Este enfoque garantiza una comunicación personalizada y permite una participación del cliente más relevante y eficaz.

### Ingesta de datos de campaña para la segmentación personalizada

Un equipo de marketing desea optimizar sus campañas de correo electrónico dirigiéndose a los clientes en función de su participación con campañas anteriores. Para ello, crean una extensión de datos de campaña en [!DNL Salesforce Marketing Cloud] para almacenar datos de participación de clientes, como aperturas de correo electrónico, clics y respuestas de campañas. Estos datos se incorporan a continuación en Experience Platform para una mayor segmentación y personalización.

Al ingerir estos datos de la extensión de datos de Campaign en Experience Platform, el equipo de marketing puede segmentar a los clientes en función de la participación anterior, como aquellos que hicieron clic en ofertas de productos o respondieron positivamente. Los clientes que participan pueden recibir promociones segmentadas en futuros correos electrónicos, mientras que aquellos que respondieron negativamente pueden recibir seguimiento del servicio de atención al cliente. Esta integración con Experience Platform garantiza que el equipo de marketing pueda ofrecer contenido más personalizado y relevante en función del comportamiento del cliente.

### Segmentación de clientes según los datos de actividades

Un equipo de marketing desea dirigirse a los clientes en función de sus actividades, como visitas a sitios web, envíos de formularios o interacciones con campañas de correo electrónico anteriores. Para conseguirlo, crean una extensión de datos de actividades para almacenar información sobre las actividades de participación de cada cliente. Estos datos se incorporan a continuación en Experience Platform para una mayor segmentación y segmentación personalizada de la campaña.

Al ingerir los datos de la extensión de datos de actividades en Experience Platform, el equipo de marketing puede segmentar a los clientes en función de su historial de participación. Por ejemplo, los clientes que recientemente visitaron el sitio web pero no completaron una compra pueden recibir correos electrónicos de recordatorio con ofertas especiales. Del mismo modo, los clientes que rellenen un formulario pueden recibir comunicaciones de seguimiento personalizadas. Este enfoque garantiza que cada cliente reciba contenido relevante en función de sus actividades más recientes, lo que mejora las tasas de participación y conversión.

## Requisitos previos {#prerequisites}

Lea las secciones siguientes para conocer la configuración de requisitos previos que debe completar antes de poder conectar su origen a Experience Platform.

### Configurar la aplicación para la autenticación {#set-up-application-for-authentication}

Al generar una integración con [!DNL Salesforce Marketing Cloud], uno de los primeros pasos es crear un **paquete instalado** en [!DNL Salesforce Marketing Cloud]. El paquete instalado genera las credenciales del cliente necesarias para autenticar las llamadas a la API y define el tipo de integración y los ámbitos de permisos asociados. Además, el paquete instalado proporciona los puntos finales de API correctos para el inquilino. También sirve como contenedor administrado para administrar, supervisar y revocar el acceso, lo que garantiza que todas las integraciones sean seguras, auditables y alineadas con el modelo de autenticación recomendado por Salesforce.

Para crear un paquete instalado, use la interfaz de usuario de [!DNL Salesforce Marketing Cloud], vaya a **[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]** y luego seleccione **[!DNL New]**. Utilice la interfaz [!DNL New Package Details] para proporcionar un nombre e información para el paquete. Cuando termine, seleccione **[!DNL Save]**.

![La nueva interfaz de paquetes de la interfaz de usuario de Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/new-package.png)

Una vez creado el nuevo paquete, seleccione **[!DNL Add Component]**.

![Interfaz de agregar componente de la interfaz de usuario de Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/add-component.png)

Seleccione **[!DNL API Integration]** como tipo de componente.

![Ventana de selección de componentes con la opción &quot;Integración de API&quot; seleccionada.](../../images/tutorials/create/sfmc/api-integration.png)

Seleccione **[!DNL Server-to-Server]** como su tipo de integración.

![Ventana de selección del tipo de integración](../../images/tutorials/create/sfmc/server-to-server.png)

Finalmente, vaya a **[!DNL Scope]** > **[!DNL Data]**. En **[!DNL Data Extensions]**, seleccione **[!DNL Read]**.

![La sección de extensiones de datos del ámbito en Salesforce Marketing](../../images/tutorials/create/sfmc/data-extensions.png)

Seleccione **[!DNL Save]** y luego copie y guarde su **secreto de cliente**. Una vez finalizado, seleccione **[!DNL Finish]**.

![Ventana de Salesforce Marketing Cloud para generar un secreto de cliente.](../../images/tutorials/create/sfmc/generate-secret.png)

Antes de salir de la interfaz de usuario de [!DNL Salesforce Marketing Cloud], copie **ID de cliente** y **prefijo único de URI base**, ya que usará ambos valores para crear una conexión con Experience Platform. Para el URI base de autenticación, asegúrese de eliminar todo después de `.auth.marketingcloudapis.com/`

![Interfaz de componentes de Salesforce Marketing Cloud en la que se pueden recuperar el identificador de cliente y el URI de base único.](../../images/tutorials/create/sfmc/client-id-and-uri.png)

Para ver los pasos detallados para crear un paquete instalado, lea la [[!DNL Salesforce] documentación](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment).

### Recopilar credenciales necesarias {#gather-required-credentials}

Debe proporcionar valores para las siguientes credenciales a fin de conectar [!DNL Salesforce Marketing Cloud] a Experience Platform.

| Credencial | Descripción |
| --- | --- |
| ID de cliente | El identificador expuesto públicamente que [!DNL Salesforce Marketing Cloud] usó para identificar su cuenta al autorizar a Experience Platform. El ID de cliente se puede recuperar del panel de componentes de la interfaz de usuario de [!DNL Salesforce Marketing Cloud]. |
| Secreto del cliente | La clave confidencial conocida sólo por la aplicación cliente y el servidor de autorización. Puede generar su secreto de cliente siguiendo los [pasos de configuración de la aplicación descritos anteriormente](#set-up-application-for-authentication). |
| Extremo base | El prefijo del URI base de autenticación de [!DNL Salesforce Marketing Cloud]. |

{style="table-layout:auto"}

## Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform

Continúe configurando la conexión de origen de [!DNL Salesforce Marketing Cloud] en Experience Platform. Para obtener una guía paso a paso sobre cómo configurar la conexión a través de la interfaz de usuario, consulte el [tutorial aquí](../../tutorials/ui/create/marketing-automation/sfmc.md). Lea este tutorial para obtener información sobre cómo conectar su cuenta de [!DNL Salesforce Marketing Cloud], seleccionar datos, asignar campos, programar ingestas y supervisar flujos de datos.
