---
title: Casos de uso de segmentación para Real-time Customer Data Platform B2B Edition
description: Una descripción general de los distintos casos de uso disponibles de Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: b436aeb8a8628d9b481041be518c1113fb54c342
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 0%

---

# Casos de uso de segmentación para Real-time Customer Data Platform B2B Edition

Este documento proporciona ejemplos de definiciones de segmentos en Adobe Real-time Customer Data Platform B2B Edition y cómo se pueden combinar distintos tipos de atributos para casos de uso B2B comunes. Para comprender cómo encajan los destinos en el flujo de trabajo B2B, consulte la [tutorial de extremo a extremo](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>Los atributos necesarios para estos casos de uso de segmentación solo están disponibles para los clientes de Real-time Customer Data Platform B2B Edition. Si no utiliza Real-time Customer Data Platform B2B Edition, consulte la [resumen de segmentación](./segmentation-overview.md) en su lugar.

## Requisitos previos {#prerequisites}

Antes de poder utilizar los atributos de segmentación para las clases B2B, debe completar los siguientes pasos:

1. Cree esquemas que utilicen las clases B2B. Las clases de B2B Edition incluyen Cuenta, Campaña, Oportunidad, Lista de marketing y más. Para obtener información sobre [cómo configurar esquemas para utilizarlos con clases B2B](../schemas/b2b.md) consulte la documentación del esquema.
1. Cree relaciones entre los esquemas B2B del Modelo de datos de experiencia (XDM). Los segmentos basados en atributos de B2B Edition requieren relaciones entre las clases para utilizar completamente la funcionalidad de segmentación B2B extendida. Consulte la documentación sobre [Cómo definir una relación entre dos esquemas B2B](../../xdm/tutorials/relationship-b2b.md) para obtener más información.
1. Ingesta de datos mediante conjuntos de datos basados en los esquemas B2B. Consulte la documentación de fuentes para [información sobre cómo introducir datos](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Lea el [Guía del usuario del generador de segmentos](../../segmentation/ui/segment-builder.md) para obtener una guía más detallada sobre cómo generar segmentos.

Una vez cumplidos estos requisitos, puede combinar estos atributos para casos de uso B2B comunes.

## Primeros pasos {#getting-started}

Una vez que los esquemas de unión de las clases B2B han establecido relaciones y se han utilizado para introducir datos, sus atributos están disponibles en el carril izquierdo del Generador de segmentos.

Las clases B2B y sus atributos se anexan con un `B2B` dentro del espacio de trabajo de segmentación para diferenciarlos de los que están disponibles como estándar en Real-time Customer Data Platform.

Para crear segmentos de forma eficaz para los casos de uso B2B, es importante tener un conocimiento profundo del esquema y comprender la apariencia del modelo de datos. También es útil tener en cuenta la ruta que los datos siguen de un objeto de datos a otro.

La siguiente imagen ilustra las relaciones entre las clases B2B disponibles en Real-Time CDP B2B Edition.

![ERD de clase B2B](../assets/segmentation/b2b-classes.png)

Dado que el modelo de datos puede ser complicado, puede utilizar la interfaz de usuario de Platform para ver una representación visual más detallada del modelo de datos y encontrar los atributos relevantes para su caso de uso. Para empezar, vaya a la interfaz de usuario de Platform y seleccione Esquemas en el panel de navegación izquierdo.

Seleccione el esquema adecuado de la lista disponible y seleccione la relación adecuada en el [!UICONTROL Composición] raíl lateral. En el ejemplo siguiente, al seleccionar la relación &quot;Persona&quot;, se muestra qué atributo del esquema actual hace referencia al esquema &quot;Persona&quot; relacionado (si es el esquema de origen de la relación) o se hace referencia a él mediante el esquema &quot;Persona&quot; (si es el esquema de referencia de la relación).

![ejemplo de clave de origen con la relación people en el espacio de trabajo de esquema](../assets/segmentation/source-key-schema-relationship-example.png)

Esta relación se refleja dentro del Generador de segmentos mediante el uso de `Key` como se muestra en la siguiente imagen.

![ejemplo de clave de origen con el generador de segmentos en el espacio de trabajo de segmentación](../assets/segmentation/source-key-segmentation-example.png)

Consulte la [Esquemas en la documentación de Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) para obtener más información sobre las clases B2B disponibles.

Los casos de uso siguientes proporcionan información sobre qué clases se utilizan para establecer relaciones entre los diferentes esquemas para lograr estos resultados. Estos ejemplos se pueden utilizar para ayudarle a crear sus propios segmentos.

## Ejemplos de diferentes casos de uso de segmentación {#use-cases}

Los siguientes casos de uso están disponibles para la segmentación con B2B Edition. En cada ejemplo se proporciona una descripción de lo que hace el segmento y una descripción de las clases utilizadas para crearlos. Las imágenes proporcionadas resaltan la ruta del archivo en la [!UICONTROL Atributos] carril lateral que refleja la estructura del esquema. El [!UICONTROL Propiedades del segmento] Esta sección de la derecha de la pantalla contiene un desglose por escrito de los atributos del segmento.

### Ejemplo 1: Encuentre a los responsables de la toma de decisiones sobre las oportunidades B2B {#find-decision-maker}

Encuentre a todas las personas que son las &quot;decisoras&quot; de cualquier oportunidad. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual de XDM] y la clase [!UICONTROL Relación de persona de oportunidad empresarial de XDM] clase.

![IU que muestra la configuración del ejemplo 1](../assets/segmentation/example-1.png)

### Ejemplo 2: Encuentre perfiles B2B asignados a oportunidades por encima de una determinada cantidad de dólares {#find-opportunities-amount}

Encuentre todas las personas que estén asignadas directamente a cualquier oportunidad cuya cantidad de oportunidad sea mayor que la cantidad dada (1 millón de dólares). Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual de XDM] clase, [!UICONTROL Relación de persona de oportunidad empresarial de XDM] clase, y [!UICONTROL Oportunidad empresarial de XDM] clase.

![IU que muestra la configuración del ejemplo 2](../assets/segmentation/example-2.png)

### Ejemplo 3: Buscar perfiles B2B asignados a oportunidades por ubicación {#find-opportunities-location}

Encuentre todas las personas que estén asignadas directamente a cualquier oportunidad donde la cuenta esté ubicada en una ubicación determinada (Canadá). Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual de XDM] clase, [!UICONTROL Relación de persona de oportunidad empresarial de XDM] clase, [!UICONTROL Oportunidad empresarial de XDM] clase, y [!UICONTROL Cuenta empresarial de XDM] clase.

![IU que muestra la configuración del ejemplo 3](../assets/segmentation/example-3.png)

### Ejemplo 4: Encuentre &quot;responsables de la toma de decisiones&quot; para conocer las oportunidades según el comportamiento de la industria y la navegación {#find-industry-browsing-behavior}

Encuentre a todas las personas que son un &quot;Tomador de decisiones&quot; de cualquier oportunidad donde la cuenta está en la industria &quot;Finanzas&quot;, y visitó la página de precios en los últimos tres días. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual de XDM] clase, [!UICONTROL Relación de persona de oportunidad empresarial de XDM] clase, [!UICONTROL Oportunidad empresarial de XDM] clase, y [!UICONTROL Cuenta empresarial de XDM] clase, y [!UICONTROL ExperienceEvent de XDM] clase.

![IU que muestra la configuración del ejemplo 4](../assets/segmentation/example-4.png)

### Ejemplo 5: Búsqueda de perfiles B2B para oportunidades por nombre de departamento y cantidad de oportunidad {#find-department-opportunity-amount}

Encuentre a todas las personas que trabajan en un departamento de Recursos Humanos (RRHH) y tienen cualquier cuenta que tiene al menos una oportunidad abierta por valor de la cantidad dada (1 millón de dólares) o más. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual de XDM] clase, [!UICONTROL Cuenta empresarial de XDM] clase, y [!UICONTROL Oportunidad empresarial de XDM] clase.

![IU que muestra la configuración del ejemplo 5](../assets/segmentation/example-5.png)

### Ejemplo 6: Búsqueda de perfiles B2B por puesto e ingresos de cuenta anual {#find-by-job-title-and-revenue}

Encuentre a todas las personas cuyo cargo sea Vicepresidente y tenga una cuenta con ingresos anuales de la cantidad determinada (100 millones de dólares) o más, y haya visitado la página de precios al menos 3 veces en el último mes. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual de XDM] clase, [!UICONTROL Cuenta empresarial de XDM] clase, y [!UICONTROL ExperienceEvent de XDM] clase.

![IU que muestra la configuración del ejemplo 6](../assets/segmentation/example-6.png)

### Ejemplo 7: Encuentre a los responsables de la toma de decisiones por estado de oportunidad y comportamiento de navegación {#find-by-opportunity-status-and-browsing-behavior}

Encuentre a todas las personas que son un &quot;tomador de decisiones&quot; de cualquier oportunidad perdida cerrada, y visitó la página de precios en la última semana. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual de XDM] clase, [!UICONTROL Relación de persona de oportunidad empresarial de XDM] clase, [!UICONTROL Oportunidad empresarial de XDM] clase, y [!UICONTROL ExperienceEvent de XDM] clase.

![IU que muestra la configuración del ejemplo 7](../assets/segmentation/example-7.png)

### Ejemplo 8: Uso de cuentas relacionadas para expandir el alcance de la segmentación {#related-accounts}

Encuentre a todas las personas que trabajan en un departamento de Recursos Humanos (RRHH) y están relacionadas con cualquier cuenta *o cualquiera de las cuentas relacionadas de la cuenta* que tenga al menos una oportunidad abierta por valor de la cantidad determinada (1 millón de dólares) o más. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual de XDM] clase, [!UICONTROL Cuenta empresarial de XDM] clase, y [!UICONTROL Oportunidad empresarial de XDM] clase.

![IU que muestra la segmentación para cuentas relacionadas](../assets/segmentation/example-8.png)

### Ejemplo 9: Usar puntuaciones de posibles clientes o de cuenta para calificar el perfil {#account-scoring}

Encuentre todos los perfiles con una puntuación de más de 80 posibles clientes.

![IU que muestra la segmentación para la puntuación predictiva de posibles clientes y cuentas](../assets/segmentation/example-9.png)

### Ejemplo 10: Encuentre perfiles B2B asociados a cuentas cuya organización principal tenga ingresos superiores a una determinada cantidad en dólares {#find-parent-org-amount}

Encuentre todas las personas asociadas con cuentas cuya organización principal tenga un ingreso mayor que la cantidad indicada (100.000.000 de dólares).

![IU que muestra la organización principal de la segmentación](../assets/segmentation/example-10.png)

### Ejemplo 11: Buscar perfiles B2B por puesto y nombre de cuenta con una relación activa {#find-by-job-title-and-account-name}

Encuentre a todas las personas que sean un &quot;Manager&quot; en la cuenta &quot;Acme&quot;, donde la relación de la cuenta es &quot;Active&quot;.

![IU que muestra la organización principal de la segmentación](../assets/segmentation/example-11.png)

### Ejemplo 12: Encuentre perfiles B2B dirigidos para campañas en las que el valor de actualCost excede el valor de budgetCost {#find-actualcost-exceed-budgetcost}

Encuentre todas las personas que son el objetivo de las campañas en las que el valor realCost superó al valor presupuestado.

![IU que muestra la organización principal de la segmentación](../assets/segmentation/example-12.png)

### Ejemplo 13: Buscar perfiles B2B que pertenezcan a una lista estática de Marketo y isDeleted=false {#find-marketo-static-list}

Busque todas las personas que pertenezcan a la lista estática de Marketo &quot;Usuarios de aniversario&quot; donde isDeleted=false.

![IU que muestra la organización principal de la segmentación](../assets/segmentation/example-13.png)

## Pasos siguientes {#next-steps}

Después de leer esta descripción general, ahora comprende las posibilidades de segmentación disponibles con Real-Time CDP, B2B Edition. Para obtener más información sobre el servicio de segmentación, lea la [Documentación de segmentación](../../segmentation/home.md).
