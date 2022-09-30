---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;
title: Información general sobre el control de acceso basado en atributos
description: Este documento proporciona información sobre el control de acceso basado en atributos en Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 1%

---

# Resumen del control de acceso basado en atributos

El control de acceso basado en atributos es una función de Adobe Experience Platform que permite a los administradores controlar el acceso a objetos específicos o a funciones basadas en atributos. Los atributos pueden ser metadatos agregados a un objeto, como una etiqueta agregada a un campo o segmento de esquema. Un administrador define políticas de acceso que incluyen atributos para administrar los permisos de acceso de los usuarios.

Esta funcionalidad le permite etiquetar campos de esquema del Modelo de datos de experiencia (XDM) con etiquetas que definen ámbitos organizativos o de uso de datos. En paralelo, los administradores pueden utilizar la interfaz de administración de usuarios y funciones para definir las políticas de acceso que rodean los campos de esquema XDM y administrar mejor el acceso dado a los usuarios o grupos de usuarios (usuarios internos, externos o de terceros). Además, el control de acceso basado en atributos permite a los administradores administrar el acceso a segmentos específicos.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a datos personales confidenciales (SPD), información de identificación personal (PII) y tipo personalizado de datos en todos los flujos de trabajo y recursos de Platform. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que se correspondan con esos campos.

## Terminología de control de acceso basado en atributos

El control de acceso basado en atributos implica los siguientes componentes:

| Terminología | Definición |
| --- | --- |
| Atributos | Los atributos son identificadores que indican la correlación entre un usuario y los recursos de Platform a los que tiene acceso. Los atributos pueden ser metadatos agregados a un objeto, como una etiqueta agregada a un campo o segmento de esquema. Un administrador define políticas de acceso que incluyen atributos para administrar los permisos de acceso de los usuarios. |
| Etiquetas | Las etiquetas permiten categorizar los conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que elige administrar los datos. Las prácticas recomendadas recomiendan el etiquetado de datos tan pronto como se incorporen a Platform o tan pronto como los datos estén disponibles para su uso en Platform. |
| Permisos | Los permisos incluyen la capacidad de ver o usar funciones de Platform, como la creación de entornos limitados, la definición de esquemas y la administración de conjuntos de datos. |
| Conjuntos de permisos | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contenga un grupo de permisos. |
| Políticas | Las políticas son declaraciones que reúnen atributos para establecer acciones permisibles e inadmisibles. Las políticas pueden ser locales o globales y pueden anular otras directivas. |
| Recurso | Un recurso es el recurso o objeto al que un sujeto puede acceder o no. Los recursos pueden ser segmentos o campos de esquema. |
| Funciones | Las funciones son formas de categorizar los tipos de usuarios que interactúan con la instancia de Platform y que son componentes básicos de las políticas de control de acceso. En un entorno de control de acceso basado en roles, el aprovisionamiento de acceso de los usuarios se agrupa a través de responsabilidades y necesidades comunes. Una función tiene un conjunto determinado de permisos y los miembros de su organización pueden asignarse a una o más funciones, según el ámbito de vista o acceso de escritura que necesiten. |
| Asunto | Un asunto es el usuario que solicita acceso a un recurso para realizar una acción. |
| Grupos de usuarios | Los grupos de usuarios son varios usuarios que se han agrupado y tienen acceso para ejecutar las mismas funciones. |

## Permisos

>[!IMPORTANT]
>
>Una vez que su organización esté habilitada para el control de acceso basado en atributos, puede empezar a utilizar Permisos en Adobe Experience Cloud, en lugar de Perfiles de producto en Adobe Admin Console, para administrar permisos para usuarios, funcionalidad, etiquetas y otros recursos de su organización.

Los permisos son el área del Experience Cloud en la que los administradores pueden definir funciones de usuario y políticas de acceso para administrar los permisos de acceso a funciones y objetos dentro de una aplicación de producto.

Mediante Permisos, puede crear y administrar funciones, así como asignar los permisos de recursos deseados para estas funciones. Los permisos también le permiten administrar las etiquetas, los entornos limitados y los usuarios asociados a una función específica. Para obtener más información, consulte la [Guía de permisos](ui/browse.md).

## API de control de acceso basado en atributos

La API de control de acceso basada en atributos le permite administrar mediante programación funciones, políticas y productos en Platform mediante API. Para obtener más información, consulte la guía de [uso de la API para administrar configuraciones de control de acceso basadas en atributos](api/overview.md).

## Control de acceso basado en atributos en Adobe Experience Platform

Las secciones siguientes proporcionan información sobre cómo se integra el control de acceso basado en atributos en otros componentes de Platform:

### Control de acceso

Aprovechamientos de la plataforma [Adobe Admin Console](https://adminconsole.adobe.com) perfiles de producto para vincular usuarios con permisos y entornos limitados. Los permisos controlan el acceso a una variedad de funcionalidades de Platform, que incluyen modelado de datos, administración de perfiles y administración de entornos limitados. Una vez que su organización esté habilitada para el control de acceso basado en atributos, puede empezar a utilizar Permisos en Adobe Experience Cloud, en lugar de Perfiles de producto en Adobe Admin Console, para administrar permisos para usuarios, funcionalidad, etiquetas y otros recursos de su organización.

Para obtener más información sobre el control de acceso, consulte la [información general sobre el control de acceso](../home.md).

### Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos desde Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

Como administrador, puede utilizar funcionalidades de control de acceso basadas en atributos para:

* Configure el acceso de los usuarios para ver segmentos específicos en el proceso de activación, según la función, los permisos y las etiquetas;
   * En el proceso de activación, es posible que los usuarios tengan que seleccionar los segmentos que desean activar en un destino. Como administrador, puede aprovisionar usuarios de su organización para que solo vean segmentos etiquetados con etiquetas a las que los usuarios tienen acceso y segmentos que no contienen etiquetas.
* Configure el acceso del usuario para ver campos específicos en el proceso de activación, según la función, los permisos y las etiquetas;
   * En el proceso de activación, es posible que los usuarios tengan que seleccionar los campos que desean activar en un destino. Como administrador, puede aprovisionar usuarios de su organización para que solo vean campos etiquetados con etiquetas a las que los usuarios tienen acceso y campos que no contienen etiquetas.

>[!IMPORTANT]
>
>En resumen, tenga en cuenta las siguientes implicaciones al trabajar con destinos y control de acceso basado en atributos:
>
>* Solo puede activar segmentos a los que tenga permiso para acceder y ver en el [vista de exploración de segmentos](/help/segmentation/ui/overview.md#browse) y [seleccionar paso de segmento](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) del flujo de trabajo de activación.
>* En el [paso de asignación del flujo de trabajo de activación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), solo puede ver y seleccionar para la activación los campos a los que tiene permiso de acceso.
>* Cuando busque activar segmentos adicionales en un destino existente donde no tenga acceso a todos los campos asignados para la exportación, el flujo de trabajo de activación se bloqueará por usted.


Para obtener más información, consulte [!DNL Destinations], consulte [[!DNL Destinations] información general](../../destinations/home.md).

### Servicio de identidad

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.

Como parte del control de acceso basado en atributos, la variable `view-identity-graph` permite determinar qué usuarios de su organización pueden acceder al gráfico de identidad a través de la interfaz de usuario o las API. Para obtener más información, consulte la guía de [uso del visor de gráficos de identidad](../../identity-service/ui/identity-graph-viewer.md).

Para obtener más información, consulte [!DNL Identity Service], consulte [[!DNL Identity Service] información general](../../identity-service/home.md).

### Perfil del cliente en tiempo real

Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar sus diferentes datos de clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

Como administrador, puede utilizar funcionalidades de control de acceso basadas en atributos para:

* Configure el acceso del usuario a atributos de perfil específicos en función de las funciones, los permisos y las etiquetas;
   * Como administrador, puede aprovisionar a los usuarios de su organización para que solo vean atributos de perfil etiquetados con etiquetas a las que los usuarios tienen acceso y atributos de perfil que no contienen ninguna etiqueta;
   * Como administrador, puede aprovisionar a los usuarios de su organización para que solo vean los atributos de perfil etiquetados con etiquetas a las que los usuarios tienen acceso al crear segmentos;
* Configure el acceso del usuario a la vista previa de los datos mediante el etiquetado de campos de datos específicos utilizados en el esquema XDM del modelo de datos.

Para obtener más información sobre Perfil, consulte la [Información general del perfil](../../profile/home.md).

### Servicio de segmentación

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

Como administrador, puede utilizar funcionalidades de control de acceso basadas en atributos para:

* Configure el acceso de los usuarios para ver y administrar segmentos específicos, según la función, los permisos y las etiquetas;
   * Como administrador, puede aprovisionar usuarios de su organización para que solo vean segmentos etiquetados con etiquetas a las que los usuarios tienen acceso y segmentos que no contienen etiquetas, al usar la interfaz de usuario de segmentación.

Para obtener más información, consulte [!DNL Segmentation Service], consulte [[!DNL Segmentation Service] información general](../../segmentation/home.md).

### XDM

Experience Data Model (XDM) es una especificación de código abierto diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios en Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

Con el control de acceso basado en atributos, puede:

* [Aplicación de etiquetas de uso de datos a grupos de campos y clases](../../xdm/tutorials/labels.md). Esto permite que varios esquemas con los mismos grupos de campos o clases tengan campos etiquetados con los mismos atributos, dependiendo de las configuraciones en el grupo de campos o nivel de clase;
* Configure el acceso del usuario a campos de esquema XDM específicos en función de los conjuntos de permisos aplicados a las funciones asignadas a los usuarios.

Para obtener más información sobre XDM, consulte la [Información general de XDM](../../xdm/home.md).