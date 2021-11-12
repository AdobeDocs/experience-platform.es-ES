---
title: Información general sobre los casos de uso de segmentación para CDP B2B Edition en tiempo real
description: Una visión general de los diversos casos de uso disponibles de CDP B2B Edition en tiempo real.
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: e6f71954d52e0a998955c3420307417cc011c24d
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---

# Información general sobre los casos de uso de segmentación para Real-time Customer Data Platform B2B Edition

Este documento proporciona ejemplos sobre la segmentación disponible para CDP B2B Edition en tiempo real y cómo se pueden combinar los distintos tipos de atributos para casos de uso comunes B2B.

>[!NOTE]
>
>Los atributos necesarios para estos casos de uso de segmentación solo están disponibles para los clientes de Real-time Customer Data Platform B2B Edition. Si no utiliza Real-time Customer Data Platform B2B Edition, consulte la [información general sobre segmentación](./segmentation-overview.md) en su lugar.

## Requisitos previos

Antes de poder usar los atributos de segmentación para las clases B2B, debe completar los siguientes pasos:

1. Cree esquemas que utilicen las clases B2B. Las clases de B2B Edition incluyen Cuenta, Campaña, Oportunidad, Lista de marketing, etc. Para obtener información sobre [configuración de esquemas para su uso con clases B2B](../schemas/b2b.md) consulte la documentación del esquema.
1. Cree relaciones entre los esquemas B2B del Modelo de datos de experiencia (XDM). Los segmentos basados en atributos de B2B Edition requieren relaciones entre las clases para utilizar completamente la funcionalidad ampliada de segmentación B2B. Consulte la documentación sobre [definición de una relación entre dos esquemas B2B](../../xdm/tutorials/relationship-b2b.md) para obtener más información.
1. Ingeste datos mediante conjuntos de datos basados en esquemas B2B. Consulte la documentación de fuentes para [información sobre cómo introducir datos](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Lea el [Guía del usuario del Generador de segmentos](../../segmentation/ui/segment-builder.md) para obtener una guía más detallada sobre cómo crear segmentos.

Una vez cumplidos estos requisitos, puede combinar estos atributos para casos de uso comunes de B2B.

## Primeros pasos

Una vez que los esquemas de unión de las clases B2B tienen relaciones establecidas y se han utilizado para introducir datos, sus atributos están disponibles en el carril izquierdo del Generador de segmentos.

Las clases B2B y sus atributos se añaden con un `B2B` en el espacio de trabajo Segmentación para diferenciarlos de los disponibles como estándar en Real-time Customer Data Platform.

Para crear segmentos de forma eficaz para casos de uso B2B, es importante tener un conocimiento profundo del esquema y comprender el aspecto que tiene el modelo de datos. También es útil tener en cuenta la ruta que toman los datos de un objeto de datos a otro.

La siguiente imagen ilustra las relaciones entre las clases B2B disponibles dentro de CDP B2B Edition en tiempo real.

![Clase B2B ERD](../assets/segmentation/b2b-classes.png)

Dado que el modelo de datos puede ser complicado, puede utilizar la interfaz de usuario de Platform para ver una representación visual más detallada del modelo de datos con el fin de encontrar los atributos relevantes para su caso de uso. Para empezar, vaya a la interfaz de usuario de Platform y seleccione Esquemas en el panel de navegación izquierdo.

Seleccione el esquema adecuado de la lista de elementos disponibles y seleccione la relación adecuada en el [!UICONTROL Composición] carril lateral. En el siguiente ejemplo, si selecciona la relación &quot;Persona&quot;, se muestra qué atributo del esquema actual hace referencia al esquema &quot;Persona&quot; relacionado (si es el esquema de origen de la relación) o está referenciado por el esquema &quot;Persona&quot; (si es el esquema de destino en la relación).

![ejemplo de clave de origen que utiliza la relación personas en el espacio de trabajo del esquema](../assets/segmentation/source-key-schema-relationship-example.png)

Esta relación se refleja dentro del Generador de segmentos mediante el uso de `Key` carpetas como se muestra en la imagen siguiente.

![ejemplo de clave de origen con el generador de segmentos en el espacio de trabajo de segmentación](../assets/segmentation/source-key-segmentation-example.png)

Consulte la [esquemas en la documentación de Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) para obtener más información sobre las clases B2B disponibles.

Los casos de uso siguientes proporcionan información sobre qué clases se utilizan para establecer relaciones entre los distintos esquemas para lograr estos resultados. Estos ejemplos se pueden utilizar para ayudarle a crear sus propios segmentos.

## Ejemplos de diferentes casos de uso

Los siguientes casos de uso están disponibles para la segmentación con B2B Edition. Cada ejemplo proporciona una descripción de lo que hace el segmento y una descripción de las clases utilizadas para crearlos. Las imágenes proporcionadas resaltan la ruta del archivo en la variable [!UICONTROL Atributos] carril lateral que refleja la estructura del esquema. La variable [!UICONTROL Propiedades del segmento] a la derecha de la pantalla contiene un desglose por escrito de los atributos del segmento.

### Ejemplo 1

Encuentre a todas las personas que son el &quot;Responsable de Decisión&quot; de cualquier oportunidad. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual XDM] y [!UICONTROL Relación de persona de oportunidad comercial XDM] Clase .

![Interfaz de usuario que muestra la configuración de ejemplo 1](../assets/segmentation/example-1.png)

### Ejemplo 2

Encuentre todas las personas directamente asignadas a cualquier oportunidad de la cual la cantidad de oportunidad sea superior a la cantidad dada (1 millón de dólares). Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual XDM] class, [!UICONTROL Relación de persona de oportunidad comercial XDM] y [!UICONTROL Oportunidad comercial XDM] Clase .

![Interfaz de usuario que muestra la configuración de ejemplo 2](../assets/segmentation/example-2.png)

### Ejemplo 3

Encuentre todas las personas que están directamente asignadas a cualquier oportunidad donde la cuenta esté ubicada en una ubicación determinada (Canadá). Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual XDM] class, [!UICONTROL Relación de persona de oportunidad comercial XDM] class, [!UICONTROL Oportunidad comercial XDM] y [!UICONTROL Cuenta comercial XDM] Clase .

![Interfaz de usuario que muestra la configuración de ejemplo 3](../assets/segmentation/example-3.png)

### Ejemplo 4

Encuentre a todas las personas que son &quot;responsables de tomar decisiones&quot; de cualquier oportunidad donde la cuenta esté en el sector &quot;financiero&quot;, y visiten la página de precios en los últimos tres días. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual XDM] class, [!UICONTROL Relación de persona de oportunidad comercial XDM] class, [!UICONTROL Oportunidad comercial XDM] y [!UICONTROL Cuenta comercial XDM] y [!UICONTROL XDM ExperienceEvent] Clase .

![Interfaz de usuario que muestra la configuración de ejemplo 4](../assets/segmentation/example-4.png)

### Ejemplo 5

Encuentre a todas las personas que trabajan en un departamento de Recursos Humanos (HR) y están relacionadas con cualquier cuenta que tenga al menos una oportunidad abierta que valga la cantidad dada (1 millón de dólares) o más. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual XDM] class, [!UICONTROL Cuenta comercial XDM] y [!UICONTROL Oportunidad comercial XDM] Clase .

![Interfaz de usuario que muestra la configuración de ejemplo 5](../assets/segmentation/example-5.png)

### Ejemplo 6

Encuentre todas las personas cuyo puesto de trabajo es vicepresidente y están relacionadas con cualquier cuenta con ingresos anuales de la cantidad dada (100 millones de dólares) o más, y hayan visitado la página de precios al menos 3 veces en el último mes. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual XDM] class, [!UICONTROL Cuenta comercial XDM] y [!UICONTROL XDM ExperienceEvent] Clase .

![Interfaz de usuario que muestra la configuración de ejemplo 6](../assets/segmentation/example-6.png)

### Ejemplo 7

Encuentre a todas las personas que son &quot;responsables de la toma de decisiones&quot; de cualquier oportunidad perdida cerrada, y visiten la página de precios en la última semana. Este segmento requiere un vínculo entre las variables [!UICONTROL Perfil individual XDM] class, [!UICONTROL Relación de persona de oportunidad comercial XDM] class, [!UICONTROL Oportunidad comercial XDM] y [!UICONTROL XDM ExperienceEvent] Clase .

![Interfaz de usuario que muestra la configuración de ejemplo 7](../assets/segmentation/example-7.png)

## Pasos siguientes

Después de leer esta descripción general, ahora conoce las posibilidades de segmentación disponibles mediante CDP en tiempo real, B2B Edition. Para obtener más información sobre el servicio de segmentación, lea la [Documentación de segmentación](../../segmentation/home.md).
