---
title: Información general sobre la extensión Marketo Munchkin
description: Obtenga información acerca de la extensión de etiquetas de Munchkin de Marketo en Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 97%

---

# Información general sobre la extensión Munchkin de Marketo

Utilice esta extensión para integrar el código de seguimiento de JavaScript de [!DNL Marketo Munchkin] con la propiedad. El código JavaScript [!DNL Marketo Munchkin] permite rastrear las visitas y los clics de la página del usuario final en las páginas de destino de Marketo y en las páginas web externas.

## Instalación de la extensión Marketo Munchkin

Si la extensión [!DNL Marketo Munchkin] aún no está instalada, abra la propiedad, seleccione **[!UICONTROL Extensions > Catalog]**, pase el puntero por encima de la extensión [!DNL Marketo Munchkin] y seleccione **[!UICONTROL Install]**.

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
