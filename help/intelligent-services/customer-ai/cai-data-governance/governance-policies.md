---
keywords: Experience Platform;guía de usuario;inteligencia artificial aplicada al cliente;temas populares;controles de acceso;crear modelo;
feature: Customer AI
title: Políticas de gobernanza para la inteligencia artificial aplicada al cliente
description: Adobe Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados.
exl-id: be3eca3a-0ea1-4b84-9454-675a4f9ac71e
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Políticas de gobernanza en Customer AI

Una vez completado el flujo de trabajo para crear un modelo y enviar su configuración, la variable [aplicación de políticas](/help/data-governance/enforcement/auto-enforcement.md) comprueba si hay alguna infracción. Si se produce una infracción de directiva, aparece una ventana emergente que indica que se han infringido una o más directivas. Esto sirve para garantizar que las operaciones de datos y las acciones de marketing de Platform cumplan con las políticas de uso de datos.

![Una ventana emergente que muestra información sobre la infracción de directiva](../images/user-guide/policy-violation-popover-cai.png).

La ventana emergente proporciona información específica sobre la infracción. Puede resolver estas infracciones mediante la configuración de directivas y otras medidas que no estén directamente relacionadas con el flujo de trabajo de configuración. Por ejemplo, puede cambiar las etiquetas para que determinados campos puedan utilizarse con fines de ciencia de datos. Como alternativa, también puede modificar la propia configuración del modelo para que no utilice nada que tenga una etiqueta. Consulte la documentación para obtener más información sobre cómo configurar [directivas](/help/data-governance/policies/overview.md).
