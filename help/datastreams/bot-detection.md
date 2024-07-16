---
title: Configuración de la detección de bots para flujos de datos
description: Aprenda a configurar la detección de bots para flujos de datos a fin de diferenciar el tráfico humano del no humano.
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: ff95e5e105f7b3e1213eab90456b9fa9000918d3
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---

# Configuración de la detección de bots para flujos de datos

El tráfico proveniente de entidades no humanas, como programas automatizados, raspadores web, arañas web o escáneres de secuencias de comandos, puede dificultar la identificación de eventos que ocurren desde visitantes humanos. Este tipo de tráfico puede afectar negativamente a métricas comerciales importantes, lo que provoca informes de tráfico incorrectos.

La detección de bots le permite identificar eventos generados por [SDK web](../web-sdk/home.md), [SDK móvil](https://developer.adobe.com/client-sdks/home/) y [[!DNL Server API]](../server-api/overview.md) como generados por arañas web y bots conocidos.

Al configurar la detección de bots para sus flujos de datos, puede identificar direcciones IP específicas, intervalos de IP y encabezados de solicitud que desee clasificar como eventos de bots.

La identificación del tráfico de bots puede proporcionar una medición más precisa de la actividad del usuario en el sitio o la aplicación móvil.

Cuando una solicitud al Edge Network coincide con cualquiera de las reglas de detección de bots, el esquema XDM se actualiza con una puntuación de bots (siempre establecida en 1), como se muestra a continuación.

```json
{
  "botDetection": {
    "score": 1
  }
}
```

Esta puntuación de bots ayuda a las soluciones que reciben la solicitud a identificar correctamente el tráfico de bots.

>[!IMPORTANT]
>
>La detección de bots no elimina ninguna solicitud de bots. Solo actualiza el esquema XDM con la puntuación de bots y reenvía el evento al [servicio de secuencia de datos](configure.md) que configuró.
>
>Las soluciones de Adobe pueden gestionar la puntuación de bots de diferentes maneras. Por ejemplo, Adobe Analytics usa su propio [servicio de filtrado de bots](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html) y no usa la puntuación establecida por el Edge Network. Los dos servicios usan la misma [lista de bots de la IAB](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), por lo que la puntuación de bots es idéntica.

Las reglas de detección de bots pueden tardar hasta 15 minutos en propagarse por el Edge Network una vez creadas.

## Requisitos previos {#prerequisites}

Para que la detección de bots funcione en la secuencia de datos, debe agregar el grupo de campos **[!UICONTROL Información de detección de bots]** al esquema. Consulte la documentación del [esquema XDM](../xdm/ui/resources/schemas.md#add-field-groups) para obtener información sobre cómo agregar campos y grupos a un esquema.

## Configuración de la detección de bots para flujos de datos {#configure}

Puede configurar la detección de bots después de crear una configuración de secuencia de datos. Consulte la documentación sobre cómo [crear y configurar un conjunto de datos](configure.md) y, a continuación, siga las instrucciones que se indican a continuación para agregar capacidades de detección de bots a su conjunto de datos.

Vaya a la lista de flujos de datos y seleccione el flujo de datos al que desea añadir la detección de bots.

![Interfaz de usuario de flujos de datos que muestra la lista de flujos de datos.](assets/bot-detection/datastream-list.png)

En la página de detalles de la secuencia de datos, seleccione la opción **[!UICONTROL Detección de bots]** en el carril derecho.

![Opción de detección de bots resaltada en la interfaz de usuario de flujos de datos.](assets/bot-detection/bot-detection.png)

Se muestra la página **[!UICONTROL Reglas de detección de bots]**.

![Configuración de detección de bots en la página de configuración de secuencia de datos.](assets/bot-detection/bot-detection-page.png)

Desde la página Reglas de detección de bots, puede configurar la detección de bots mediante las siguientes funcionalidades:

* Usando [!DNL [IAB/ABC International Spiders and Bots List]](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/).
* Creación de sus propias reglas de detección de bots.

### Utilice la Lista internacional de arañas web y bots de la IAB/ABC {#iab-list}

La [Lista internacional de arañas web y bots de la IAB/ABC](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) es una lista estándar de terceros de arañas web y bots, que le ayuda a identificar el tráfico automatizado, como rastreadores de motores de búsqueda, herramientas de supervisión y otro tráfico no humano, que es posible que no desee que aparezca en sus recuentos de análisis.

Para configurar la secuencia de datos para que use [!DNL IAB/ABC International Spiders and Bots List], active la opción **[!UICONTROL Usar la lista internacional de arañas web y bots de IAB/ABC para la detección de bots en esta secuencia de datos]** y, a continuación, seleccione Guardar para aplicar la configuración de detección de bots a la secuencia de datos.

![Lista de bots y arañas IAB habilitada.](assets/bot-detection/bot-detection-list.png)

### Creación de reglas de detección de bots {#rules}

Además de usar la [Lista internacional de arañas web y bots de IAB/ABC](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), puede definir sus propias reglas de detección de bots para cada secuencia de datos.

Puede crear reglas de detección de bots basadas en **direcciones IP** e **intervalos de direcciones IP**.

Si necesita reglas de detección de bots más granulares, puede combinar las condiciones de IP con condiciones de encabezado de solicitud. Las reglas de detección de bots pueden utilizar los siguientes encabezados:

| Encabezado HTTP | Descripción |
| --- | --- |
| `user-agent` | Un encabezado que permite a los servidores y a los iguales de red identificar la aplicación, el sistema operativo, el proveedor y la versión del agente de usuario solicitante. |
| `content-type` | Indica el tipo de medio original del recurso (antes de cualquier codificación de contenido aplicada para el envío). |
| `referer` | Identifica la dirección de la página web desde la que se ha solicitado el recurso. |
| `sec-ch-ua` | Proporciona la marca y la versión significativa de cada marca asociada con el explorador en una lista separada por comas. |
| `sec-ch-ua-mobile` | Indica si el explorador está en un dispositivo móvil. También lo puede utilizar un explorador de escritorio para indicar una preferencia por una experiencia de usuario móvil. |
| `sec-ch-ua-platform` | Proporciona la plataforma o el sistema operativo en los que se está ejecutando el agente de usuario. Por ejemplo: &quot;Windows&quot; o &quot;Android&quot;. |
| `sec-ch-ua-platform-version` | Proporciona la versión del sistema operativo en el que se está ejecutando el agente de usuario. |
| `sec-ch-ua-arch` | Proporciona la arquitectura de CPU subyacente del agente de usuario, como ARM o x86. |
| `sec-ch-ua-model` | Indica el modelo de dispositivo en el que se está ejecutando el explorador. |
| `sec-ch-ua-bitness` | Proporciona el &quot;bit&quot; de la arquitectura de CPU subyacente del agente de usuario. Es el tamaño en bits de un número entero o dirección de memoria, normalmente 64 o 32 bits. |
| `sec-ch-ua-wow64` | Indica si un binario de agente de usuario se está ejecutando en modo de 32 bits en Windows de 64 bits. |

Para crear una regla de detección de bots, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Agregar nueva regla]**.

   ![Pantalla de configuración de detección de bots con el botón Agregar nueva regla resaltado.](assets/bot-detection/bot-detection-new-rule.png)

2. Escriba un nombre para la regla en el campo **[!UICONTROL Nombre de regla]**.

   ![Pantalla de regla de detección de bots con el nombre de regla resaltado.](assets/bot-detection/rule-name.png)

3. Seleccione **[!UICONTROL Agregar nueva condición de IP]** para agregar una nueva regla basada en IP. Puede definir la regla por dirección IP o por intervalo de direcciones IP.

   ![Pantalla de regla de detección de bots con el campo de dirección IP resaltado.](assets/bot-detection/ip-address-rule.png)

   ![Pantalla de regla de detección de bots con el campo de intervalo de IP resaltado.](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >Las condiciones de IP se basan en una operación `OR` lógica. Una solicitud se marca como originada en un bot si coincide con cualquiera de las condiciones de IP definidas.

4. Si desea agregar condiciones de encabezado a la regla, seleccione **[!UICONTROL Agregar grupo de condiciones de encabezado]** y, a continuación, seleccione los encabezados que desea que utilice la regla.

   ![Pantalla de regla de detección de bots con las condiciones de encabezado resaltadas.](assets/bot-detection/header-conditions.png)

   A continuación, añada las condiciones que desea utilizar para el encabezado seleccionado.

   ![Pantalla de regla de detección de bots con las condiciones de encabezado resaltadas.](assets/bot-detection/header-condition-rule.png)

5. Después de configurar las reglas de detección de bots que desee, seleccione **[!UICONTROL Guardar]** para que se apliquen las reglas a su secuencia de datos.

   ![Pantalla de regla de detección de bots con las condiciones de encabezado resaltadas.](assets/bot-detection/bot-detection-save.png)


## Ejemplos de reglas de detección de bots {#examples}

Para empezar a utilizar la detección de bots, puede utilizar los ejemplos detallados a continuación para crear reglas de detección de bots.

### Detección de bots basada en una dirección IP {#one-ip}

Para marcar todas las solicitudes procedentes de una dirección IP específica como tráfico de bots, cree una nueva regla de detección de bots que evalúe una sola dirección IP, como se muestra en la imagen siguiente.

![Regla de detección de bots basada en una dirección IP.](assets/bot-detection/bot-detection-one-ip.png)

### Detección de bots basada en dos direcciones IP {#two-ip}

Para marcar todas las solicitudes procedentes de cualquiera de las dos direcciones IP específicas como tráfico de bots, cree una nueva regla de detección de bots que evalúe dos direcciones IP, como se muestra en la siguiente imagen.

![Regla de detección de bots basada en dos direcciones IP.](assets/bot-detection/bot-detection-two-ips.png)

### Detección de bots basada en un intervalo de direcciones IP {#range}

Para marcar todas las solicitudes procedentes de cualquier dirección IP de un intervalo específico como tráfico de bots, cree una nueva regla de detección de bots que evalúe un intervalo de direcciones IP completo, como se muestra en la siguiente imagen.

![Regla de detección de bots basada en el intervalo de IP.](assets/bot-detection/bot-detection-range.png)

### Detección de bots basada en una dirección IP y un encabezado de solicitud {#ip-header}

Para marcar todas las solicitudes procedentes de una dirección IP específica y que contengan un encabezado de solicitud específico como tráfico de bots, cree una nueva regla de detección de bots como se muestra en la imagen siguiente.

Esta regla comprueba si la solicitud se origina desde una dirección IP específica y si el encabezado de solicitud `referer` comienza con `www.adobe.com`.

![Regla de detección de bots basada en la dirección IP y el encabezado de solicitud.](assets/bot-detection/bot-detection-header-ip.png)

### Detección de bots basada en varias condiciones {#multiple-conditions}

Puede crear reglas de detección de bots basadas en lo siguiente:

* **Varias condiciones diferentes**: Las distintas condiciones se evalúan como una operación lógica `AND`, lo que significa que las condiciones deben cumplirse simultáneamente para que se pueda identificar la solicitud como originada en un bot.
* **Varias condiciones del mismo tipo**: Las condiciones del mismo tipo se evalúan como una operación lógica `OR`, lo que significa que si se cumple cualquiera de las condiciones, se identifica que la solicitud se origina desde un bot.

La regla que se muestra en la siguiente imagen identifica una solicitud de origen de bots si se cumplen las siguientes condiciones:

La solicitud se origina desde cualquiera de las dos direcciones IP, el encabezado `referer` comienza con `www.adobe.com` y el encabezado `sec-ch-ua-mobile` identifica la solicitud como originada desde un explorador de escritorio.

![Regla de detección de bots basada en varias condiciones.](assets/bot-detection/bot-detection-multiple.png)
