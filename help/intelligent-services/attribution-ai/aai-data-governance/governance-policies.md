---
keywords: Experience Platform;guía del usuario;inteligencia artificial aplicada a la atribución;temas populares;controles de acceso;crear un modelo;
feature: Attribution AI
title: Políticas de gobernanza para el Attribution AI
description: Adobe Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados.
exl-id: 448b10c8-8eac-41cb-9b77-66aa283c0a9d
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Políticas de gobernanza

Una vez que haya pasado por el flujo de trabajo para crear un modelo y enviar su configuración, la variable [aplicación de políticas](../../../data-governance/enforcement/auto-enforcement.md) comprueba si hay alguna infracción. Si se produce una infracción de directiva, aparece una ventana emergente que indica que se han infringido una o más directivas. Esto sirve para garantizar que las operaciones de datos y las acciones de marketing de Platform cumplan con las políticas de uso de datos.

## Ventana emergente de infracción de directiva

[Una ventana emergente que muestra información sobre la infracción de directiva](../../attribution-ai/images/data-governance/policy-violation-popover-aai.png).

La ventana emergente proporciona información específica sobre la infracción. Puede resolver estas infracciones mediante la configuración de directivas y otras medidas que no estén directamente relacionadas con el flujo de trabajo de configuración. Por ejemplo, puede cambiar las etiquetas para que determinados campos puedan utilizarse con fines de ciencia de datos. Como alternativa, también puede modificar la propia configuración del modelo para que no utilice nada que tenga una etiqueta. Consulte la documentación para obtener más información sobre cómo configurar directivas.
