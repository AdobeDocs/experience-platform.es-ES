---
description: La API de prueba de destino basada en archivos es una colección de extremos que puede utilizar para validar la configuración de los destinos basados en archivos creada mediante el Destination SDK.
title: API de prueba de destino basada en archivos
source-git-commit: d2d362f4b61e04fc2fa4d9cd9db70ed94a850642
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# API de prueba de destino basada en archivos

## Información general {#overview}

La API de prueba de destino basada en archivos es un conjunto de extremos que puede utilizar para validar la configuración de los destinos basados en archivos creada mediante el Destination SDK.

Se recomienda utilizar estas herramientas para validar la configuración antes de [envío](submit-destination.md) su destino para su revisión a Adobe.

Para obtener los mejores resultados de prueba, se recomienda utilizar esta API en función del diagrama de flujo que aparece a continuación.

![Diagrama que muestra el flujo de prueba de destino recomendado](assets/file-based-testing-flow.png)

Consulte las secciones siguientes para obtener una breve descripción general de lo que puede hacer cada punto final.

## Extremo de generación de muestras {#sample-generation-endpoint}

Este extremo le ayuda a generar perfiles de muestra basados en el esquema de origen existente.

Los perfiles de muestra están pensados para ayudarle a comprender la estructura JSON de un perfil. Además, le proporcionan una estructura básica que puede personalizar con sus propios datos de perfil para realizar más pruebas de destino.

Consulte la [documentación dedicada](file-based-sample-profile-generation-api.md) para obtener información sobre cómo generar perfiles de muestra.

## Punto final de prueba de configuración de destino {#destination-configuration-testing-endpoint}

Este extremo le ayuda a comprobar si el destino basado en archivos está configurado correctamente y a verificar la integridad de los flujos de datos en el destino configurado.

Puede realizar solicitudes en el extremo de prueba con o sin agregar [perfiles de muestra](file-based-sample-profile-generation-api.md) a la llamada . Si no envía ningún perfil en la solicitud, la API genera un perfil de muestra automáticamente y lo añade a la solicitud.

Consulte la [documentación dedicada](file-based-destination-testing-api.md) para aprender a probar la configuración de destino con perfiles de ejemplo.

## Punto final de los resultados de activación {#activation-results}

Este extremo le ayuda a ver los detalles completos de los resultados de las pruebas de destino basadas en archivos.

Este extremo de API devuelve el mismo resultado que obtendría al usar la variable [API del servicio de flujo](../api/update-destination-dataflows.md) para controlar los flujos de datos.

Consulte la [documentación dedicada](file-based-destination-results-api.md) para obtener información sobre cómo ver los resultados de activación detallados.

## Campos de cliente que procesan puntos de conexión {#customer-fields-rendering-endpoint}

Este extremo le ayuda a visualizar cómo se le aplica la plantilla [campos de datos del cliente](file-based-destination-configuration.md#customer-data-fields) definido en la configuración de destino tendría el aspecto siguiente.

El extremo genera valores aleatorios para los campos de datos del cliente y los devuelve en la respuesta. Esto le ayuda a validar la estructura semántica de los campos de datos del cliente, como los nombres de bloque o las rutas de carpeta.

Consulte la [documentación dedicada](file-based-render-template-api.md) para obtener información sobre cómo ver los resultados de activación detallados.