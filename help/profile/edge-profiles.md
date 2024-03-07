---
title: Perfiles de Edge
description: Obtenga información acerca de los perfiles de Edge, así como la terminología relacionada, las regiones disponibles para perfiles de Edge y los servicios disponibles para perfiles de Edge.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: 6a17febf845d2b9566e49423fc68491315b2d4d7
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# Perfiles de borde

En Adobe Experience Platform, el perfil del cliente en tiempo real es la única fuente fiable para los datos de entidades. Estos datos de perfil se encuentran en un concentrador central y se ocupan de casos de uso que dependen de la exhaustividad e integridad de los datos. Sin embargo, en casos de uso más en tiempo real, en los que la sensibilidad temporal es más importante, los perfiles de Edge son la opción preferida. Los perfiles de Edge son perfiles ligeros que se sientan en los bordes y ayudan en casos de uso de personalización en tiempo real.

Por ejemplo, las aplicaciones de Adobe como Adobe Target, Personalization Destination y Adobe Campaign utilizan perímetros para ofrecer experiencias del cliente personalizadas en tiempo real. Los datos se enrutan a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que estará disponible en el borde.

## Terminología {#terminology}

Cuando trabaje con aristas, asegúrese de comprender los siguientes conceptos:

- **Edge**: un perímetro es un servidor ubicado geográficamente que almacena datos y hace que sea fácilmente accesible para las aplicaciones.
- **Configuración de proyección**: una configuración de proyección describe cómo se debe replicar una entidad determinada en los perímetros de un cliente determinado y en qué condiciones. Por ejemplo, para Luma (un cliente de muestra), solo los campos de edad y sexo del conjunto de datos que siguen el esquema Profile se deben propagar a los perímetros.
- **Proyección de borde**: una proyección de Edge es la aplicación de una configuración de proyección en un perímetro específico a un fragmento de datos con un ID único que se ajusta a un esquema determinado para un cliente determinado. Por ejemplo, una entidad que respeta el esquema de Perfil con ID `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, visitante del sitio web de Luma, replicado en el centro de datos VA6, que contiene los campos `age = 35` y `gender = male`.

En otros términos, los datos se enrutan a un borde mediante una proyección, con el **destino de proyección** definitorio **que** edge al que se enviarán los datos y la variable **configuración de proyección** definitorio **qué** se enviarán los datos al perímetro especificado.

## Regiones disponibles {#regions}

Las siguientes regiones están disponibles para su uso con edge:

- VA6
- O2
- IRL1
- AUS3
- SGP3
- JPN3
- IND1

Todas estas regiones son opciones válidas para que los perfiles aterricen.

## Servicios disponibles {#services}

Los siguientes servicios están habilitados para la búsqueda de perfiles en Edge:

- [Servicio de configuración de perfil de Edge](#edge-profile-configuration-service)
- [Servicio de trabajador de proyección](#mepw)
- [Servicio de perfil rápido](#xps)

### Servicio de configuración de perfil de Edge {#edge-profile-configuration-service}

El servicio de configuración de perfiles de Edge expone las API para soluciones y aplicaciones de flujo descendente para crear configuraciones de proyección. Puede utilizar estas API para especificar los atributos y las audiencias de un perfil que deben enviarse a los bordes, así como las regiones de borde a las que debe enviarse la proyección. En este momento, puede especificar lo siguiente **cualquiera** de las regiones de borde para las proyecciones.

### Servicio de trabajador de proyección {#mepw}

El servicio de trabajo de proyección (MEPW) supervisa los cambios que se producen en el concentrador de perfiles. Después de examinar los cambios en las configuraciones, este servicio prepara las proyecciones y las envía a las regiones de borde previamente especificadas. Además, este servicio procesa las solicitudes de actualización de la entidad y envía las proyecciones necesarias a las regiones necesarias. Las actualizaciones de entidad se utilizan para garantizar que se pueda acceder a la entidad con alta disponibilidad.

### Servicio de perfil rápido {#xps}

El servicio de perfil rápido (XPS) recupera los perfiles en los distintos extremos. Este servicio recibe solicitudes de soluciones descendentes, como destinos de Adobe Target o Personalización personalizada, busca los perfiles de las bases de datos en los perímetros y envía el perfil solicitado a la solución solicitante. Si no se encuentra el perfil, se envía una solicitud de actualización al concentrador asociado.

## Pasos siguientes

Después de leer esta guía, debe tener una comprensión básica de los perfiles de Edge, incluida información sobre las regiones y servicios disponibles para los perfiles de Edge. Para obtener más información sobre Adobe Experience Edge, lea la [Información general de Edge Network](../web-sdk/home.md#edge-network).

## Apéndice

La siguiente sección enumera las preguntas más frecuentes sobre los perfiles de Edge:

### ¿En qué regiones pueden aterrizar los perfiles de Edge?

Los perfiles de borde pueden aterrizar en diferentes regiones según la situación en cuestión.

En el caso de las configuraciones de proyección, cualquier cambio en el perfil se propagará a todas las regiones mencionadas dentro de la configuración del perfil.

Además, cada perfil perimetral tiene un atributo de esquema denominado Región de actividad de usuario (UAR). Todos los bordes que ha visitado este perfil en los últimos 14 días se enumeran en este atributo de perfil. Como resultado, cuando este atributo está presente en un perfil, cualquier cambio en el perfil también se envía a todas las regiones enumeradas en la UAR.

### ¿Cómo funciona la caducidad de los datos con los perfiles de Edge?

En el caso de los perfiles Edge, la caducidad de los datos determina cuánto tiempo permanecerá el perfil en Edge antes de eliminarlo. La caducidad de los datos es **laminado**, lo que significa que, cada vez que se accede al perfil en Edge, se restablece el tiempo de caducidad de los datos. De forma predeterminada, la caducidad de los datos dura 14 días.

### ¿Qué datos se almacenan en el perfil de Edge?

El perfil de Edge almacena los atributos de perfil, los ID de perfil y los ID de audiencia cualificados. De forma predeterminada, la caducidad de los datos dura 14 días.
