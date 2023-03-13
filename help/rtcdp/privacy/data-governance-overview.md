---
keywords: control de datos rtcdp;control de datos rtcdp;control de datos del perfil de datos del cliente en tiempo real
title: Resumen de gobernanza de datos
description: La gobernanza de datos le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Administración de datos en Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) reúne datos de varios sistemas empresariales, lo que permite a los especialistas en marketing identificar, comprender y captar mejor a sus clientes. Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por disposiciones legales. Por lo tanto, es importante asegurarse de que Real-Time CDP cumpla con las políticas de uso al administrar los datos.

Administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de Real-Time CDP, ya que le permite definir políticas de uso, categorizar los datos en función de esas políticas y comprobar violaciones de políticas al realizar determinadas acciones de marketing.

Real-Time CDP se basa en Adobe Experience Platform y, por lo tanto, la mayoría de las funciones de control de datos se tratan en la [!DNL Experience Platform] documentación. Este documento tiene por objeto complementar la [Resumen de gobernanza de datos](../../data-governance/home.md) para [!DNL Experience Platform], y describe las funciones de gobernanza disponibles en Real-Time CDP. Se tratan los siguientes temas:

* [Aplicar etiquetas de uso a los datos](#labels)
* [Administrar políticas de uso de datos](#policies)
* [Aplicar cumplimiento de uso de datos](#enforce)

## Aplicar etiquetas de uso a los datos {#labels}

El control de datos le permite aplicar etiquetas de uso a los datos, ya sea en el nivel de conjunto de datos o de campo. Las etiquetas de uso de datos le permiten categorizar los datos según las políticas de uso que se aplican a esos datos.

Para obtener información detallada sobre cómo trabajar con etiquetas de uso de datos, consulte la [guía del usuario sobre etiquetas de uso de datos](../../data-governance/labels/overview.md) para Adobe Experience Platform.

## Configuración de acciones de marketing para destinos {#destinations}

Puede establecer restricciones del uso de datos en un destino definiendo acciones de marketing (también denominadas casos de uso de marketing) para ese destino. Una acción de marketing para un destino indica la intención de los datos que se exportarán a ese destino.

>[!NOTE]
>
>Para obtener más información sobre las acciones de marketing y su uso en las políticas de uso de datos, consulte la [información general sobre políticas de uso de datos](../../data-governance/policies/overview.md) en el [!DNL Experience Platform] documentación.

La definición de acciones de marketing en destinos le permite asegurarse de que todos los perfiles o segmentos enviados a esos destinos sean compatibles con las políticas de uso de datos. Por lo tanto, debe agregar acciones de marketing adecuadas a los destinos en función de las necesidades de su organización para aplicar restricciones de política en la activación.

Las acciones de marketing solo se pueden seleccionar al configurar un destino por primera vez. Según el tipo de destino con el que trabaje, la oportunidad de configurar acciones de marketing se mostrará en diferentes puntos del flujo de trabajo de configuración. Consulte la [documentación de destinos](../destinations/overview.md) para ver los pasos sobre cómo configurar un destino concreto.

## Administrar políticas de uso de datos {#policies}

Para que las etiquetas de uso de datos respalden con eficacia el cumplimiento, las políticas de uso de datos deben definirse y habilitarse. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de Real-Time CDP. Consulte la sección &quot;Políticas de uso de datos&quot; en las [!DNL Experience Platform] [Resumen de gobernanza de datos](../../data-governance/home.md) para obtener más información.

Adobe Experience Platform proporciona varias políticas principales para casos de uso comunes de experiencias del cliente. Estas políticas se pueden ver en la interfaz de usuario navegando hasta **[!UICONTROL Políticas]** espacio de trabajo y seleccionar **[!UICONTROL Examinar]** pestaña. Consulte la [guía del usuario de directivas](../../data-governance/policies/user-guide.md) en el [!DNL Experience Platform] para ver los pasos más detallados sobre cómo trabajar con directivas en la interfaz de usuario de, incluido cómo crear sus propias directivas personalizadas.

## Aplicar cumplimiento de uso de datos {#enforce}

Una vez etiquetados los datos y definidas las políticas de uso, puede aplicar el cumplimiento de las políticas por el uso de datos. Al activar segmentos de audiencia en destinos en Real-Time CDP, la gobernanza de datos aplica automáticamente políticas de uso en caso de que se produzca alguna infracción.

Consulte el documento sobre [aplicación automática de políticas](../../data-governance/enforcement/auto-enforcement.md) para obtener más información.

## Pasos siguientes

Ahora que se le han presentado las funciones clave de control de datos en Real-Time CDP y cómo [!DNL Experience Platform] los habilita, continúe a la [Documentación de Administración de datos en Adobe Experience Platform](../../data-governance/home.md). La documentación proporciona información general sobre los conceptos esenciales de control de datos, así como flujos de trabajo paso a paso para administrar las etiquetas y políticas de uso de datos.

El siguiente vídeo proporciona información general sobre la gobernanza de datos en Real-Time CDP, incluido el uso de casos de uso de marketing en destinos y ejemplos de flujos de trabajo para diferentes situaciones:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
