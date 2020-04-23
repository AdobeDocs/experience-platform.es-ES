---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión de la plataforma de experiencia 11 de diciembre de 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 817f994fc0622b1c46e98f8d773a4d91c1064824

---


# Notas de la versión de Adobe Experience Platform

## Fecha de versión: 11 de diciembre de 2019

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [Servicio de segmentación](#segmentation)
* [Servicio de decisiones](#decisioning)
* [Fuentes](#sources)
* [Sistema de modelo de datos de experiencia (XDM)](#xdm)

## Servicio de segmentación {#segmentation}

El servicio de segmentación de la plataforma de experiencia de Adobe proporciona una interfaz de usuario y una API RESTful que le permite crear segmentos y generar audiencias a partir de los datos de Perfil de clientes en tiempo real. Estos segmentos se configuran y mantienen de forma centralizada en Platform, lo que los hace fácilmente accesibles para cualquier aplicación de Adobe.

El servicio de segmentación define un subconjunto particular de perfiles al describir los criterios que distinguen a un grupo comercializable de personas dentro de la base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Ficha Audiencias combinadas en el Generador de segmentos | Las fichas _Segmentos_ y _Audiencias_ del Generador de segmentos se han combinado en una sola ficha _Audiencias_ . Esta ficha le permite explorar y buscar audiencias existentes, que puede arrastrar y soltar en el lienzo del generador de reglas para crear una nueva definición de segmento. Al hacer referencia a una audiencia se puede agregar uno de los siguientes conjuntos de lógica de regla a la nueva definición de segmento: Pertenencia a la Audiencia como regla, conjunto completo de lógica de regla que definió la audiencia a la que se hace referencia. |
| Nueva ubicación para el selector de directivas de combinación | Se ha cambiado la ubicación del selector de directivas de combinación en el Generador de segmentos. Para seleccionar una directiva de combinación para una definición de segmento, haga clic en el icono de engranaje de la ficha _Campos_ y, a continuación, utilice el menú desplegable _Combinar directiva_ para seleccionar la directiva de combinación que desee utilizar. |

**Problemas conocidos**

* None

Para obtener más información, consulte la descripción general [del servicio](../../segmentation/home.md)de segmentación.

## Servicio de decisiones {#decisioning}

El servicio de toma de decisiones de la plataforma de experiencia de Adobe permite seleccionar de forma programada e inteligente la &quot;Mejor experiencia siguiente&quot; de un conjunto de opciones disponibles para un individuo determinado, distribuirlas en cualquier canal o aplicación y realizar sistemas de informes y análisis.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Funciones de clasificación | El orden de ofertas para perfiles ahora se deriva a través de una función de clasificación, en lugar de un conjunto fijo de ofertas en todos los perfiles. |

**Problemas conocidos**

* None.

Consulte la información general [del servicio de](../../decisioning-service/home.md) decisiones para obtener una introducción completa al servicio.

## Fuentes {#sources}

Adobe Experience Platform puede ingestar datos de fuentes externas y permitirle estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

La plataforma de experiencia proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse en sus sistemas almacenamiento y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ---------- | ------------ |
| Conexión de flujo continuo | La ingestión de flujo continuo le permite enviar datos desde dispositivos del lado del cliente y del servidor a la plataforma de experiencias en tiempo real. La versión incluye una nueva interfaz de usuario de conexión de flujo continuo. |
| Compatibilidad con conectores para la tienda Google Cloud | Compatibilidad con la recopilación de datos de la Tienda Google Cloud. |

**Problemas conocidos**

* None.

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.

## Sistema de modelo de datos de experiencia (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave que sustentan la plataforma de experiencia. El modelo de datos de experiencia (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de la plataforma Adobe Experience. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Validación de esquema mejorada | Nuevas comprobaciones para asegurarse de que las referencias se resuelven en campos adicionales según lo esperado. Se Añadieron comprobaciones adicionales a los campos definidos como una matriz de objetos para asegurarse de que los objetos están completamente definidos. Se han mejorado los mensajes de error para ayudar a identificar y corregir problemas. |

**Corrección de errores**

* Mantenimiento y mejoras relacionadas con controles de acceso y entornos limitados.
* Compatibilidad con `eTag` el extremo `/descriptors` en la API del Registro de Esquema.

**Problemas conocidos**

* None

Para obtener más información sobre cómo trabajar con XDM mediante la API del Registro de Esquema y la interfaz de usuario del Editor de Esquemas, lea la documentación [del sistema](../../xdm/home.md)XDM.