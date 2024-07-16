---
title: Información general sobre la extensión Marketo Munchkin
description: Obtenga información acerca de la extensión de etiquetas de Munchkin de Marketo en Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 89%

---

# Información general sobre la extensión Munchkin de Marketo

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Utilice esta extensión para integrar el código de seguimiento de JavaScript de [!DNL Marketo Munchkin] con la propiedad. El código JavaScript [!DNL Marketo Munchkin] permite rastrear las visitas y los clics de la página del usuario final en las páginas de destino de Marketo y en las páginas web externas.

## Instalación de la extensión Marketo Munchkin

Si la extensión [!DNL Marketo Munchkin] todavía no está instalada, abra su propiedad, seleccione **[!UICONTROL Extensiones > Catálogo]**, pase el cursor sobre la extensión [!DNL Marketo Munchkin] y seleccione **[!UICONTROL Instalar]**.

Esta extensión no tiene la configuración necesaria.

## Tipos de acciones de la extensión Marketo Munchkin

Esta sección describe los tipos de acción que están disponibles en la extensión [!DNL Marketo Munchkin].

### Inicializar

![](../../../images/munchkin-Init.png)

**Munchkin ID: (obligatorio)** Encontrará el ID de cuenta de Munchkin en el menú Administración > Integración > Menu de Munchkin.

**Configurations:** Todos los parámetros configurables se incluyen [aquí](https://developers.marketo.com/javascript-api/lead-tracking/configuration/).

### Visite la página web

![](../../../images/munchkin-visit-page.png)

**url: (obligatorio)** La ruta de archivo URL utilizada para registrar una visita a la página.

**params:** Una cadena de consulta de los parámetros deseados que se van a registrar.

**name:** Nombre personalizado del recurso de página web.

### Haga clic en el vínculo

![](../../../images/munchkin-click-link.png)

**href: (obligatorio)** ruta de archivo URL utilizada para registrar la selección de un vínculo.
