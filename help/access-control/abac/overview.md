---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;
title: Resumen de control de acceso basado en atributos
description: Este documento proporciona información sobre el control de acceso basado en atributos en Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: 900e0dc323e9055a92313788a4a191c615d0b8cd
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Información general de control de acceso basado en atributos {#attribute-based-access-control-overview}

>[!CONTEXTUALHELP]
>id="platform_accesscontrol_abac_labelusageaccesspolicy"
>title="Política de acceso al uso de etiquetas"
>abstract=""

El control de acceso basado en atributos es una capacidad de Adobe Experience Platform que permite a los administradores controlar el acceso a objetos específicos o a funcionalidades basadas en atributos. Los atributos pueden ser metadatos añadidos a un objeto, como una etiqueta añadida a un campo o segmento de esquema. Un administrador define directivas de acceso que incluyen atributos para administrar permisos de acceso de usuarios.

Utilice esta funcionalidad para etiquetar campos de esquema del Modelo de datos de experiencia (XDM) con etiquetas que definen ámbitos organizativos o de uso de datos. En paralelo, los administradores pueden utilizar la interfaz de administración de usuarios y funciones para definir políticas de acceso alrededor de los campos de esquema XDM y administrar mejor el acceso dado a usuarios o grupos de usuarios (usuarios internos, externos o de terceros). Además, el control de acceso basado en atributos permite a los administradores gestionar el acceso a segmentos específicos.

>[!IMPORTANT]
>
>El control de acceso basado en atributos no se debe confundir con las capacidades de control de datos de Experience Platform, que le permiten utilizar etiquetas y directivas para controlar cómo se utilizan los datos en Platform en lugar de qué usuarios de su organización tienen acceso a ellos. Consulte la [información general sobre gobernanza de datos](../../data-governance/home.md) para obtener más información.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a los datos personales confidenciales (SPD), la información de identificación personal (PII) y el tipo personalizado de datos en todos los flujos de trabajo y recursos de la plataforma. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que correspondan a esos campos.

El siguiente vídeo tiene como objetivo facilitar la comprensión del control de acceso basado en atributos y describe cómo configurar funciones, recursos y directivas.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)

## Terminología de control de acceso basado en atributos

El control de acceso basado en atributos implica los siguientes componentes:

| Terminología | Definición |
| --- | --- |
| Atributos | Los atributos son identificadores que indican la correlación entre un usuario y los recursos de Platform a los que tiene acceso. Los atributos pueden ser metadatos añadidos a un objeto, como una etiqueta añadida a un campo o segmento de esquema. Un administrador define directivas de acceso que incluyen atributos para administrar permisos de acceso de usuarios. |
| Etiquetas | Las etiquetas permiten clasificar los conjuntos de datos y campos según las directivas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Las prácticas recomendadas alientan el etiquetado de datos en cuanto se incorporan a Platform o en cuanto los datos están disponibles para su uso en Platform. |
| Permisos | Los permisos incluyen la capacidad de ver o utilizar funciones de Platform, como crear entornos limitados, definir esquemas y administrar conjuntos de datos. |
| Conjuntos de permisos | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contiene un grupo de permisos. |
| Políticas | Las directivas son declaraciones que reúnen atributos para establecer acciones permitidas y no permitidas. Las directivas pueden ser locales o globales, y pueden anular otras directivas. |
| Recurso | Un recurso es el recurso o el objeto al que puede tener acceso o al que no puede tener acceso un sujeto. Los recursos pueden ser segmentos o campos de esquema. |
| Funciones | Las funciones son formas de clasificar los tipos de usuarios que interactúan con la instancia de Platform y que son componentes básicos de las directivas de control de acceso. En un entorno de control de acceso basado en funciones, el aprovisionamiento de acceso de los usuarios se agrupa a través de responsabilidades y necesidades comunes. Una función tiene un conjunto determinado de permisos y a los miembros de su organización se les puede asignar una o más funciones, según el ámbito de vista o acceso de escritura que necesiten. |
| Asunto | Un asunto es el usuario que solicita acceso a un recurso para realizar una acción. |
| Grupos de usuarios | Los grupos de usuarios son varios usuarios que se han agrupado y tienen acceso para ejecutar las mismas funciones. |

## Permisos

>[!IMPORTANT]
>
>Una vez que su organización esté habilitada para el control de acceso basado en atributos, puede empezar a utilizar Permisos en Adobe Experience Cloud, en lugar de Funciones en Adobe Admin Console, para administrar permisos para usuarios, funcionalidad, etiquetas y otros recursos de la organización.

Permisos es el área del Experience Cloud donde los administradores pueden definir funciones de usuario y directivas de acceso para administrar permisos de acceso para funciones y objetos dentro de una aplicación de producto.

Mediante Permisos, puede crear y administrar funciones, así como asignar los permisos de recursos deseados para estas. Los permisos también le permiten administrar las etiquetas, los entornos limitados y los usuarios asociados a una función específica. Para obtener más información, consulte la [Guía de permisos](ui/browse.md).

## API de control de acceso basado en atributos

La API de control de acceso basada en atributos le permite administrar mediante programación funciones, directivas y productos dentro de Platform mediante API. Para obtener más información, consulte la guía de [uso de la API para administrar configuraciones de control de acceso basadas en atributos](api/overview.md).

## Control de acceso basado en atributos en Adobe Experience Platform

Las secciones siguientes proporcionan información sobre cómo el control de acceso basado en atributos está integrado en otros componentes de Platform:

### Control de acceso

Platform aprovecha [Adobe Admin Console](https://adminconsole.adobe.com) funciones para vincular usuarios con permisos y zonas protegidas. Los permisos controlan el acceso a una variedad de funcionalidades de Platform, incluido el modelado de datos, la administración de perfiles y la administración de zonas protegidas. Una vez que su organización esté habilitada para el control de acceso basado en atributos, puede empezar a utilizar Permisos en Adobe Experience Cloud, en lugar de Funciones en Adobe Admin Console, para administrar permisos para usuarios, funcionalidad, etiquetas y otros recursos de la organización.

Hay disponibilidad limitada para el control de acceso basado en atributos para clientes que compran Escudos de atención médica o de privacidad. Entre las características de esta funcionalidad se incluyen:

* Interfaz de permisos: proporciona una interfaz para definir funciones de usuario, permisos y directivas para el control de acceso basado en atributos.

* Etiquetado: Añada, edite y elimine etiquetas a las funciones de usuario, los campos de esquema, los segmentos y otros objetos admitidos para aprovechar las políticas de control de acceso. **Nota:** Cualquier segmento que utilice un atributo etiquetado debe etiquetarse también si desea que se le apliquen las mismas restricciones de acceso.

Se están cambiando los flujos de trabajo de administración de todas las aplicaciones con tecnología de Experience Platform de Admin Console a la nueva interfaz de Permisos.

>[!IMPORTANT]
>
>Sus funciones se migran automáticamente a la interfaz Permisos cuando su organización está habilitada. Las funciones en Admin Console se mantendrán sin cambios por el momento. Por favor **no** modifique sus funciones una vez habilitada su organización.

Para obtener más información sobre el control de acceso, consulte [información general de control de acceso](../home.md).

### Destinos {#destinations}

[!DNL Destinations] son integraciones creadas previamente con plataformas de destino que permiten la activación perfecta de los datos de Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

Como administrador, puede utilizar las funcionalidades de control de acceso basadas en atributos para lo siguiente:

* Configurar el acceso de los usuarios para ver segmentos específicos en el proceso de activación, en función de la función, los permisos y las etiquetas.
   * En el proceso de activación, es posible que los usuarios tengan que seleccionar los segmentos que desean activar en un destino. Como administrador, puede aprovisionar usuarios de su organización para que solo vean segmentos etiquetados con etiquetas a las que los usuarios tienen acceso y segmentos que no contienen etiquetas.
* Configurar el acceso de los usuarios para ver campos específicos en el proceso de activación, en función de la función, los permisos y las etiquetas.
   * En el proceso de activación, es posible que los usuarios tengan que seleccionar los campos que desean activar en un destino. Como administrador, puede aprovisionar usuarios de su organización para que solo vean campos etiquetados con etiquetas a las que los usuarios tienen acceso y campos que no contienen etiquetas.

>[!IMPORTANT]
>
>En resumen, tenga en cuenta las siguientes implicaciones al trabajar con destinos y control de acceso basado en atributos:
>
>* Solo puede activar segmentos para los que tenga permiso de acceso y visualización en la [vista de exploración de segmentos](/help/segmentation/ui/overview.md#browse) y [paso seleccionar segmento](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) del flujo de trabajo de activación.
>* En el [paso de asignación del flujo de trabajo de activación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), solo puede ver y seleccionar para su activación los campos para los que tiene permiso de acceso.
>* Si desea activar segmentos adicionales en un destino existente en el que no tenga acceso a todos los campos asignados para la exportación, el flujo de trabajo de activación se bloqueará por usted.

Para obtener más información sobre [!DNL Destinations], consulte la [[!DNL Destinations] descripción general](../../destinations/home.md).

### Servicio de identidad

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

Como parte del control de acceso basado en atributos, la variable `view-identity-graph` El permiso le permite determinar qué usuarios de su organización pueden acceder al gráfico de identidades a través de la interfaz de usuario o las API. Para obtener más información, consulte la guía de [uso del visualizador de gráficos de identidad](../../identity-service/features/identity-graph-viewer.md).

Para obtener más información sobre [!DNL Identity Service], consulte la [[!DNL Identity Service] descripción general](../../identity-service/home.md).

### Perfil del cliente en tiempo real

Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los distintos datos de clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

Como administrador, puede utilizar las funcionalidades de control de acceso basadas en atributos para lo siguiente:

* Configurar el acceso de los usuarios a atributos de perfil específicos en función de la función, los permisos y las etiquetas.
   * Como administrador, puede aprovisionar usuarios de su organización para que solo vean atributos de perfil etiquetados con etiquetas a las que los usuarios tienen acceso y atributos de perfil que no contienen ninguna etiqueta;
   * Como administrador, puede aprovisionar usuarios de su organización para que solo vean atributos de perfil etiquetados con etiquetas a las que los usuarios tienen acceso al crear segmentos;
* Configure el acceso de los usuarios a la vista previa de datos mediante el etiquetado de campos de datos específicos utilizados en el esquema XDM del modelo de datos.

Para obtener más información sobre el perfil, consulte [Resumen del perfil](../../profile/home.md).

### Servicio de segmentación

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

Como administrador, puede utilizar las funcionalidades de control de acceso basadas en atributos para lo siguiente:

* Configurar el acceso de los usuarios para ver y administrar segmentos específicos, según la función, los permisos y las etiquetas.
   * Como administrador, puede aprovisionar a los usuarios de su organización para que solo vean segmentos etiquetados con etiquetas a las que los usuarios tienen acceso y segmentos que no contienen etiquetas al utilizar la interfaz de usuario de segmentación.

Para obtener más información sobre [!DNL Segmentation Service], consulte la [[!DNL Segmentation Service] descripción general](../../segmentation/home.md).

### XDM

Experience Data Model (XDM) es una especificación de código abierto diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación para comunicarse con servicios en Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

Con el control de acceso basado en atributos, puede:

* [Aplicar etiquetas de uso de datos a grupos y clases de campos](../../xdm/tutorials/labels.md). Esto permite que varios esquemas con los mismos grupos de campos o clases tengan campos etiquetados con los mismos atributos, según las configuraciones en el nivel de grupo de campos o clase;
* Configure el acceso de los usuarios a campos de esquema XDM específicos según los conjuntos de permisos aplicados a las funciones asignadas a los usuarios.

Para obtener más información sobre XDM, consulte la [Información general de XDM](../../xdm/home.md).