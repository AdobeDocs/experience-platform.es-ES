---
title: Implementación de la extensión de Adobe Experience Platform Assurance
description: En esta guía se explica cómo implementar e instalar la extensión de Adobe Experience Platform Assurance.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 100%

---

# Implementación de la extensión de Adobe Experience Platform Assurance

Este tutorial explica cómo instalar e implementar la extensión de Platform Assurance en el SDK móvil. Para obtener instrucciones sobre cómo agregar la extensión Assurance a la aplicación, lea la [Información general sobre la extensión Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Introducción

Para instalar e implementar la extensión de Assurance, necesitará acceso a los siguientes servicios:

- El [IU de recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Cree una propiedad móvil

>[!NOTE]
>
>Si ya tiene una propiedad móvil, puede continuar con el siguiente paso.

En la IU de recopilación de datos, seleccione **[!UICONTROL Etiquetas]**. Aparecerá una lista de propiedades móviles y web con información sobre las propiedades que pertenecen a su organización. Seleccionar **[!UICONTROL Nueva propiedad]** para crear una propiedad nueva.

![El botón Nueva propiedad aparece resaltado y muestra lo que selecciona para crear una nueva propiedad](./images/implement-assurance/create-new-property.png)

Aparece la página **[!UICONTROL Crear propiedad]**. Introduzca el nombre de la nueva propiedad y seleccione **[!UICONTROL Móvil]** como su plataforma. Después de insertar los detalles, seleccione **[!UICONTROL Guardar]** para crear la propiedad móvil.

>[!NOTE]
>
>La configuración de **[!UICONTROL Privacidad]** de la propiedad móvil **no** afecta a la recopilación de datos de Assurance.

![Se muestra la página Crear propiedad. Puede insertar información sobre su propiedad móvil aquí.](./images/implement-assurance/create-property.png)

## Instalación de la extensión de Assurance

Seleccione la propiedad móvil en la que desea instalar la extensión de Assurance.

![Se muestra la página Propiedades de la etiqueta con la propiedad móvil seleccionada resaltada.](./images/implement-assurance/select-mobile-property.png)

Aparece la página **detalles de la propiedad móvil**. Seleccionar **[!UICONTROL Extensiones]** para que aparezca una lista con las extensiones que están asociadas actualmente a su propiedad móvil.

![Se muestra la página de detalles de la propiedad móvil. Se muestra información sobre actividades recientes. La pestaña de extensiones está resaltada.](./images/implement-assurance/tag-properties.png)

Seleccionar **[!UICONTROL Catálogo]** para ver una lista de extensiones que puede agregar a la propiedad móvil. Mediante el filtro, busque la extensión **[!UICONTROL AEP Assurance]** y seleccione **[!UICONTROL Instalar]**.

![Se muestra el catálogo de extensiones. La extensión de Assurance se filtra y se muestra con el botón de instalación resaltado.](./images/implement-assurance/assurance-extension.png)

## Pasos siguientes

Ahora que ha instalado la extensión Assurance en su propiedad móvil, puede empezar a utilizar Assurance en sus aplicaciones. Para obtener información sobre cómo agregar la extensión Assurance a la aplicación, lea la [Información general sobre la extensión Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Para aprender a utilizar Assurance, lea la [Guía de uso de Assurance](./using-assurance.md).
