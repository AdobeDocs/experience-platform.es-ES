---
description: La API de prueba de destino basada en archivos es una colección de puntos de conexión que puede utilizar para validar la configuración de los destinos basados en archivos creados mediante el Destination SDK.
title: API de prueba de destino basada en archivos
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# API de prueba de destino basada en archivos

## Información general {#overview}

La API de prueba de destino basada en archivos es un conjunto de puntos de conexión que puede utilizar para validar la configuración de los destinos basados en archivos creados mediante el Destination SDK.

Se recomienda utilizar estas herramientas para validar la configuración antes de [enviando](submit-destination.md) Seleccione su destino para revisar el Adobe.

Para obtener los mejores resultados de las pruebas, recomendamos utilizar esta API en función del diagrama de flujo que aparece a continuación.

![Diagrama que muestra el flujo de prueba de destino recomendado](assets/file-based-testing-flow.png)

Consulte las secciones siguientes para obtener una breve descripción de lo que puede hacer cada extremo.

## Generación de perfiles de muestra {#generate-sample-profiles}

Utilice el `/sample-profiles` Extremo de API para generar perfiles de muestra basados en el esquema de origen existente.

Los perfiles de muestra pueden ayudarle a comprender la estructura JSON de un perfil. Además, le proporcionan un valor predeterminado que puede personalizar con sus propios datos de perfil para realizar más pruebas de destino.

Consulte la [documentación dedicada](file-based-sample-profile-generation-api.md) para obtener información sobre cómo generar perfiles de muestra.

## Probar configuración de destino {#test-destination-configuration}

Utilice el `/testing/destinationInstance` Punto final de API para probar si el destino basado en archivos está configurado correctamente y comprobar la integridad de los flujos de datos al destino configurado.

Puede realizar solicitudes al extremo de prueba con o sin agregar [perfiles de muestra](file-based-sample-profile-generation-api.md) a la llamada. Si no envía ningún perfil en la solicitud, la API genera un perfil de muestra automáticamente y lo añade a la solicitud.

Consulte la [documentación dedicada](file-based-destination-testing-api.md) para obtener información sobre cómo probar la configuración de destino con perfiles de muestra.

## Ver resultados detallados de la activación {#view-detailed-activation-results}

Utilice el `/testing/destinationInstance` Punto final de API para ver los detalles completos de los resultados de las pruebas de destino basadas en archivos.

Este extremo de API devuelve el mismo resultado que obtendría al usar el [API de Flow Service](../api/update-destination-dataflows.md) para monitorizar flujos de datos.

Consulte la [documentación dedicada](file-based-destination-results-api.md) para obtener información sobre cómo ver los resultados detallados de la activación.

## Procesar campos de datos de clientes {#render-customer-data-fields}

Utilice el `/authoring/testing/template/render` Extremo de API para visualizar cómo se personalizan las plantillas [campos de datos del cliente](file-based-destination-configuration.md#customer-data-fields) definido en la configuración de destino tendría el siguiente aspecto:.

El extremo de la API genera valores aleatorios para los campos de datos del cliente y los devuelve en la respuesta. Esto le ayuda a validar la estructura semántica de los campos de datos del cliente, como los nombres de los bloques o las rutas de carpetas.

Consulte la [documentación dedicada](file-based-render-template-api.md) para aprender a generar y visualizar valores para los campos de datos de clientes.
