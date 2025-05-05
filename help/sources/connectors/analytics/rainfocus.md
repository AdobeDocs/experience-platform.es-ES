---
title: Resumen de fuentes de RainFocus
description: Aprenda a llevar los datos de análisis y administración de eventos de su cuenta de RainFocus a Experience Platform
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 4%

---

# [!DNL RainFocus]

>[!NOTE]
>
>El origen [!DNL RainFocus] está en la versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

[!DNL RainFocus] es una plataforma que puede usar para promocionar eventos y crear audiencias. Puede usar [!DNL RainFocus] para crear hermosas páginas promocionales, rastrear el rendimiento de las campañas y optimizar las conversiones de registro.

Utilice el origen [!DNL RainFocus] en Adobe Experience Platform y Real-time Customer Data Platform para enriquecer automáticamente los perfiles de datos de los clientes con los eventos de experiencia de los asistentes en tiempo real. Una vez activados, los eventos de experiencia se transmiten automáticamente a Real-Time CDP, lo que permite una potente segmentación de audiencia, análisis de datos y activación del recorrido de los asistentes con destinos posteriores y aplicaciones como Customer Journey Analytics y Adobe Journey Optimizer.

>[!IMPORTANT]
>
>El equipo [!DNL RainFocus] crea y mantiene este conector de origen y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en clientcare<span>@rainfocus.com o visite el [[!DNL RainFocus] Centro de ayuda](https://help.rainfocus.com/hc/en-us)

## Requisitos previos

Debe completar los siguientes requisitos previos para activar la integración de [!DNL RainFocus] en el Experience Platform:

[Crear una cuenta de servicio (JWT) de Adobe en el portal de Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>El Adobe de ha anunciado recientemente la desaprobación de los tokens JWT en favor de OAuth. Para dar cabida a este cambio, el origen de [!DNL RainFocus] se migrará a OAuth en un futuro próximo.

### Recopilar credenciales necesarias

Para conectar [!DNL RainFocus] al Experience Platform, debe proporcionar valores para las siguientes propiedades de conexión en [!DNL RainFocus]:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| ID de cliente | El ID de cliente se puede obtener de la cuenta de servicio de Adobe en el portal de Adobe Developer. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Secreto del cliente | El secreto de cliente se puede obtener de la cuenta de servicio de Adobe en el portal de Adobe Developer. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| ID de cuenta técnica | El ID de cuenta técnica se puede obtener de la cuenta de servicio de Adobe en el portal de Adobe Developer. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| ID de organización | El ID de organización se puede obtener de la cuenta de servicio de Adobe en el portal de Adobe Developer | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Creación de un esquema XDM y definición del campo de identidad {#create-an-xdm-schema-and-define-the-identity-field}

Para almacenar los eventos de experiencia de [!DNL RainFocus] en el Experience Platform, debe crear un esquema del Modelo de datos de experiencia (XDM) para describir un conjunto de datos que pueda almacenar los posibles campos y tipos de datos que se enviarán desde [!DNL RainFocus].

[!DNL RainFocus] recomienda los siguientes campos, que abarcan todos los datos posibles enviados de forma predeterminada.

También se recomiendan los siguientes grupos de campos (marcados con un prefijo):

* Asistente
* Expositor
* Posible cliente
* Session
* SessionTime

**El esquema debe contener los siguientes campos:**

| Campo | Tipo | Ejemplo | Descripción |
| --- | --- | --- | --- |
| `attendee.registered` | Cadena | Sí | Un indicador que determina si se considera que el asistente está registrado. |
| `attendee.attendeeId` | Cadena | 1619119968857001fvLB | Identificador de asistente en [!DNL RainFocus]. |
| `attendee.externalId` | Cadena | 1666809456617001wyPj | El ID externo especificado por una organización. |
| `attendee.clientId` | Cadena | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | El ID del cliente SSO de asistente. |
| `attendee.email` | Cadena | user<span>@company.com | La dirección de correo electrónico del asistente. |
| `transmissionId` | Cadena | 1680309557133001YHz | Un identificador único utilizado para la inserción de datos. |
| `eventType` | Cadena | SessionScheduled | Nombre del evento de experiencia del asistente. |
| `timestamp` | Fecha/Hora | 2023-04-01T00:41:57.000Z | La marca de tiempo de la inserción de datos. |
| `event.name` | Cadena | Adobe Summit de 2023 | El nombre del evento en el que tuvo lugar una transmisión. |
| `exhibitor.exhibitorId` | Cadena | 1680309557133001YHz | El identificador [!DNL RainFocus] del expositor. |
| `exhibitor.externalId` | Cadena | 1666809514105001lSJN | El identificador del expositor en el sistema cliente. |
| `exhibitor.name` | Cadena | IBM | El nombre del expositor. |
| `lead.leadId` | Cadena | 1666809456617001wyPj | El identificador [!DNL RainFocus] del posible cliente. |
| `lead.note` | Cadena | | |
| `session.sessionId` | Cadena | 1666809373585001t4aV | El identificador [!DNL RainFocus] de la sesión. |
| `session.externalId` | Cadena | 1666809456617001wyPj | El identificador de la sesión en el sistema cliente. |
| `session.code` | Cadena | GS3 | El código de la sesión. |
| `session.title` | Cadena | Presentación de inspiración | El título de la sesión. |
| `session.length` | Entero | 90 | La duración de la sesión. |
| `sessiontime.sessiontimeId` | Cadena | 1673033149739001JLZ | El identificador [!DNL RainFocus] para la hora de la sesión. |
| `sessiontime.startTime` | Cadena | 22-03-2023 10:00:00 | Hora de inicio de la sesión. |
| `sessiontime.endTime` | Cadena | 22-03-2023 10:00:00 | Hora de finalización de la sesión. |
| `sessiontime.room` | Cadena | B32 | La sala utilizada para la sesión. |

{style="table-layout:auto"}

Para crear el esquema para los datos de [!DNL RainFocus], lea la siguiente documentación para ver los pasos sobre cómo crear un esquema mediante las API o la interfaz de usuario.

* [Creación del esquema con la interfaz de usuario](../../../xdm/tutorials/create-schema-ui.md)
* [Cree el esquema con la API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* El esquema debe ampliar la clase **XDM ExperienceEvent.**
>* Debe asegurarse de que el esquema incluya una **identidad principal** y de que esté **habilitado para el perfil**. Para obtener más información, lea la guía sobre [definición de campos de identidad en la interfaz de usuario](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html?lang=es)
>* Puede sustituir la identidad de ejemplo (Correo electrónico) por otro identificador adecuado, como un correo electrónico sha256 o un ECID.

### Creación de un perfil de integración en RainFocus {#create-an-integration-profile-in-rainfocus}

Una vez que la cuenta de servicio y el esquema XDM estén listos, ahora puede activar [!DNL Integration Profile] a través de la plataforma [!DNL RainFocus]. [!DNL Integration Profile] es responsable de la transmisión de datos al Experience Platform.

Inicie sesión en [[!DNL RainFocus] platform](https://app.rainfocus.com). En la navegación principal, seleccione **[!DNL Libraries]** y luego seleccione **[!DNL Integration Profiles]**

![La interfaz de usuario de RainFocus con las bibliotecas y los perfiles de integración seleccionados.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Para crear un nuevo perfil, seleccione el icono **(`+`)**. A continuación, selecciona **Adobe Real-time Customer Data Platform** y luego selecciona **Aceptar**.

![Ventana Crear perfil de integración en la interfaz de usuario de RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

A continuación, proporcione las credenciales que ha recuperado en el proyecto del portal de Adobe Developer:

* **ID de cliente**
* **Secreto de cliente**
* **Id. de cuenta técnica**
* **ID de organización**

Una vez proporcionadas las credenciales, seleccione **[!DNL Save]**. Ahora debería ver el nuevo [!DNL Integration Profile] en el panel [!DNL RainFocus].

Seleccione el [!DNL Integration Profile] que acaba de crear para ver una lista de **tipos de inserción** predefinidos ya configurados. Estos son los [Eventos de experiencia](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=es) que se enviarán al Experience Platform cuando ocurran.

![Lista de tipos de inserción predefinidos en el panel RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Para recuperar una copia de la carga útil JSON de ejemplo, seleccione **[!DNL Sample JSON Payload]**. A continuación, resalte y copie la carga útil JSON de muestra y **guárdela en un nuevo archivo con la extensión .json**. Se usará más adelante en el Experience Platform para [configuraciones de asignación](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Carga útil JSON de muestra en el panel de RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**La instalación aún no se ha completado**: Una vez que se haya creado el flujo de datos, tendrá que volver al panel de [!DNL RainFocus] para completar su [!DNL Integration Profile] proporcionando su **URL de extremo de flujo continuo** y **ID de flujo de datos**.

## Pasos siguientes

Al leer este documento, ha completado la configuración de requisitos previos necesaria para transmitir los datos de su cuenta de [!DNL RainFocus] al Experience Platform. Ahora puede continuar con la guía de [conexión [!DNL RainFocus] al Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/analytics/rainfocus.md).
