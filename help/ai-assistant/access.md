---
title: Acceso al asistente de IA (heredado) en Experience Platform
description: Obtenga información sobre cómo acceder al asistente de IA en la interfaz de usuario de Experience Cloud.
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: daaf3ff0218b73a9fd827ab2ef090d8046cef3bb
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# Acceso al asistente de IA (heredado) en Experience Platform

>[!IMPORTANT]
>
>Este documento se aplica al asistente de IA (heredado). Para obtener información sobre el asistente de IA (próxima generación), lee la [guía de la interfaz de usuario del asistente de IA](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) en la documentación de [AI en Experience Cloud](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/home).

Consulte la siguiente tabla para ver una comparación de AI Assistant (Legacy) y AI Assistant (Next-Gen):

| Área de funciones | Asistente de IA (heredado) | Asistente de IA (próxima generación) |
| --- | --- | --- |
| Experiencia del usuario | El asistente de IA (heredado) solo está disponible en un panel del carril derecho. | El asistente de IA (próxima generación) está disponible tanto en el panel derecho como en la experiencia de pantalla completa envolvente. |
| Ámbito de las capacidades | Puede utilizar el asistente de IA (heredado) para obtener conocimientos del producto y perspectivas operativas. | Puede utilizar el asistente de IA (próxima generación) para obtener conocimientos del producto, perspectivas operativas, así como habilidades agénticas avanzadas y ejecución de tareas de varios pasos. |
| Arquitectura de plataforma | El asistente de IA (heredado) no se crea en la pila de Agent Orchestrator. | El Asistente de IA (próxima generación) cuenta con la tecnología [Adobe Experience Platform Agent Orchestrator](https://experienceleague.adobe.com/es/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator), lo que permite la extensibilidad y la coordinación avanzada entre las distintas funcionalidades. |
| Cobertura de aplicación | El asistente de IA (heredado) es una implementación específica de la aplicación. | Puede utilizar el asistente de IA (próxima generación) para obtener una experiencia de asistente de IA unificada en todas las aplicaciones de Adobe Experience Cloud. |
| Modelo de acceso y permiso | Modelo de acceso con ámbito de aplicación alineado con los límites de cada producto. | Todos los usuarios tienen acceso al asistente de IA (próxima generación) y a los agentes de Experience Platform asociados. **Nota**: <ul><li>**Adobe Experience Manager**: el administrador debe concederle permiso para acceder al Asistente de IA (próxima generación) a través de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html).</li><li>**Customer Journey Analytics**: el administrador debe concederle permiso para acceder al Asistente de IA a través de [Control de acceso de Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/technotes/access-control?lang=en). Esto le permite hacer preguntas sobre el conocimiento del producto y las perspectivas de datos. |

Puede acceder al asistente de IA (heredado) en varias aplicaciones de Adobe Experience Cloud.

>[!NOTE]
>
>Si recibe un mensaje emergente en la interfaz de usuario de permisos que le informa de que su organización debe aceptar primero términos legales adicionales para obtener acceso al asistente de IA (heredado) y, a continuación, póngase en contacto con el equipo de su cuenta de Adobe para obtener instrucciones sobre estos términos.

## Introducción {#get-started}

Debe completar dos pasos previos para poder acceder al asistente de IA (heredado).

1. Su organización debe aceptar primero los términos legales. Para obtener más información, póngase en contacto con el equipo de cuenta de Adobe.
2. Los administradores deben concederle permisos suficientes para acceder al asistente de IA (heredado).

Si no ha completado ninguno de estos dos pasos previos, verá los siguientes mensajes cuando seleccione el icono de chat Asistente de IA (heredado) en la interfaz de usuario de Experience Platform.

>[!BEGINTABS]

>[!TAB Su organización no puede utilizar el Asistente para IA (heredado)]

Verá el siguiente mensaje si utiliza una organización que no cumple los requisitos legales para utilizar el asistente de IA (heredado). En esta situación, debe ponerse en contacto con el equipo de su cuenta de Adobe para resolver el acceso.

![Mensaje emergente que aparece en la interfaz de usuario de Experience Platform si la organización no puede utilizar el Asistente para IA (heredado).](./images/access/modal-one.png)

>[!TAB No cuenta con los permisos adecuados]

Si su organización cumple los requisitos legales para utilizar el asistente de IA (heredado) y aún no puede acceder a la función, verá el siguiente mensaje en la interfaz de usuario de Experience Platform. Este escenario significa que no tiene los permisos suficientes para acceder a la función y debe ponerse en contacto con los administradores para resolver los permisos.

![Mensaje emergente que aparece en la interfaz de usuario de Experience Platform si no tiene los permisos necesarios para el Asistente de IA (heredado).](./images/access/modal-two.png)

>[!ENDTABS]

## Obtener acceso al asistente de IA (heredado) {#get-access-to-ai-assistant}

El acceso al asistente de IA (heredado) se rige por los siguientes parámetros:

* **Acceda a la aplicación:** Puede acceder al Asistente de IA (heredado) en Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer y [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/ai-assistant).
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant (Legacy). Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant (Legacy).  -->
* **Permisos:** Use la [IU de permisos](../access-control/abac/ui/permissions.md) para conceder o revocar el acceso al Asistente de IA (heredado) en su organización. Para usar el Asistente de IA (heredado), un usuario dado debe pertenecer a un rol que esté aprovisionado con los permisos **Habilitar el Asistente de IA** y **Ver perspectivas operativas**.
   * Como administrador, puede agregar **Habilitar el asistente de IA** a una función determinada y agregar un usuario a esa función para permitirles acceder al asistente de IA (heredado) en su organización. **Nota**: Este permiso permite que dicho usuario acceda al Asistente de IA (heredado), no le otorga ninguna capacidad administrativa para luego dar a otros acceso al Asistente de IA (heredado).
   * Como administrador, puede agregar **Ver perspectivas operativas** a una función determinada y agregar un usuario a esa función, para permitirles utilizar las capacidades de perspectivas operativas del Asistente de IA (heredado).

Use la interfaz de usuario de [permisos](../access-control/abac/ui/roles.md) para conceder permisos para usar el Asistente de IA (heredado) en Experience Platform y Journey Optimizer. Para obtener información sobre cómo acceder al asistente de IA (heredado) en Customer Journey Analytics. Lea la documentación en [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/ai-assistant).

![La página de la interfaz de usuario de permisos con los permisos Habilitar el asistente de IA (heredado) y Ver las perspectivas operativas incluidos en una función determinada.](./images/access/access-permissions.png)

Una vez que tenga los permisos necesarios, podrá acceder al Asistente de IA (heredado) seleccionando el icono ![Asistente de IA (heredado)](/help/images/icons/ai-assistant.png) en el encabezado superior de la aplicación que está utilizando.

![Asistente de IA (heredado) con experiencia de usuario por primera vez.](./images/access/access-home.png)

Vea el siguiente vídeo para aprender a configurar el acceso al asistente de IA (heredado) para sus organizaciones y usuarios.

>[!VIDEO](https://video.tv.adobe.com/v/3436470/?learn=on)

## Próximos pasos

Una vez que tenga acceso completo al Asistente de IA (heredado), puede continuar usando la función durante sus flujos de trabajo. Lea la [guía de la interfaz de usuario del Asistente de IA (heredado)](./ui-guide.md) para obtener más información.
