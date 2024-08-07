---
title: Perfiles de Edge
description: Obtenga información acerca de los perfiles de Edge, así como la terminología relacionada, las regiones disponibles para perfiles de Edge y los servicios disponibles para perfiles de Edge.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Perfiles de Edge

En Adobe Experience Platform, el perfil del cliente en tiempo real es la única fuente fiable para los datos de entidades. Estos datos de perfil se encuentran en un concentrador central y se ocupan de casos de uso que dependen de la exhaustividad e integridad de los datos. Sin embargo, en casos de uso más en tiempo real, en los que la sensibilidad temporal es más importante, los perfiles de Edge son la opción preferida. Los perfiles de Edge son perfiles ligeros que se sientan en los bordes y ayudan en casos de uso de personalización en tiempo real.

Por ejemplo, las aplicaciones de Adobe como Adobe Target, Destino personalizado de Personalization y Adobe Campaign utilizan perímetros para ofrecer experiencias del cliente personalizadas en tiempo real. Los datos se enrutan a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos.

## Terminología {#terminology}

Cuando trabaje con aristas, asegúrese de comprender los siguientes conceptos:

- **Edge**: un perímetro es un servidor ubicado geográficamente que almacena datos y hace que sea fácilmente accesible para las aplicaciones.
- **proyección de Edge**: una proyección de Edge es la vista de proyección del sistema de un perfil en un perímetro específico para representar datos de perfil con un ID único que se ajusta a un esquema determinado para un cliente determinado. Por ejemplo, una entidad que respeta el esquema Perfil con ID `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, visitante del sitio web de Luma, replicó en el centro de datos de VA6, y que contiene los campos `age = 35` y `gender = male`.

En otros términos, los datos se enrutan a un borde mediante una proyección, con el **destino de proyección** que define **a qué borde** se enviarán los datos.

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

- [Servicio de trabajador de proyección](#mepw)
- [Servicio de perfil rápido](#xps)

### Servicio de trabajador de proyección {#mepw}

El servicio de trabajo de proyección (MEPW) supervisa los cambios que se producen en el concentrador de perfiles. Después de examinar los cambios en las configuraciones, este servicio prepara las proyecciones y las envía a las regiones de borde previamente especificadas. Además, este servicio procesa las solicitudes de actualización de la entidad y envía las proyecciones necesarias a las regiones necesarias. Las actualizaciones de entidad se utilizan para garantizar que se pueda acceder a la entidad con alta disponibilidad.

### Servicio de perfil rápido {#xps}

El servicio de perfil rápido (XPS) recupera los perfiles en los distintos extremos. Este servicio recibe solicitudes de soluciones de flujo descendente, como destinos de Adobe Target o Personalization personalizados, busca los perfiles de las bases de datos en los perímetros y envía el perfil solicitado a la solución solicitante. Si no se encuentra el perfil, se envía una solicitud de actualización al concentrador asociado.

## Pasos siguientes

Después de leer esta guía, debe tener una comprensión básica de los perfiles de Edge, incluida información sobre las regiones y servicios disponibles para los perfiles de Edge. Para obtener más información sobre el Adobe Experience Edge, lea [descripción general del Edge Network](../web-sdk/home.md#edge-network).

## Apéndice

La siguiente sección enumera las preguntas más frecuentes sobre los perfiles de Edge:

### ¿En qué regiones pueden aterrizar los perfiles de Edge?

Los perfiles de Edge pueden aterrizar en diferentes regiones según la situación.

Además, cada perfil perimetral tiene un atributo de esquema denominado Región de actividad de usuario (UAR). Todos los bordes que ha visitado este perfil en los últimos 14 días se enumeran en este atributo de perfil. Como resultado, cuando este atributo está presente en un perfil, cualquier cambio en el perfil también se envía a todas las regiones enumeradas en la UAR.

### ¿Cómo funciona la caducidad de los datos con los perfiles de Edge?

En el caso de los perfiles Edge, la caducidad de los datos determina cuánto tiempo permanecerá el perfil en Edge antes de eliminarlo. La caducidad de los datos es **móvil**, lo que significa que cada vez que se accede al perfil en Edge, la hora de caducidad de los datos se restablece. De forma predeterminada, la caducidad de los datos dura 14 días.

### ¿Qué datos se almacenan en el perfil de Edge?

El perfil de Edge almacena los atributos de perfil, los ID de perfil y los ID de audiencia cualificados. De forma predeterminada, la caducidad de los datos dura 14 días.
