---
keywords: administración de datos rtcdp;administración de datos rtcdp;administración de datos del perfil de datos del cliente en tiempo real
title: Información general sobre la administración de datos
seo-title: Administración de datos en la plataforma de datos del cliente en tiempo real
description: 'La Administración de datos le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. '
seo-description: 'La Administración de datos le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. '
translation-type: tm+mt
source-git-commit: 5435661d750c4138ea6a2d40619a48236b7b1e4f
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---


# [!DNL Data Governance] en tiempo real CDP

[!DNL Real-time Customer Data Platform] (CDP en tiempo real) aúna los datos de varios sistemas empresariales, lo que permite a los especialistas en mercadotecnia identificar, comprender y captar mejor a sus clientes. Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por las regulaciones legales. Por lo tanto, es importante asegurarse de que CDP en tiempo real cumpla con las políticas de uso al manejar sus datos.

Adobe Experience Platform [!DNL Data Governance] le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de CDP en tiempo real, permitiéndole definir políticas de uso, categorizar los datos en base a esas políticas y verificar las infracciones de políticas al realizar ciertas acciones de mercadotecnia.

CDP en tiempo real se basa en Adobe Experience Platform y, por lo tanto, la mayoría de las funcionalidades [!DNL Data Governance] se cubren en la documentación de [!DNL Experience Platform]. Este documento está diseñado para complementar la [información general de la administración de datos](../../data-governance/home.md) para [!DNL Experience Platform] y describe las características de la administración que están disponibles en tiempo real CDP. Se tratan los siguientes temas:

* [Aplicar etiquetas de uso a los datos](#labels)
* [Administrar directivas de uso de datos](#policies)
* [Aplicar el cumplimiento de uso de datos](#enforce)

## Aplicar etiquetas de uso a los datos {#labels}

[!DNL Data Governance] permite aplicar etiquetas de uso a los datos, ya sea en el nivel de conjunto de datos o campo de conjunto de datos. Las etiquetas de uso de datos permiten clasificar los datos según las políticas de uso que se aplican a esos datos.

Para obtener información detallada sobre cómo trabajar con etiquetas de uso de datos, consulte la [guía del usuario de etiquetas de uso de datos](../../data-governance/labels/overview.md) para Adobe Experience Platform.

## Configurar acciones de mercadotecnia para destinos {#destinations}

Puede establecer restricciones de uso de datos en un destino definiendo acciones de marketing (también denominadas casos de uso de marketing) para ese destino. Una acción de marketing para un destino indica la intención de los datos que se exportarán a ese destino.

>[!NOTE]
>
>Para obtener más información sobre las acciones de mercadotecnia y su uso en las políticas de uso de datos, consulte la [información general de las directivas de uso de datos](../../data-governance/policies/overview.md) en la documentación de [!DNL Experience Platform].

La definición de acciones de marketing en los destinos le permite asegurarse de que todos los perfiles o segmentos enviados a dichos destinos cumplen las directivas de uso de datos. Por lo tanto, debe agregar las acciones de mercadotecnia apropiadas a los destinos en función de las necesidades de su organización para aplicar restricciones de directiva en la activación.

Las acciones de marketing solo se pueden seleccionar al configurar un destino por primera vez. Según el tipo de destino con el que esté trabajando, la oportunidad de configurar acciones de marketing aparecerá en diferentes puntos del flujo de trabajo de configuración. Consulte la [documentación de destinos](../destinations/overview.md) para ver los pasos para configurar el destino en particular.

## Administrar directivas de uso de datos {#policies}

Para que las etiquetas de uso de datos admitan de manera efectiva el cumplimiento de los datos, las políticas de uso de datos deben definirse y habilitarse. Las políticas de uso de datos son reglas que describen los tipos de acciones de mercadotecnia que se le permite o se le restringe la realización de datos dentro de CDP en tiempo real. Consulte la sección &quot;Políticas de uso de datos&quot; en la [!DNL Experience Platform] [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información.

Adobe Experience Platform proporciona varias políticas principales para casos de uso comunes de la experiencia del cliente. Estas directivas se pueden ver en la interfaz de usuario navegando al espacio de trabajo **[!UICONTROL Directivas]** y seleccionando la ficha **[!UICONTROL Examinar]**. Consulte la [guía del usuario de directivas](../../data-governance/policies/user-guide.md) en la documentación de [!DNL Experience Platform] para ver los pasos más detallados sobre cómo trabajar con políticas en la interfaz de usuario, incluido cómo crear sus propias políticas personalizadas.

## Aplicar el cumplimiento del uso de datos {#enforce}

Una vez etiquetados los datos y definidas las políticas de uso, puede imponer el cumplimiento de las políticas en el uso de los datos. Al activar segmentos de audiencia en destinos en tiempo real CDP, [!DNL Data Governance] aplica automáticamente las políticas de uso en caso de que se produzcan infracciones.

Consulte el documento de [aplicación automática de políticas](../../data-governance/enforcement/auto-enforcement.md) para obtener más información.

## Pasos siguientes

Ahora que se le han presentado las características clave [!DNL Data Governance] en CDP en tiempo real y cómo [!DNL Experience Platform] las habilita, continúe con la [documentación para la Administración de datos en Adobe Experience Platform](../../data-governance/home.md). La documentación proporciona información general sobre conceptos [!DNL Data Governance] esenciales, así como flujos de trabajo paso a paso para administrar las políticas y etiquetas de uso de datos.

En el siguiente vídeo se ofrece una descripción general de [!DNL Data Governance] en tiempo real CDP, incluido el uso de casos de uso de mercadotecnia en destinos y flujos de trabajo de ejemplo para diferentes escenarios:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)