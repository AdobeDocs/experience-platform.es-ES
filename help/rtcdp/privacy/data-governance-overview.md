---
keywords: control de datos rtcdp;control de datos rtcdp;control de datos del perfil de datos del cliente en tiempo real
title: Información general sobre la administración de datos
description: 'La administración de datos permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. '
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Control de datos en tiempo real CDP

[!DNL Real-time Customer Data Platform] (CDP en tiempo real) aúna los datos de varios sistemas empresariales, lo que permite a los especialistas en marketing identificar, comprender y captar mejor a sus clientes. Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por las regulaciones legales. Por lo tanto, es importante asegurarse de que CDP en tiempo real cumpla con las políticas de uso cuando gestione sus datos.

La administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de CDP en tiempo real, permitiéndole definir políticas de uso, categorizar los datos en función de esas políticas y comprobar las infracciones de políticas al realizar ciertas acciones de marketing.

CDP en tiempo real se basa en Adobe Experience Platform y, por lo tanto, la mayoría de las funcionalidades de control de datos se incluyen en la [!DNL Experience Platform] documentación. El objetivo de este documento es complementar el [Información general sobre la administración de datos](../../data-governance/home.md) para [!DNL Experience Platform], y describe las funciones de administración disponibles en CDP en tiempo real. Se tratan los siguientes temas:

* [Aplicar etiquetas de uso a los datos](#labels)
* [Administrar políticas de uso de datos](#policies)
* [Cumplimiento del uso de datos](#enforce)

## Aplicar etiquetas de uso a los datos {#labels}

La administración de datos le permite aplicar etiquetas de uso a sus datos, ya sea en el nivel de conjunto de datos o de campo de conjunto de datos. Las etiquetas de uso de datos le permiten clasificar los datos según las políticas de uso que se aplican a esos datos.

Para obtener información detallada sobre cómo trabajar con etiquetas de uso de datos, consulte la [guía del usuario de etiquetas de uso de datos](../../data-governance/labels/overview.md) para Adobe Experience Platform.

## Configurar acciones de marketing para destinos {#destinations}

Puede establecer restricciones de uso de datos en un destino definiendo acciones de marketing (también denominadas casos de uso de marketing) para ese destino. Una acción de marketing para un destino indica la intención de los datos que se exportarán a ese destino.

>[!NOTE]
>
>Para obtener más información sobre las acciones de marketing y su uso en las políticas de uso de datos, consulte la [información general sobre las políticas de uso de datos](../../data-governance/policies/overview.md) en el [!DNL Experience Platform] documentación.

La definición de acciones de marketing en los destinos permite garantizar que todos los perfiles o segmentos enviados a esos destinos cumplan las políticas de uso de datos. Por lo tanto, debe agregar las acciones de marketing apropiadas a los destinos en función de las necesidades de su organización de aplicar restricciones de directiva en la activación.

Las acciones de marketing solo se pueden seleccionar al configurar un destino por primera vez. Según el tipo de destino con el que esté trabajando, la oportunidad de configurar acciones de marketing aparecerá en diferentes puntos del flujo de trabajo de configuración. Consulte la [documentación de destinos](../destinations/overview.md) para ver los pasos sobre cómo configurar un destino determinado.

## Administrar políticas de uso de datos {#policies}

Para que las etiquetas de uso de datos admitan de forma eficaz el cumplimiento de los datos, deben definirse y habilitarse las políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que puede realizar, o que están restringidas, en los datos dentro de CDP en tiempo real. Consulte la sección &quot;Políticas de uso de datos&quot; en la sección [!DNL Experience Platform] [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información.

Adobe Experience Platform proporciona varias políticas principales para casos de uso comunes de experiencias del cliente. Estas directivas se pueden ver en la interfaz de usuario navegando hasta el **[!UICONTROL Políticas]** espacio de trabajo y selección de la **[!UICONTROL Examinar]** pestaña . Consulte la [guía del usuario sobre directivas](../../data-governance/policies/user-guide.md) en el [!DNL Experience Platform] documentación para ver los pasos más detallados sobre cómo trabajar con políticas en la interfaz de usuario, incluido cómo crear sus propias políticas personalizadas.

## Cumplimiento del uso de datos {#enforce}

Una vez etiquetados los datos y definidas las políticas de uso, puede hacer cumplir las políticas de uso de los datos. Al activar segmentos de audiencia en destinos en tiempo real CDP, el control de datos aplica automáticamente las políticas de uso en caso de que se produzcan infracciones.

Consulte el documento en [aplicación automática de directivas](../../data-governance/enforcement/auto-enforcement.md) para obtener más información.

## Pasos siguientes

Ahora que ha sido introducido en las funciones clave de control de datos en CDP en tiempo real y en cómo [!DNL Experience Platform] los habilita, continúe con el [documentación de Control de datos en Adobe Experience Platform](../../data-governance/home.md). La documentación proporciona información general sobre conceptos esenciales de control de datos, así como flujos de trabajo paso a paso para administrar las etiquetas y políticas de uso de datos.

En el siguiente vídeo se ofrece una descripción general de la Gestión de datos en tiempo real de CDP, incluido el uso de casos de uso de marketing en destinos y flujos de trabajo de ejemplo para diferentes situaciones:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
