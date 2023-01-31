---
keywords: Experience Platform;guía del usuario;ai de atribución;temas populares;controles de acceso;crear un modelo;
feature: Attribution AI
title: Políticas de gobernanza para la Attribution AI
description: Adobe Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados.
source-git-commit: 2cce166592c4d4b7f9d62bc3385fb8ccdd74c958
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Políticas de gobernanza

Una vez que revise el flujo de trabajo para crear un modelo y enviar la configuración del modelo, la variable [aplicación de políticas](../../../data-governance/enforcement/auto-enforcement.md) comprueba si hay alguna infracción. Si se produce una infracción de política, aparece una ventana emergente que indica que se han violado una o más políticas. Esto sirve para garantizar que las operaciones de datos y las acciones de marketing dentro de Platform sean compatibles con las políticas de uso de datos.

## Entrega de infracciones de directivas

[Una ventana emergente que muestra información sobre la infracción de directiva](../../attribution-ai/images/data-governance/policy-violation-popover-aai.png).

La ventana emergente proporciona información específica sobre la infracción. Puede resolver estas infracciones mediante la configuración de directivas y otras medidas que no están directamente relacionadas con el flujo de trabajo de configuración. Por ejemplo, puede cambiar las etiquetas para que se puedan usar ciertos campos con fines científicos de datos. Como alternativa, también puede modificar la configuración del modelo en sí para que no use nada con una etiqueta en ella. Consulte la documentación para obtener más información sobre cómo configurar directivas.