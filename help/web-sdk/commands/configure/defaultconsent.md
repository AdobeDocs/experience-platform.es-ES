---
title: defaultConsent
description: Establezca el método de recopilación de consentimiento predeterminado para su propiedad web.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 5%

---


# `defaultConsent`

La propiedad `defaultConsent` determina cómo se administra el consentimiento de recopilación de datos antes de llamar al comando [`setConsent`](../setconsent.md). Esta propiedad es valiosa cuando no desea recopilar accidentalmente datos de personas que residen en áreas en las que se requiere consentimiento antes de recopilar datos.

De forma predeterminada, los usuarios se incluyen en todos los propósitos y el SDK web puede realizar las siguientes tareas:

* Enviar datos desde y hacia los servidores de Adobe.
* Leer y escribir cookies o elementos de almacenamiento web.

Si los usuarios se excluyen de todos los propósitos, el SDK web no realiza ninguna de estas tareas.

La propiedad `defaultConsent` admite tres valores:

* **`in`**: la recopilación de datos se realiza de la forma habitual, hasta que el usuario se excluye.
* **`out`**: los datos se descartan permanentemente hasta que el usuario se incluye.
* **`pending`**: los datos se almacenan localmente hasta que el usuario decida participar usando el comando [`setConsent`](../setconsent.md). Cuando el consentimiento predeterminado para el propósito general está establecido en `pending`, al intentar ejecutar cualquier comando que dependa de las preferencias de inclusión del usuario (por ejemplo, el comando [`sendEvent`](../sendevent/overview.md)), el comando se pone en cola en el SDK web. Los comandos en cola no se procesan hasta que no haya comunicado las preferencias de inclusión del usuario al SDK web.

>[!NOTE]
>
> Los datos de consentimiento no persisten entre cargas de página.

Si tiene un visitante que no se encuentra dentro de la jurisdicción del Reglamento General de Protección de Datos (RGPD), el consentimiento predeterminado podría establecerse en `in`. Los visitantes dentro de la jurisdicción del RGPD pueden tener el consentimiento predeterminado establecido en `pending`. Su plataforma de administración de consentimiento (CMP) puede detectar la región del cliente y proporcionar el indicador `gdprApplies` a IAB TCF 2.0. Este indicador se puede utilizar para establecer el consentimiento predeterminado.

Si no desea recopilar los eventos que se produjeron antes de que se establecieran las preferencias de inclusión del usuario, puede pasar `"defaultConsent": "out"` durante la configuración del SDK web. El intento de ejecutar cualquier comando que dependa de las preferencias de inclusión del usuario no surtirá efecto hasta que haya comunicado las preferencias de inclusión del usuario al SDK web.

>[!NOTE]
>
>Actualmente, el SDK web solo admite un único propósito de todo o nada. Aunque planeamos crear un conjunto más sólido de propósitos o categorías que se correspondan con las diferentes capacidades de Adobe y ofertas de productos, la implementación actual es un enfoque de inclusión de todo o nada.  Esto solo se aplica a [!DNL Web SDK] y NO a otras bibliotecas de JavaScript de Adobe.

## Usando `defaultConsent` junto con `setConsent` {#using-consent}

El SDK web ofrece dos comandos de configuración de consentimiento complementarios:

* [`defaultConsent`](defaultconsent.md): este comando está diseñado para capturar las preferencias de consentimiento de los clientes de Adobe que utilizan el SDK web.
* [`setConsent`](../setconsent.md): este comando está diseñado para capturar las preferencias de consentimiento de los visitantes del sitio.

Cuando se utilizan juntos, esta configuración puede llevar a diferentes resultados de recopilación de datos y configuración de cookies, según sus valores configurados.

Consulte la tabla siguiente para comprender cuándo se produce la recopilación de datos y cuándo se configuran las cookies, según la configuración de consentimiento.

| defaultConsent | setConsent | Se produce la recopilación de datos | El SDK web establece cookies de explorador |
|---------|----------|---------|---------|
| `in` | `in` | Sí | Sí |
| `in` | `out` | No | Sí |
| `in` | Sin configurar | Sí | Sí |
| `pending` | `in` | Sí | Sí |
| `pending` | `out` | No | Sí |
| `pending` | Sin configurar | No | No |
| `out` | `in` | Sí | Sí |
| `out` | `out` | No | Sí |
| `out` | Sin configurar | No | No |

Las siguientes cookies se establecen cuando la configuración de consentimiento lo permite:

| Nombre | Edad máxima | Descripción |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 días) | Presente cuando [`idMigrationEnabled`](../configure/idmigrationenabled.md) está habilitado. Ayuda al realizar la transición al SDK web mientras algunas partes del sitio siguen utilizando `visitor.js`. |
| **Cookie Demdex** | 15552000 (180 días) | Presente si la sincronización de ID está habilitada. El Audience Manager establece esta cookie para asignar un ID único a un visitante del sitio. La cookie demdex ayuda a Audience Manager a realizar diversas funciones básicas, como la identificación del visitante, la sincronización de ID, la segmentación, el modelado, la creación de informes, etc. |
| **kndctr_orgid_cluster** | 1800 (30 minutos) | Almacena la región del Edge Network que sirve las solicitudes del usuario actual. La región se utiliza en la ruta URL para que el Edge Network pueda enrutar la solicitud a la región correcta. Si un usuario se conecta con una dirección IP diferente o en una sesión diferente, la solicitud se vuelve a dirigir a la región más cercana. |
| **kndct_orgid_identity** | 34128000 (395 días) | Almacena el ECID, así como otra información relacionada con el ECID. |
| **kndctr_orgid_permission** | 15552000 (180 días) | Almacena la preferencia de consentimiento de los usuarios para el sitio web. |
| **s_ecid** | 63115200 (2 años) | Contiene una copia del identificador de Experience Cloud ([!DNL ECID]) o del MID. El MID se almacena en un par de clave-valor que sigue esta sintaxis, `s_ecid=MCMID\|<ECID>`. |

## Definir consentimiento predeterminado con la extensión de etiqueta del SDK web

Seleccione el botón de opción deseado en **[!UICONTROL Consentimiento predeterminado]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Privacidad] y, a continuación, seleccione el **[!UICONTROL consentimiento predeterminado]** deseado.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

## Establecer el consentimiento predeterminado mediante la biblioteca de JavaScript del SDK web

Establezca la propiedad de cadena `defaultConsent` en el nivel de consentimiento deseado al ejecutar el comando `configure`. Esta propiedad distingue entre mayúsculas y minúsculas y sólo admite los tres valores siguientes: `"in"`, `"out"` y `"pending"`. Si intenta utilizar cualquier otro valor, la biblioteca genera un error.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
