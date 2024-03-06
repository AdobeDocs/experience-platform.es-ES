---
title: Resumen de origen de corrientes de Bear
description: Aprenda a transmitir datos de Braze Currents a Experience Platform.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 2%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>El [!DNL Braze Currents] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde aplicaciones de streaming. La compatibilidad con proveedores de streaming incluye [!DNL Braze Currents].

[!DNL Braze] potencia las interacciones centradas en el cliente entre consumidores y marcas en tiempo real. [!DNL Braze Currents] es un flujo de datos en tiempo real de eventos de participación de la plataforma Braze que es la exportación más sólida pero granular de [!DNL Braze] plataforma.

## Requisitos previos

Para completar los pasos de esta guía, necesitará lo siguiente:

* Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y permiso para crear una nueva conexión de origen de flujo continuo.
* Inicie sesión en su [[!DNL Braze] tablero](https://dashboard.braze.com/sign_in), y sin utilizar [Licencia del conector actual](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)y permisos para crear un conector. Para obtener más información, lea la [requisitos para la configuración [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Recopilar credenciales necesarias

Para enviar correctamente su [!DNL Braze Currents] para enviar datos a Experience Platform, debe introducir las siguientes credenciales de Experience Platform en la [!DNL Braze] Panel de IU.

| Campo | Descripción |
| --- | --- |
| ID de cliente | El ID de cliente asociado con el origen del Experience Platform. |
| Secreto de cliente | El secreto de cliente asociado con el origen del Experience Platform. |
| ID de inquilino | El ID de inquilino asociado con el origen del Experience Platform. |
| Nombre de la zona protegida | La zona protegida asociada a la fuente del Experience Platform. |
| ID de flujo de datos | El ID de flujo de datos asociado con el origen del Experience Platform. |
| Punto final de streaming | El extremo de flujo continuo asociado con el origen del Experience Platform. **Nota**: [!DNL Braze] convierte automáticamente esto en el punto final de flujo por lotes. |

Para obtener información sobre cómo recuperar estos valores, lea la guía sobre [introducción a las API de Platform](../../../landing/api-authentication.md). Para obtener información sobre el uso de [!DNL Braze] panel, lea la [!DNL Braze] guía sobre cómo [Navegar a Corrientes](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Pasos siguientes

Al leer este documento, ha completado la configuración de requisitos previos necesaria para transmitir los datos de su [!DNL Braze Currents] cuenta para el Experience Platform. Ahora puede continuar con la guía de [conectador [!DNL Braze Currents] al Experience Platform mediante la interfaz de usuario de](../../tutorials/ui/create/marketing-automation/braze.md).