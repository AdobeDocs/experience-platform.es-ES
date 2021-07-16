---
title: Notas de la versión
description: Últimas notas de la versión para etiquetas en Adobe Experience Platform.
source-git-commit: 7a6bec77895458cf1735bc7a00d16b78df9776a5
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 67%

---

# Notas de la versión

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## 17 de mayo de 2021

**Mejor gestión de los cambios no guardados**: Antes, cada vez que se alejaba de una vista de configuración (extensiones, elementos de datos y componentes de regla), se le preguntaba si quería descartar los cambios. Pero la lógica para determinar eso no era la mejor, así que la mayor parte del tiempo se le pedía que guardara los cambios aunque no hubiera ninguno. Se ha solucionado. A partir de ahora, solo debería ver ese mensaje cuando haya realizado cambios.

## 10 de mayo de 2021

**Publicación simplificada**: Ya no es necesario compilar en el entorno de ensayo. Si tiene los derechos adecuados, puede omitir completamente el estado Enviado y publicar directamente desde Desarrollo, siempre y cuando la compilación se haya hecho correctamente y no haya otras bibliotecas en orden ascendente.

## 22 de abril de 2021

**Recopilación de datos en Adobe Experience Platform** : el envío de datos a Adobe no se trata solo de implementar etiquetas en el sitio o de configurar en la aplicación.  El uso de los SDK de Experience Platform y de la red perimetral requiere acceso a otras funcionalidades de Platform. Esto requería iniciar sesión en varias herramientas diferentes, pero ahora están juntas en un solo lugar.

La recopilación de datos en Platform consta de seis funciones y la navegación recién optimizada solo contendrá los elementos a los que tienen acceso su empresa y su cuenta de usuario.  Algunos de los nombres de las capacidades también se han actualizado para que coincidan con los patrones de nomenclatura de Experience Platform.

* Cliente (anteriormente conocido como &quot;lado del cliente&quot;)
* Datastreams (anteriormente conocido como &quot;Configuración de Edge&quot;)
* Servidor (anteriormente conocido como &quot;lado del servidor&quot;)
* Configuraciones de aplicaciones
* Esquemas
* Identidades

Esperamos recibir más actualizaciones a medida que Experience Platform y la recopilación de datos sigan evolucionando.

## 18 de febrero de 2021

* Se ha actualizado la interfaz de usuario de recopilación de datos para la versión 3 del espectro de reacción
* Se han actualizado las tarjetas de extensión a los últimos patrones de espectro
* Se ha aumentado el tamaño de los campos de nombre en toda la aplicación

## 13 de enero de 2021

**Disponibilidad general: Reenvío de** eventosEnvíe datos de nivel de evento a la red perimetral de Adobe Experience Platform y, a continuación, utilice el reenvío de eventos para transformar, enriquecer y enviar esos datos a un extremo que no sea de Adobe mediante los servidores de Adobe, no el cliente, con baja latencia.

Consulte la [descripción general del reenvío de eventos](../ui/event-forwarding/overview.md) y [guía de introducción](../ui/event-forwarding/getting-started.md) para obtener más información.
