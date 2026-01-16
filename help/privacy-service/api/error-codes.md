---
title: Códigos de error de Privacy Service en Adobe Experience Platform
description: Comprenda los códigos de error de Privacy Service para poder diagnosticar errores, gestionar los resultados de los trabajos mediante programación y determinar los pasos siguientes al enviar o supervisar trabajos de privacidad.
keywords: privacy service, códigos de error, trabajos de privacidad, errores de api
solution: Experience Platform
source-git-commit: a312dabf5b8c3b52af31e2e127cd4bbeb8dd0021
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 4%

---

# Códigos de error de Privacy Service {#privacy-service-error-codes}

Use esta referencia para identificar resultados de trabajos de Privacy Service, diagnosticar errores y determinar los pasos siguientes adecuados al enviar o supervisar trabajos de privacidad en **Adobe Experience Platform**. Para obtener información sobre cómo crear, enviar y supervisar trabajos de privacidad, consulte la [guía de extremo de trabajos de privacidad](./privacy-jobs.md) o la [guía de usuario de IU de Privacy Service](../ui/user-guide.md).

Los códigos de error de Privacy Service son un contrato público estable. Cada código de error identifica de forma exclusiva un estado de error o finalización en el que puede confiar para la gestión programática y los flujos de trabajo operativos.

Al crear flujos de trabajo de automatización o monitorización, se aplican las siguientes garantías:

* Los códigos de error son estables una vez publicados.
* Los mensajes de error pueden cambiar para mejorar la claridad, pero el valor del código no.
* Los nuevos códigos de error se pueden añadir con el tiempo; los códigos existentes no se vuelven a utilizar.

Utilice códigos de error, no texto de mensaje, para implementar la automatización o la lógica de decisión. Para obtener instrucciones sobre cómo procesar de forma eficaz los trabajos de privacidad, supervisar el estado de los trabajos y administrar los errores sin depender de las cadenas de sondeo o de mensaje, consulte [Prácticas recomendadas de Privacy Service](../best-practices.md).

## Formato de respuesta de error {#error-response-format}

Privacy Service devuelve información de error en las respuestas de trabajo y solicitud. La respuesta incluye un código de error numérico y un mensaje legible en lenguaje natural en la carga útil de respuesta.

El código de error transmite el resultado autorizado. El mensaje proporciona contexto adicional para la resolución de problemas.

Este documento describe el significado y la intención de cada código de error. Para obtener esquemas de respuesta de nivel de campo y detalles de solicitud, consulte la [documentación de la API de Privacy Service](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

## Dominios de error {#error-domains}

Los códigos de error se agrupan por dominio funcional para ayudarle a diagnosticar los problemas con mayor rapidez.

Los dominios utilizados en este documento incluyen:

* **Validación de solicitud**: La solicitud tiene un formato incorrecto o contiene valores no válidos. Consulte la [guía de extremo de trabajos de privacidad](./privacy-jobs.md) para conocer la estructura de solicitudes y los requisitos de validación.
* **Autorización y aprovisionamiento**: Su organización o usuario carece del acceso requerido. Consulte [administrar permisos](../permissions.md) para revisar los requisitos de permisos basados en roles.
* **Identidad y aplicabilidad**: los identificadores o áreas de nombres no son aplicables a la solicitud. Vea [datos de identidad para solicitudes de privacidad](../identity-data.md) para conocer los tipos de identidad compatibles y los requisitos de área de nombres.
* **Limitación de velocidad**: el volumen de envío supera los límites de la plataforma. Cuando se produzca este error, reduzca la tasa de envío e inténtelo de nuevo.
* **Acceso y procesamiento de datos**: el sistema no puede acceder a los datos solicitados ni procesarlos. Consulte la [guía de solución de problemas](../troubleshooting-guide.md) para ver las causas comunes y los pasos de corrección.
* **Cifrado y administración de claves**: las claves de cifrado requeridas no están disponibles. Consulte [Claves administradas por el cliente](../../landing/governance-privacy-security/customer-managed-keys/overview.md) para obtener instrucciones de acceso, configuración y recuperación de claves.
* **Estado de ejecución del trabajo**: el trabajo se completó total, parcialmente o con errores. Consulte la [guía de extremo de trabajos de privacidad](./privacy-jobs.md#status-categories) para obtener descripciones de las categorías de estado del trabajo y sus significados.

>[!NOTE]
>
>Las asignaciones de dominio reflejan la intención del código de error, no los límites internos del servicio.

## Referencia de código de error {#error-code-reference}

La siguiente tabla enumera todos los códigos de error públicos de Privacy Service.

| Código de error | Estado HTTP | Título | Descripción |
| ---------- | ----------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| 1000-400 | 400 | Error de formato | Uno o varios valores de datos de la aplicación especificada tienen problemas de formato. Consulte los detalles del trabajo para obtener más información. |
| 1001-400 | 400 | No autorizado | Su organización no está aprovisionada. Póngase en contacto con el administrador para obtener más información. |
| 1010-400 | 400 | Permisos faltantes | No tiene los permisos necesarios para realizar esta acción. Póngase en contacto con el administrador para solicitar el acceso. |
| 1020-400 | 400 | Error de carga y archivo | Se ha producido un problema al cargar y archivar datos de acceso. Cargue los datos de acceso e inténtelo de nuevo. |
| 1021-400 | 400 | Error del trabajo | Error en uno o varios trabajos de privacidad creados a partir de la solicitud. Revise los detalles de los trabajos con errores para obtener más información. |
| 1022-400 | 400 | Error de acceso a datos | Se ha producido un problema al acceder a los datos especificados. Revise los detalles del trabajo para obtener más información. |
| 1023-400 | 400 | Error de acceso a datos | Se ha producido un problema al acceder o localizar los ID de conjuntos de datos especificados. Compruebe que los ID proporcionados son válidos e inténtelo de nuevo. |
| 1024 - 400 | 400 | Error inesperado | Error inesperado. Revise los detalles del trabajo para obtener más información. |
| 1030-400 | 400 | Límite de tasa de documento excedido | La carga de trabajo ha superado el límite de tasa del documento. Reduzca la tasa de envío e inténtelo de nuevo. |
| 1040-400 | 400 | Error de acceso de cifrado de claves | No se pudieron procesar los datos porque el almacén de datos está cifrado y se revocó el acceso a la clave. Póngase en contacto con el administrador del almacén de claves para restaurar el acceso a la clave del cliente. |
| 6000-200 | 200 | Correcto | El trabajo se ha completado correctamente. Revise los detalles del trabajo para confirmar los registros y resultados procesados. |
| 6051-200 | 200 | No aprovisionado | Su organización no está aprovisionada para la aplicación solicitada. La solicitud no es aplicable. |
| 6052-200 | 200 | ID de usuario no encontrados | No se han encontrado algunos ID de usuario y los desconocidos no son aplicables a este producto. Asegúrese de que los ID de usuario sean válidos e inténtelo de nuevo. |
| 6053-200 | 200 | Área de nombres no válida | El área de nombres de identidad proporcionada no es válida para esta aplicación. Utilice un área de nombres reconocida por el sistema. |
| 6054-200 | 200 | Completado parcialmente | Se ha completado el trabajo para los datos aplicables, pero algunos no eran aplicables a la solicitud. Revise los detalles del trabajo para obtener más información. |

{style="table-layout:auto"}
