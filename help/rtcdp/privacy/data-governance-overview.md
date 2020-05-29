---
title: Información general sobre la administración de datos
seo-title: Administración de datos en la plataforma de datos del cliente en tiempo real
description: 'La Administración de datos le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. '
seo-description: 'La Administración de datos le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. '
translation-type: tm+mt
source-git-commit: af7fa6048fa60392a98975fe6fc36e8302355a05
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---


# Administración de datos en tiempo real CDP

La plataforma de datos del cliente en tiempo real (CDP en tiempo real) reúne los datos de varios sistemas empresariales, lo que permite a los especialistas en mercadotecnia identificar, comprender y captar mejor a sus clientes. Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por las regulaciones legales. Por lo tanto, es importante asegurarse de que CDP en tiempo real cumpla con las políticas de uso al manejar sus datos.

El Gobierno de datos de la plataforma de experiencia de Adobe le permite administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de CDP en tiempo real, permitiéndole definir políticas de uso, categorizar los datos en base a esas políticas y verificar las infracciones de políticas al realizar ciertas acciones de mercadotecnia.

CDP en tiempo real se basa en la plataforma Adobe Experience y, por lo tanto, la mayoría de las funciones de administración de datos se incluyen en la documentación de la plataforma de experiencia. Este documento está diseñado para complementar la información general [sobre la gobernanza de](../../data-governance/home.md) datos para la plataforma de experiencia y describe las características de gobernanza disponibles en CDP en tiempo real. Se tratan los siguientes temas:

* [Aplicar etiquetas de uso a los datos](#labels)
* [Administrar directivas de uso de datos](#policies)
* [Aplicar el cumplimiento de uso de datos](#enforcement)

## Aplicar etiquetas de uso a los datos {#labels}

La Administración de datos permite aplicar etiquetas de uso a los datos, ya sea a nivel de conjunto de datos o campo de conjunto de datos. Las etiquetas de uso de datos permiten clasificar los datos según las políticas de uso que se aplican a esos datos.

Para obtener información detallada sobre cómo trabajar con etiquetas de uso de datos, consulte la guía [de usuario de etiquetas de uso de](../../data-governance/labels/overview.md) datos para Adobe Experience Platform.

## Establecer restricciones en destinos

Puede establecer restricciones de uso de datos en un destino definiendo casos de uso de mercadotecnia para ese destino. La definición de casos de uso para destinos permite comprobar si hay infracciones de directivas de uso y asegurarse de que los perfiles o segmentos enviados a ese destino son compatibles con las reglas de administración de datos.

Los casos de uso de marketing se pueden definir durante la fase de _configuración_ del flujo de trabajo de _edición de destino_ . Consulte la documentación de destino para obtener más información.


## Administrar directivas de uso de datos {#policies}

Para que las etiquetas de uso de datos admitan de manera efectiva el cumplimiento de los datos, las políticas de uso de datos deben definirse y habilitarse. Las políticas de uso de datos son reglas que describen los tipos de acciones de mercadotecnia que se le permite o se le restringe la realización de datos dentro de CDP en tiempo real. Consulte la sección &quot;Políticas de uso de datos&quot; en la descripción general [del Gobierno de](../../data-governance/home.md) datos de la plataforma de experiencia para obtener más información.

Adobe Experience Platform proporciona varias políticas **** principales para casos de uso comunes de la experiencia del cliente. Estas directivas se pueden ver realizando una solicitud a la [DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml), como se muestra en la sección &quot;Lista de todas las políticas&quot; de la guía [para desarrolladores de](../../data-governance/policies/overview.md)Policy Service. También puede crear sus propias políticas **** personalizadas para modelar las restricciones de uso personalizadas, como se muestra en la sección &quot;Crear una política&quot; de la guía para desarrolladores.

## (Beta) Aplicar el cumplimiento del uso de datos {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Esta función está en fase beta y no está disponible para todos los usuarios. Se puede habilitar si se solicita. La documentación y las funciones están sujetas a cambios.

Una vez etiquetados los datos y definidas las políticas de uso, puede imponer el cumplimiento de las políticas en el uso de los datos. Cuando se activan segmentos de audiencia a destinos en tiempo real CDP, la Administración de datos aplica automáticamente las políticas de uso en caso de que se produzcan infracciones.

El diagrama siguiente ilustra cómo se integra la aplicación de políticas en el flujo de datos de la activación de segmentos:

![](assets/enforcement-flow.png)

Cuando se activa un segmento por primera vez, el servicio de directivas DULE comprueba si hay infracciones de directivas en función de los siguientes factores:

* Las etiquetas de uso de datos aplicadas a los campos y conjuntos de datos dentro del segmento que se va a activar.
* El propósito de marketing del destino.

### Mensajes de infracción de directiva {#enforcement}

Si se produce una infracción de directiva al intentar activar un segmento (o [realizar modificaciones en un segmento](#policy-enforcement-for-activated-segments)ya activado), se evita la acción y aparece una ventana emergente que indica que se han infringido una o varias directivas. Seleccione una infracción de directiva en la columna izquierda de la ventana emergente para mostrar los detalles de dicha infracción.

![](assets/violation-popover.png)

La ficha *Detalles* de la ventana emergente indica la acción que activó la infracción y el motivo por el que se produjo la infracción, y proporciona sugerencias sobre cómo resolver el problema en forma potencial.

Haga clic en Línea **de datos** para rastrear los destinos, segmentos, políticas de combinación o conjuntos de datos cuyas etiquetas de datos activaron la infracción.

![](assets/data-lineage.png)

Una vez que se ha activado una infracción, el botón **Guardar** se desactiva para la activación hasta que se actualizan los componentes correspondientes para cumplir con las políticas de uso de datos.

### Aplicación de directivas para segmentos activados {#policy-enforcement-for-activated-segments}

La aplicación de políticas sigue aplicándose a los segmentos después de activarlos, lo que restringe cualquier cambio en un segmento o en su destino que pueda provocar una infracción de la política. Debido a los numerosos componentes involucrados en la activación de segmentos a destinos, cualquiera de las siguientes acciones puede potencialmente desencadenar una infracción:

* Actualización de etiquetas de uso de datos
* Cambio de conjuntos de datos para un segmento
* Cambio de predicados de segmentos
* Cambio de las configuraciones de destino

Si alguna de las acciones anteriores desencadena una infracción, se evita que se guarde esa acción y se muestra un mensaje de infracción de directiva, lo que garantiza que los segmentos activados sigan cumpliendo con las directivas de uso de datos al modificarse.

## Pasos siguientes

Ahora que ha sido presentado a las funciones clave de Gobierno de datos en CDP en tiempo real y cómo las habilita la plataforma de experiencia, continúe con la [documentación de Administración de datos en la plataforma](../../data-governance/home.md)de experiencia de Adobe. La documentación proporciona información general sobre los conceptos esenciales de la administración de datos, así como flujos de trabajo paso a paso para administrar las etiquetas y políticas de uso de datos.

El siguiente vídeo proporciona información general sobre la administración de datos en tiempo real de CDP, incluido el uso de casos de uso de mercadotecnia en destinos y flujos de trabajo de ejemplo para diferentes escenarios:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)