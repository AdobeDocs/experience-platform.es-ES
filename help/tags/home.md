---
title: Información general sobre etiquetas
description: Las etiquetas de Adobe Experience Platform son la próxima generación de funcionalidades de administración de etiquetas de Adobe. Las etiquetas ofrecen a los clientes una alternativa sencilla para implementar y administrar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente.
exl-id: 23d882a5-1ddd-404b-a7e9-3000f1804971
source-git-commit: 13c02dd5930905e3851ff147c0ea4d914e3dc6c7
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 92%

---

# Información general sobre etiquetas

>[!NOTE]
>
>El reenvío de eventos es una función de pago que se incluye como parte de las ofertas Adobe Real-time Customer Data Platform Connections, Prime o Ultimate.

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](./term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Las etiquetas de Adobe Experience Platform son la próxima generación de funcionalidades de administración de etiquetas de Adobe. Las etiquetas ofrecen a los clientes una alternativa sencilla para implementar y administrar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente.

Las etiquetas ofrecen a los usuarios las herramientas necesarias para desarrollar y mantener sus propias integraciones, que se denominan *extensiones*. Los clientes de [!DNL Adobe Experience Cloud] pueden encontrar estas extensiones en las tiendas de aplicaciones para instalar, configurar e implementar rápidamente sus etiquetas.

Las etiquetas se ofrecen a los clientes de [!DNL Adobe Experience Cloud] como una funcionalidad incluida que añade valor.

## Ventajas principales {#key-benefits}

* Obtención de valor en menos tiempo.
* Datos fiables a través de la recopilación, organización y entrega centralizadas mediante elementos de datos.
* Experiencias convincentes mediante la integración de tecnología de marketing y datos con ayuda del generador de reglas.

## Funciones principales {#key-features}

### Extensiones {#extensions}

Una extensión es un paquete de código (JavaScript, HTML y CSS) que amplía la funcionalidad de las etiquetas. Cree, gestione y actualice sus integraciones con una interfaz de autoservicio virtual. Puede considerar las extensiones como aplicaciones que utiliza para realizar sus tareas.

### Catálogo de extensiones {#extension-catalog}

Examine, configure e implemente herramientas de marketing/publicidad, que crean y mantienen proveedores de software independientes.

### Generador de reglas {#rule-builder}

Cree reglas sólidas que combinen varios eventos, ordenadas de la forma que usted determine mediante una lógica de “si/entonces” con condiciones y excepciones. Las extensiones ofrecen opciones para:

* Eventos
* Condiciones
* Excepciones
* Acciones

El generador de reglas incluye comprobación de errores en tiempo real y resaltado de sintaxis para el código personalizado.

Cuando se cumplen los criterios descritos en las reglas y las condiciones, las acciones definidas se ejecutan en orden.

### Elementos de datos {#data-elements}

Recopile, organice y entregue datos mediante tecnologías de publicidad y marketing basadas en web.

### Publicación empresarial {#enterprise-publishing}

El proceso de publicación les permite a los equipos publicar código en las páginas. Distintas personas pueden crear una implementación, aprobarla y publicarla en sus páginas.

* Los cambios que se realicen en su código se encapsulan dentro de las bibliotecas que defina.
* Usted especifica dónde y cuándo desea que se implemente su código.
* Diferentes equipos pueden crear varias bibliotecas paralelamente.
* Entornos de desarrollo ilimitados.
* Un proceso deliberado y basado en permisos para combinar bibliotecas.

### Abrir las API {#open-apis}

Automatice las implementaciones de tecnologías individuales o de un grupo de tecnologías.

* Las etiquetas interactúan con la API de Reactor.
* Las implementaciones se pueden automatizar mediante API.
* Integración de las API de con sus propios sistemas internos.
* Si lo desea, puede crear su propia interfaz de usuario.

### Contenedor de etiquetas modular y ligero {#modular-tag}

El contenido del contenedor se minimiza, incluido el código personalizado. Todo es modular. Si no necesita un elemento, este no se incluye en la biblioteca. El resultado es una implementación rápida y compacta. Consulte [Minification](./ui/publishing/builds.md).

## Otros aspectos destacados {#other-highlights}

Etiquetas proporciona varias mejoras con respecto a los sistemas similares, entre las que se incluyen:

* No se usa `document.write ()` donde Chrome no lo permite.
* Las reglas Principio de la página y Final de la página están agrupadas en la biblioteca principal para reducir las llamadas a HTTP innecesarias.
* Los scripts de acción personalizados dentro de una regla se pueden cargar en paralelo, pero se ejecutan de forma secuencial.
* Si evita las reglas Principio de la página y Final de la página, el código resulta generalmente asíncrono, con una ruta para ser totalmente asíncrono.
