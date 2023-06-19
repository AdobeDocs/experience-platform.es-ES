---
title: Resumen de fuentes de RainFocus
description: Aprenda a llevar los datos de análisis y administración de eventos de su cuenta de RainFocus a Experience Platform
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: e9728e1e673a4018d1d776a9d9ddad023ad1393e
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 6%

---

# [!DNL RainFocus]

>[!NOTE]
>
>El [!DNL RainFocus] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

[!DNL RainFocus] es una plataforma que puede utilizar para promocionar eventos y crear audiencias. Puede utilizar [!DNL RainFocus] para crear páginas promocionales atractivas, realizar un seguimiento del rendimiento de las campañas y optimizar las conversiones de registro.

Utilice el [!DNL RainFocus] fuente en Adobe Experience Platform y Real-time Customer Data Platform para enriquecer automáticamente los perfiles de datos de los clientes con eventos de experiencia de los asistentes en tiempo real. Una vez activados, los eventos de experiencia se transmiten automáticamente a Real-Time CDP, lo que permite una potente segmentación de audiencia, análisis de datos y activación del recorrido de los asistentes con destinos posteriores y aplicaciones como Customer Journey Analytics y Adobe Journey Optimizer.

>[!IMPORTANT]
>
>Esta página de documentación fue creada por el [!DNL RainFocus] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en clientcare<span>@rainfocus.com o visite [[!DNL RainFocus] Centro de ayuda](https://help.rainfocus.com/hc/en-us)

## Requisitos previos

Debe completar los siguientes requisitos previos para poder activar el [!DNL RainFocus] integración en el Experience Platform:

[Creación de una cuenta de servicio de Adobe (JWT) en el portal de Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>El Adobe de ha anunciado recientemente la desaprobación de los tokens JWT en favor de OAuth. Para dar cabida a este cambio, la variable [!DNL RainFocus] La fuente de se migrará a OAuth en un futuro próximo.

### Recopilar credenciales necesarias

Para poder conectarse [!DNL RainFocus] al Experience Platform, debe proporcionar valores para las siguientes propiedades de conexión en [!DNL RainFocus]:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| ID del cliente | El ID de cliente se puede obtener de la cuenta de servicio de Adobe en el portal de Adobe Developer. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Secreto de cliente | El secreto de cliente se puede obtener de la cuenta de servicio de Adobe en el portal de Adobe Developer. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| ID de cuenta técnica | El ID de cuenta técnica se puede obtener de la cuenta de servicio de Adobe en el portal de Adobe Developer. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| ID de organización | El ID de organización se puede obtener de la cuenta de servicio de Adobe en el portal de Adobe Developer | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Creación de un esquema XDM y definición del campo de identidad {#create-an-xdm-schema-and-define-the-identity-field}

Para almacenar los eventos de experiencia de [!DNL RainFocus] en Experience Platform, debe crear un esquema del Modelo de datos de experiencia (XDM) para describir un conjunto de datos que pueda almacenar los posibles campos y tipos de datos que se enviarán desde [!DNL RainFocus].

[!DNL RainFocus] recomienda los siguientes campos, que abarcan todos los datos posibles enviados de forma predeterminada.

También se recomiendan los siguientes grupos de campos (marcados con un prefijo):

* Asistente
* Expositor
* Posible cliente
* Session
* SessionTime

**El esquema debe contener los campos siguientes:**

| Campo | Tipo | Ejemplo | Descripción |
| --- | --- | --- | --- |
| `attendee.registered` | Cadena | Sí | Un indicador que determina si se considera que el asistente está registrado. |
| `attendee.attendeeId` | Cadena | 1619119968857001fvLB | El ID de asistente en [!DNL RainFocus]. |
| `attendee.externalId` | Cadena | 1666809456617001wyPj | El ID externo especificado por una organización. |
| `attendee.clientId` | Cadena | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | El ID del cliente SSO de asistente. |
| `attendee.email` | Cadena | usuario<span>@company.com | La dirección de correo electrónico del asistente. |
| `transmissionId` | Cadena | 1680309557133001YHhz | Un identificador único utilizado para la inserción de datos. |
| `eventType` | Cadena | SessionScheduled | Nombre del evento de experiencia del asistente. |
| `timestamp` | DateTime | 01-04-2023:41:57,000Z | La marca de tiempo de la inserción de datos. |
| `event.name` | Cadena | Adobe Summit 2023 | El nombre del evento en el que tuvo lugar una transmisión. |
| `exhibitor.exhibitorId` | Cadena | 1680309557133001YHhz | El [!DNL RainFocus] identificador del expositor. |
| `exhibitor.externalId` | Cadena | 1666809514105001lSJN | El identificador del expositor en el sistema cliente. |
| `exhibitor.name` | Cadena | IBM | El nombre del expositor. |
| `lead.leadId` | Cadena | 1666809456617001wyPj | El [!DNL RainFocus] identificador del posible cliente. |
| `lead.note` | Cadena | | |
| `session.sessionId` | Cadena | 1666809373585001t4aV | El [!DNL RainFocus] identificador de la sesión. |
| `session.externalId` | Cadena | 1666809456617001wyPj | El identificador de la sesión en el sistema cliente. |
| `session.code` | Cadena | GS3 | El código de la sesión. |
| `session.title` | Cadena | Presentación de inspiración | El título de la sesión. |
| `session.length` | Número entero | 90 | La duración de la sesión. |
| `sessiontime.sessiontimeId` | Cadena | 1673033149739001OJLZ | El [!DNL RainFocus] identificador de la hora de la sesión. |
| `sessiontime.startTime` | Cadena | 2023-03-22 10:00:00 | Hora de inicio de la sesión. |
| `sessiontime.endTime` | Cadena | 2023-03-22 10:00:00 | Hora de finalización de la sesión. |
| `sessiontime.room` | Cadena | B32 | La sala utilizada para la sesión. |

{style="table-layout:auto"}

Para crear el esquema para [!DNL RainFocus] Para obtener más información sobre cómo crear un esquema con las API o la interfaz de usuario, lea la siguiente documentación.

* [Creación del esquema con la interfaz de usuario](../../../xdm/tutorials/create-schema-ui.md)
* [Cree el esquema con la API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* El esquema debe ampliar el **clase XDM ExperienceEvent.**
>* Debe asegurarse de que el esquema incluya un **identidad principal**, y es **habilitado para el perfil**. Para obtener más información, lea la guía de [definición de campos de identidad en la IU](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* Puede sustituir la identidad de ejemplo (Correo electrónico) por otro identificador adecuado, como un correo electrónico sha256 o un ECID.

### Creación de un perfil de integración en RainFocus {#create-an-integration-profile-in-rainfocus}

Una vez que la cuenta de servicio y el esquema XDM estén listos, ahora puede activar el [!DNL Integration Profile] a través de [!DNL RainFocus] plataforma. El [!DNL Integration Profile] es responsable de la transmisión de datos al Experience Platform.

Inicie sesión en [[!DNL RainFocus] plataforma](https://app.rainfocus.com). En la navegación principal, seleccione **[!DNL Libraries]** y luego seleccione **[!DNL Integration Profiles]**

![La interfaz de usuario de RainFocus con Bibliotecas y Perfiles de integración seleccionados.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Para crear un nuevo perfil, seleccione la **(`+`)** icono. A continuación, seleccione **Adobe Real-time Customer Data Platform** y luego seleccione **OK**.

![La ventana Crear perfil de integración en la interfaz de usuario de RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

A continuación, proporcione las credenciales que ha recuperado en el proyecto del portal de Adobe Developer:

* **ID del cliente**
* **Secreto de cliente**
* **ID de cuenta técnica**
* **ID de organización**

Una vez proporcionadas las credenciales, seleccione **[!DNL Save]**.Ahora debería ver el nuevo [!DNL Integration Profile] enumerados en la [!DNL RainFocus] panel.

Seleccione el [!DNL Integration Profile] que acaba de crear para ver una lista de **tipos de push** ya está configurado. Estas son las [Eventos de experiencia](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html) que se enviarán al Experience Platform cuando se produzcan.

![Una lista de tipos de pulsaciones predefinidas en el tablero Enfoque de lluvia.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Para recuperar una copia de la carga útil JSON de ejemplo, seleccione **[!DNL Sample JSON Payload]**. A continuación, resalte y copie la carga útil JSON de muestra y **guárdelo en un nuevo archivo con la extensión .json**. Se utilizará más adelante en Experience Platform para [asignación de configuraciones](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Una carga útil JSON de muestra en el panel de RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**La instalación aún no se ha completado**: Una vez creado el flujo de datos, debe volver a la [!DNL RainFocus] tablero para completar su [!DNL Integration Profile] al proporcionar su **URL de extremo de flujo continuo** y **ID de flujo de datos**.

## Pasos siguientes

Al leer este documento, ha completado la configuración de requisitos previos necesaria para transmitir los datos de su [!DNL RainFocus] cuenta para el Experience Platform. Ahora puede continuar con la guía de [conectador [!DNL RainFocus] al Experience Platform mediante la interfaz de usuario de](../../tutorials/ui/create/analytics/rainfocus.md).