---
title: Resumen de Source de Braze Currents
description: Aprenda a transmitir datos de Braze Currents a Experience Platform.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 4%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>El origen [!DNL Braze Currents] está en la versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde aplicaciones de streaming. La compatibilidad con los proveedores de streaming incluye [!DNL Braze Currents].

[!DNL Braze] potencia las interacciones centradas en el cliente entre consumidores y marcas en tiempo real. [!DNL Braze Currents] es un flujo de datos en tiempo real de eventos de participación de la plataforma Braze que es la exportación más sólida pero granular de la plataforma [!DNL Braze].

## Requisitos previos

Para completar los pasos de esta guía, necesitará lo siguiente:

* Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y obtener permiso para crear una nueva conexión de origen de flujo continuo.
* Iniciar sesión en [[!DNL Braze] panel](https://dashboard.braze.com/sign_in), obtener una licencia de [Currents Connector](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) sin usar y obtener permisos para crear un conector. Para obtener más información, lea los [requisitos para configurar [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Recopilar credenciales necesarias

Para enviar correctamente los datos de [!DNL Braze Currents] a Experience Platform, debe escribir las siguientes credenciales de Experience Platform en el panel de interfaz de usuario de [!DNL Braze].

| Campo | Descripción |
| --- | --- |
| ID de cliente | El ID de cliente asociado con el origen de Experience Platform. |
| Secreto del cliente | El secreto de cliente asociado con el origen de Experience Platform. |
| ID de inquilino | El ID de inquilino asociado con el origen de Experience Platform. |
| Nombre de la zona protegida | La zona protegida asociada a su origen de Experience Platform. |
| ID de flujo de datos | El ID de flujo de datos asociado con el origen de Experience Platform. |
| Punto final de streaming | Punto final de flujo continuo asociado a la fuente de Experience Platform. **Nota**: [!DNL Braze] convierte automáticamente esto en el extremo de flujo continuo por lotes. |

Para obtener información sobre cómo recuperar estos valores, lea la guía sobre [introducción a las API de Experience Platform](../../../landing/api-authentication.md). Para obtener información sobre cómo usar el panel [!DNL Braze], lea la guía [!DNL Braze] sobre cómo [navegar a las corrientes](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Pasos siguientes

Al leer este documento, ha completado la configuración de requisitos previos necesaria para transmitir datos de su cuenta de [!DNL Braze Currents] a Experience Platform. Ahora puede continuar con la guía de [conexión [!DNL Braze Currents] a Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/marketing-automation/braze.md).
