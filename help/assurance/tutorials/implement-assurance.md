---
title: Implementación de la extensión de Adobe Experience Platform Assurance
description: Esta guía explica cómo implementar e instalar la extensión de Adobe Experience Platform Assurance.
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---


# Implementación de la extensión de Adobe Experience Platform Assurance

Este tutorial explica cómo instalar e implementar la extensión Platform Assurance en el SDK móvil. Para obtener instrucciones sobre cómo añadir la extensión de Assurance a su aplicación, lea la [Información general sobre la extensión de Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Primeros pasos

Para instalar e implementar la extensión de Assurance, necesita acceder a los siguientes servicios:

- La variable [Interfaz de usuario de recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Cree una propiedad móvil

>[!NOTE]
>
>Si ya tiene una propiedad móvil, puede continuar con el siguiente paso.

En la interfaz de usuario de la recopilación de datos, seleccione **[!UICONTROL Etiquetas]**. Aparece una lista de propiedades móviles y web, con información sobre las propiedades que pertenecen a su organización. Select **[!UICONTROL Nueva propiedad]** para crear una nueva propiedad.

![Se resalta el botón New property , que muestra lo que se selecciona para crear una nueva propiedad](./images/implement-assurance/create-new-property.png)

La variable **[!UICONTROL Crear propiedad]** se abre. Introduzca el nombre de la nueva propiedad y seleccione **[!UICONTROL Móvil]** como plataforma. Después de insertar los detalles, seleccione **[!UICONTROL Guardar]** para crear la propiedad móvil.

>[!NOTE]
>
>La propiedad móvil **[!UICONTROL Privacidad]** establecer hace **not** afectan a la recopilación de datos de Assurance.

![Se muestra la página Crear propiedad . Puede insertar información sobre su propiedad móvil aquí.](./images/implement-assurance/create-property.png)

## Instalación de la extensión de Assurance

Seleccione la propiedad móvil en la que desea instalar la extensión Assurance.

![Se muestra la página Propiedades de la etiqueta , con la propiedad móvil seleccionada resaltada.](./images/implement-assurance/select-mobile-property.png)

La variable **detalles de propiedad móvil** se abre. Select **[!UICONTROL Extensiones]** para que aparezca una lista de las extensiones que están asociadas actualmente a su propiedad móvil.

![Se muestra la página de detalles de la propiedad móvil. Se muestra información sobre actividades recientes. La pestaña de extensiones está resaltada.](./images/implement-assurance/tag-properties.png)

Select **[!UICONTROL Catálogo]** para ver una lista de extensiones que puede agregar a la propiedad móvil. Con el filtro, busque la variable **[!UICONTROL AEP Assurance]** y seleccione **[!UICONTROL Instalar]**.

![Se muestra el catálogo de extensiones. La extensión Assurance se filtra y se muestra, con el botón de instalación resaltado.](./images/implement-assurance/assurance-extension.png)

## Pasos siguientes

Ahora que ha instalado la extensión Assurance en su propiedad móvil, puede empezar a utilizar Assurance en sus aplicaciones. Para obtener información sobre cómo añadir la extensión de Assurance a la aplicación, lea la [Información general sobre la extensión de Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Para aprender a utilizar Assurance, lea la [uso de la guía de Assurance](./using-assurance.md).
