---
title: Guía de solución de problemas de Adobe Experience Platform Assurance
description: Este documento describe las soluciones a los problemas comunes que se producen al utilizar Adobe Experience Platform Assurance.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# Solucionar problemas de Adobe Experience Platform Assurance

Si tiene problemas para que Assurance funcione, consulte las sugerencias en los siguientes temas para resolver los problemas que se encuentran con más frecuencia.

Para habilitar una implementación más suave y descubrir cualquier problema potencial, asegúrese de que tiene activado el inicio de sesión del SDK por [Habilitar registro de depuración](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) en la sección Introducción.

Puede cambiar los niveles de registro del SDK con las variables [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API.

## Problemas de la aplicación en el dispositivo

### El código QR no abre la aplicación

* Acceda al vínculo directamente. Copiar el vínculo de **Detalles de sesión**. Péguelo en la barra de direcciones del explorador del dispositivo para abrirlo. Si no se abre, consulte la sección [La aplicación no abrirá el vínculo](#app-does-not-open-link).
* Utilice un lector QR diferente. Para iOS 11 o bueno, utilice la aplicación Photo para leer el código QR.

### La aplicación no abre el vínculo

* Compruebe que la implementación de vínculos profundos está configurada correctamente en la aplicación.
   * **Android:** Vínculos profundos (vínculos de la aplicación)
      * [Creación de vínculos profundos al contexto de la aplicación](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Esquema URL personalizado o vínculos universales
      * [Definición de un esquema de URL personalizado para la aplicación](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Compatibilidad con vínculos universales en la aplicación](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Para Android, la variable `startSession` No es necesario llamar explícitamente a la API. Para iOS, utilice la API como se describe en [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### Aparece la superposición de autenticación, pero la aplicación no se puede conectar

* Garantizar la conectividad a Internet del dispositivo a través del explorador web del dispositivo.
* Si la aplicación nunca se ha conectado correctamente al servicio Assurance, asegúrese de que esté configurada correctamente para Assurance. Consulte las instrucciones de instalación de [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) Biblioteca de SDK.
* Compruebe que la sesión coincide con el vínculo y que se introduce correctamente en la sesión esperada. Consulte [Mensaje de registro &quot;La información de OrgID no está disponible&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (esto es poco común y relevante solo si tiene acceso a más de una instancia de ORG).

### Depuración de Adobe Analytics

**Estado posterior al procesamiento: sin indicador de depuración**

En la vista Eventos de Analytics, si los eventos fallan con el estado Posterior al procesamiento &quot;Sin indicador de depuración&quot;, es posible que la versión actual de Adobe Analytics o del SDK de Assurance no admita la función de depuración de Analytics.
Actualice las extensiones del SDK de Adobe Analytics y Assurance a las versiones más recientes para resolver este problema.

| Requisito mínimo de versión | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### Compatibilidad de React Native MobileCore y AEPAssurance

| Versión de AEP Assurance | Versión principal de Mobile | Instrucción de instalación |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-capcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Si está utilizando `react-native-acpcore` con Assurance, la aplicación React Native puede fallar al generar con uno de los siguientes mensajes de error:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

o

```
AppDelegate: AEPAssurance.h file not found
```

**Solución**

Si esto ocurre, reduzca su categoría `react-native-aepassurance` utilizando el siguiente comando npm:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Este error se produce porque la variable `react-native-acpcore` la extensión es **solamente** compatible con `react-native-aepassurance` versiones 2.x.x y posteriores.
