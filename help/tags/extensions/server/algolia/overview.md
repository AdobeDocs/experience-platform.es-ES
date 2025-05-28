---
title: Información general sobre la extensión Algolia Event Forwarding
description: Obtenga información sobre cómo configurar y utilizar la extensión de reenvío de eventos Algolia en Adobe Experience Platform. Reenvíe datos de comportamiento del usuario a través de la API de Insights, configure reglas, asigne campos XDM y verifique la entrega de eventos.
last-substantial-update: 2025-05-09T00:00:00Z
source-git-commit: d1b641ed0b48357a2f4b78d6829ccab52e4889ca
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---


# Información general sobre la extensión de reenvío de eventos [!DNL Algolia] {#overview}

>[!NOTE]
>
>Adobe Experience Platform Launch ahora forma parte de las tecnologías de recopilación de datos de Adobe Experience Platform. Como resultado, se han realizado actualizaciones terminológicas en toda la documentación del producto. Para obtener una lista completa de estos cambios, consulte la [guía de actualizaciones terminológicas](../../../../tags/term-updates.md).

Use [!DNL Algolia] para ofrecer experiencias de búsqueda rápidas, relevantes y personalizadas. Con la optimización con tecnología de IA, puede mejorar los resultados de búsqueda y las recomendaciones para ayudar a los usuarios a encontrar rápidamente los productos, el contenido o la información que necesitan.

Utilice la extensión de reenvío de eventos [!DNL Algolia] para enviar eventos de comportamiento de usuario a [!DNL Algolia] mediante [!DNL Insights API]. Estos datos de comportamiento habilitan recomendaciones impulsadas por IA, experiencias personalizadas y capacidades de búsqueda inteligente.

## Requisitos previos {#prerequisites}

Antes de instalar la extensión, asegúrese de que dispone de una cuenta de [!DNL Algolia] con acceso a [!DNL Insights API]. Si no tiene una cuenta, [regístrese](https://dashboard.algolia.com/users/sign_up) y habilite el acceso a la API.

Asegúrese también de comprender cómo usar [!DNL Algolia] [!DNL Insights API]. Para obtener información general sobre cómo enviar eventos, consulte [envío de eventos con la API de Insights](https://www.algolia.com/doc/guides/sending-events/getting-started/).

Recopile los siguientes valores de su tablero de cuenta de [!DNL Algolia]:
- **[!UICONTROL ID de aplicación]**
- **[!UICONTROL Clave de API de búsqueda]**
- **[!UICONTROL Nombre de índice]**

## Instalación de la extensión {#install}

Para instalar la extensión [!DNL Algolia], siga estos pasos:

Vaya a **[!UICONTROL Recopilación de datos]** en [!DNL Adobe Experience Platform]. Seleccione la ficha **[!UICONTROL Extensiones]**.

Abra **[!UICONTROL Catalog]**, busque la extensión **[!UICONTROL Reenvío de eventos de Algolia]** y, a continuación, seleccione **[!UICONTROL Instalar]**.

![Proceso de instalación de la extensión de reenvío de eventos de Algolia en Adobe Experience Platform](../../../images/extensions/server/algolia/install-extension.png)

### Configuración de la extensión {#configure-extension}

Para configurar la extensión de reenvío de eventos [!DNL Algolia], vaya a la pestaña **[!UICONTROL Extensiones]**, seleccione la extensión **[!UICONTROL Algolia]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

![Pantalla de configuración de la extensión de reenvío de eventos Algolia en Adobe Experience Platform](../../../images/extensions/server/algolia/configure.png)

| Propiedad | Descripción |
|----------|-------------|
| **[!UICONTROL ID de aplicación]** | Escriba el [!UICONTROL ID de aplicación] que se encuentra en el panel de Algolia en la sección [Claves de API](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Clave API de búsqueda]** | Escriba la [!UICONTROL clave de API de búsqueda] que se encuentra en el panel de Algolia en la sección [claves de API](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Nombre de índice]** | Escriba el [!UICONTROL Nombre de índice] que contiene sus productos o contenido. Este índice se utiliza como valor predeterminado. |

{style="table-layout:auto"}

## [!DNL Algolia] tipos de acciones de extensión de reenvío de eventos {#action-types}

La extensión de reenvío de eventos [!DNL Algolia] ofrece un único tipo de acción que se puede usar en la sección **[!UICONTROL Then]** de una regla:

### Enviar evento {#send-event}

Configure la acción **[!UICONTROL Enviar evento]** para reenviar eventos a [!DNL Algolia]:

Seleccione **[!UICONTROL Reglas]** > **[!UICONTROL Agregar regla]** o seleccione una regla existente. En la parte **[!UICONTROL Then]** de la regla, agrega una acción y selecciona **[!UICONTROL Extensión]**: [!DNL Algolia] Reenvío de eventos > **[!UICONTROL Tipo de acción]**: **[!UICONTROL Enviar eventos]**.

![Configuración de la acción Enviar evento en la extensión de reenvío de eventos de Algolia.](../../../images/extensions/server/algolia/send-event.png)

## Implementar el grupo de campos de evento [!DNL Algolia] {#algolia-field-group}

Asegúrese de agregar el grupo de campos de evento [!DNL Algolia] al esquema antes de usar la extensión de reenvío de eventos [!DNL Algolia]. Es uno de los grupos de campos estándar que se proporcionan a través de Experience Platform.

![Configuración del grupo de campos de eventos de Algolia](../../../images/extensions/server/algolia/algolia-field-groups.png)

### Agregar el grupo de campos de evento [!DNL Algolia] al esquema {#add-algolia-field-group}

Para agregar el grupo de campos de evento [!DNL Algolia]:

Vaya a **[!UICONTROL Esquemas]** y seleccione **[!UICONTROL Examinar]**.

Agrega un nuevo esquema o actualiza un esquema existente que uses para enviar eventos web y pasa el ratón sobre el icono **[!UICONTROL Agregar]**. Escriba *[!DNL Algolia]* en el cuadro de búsqueda para reducir los resultados.

Seleccione el botón **[!DNL Algolia]Detalles del evento** grupo de campos > **[!UICONTROL Agregar grupo de campos]** > **[!UICONTROL Guardar]**.

![Configuración del grupo de campos de perfil de Algolia en Experience Platform](../../../images/extensions/server/algolia/algolia-profile-field-group.png)

### Asignar y enviar datos con la etiqueta [!UICONTROL recopilación de datos]

La extensión de reenvío de eventos [!DNL Algolia] se puede usar con **[!DNL Adobe Experience Platform Web SDK]** para enviar datos del sitio web a [!DNL Algolia]. Para ello, cree una propiedad de etiqueta, asigne datos al objeto [!DNL XDM] y configure las reglas para enviar eventos.

#### Paso 1: Crear una propiedad de etiquetas con la web SDK

1. Cree una propiedad de etiqueta.
2. Instale la extensión [!DNL Adobe Experience Platform Web SDK].
3. Utilice esta extensión para asignar datos de HTML al grupo de campos **[!DNL Algolia]Evento**.

![Ejemplo de un conjunto de datos de HTML que se está asignando al grupo de campos de eventos Algolia](../../../images/extensions/server/algolia/html-dataset.png)

#### Paso 2: Crear un elemento de datos para la asignación [!DNL XDM]

1. Crear un [!UICONTROL elemento de datos] con **[!DNL Adobe Experience Platform Web SDK]**.
2. Seleccione **[!UICONTROL objeto XDM]** como tipo de elemento de datos.
3. Asigne los datos a los [!DNL XDM] campos apropiados, asegurándose de que se rellenen los campos específicos de [!DNL Algolia].

![](../../../images/extensions/server/algolia/xdm-mapping.png)

#### Paso 3: Crear una regla para enviar eventos

1. Cree una nueva regla en la propiedad de etiquetas.
2. Añada los déclencheur de evento necesarios, como la carga de página o los eventos de clic.
3. Agregar una acción mediante **[!DNL Adobe Experience Platform Web SDK]**.
4. Seleccione **[!UICONTROL Enviar evento]** como tipo de acción.
5. Configure la acción para utilizar el elemento de datos [!DNL XDM].

![Ejemplo de configuración de una acción de regla en la extensión de reenvío de eventos de Algolia](../../../images/extensions/server/algolia/rule-action.png)

#### Paso 4: Publicación y prueba

1. Publique las reglas y los cambios de extensión en el entorno de destino.
2. Use [!DNL Adobe Experience Platform Debugger] para comprobar que los datos se envían a Adobe Experience Platform y se reenvían a [!DNL Algolia].

![Configure una regla para enviar eventos con la extensión Algolia](../../../images/extensions/server/algolia/adobe-debugger.png)

### Verificar eventos en [!DNL Algolia]

Después de configurar la extensión de reenvío de eventos [!DNL Algolia], puede comprobar que los eventos se envían y reciben correctamente siguiendo estos pasos:

Vaya al panel de [!DNL Algolia] y luego a **[!UICONTROL Fuentes de datos > Eventos > Depurador]**.

Seleccione el evento que coincida con el evento enviado desde la extensión de reenvío de eventos de [!DNL Algolia] y compruebe que los datos esperados estén presentes en el evento.

![Verificar eventos en el depurador de Algolia](../../../images/extensions/server/algolia/algolia-debugger.png)

## Escenarios de implementación comunes

Utilice la extensión de reenvío de eventos [!DNL Algolia] para capturar y enviar datos de interacción del usuario en varios casos de uso, lo que mejora la relevancia y personalización de las búsquedas.

### Seguimiento de vistas de productos o contenido

Utilice la extensión para rastrear cuándo ven los usuarios las páginas de producto o contenido, lo que ayuda a [!DNL Algolia] a comprender los intereses de los usuarios.

### Seguimiento de eventos de conversión

Rastree eventos de complementos al carro de compras y otros eventos de conversión para optimizar las recomendaciones de [!DNL Algolia] que utilizan IA.

## Resolución de problemas

Si tiene problemas al implementar la extensión de reenvío de eventos [!DNL Algolia], siga estos pasos para la solución de problemas:

### Los eventos no aparecen en [!DNL Algolia]

Si los eventos no aparecen en [!DNL Algolia], compruebe lo siguiente:

- **Verificar credenciales de API**: Asegúrese de que el **[!UICONTROL ID de aplicación]** y la **[!UICONTROL clave de API]** coinciden con los valores del panel de [!DNL Algolia].
- **Comprobar el depurador de eventos**: use el depurador de eventos [!DNL Algolia] para confirmar si se reciben eventos. Si no es así, compruebe la configuración de reglas del reenvío de eventos.
- **Inspeccionar asignación XDM**: Asegúrese de que todos los campos obligatorios del esquema [!DNL Algolia] estén asignados correctamente en el objeto [!DNL XDM].

### Datos de evento incorrectos

- Asegúrese de que el elemento de datos del objeto [!DNL XDM] esté asignado con precisión al esquema [!DNL Algolia], con todos los campos obligatorios.
- Confirme que los parámetros de evento coinciden con el formato y la estructura esperados descritos en la documentación de la API de Insights de [!DNL Algolia].

## Pasos siguientes

En esta guía se explica cómo enviar datos a [!DNL Algolia] mediante [!DNL Algolia Event Forwarding Extension]. Para obtener más información sobre las capacidades de reenvío de eventos en [!DNL Adobe Experience Platform], lea la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).

Para obtener más información sobre cómo depurar la implementación con la herramienta de supervisión de Experience Platform Debugger y reenvío de eventos, lea la [descripción general de Adobe Experience Platform Debugger](../../../../debugger/home.md) y [Supervisar las actividades en el reenvío de eventos](../../../ui/event-forwarding/monitoring.md).

## Recursos adicionales

- [[!DNL Algolia] Documentación de la API de Insights](https://www.algolia.com/doc/rest-api/insights/)
- [[!DNL Algolia] Documentación de eventos](https://www.algolia.com/doc/guides/sending-events/getting-started/)
- [[!DNL Adobe Experience Platform] Documentación del reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)
- [[!DNL Algolia] Resumen de características de IA](https://www.algolia.com/products/ai-search/)
