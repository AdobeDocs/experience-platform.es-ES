---
title: Información general sobre la extensión de Adobe Experience Manager Forms
description: Obtenga información sobre la extensión de etiqueta Adobe Experience Manager Forms en Adobe Experience Platform.
source-git-commit: f31a1d2e84dee262e04f1db0415ffd76248ecb6c
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# Información general sobre la extensión de Adobe Experience Manager Forms

Este documento proporciona información general sobre la extensión de etiquetas Adobe Experience Manager Forms en Adobe Experience Platform.

## Eventos

La extensión proporciona los siguientes tipos de eventos:

1. **Renderización**: Déclencheur cuando el usuario procesa (abre) un formulario.
1. **Error**: Déclencheur cuando el usuario comete un error de validación en un formulario.
1. **Ayuda**: Déclencheur cuando el usuario hace clic en el icono de ayuda de un campo.
1. **Enviar**: Déclencheur en el envío de formulario.
1. **Visita** de campo: Déclencheur cuando se visita un campo.
1. **Abandono**: Déclencheur cuando el usuario cierra la pestaña o navega a una dirección URL diferente.
1. **Guardar**: Déclencheur cuando un formulario se guarda en portal.

>[!IMPORTANT]
>
>El suceso Save no está disponible actualmente para forms as a cloud service. Los eventos personalizados distribuidos por el editor de reglas en Forms adaptable se pueden capturar mediante el evento principal &quot;Capture custom event&quot;.

## Elementos de datos

La extensión proporciona varios elementos de datos que se pueden utilizar para enviar propiedades en llamadas de Analytics.

## Primeros pasos

Siga los pasos a continuación para comenzar con la extensión.

1. Instale la extensión de Adobe Experience Manager Forms desde el catálogo de extensiones. No se requiere ninguna configuración posterior a la instalación.
2. Instale y configure la [extensión de Adobe Analytics](../analytics/overview.md#Configure-the-Adobe-Analytics-extension).

## Creación de una regla

Una regla que utilice la extensión Forms de Experience Manager tendría el siguiente aspecto:

![Configuración de la acción](./images/rule.png)

Siga los pasos descritos a continuación para crear una regla similar para la implementación.

### Añadir un evento

1. Seleccione **Adobe Experience Manager Forms** en la lista desplegable de extensiones.
2. Seleccione el evento que desea capturar.

![Configuración de la acción](./images/AEM-forms-event.png)

### Añada una acción

1. Seleccione &quot;Adobe Analytics&quot; en la lista desplegable de extensiones.
2. Seleccione &quot;establecer variable&quot; en la lista desplegable Tipo de acción .
3. En la vista de configuración, elija las propiedades y los eventos que se enviarán.
4. Agregue una acción &quot;enviar señalización&quot; para enviar la llamada de análisis con eventos y propiedades establecidos en el paso 3
   ![Configuración de la acción](./images/AEM-forms-sendBeacon.png)
5. Agregue una acción &quot;clear variable&quot;.

![Configuración de la acción](./images/AEM-forms-action.png)