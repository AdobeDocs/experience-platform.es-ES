---
keywords: Experience Platform;guía del usuario;ai del cliente;temas populares;controles de acceso;crear modelo;
feature: Customer AI
title: Políticas de gobernanza para Customer AI
description: Adobe Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados.
source-git-commit: 66d20dc1141ff33211635ba74d320350f8b27fb7
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Políticas de gobernanza

Una vez completado el flujo de trabajo para crear un modelo y enviar la configuración del modelo, la variable [aplicación de políticas](/help/data-governance/enforcement/auto-enforcement.md) comprueba si hay alguna infracción. Si se produce una infracción de política, aparece una ventana emergente que indica que se han violado una o más políticas. Esto sirve para garantizar que las operaciones de datos y las acciones de marketing dentro de Platform sean compatibles con las políticas de uso de datos.

![Una ventana emergente que muestra información sobre la infracción de directiva](../images/user-guide/policy-violation-popover-cai.png).

La ventana emergente proporciona información específica sobre la infracción. Puede resolver estas infracciones mediante la configuración de directivas y otras medidas que no están directamente relacionadas con el flujo de trabajo de configuración. Por ejemplo, puede cambiar las etiquetas para que se puedan usar ciertos campos con fines científicos de datos. Como alternativa, también puede modificar la configuración del modelo en sí para que no use nada con una etiqueta en ella. Consulte la documentación para obtener más información sobre cómo configurar [políticas](/help/data-governance/policies/overview.md).