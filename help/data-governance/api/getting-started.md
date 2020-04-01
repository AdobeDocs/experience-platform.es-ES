---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del desarrollador de la API del servicio de directivas DULE
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# Guía del desarrollador de la API del servicio de directivas DULE

El etiquetado y cumplimiento del uso de datos (DULE) es el mecanismo central del control de datos de la plataforma de experiencia de Adobe. El servicio de directivas DULE proporciona una API RESTful que le permite crear y administrar políticas de uso de datos para determinar qué acciones de mercadotecnia se pueden realizar con datos que se han etiquetado con ciertas etiquetas de uso de datos.

Este documento proporciona instrucciones para realizar las operaciones clave disponibles en la API de servicio de directivas. Si aún no lo ha hecho, comience por revisar la información general [sobre el Gobierno de](../home.md) datos para familiarizarse con el marco DULE. Para obtener instrucciones paso a paso sobre cómo crear y aplicar políticas DULE, consulte el tutorial sobre políticas [DULE](../policies/create.md).

Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de servicio de directivas.

## Introducción a DULE Policy Service

Antes de comenzar a trabajar con el servicio de directivas, los datos de la plataforma de experiencias deben tener aplicadas las etiquetas DULE correspondientes. Encontrará instrucciones paso a paso completas para aplicar etiquetas de uso de datos a conjuntos de datos y campos en la guía [del usuario de etiquetas](../labels/user-guide.md)DULE.

## Requisitos previos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Administración](../home.md)de datos: El marco en el que la plataforma de experiencia impone la compatibilidad con el uso de datos.
   * [Etiquetas](../labels/overview.md)DULE: Las etiquetas de uso de datos se aplican a los campos de datos del Modelo de datos de experiencia (XDM), especificando restricciones para acceder a los datos.
* [Sistema](../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
* [Perfil](../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Simuladores](../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

## Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia, incluidos los que pertenecen a la administración de datos, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Recursos principales vs. personalizados

Dentro de la API de servicio de directivas, todas las directivas y acciones de marketing se denominan `core` o `custom` recursos.

Los recursos `core` son los definidos y mantenidos por Adobe, mientras que `custom` los recursos son creados y mantenidos por clientes individuales y, por lo tanto, son únicos y visibles únicamente para la organización de IMS que los creó. Como tal, las operaciones de listado y búsqueda (`GET`) son las únicas operaciones permitidas en `core` los recursos, mientras que las operaciones de listado, búsqueda y actualización (`POST`, `PUT`, `PATCH`y `DELETE`) están disponibles para `custom` los recursos.

## Estado de la directiva

Las directivas de uso de datos pueden tener uno de los tres estados posibles: `DRAFT`, `ENABLED`o `DISABLED`.

De forma predeterminada, solo las directivas &quot;HABILITADAS&quot; participan en la evaluación de políticas.

Las políticas de &quot;BORRADOR&quot; también pueden considerarse en la evaluación de políticas, pero sólo estableciendo el parámetro de consulta `?includeDraft=true`. Al final del presente documento puede encontrarse más información sobre la evaluación de políticas en la sección del documento sobre la aplicación de [políticas](../enforcement/overview.md) .

## Nombres de acciones de marketing {#marketing-actions}

Los nombres de las acciones de mercadotecnia son identificadores únicos para las acciones de mercadotecnia. Cada acción `core` de marketing tiene un nombre único que se aplica a todas las organizaciones de IMS. Adobe define y mantiene estos nombres. Mientras tanto, todas las acciones de mercadotecnia definidas por el cliente (`custom` los recursos) son únicas dentro de su organización individual y no son visibles ni se comparten con otras organizaciones de IMS.

Los pasos para trabajar con acciones de marketing en la API de servicio de directivas se describen en la sección Acciones [de](#marketing-actions) marketing más adelante en este documento.

## Pasos siguientes

Ahora que tiene los conocimientos y las credenciales de requisito previo, puede seguir leyendo las llamadas de API de muestra que se proporcionan en esta guía para desarrolladores:

* [Acciones de mercadotecnia](marketing-actions.md)
* [Políticas](policies.md)