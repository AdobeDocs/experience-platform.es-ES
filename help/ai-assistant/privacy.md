---
title: Privacidad, seguridad y administración en el asistente de IA
description: Obtenga información acerca de las prácticas de privacidad, seguridad y gobernanza de AI Assistant.
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: 1762fcbcc730ccb08340a71383c90404c3fea614
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Privacidad, seguridad y administración en el asistente de IA

El asistente de IA de Adobe Experience Platform está diseñado con privacidad, seguridad y administración en la vanguardia.

Lea este documento para obtener más información acerca de las capacidades centradas en la confianza del cliente que puede esperar de AI Assistant:

* En la actualidad, AI Assistant no utiliza datos personales, ni siquiera con fines formativos.
* El asistente de IA no tiene conocimiento de los datos de los consumidores.
* Todos los existentes [control de acceso](../access-control/home.md) El asistente de IA respetará las políticas.
   * Cualquier nueva política de control de acceso basada en atributos se reflejará en el asistente de IA después de un máximo de 24 horas*
* Se le debe otorgar permiso explícito para interactuar con el Ayudante de IA.
   * Puede definir permisos de forma diferente para Experience Platform y Journey Optimizer mediante el [IU de permisos](../access-control/abac/ui/permissions.md) y puede utilizar el [Admin Console](../access-control/ui/browse.md) para asignar permisos para el Customer Journey Analytics.
   * Los permisos son granulares y el administrador de la zona protegida puede configurar cuál de los usuarios puede hacer diferentes categorías de preguntas (preguntas basadas en el conocimiento del producto con el asistente de IA o preguntas sobre perspectivas operativas).
* El Asistente de IA es una función compatible con HIPAA y cumple con los requisitos de HIPAA en cuanto al procesamiento y uso de la Información médica protegida (PHI).
* Puede ver un registro de las interacciones anteriores con el asistente de IA con una política de retención de 30 días.
* El asistente de IA se basa en datos específicos de zonas protegidas y en la documentación de Adobe público al responder a las solicitudes de los usuarios. Los datos no se comparten en entornos limitados.
* Los mensajes que proporcione al asistente de IA no se comparten con otros clientes.


**Esto implica que si se añaden nuevas etiquetas a los campos y objetos o se crean nuevas políticas, el asistente de IA tardará hasta 24 horas en respetarlas. Durante esas 24 horas, los usuarios con acceso recién restringido aún pueden acceder a esos campos y objetos.*
