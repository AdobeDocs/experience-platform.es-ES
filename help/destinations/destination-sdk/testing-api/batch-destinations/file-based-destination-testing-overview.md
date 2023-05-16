---
description: Aprenda a utilizar la API de prueba de destino basada en archivos para validar la configuración de los destinos basados en archivos creada mediante el Destination SDK.
title: API de prueba de destino basada en archivos
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Resumen de la API de prueba de destino basada en archivos

La API de prueba de destino basada en archivos es un conjunto de extremos que puede utilizar para validar la configuración de los destinos basados en archivos creada mediante el Destination SDK.

Se recomienda utilizar estas herramientas para validar la configuración antes de [envío](../../guides/submit-destination.md) su destino para su revisión a Adobe.

Para obtener los mejores resultados de prueba, se recomienda utilizar esta API en función del diagrama de flujo que aparece a continuación.

![Diagrama que muestra el flujo de prueba de destino recomendado](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

Consulte las secciones siguientes para obtener una breve descripción general de lo que puede hacer cada punto final.

## Generación de perfiles de ejemplo {#generate-sample-profiles}

Utilice la variable `/sample-profiles` Punto final de API para generar perfiles de muestra basados en el esquema de origen existente.

Los perfiles de muestra pueden ayudarle a comprender la estructura JSON de un perfil. Además, le proporcionan un valor predeterminado que puede personalizar con sus propios datos de perfil para realizar más pruebas de destino.

Consulte la [documentación dedicada](file-based-sample-profile-generation-api.md) para obtener información sobre cómo generar perfiles de muestra.

## Probar la configuración de destino {#test-destination-configuration}

Utilice la variable `/testing/destinationInstance` Punto final de API para comprobar si el destino basado en archivos está configurado correctamente y para verificar la integridad de los flujos de datos en el destino configurado.

Puede realizar solicitudes en el extremo de prueba con o sin agregar [perfiles de muestra](file-based-sample-profile-generation-api.md) a la llamada . Si no envía ningún perfil en la solicitud, la API genera un perfil de muestra automáticamente y lo añade a la solicitud.

Consulte la [documentación dedicada](file-based-destination-testing-api.md) para aprender a probar la configuración de destino con perfiles de ejemplo.

## Ver resultados de activación detallados {#view-detailed-activation-results}

Utilice la variable `/testing/destinationInstance` punto final de API para ver los detalles completos de los resultados de las pruebas de destino basadas en archivos.

Este extremo de API devuelve el mismo resultado que obtendría al usar la variable [API del servicio de flujo](../../../api/update-destination-dataflows.md) para controlar los flujos de datos.

Consulte la [documentación dedicada](file-based-destination-results-api.md) para obtener información sobre cómo ver los resultados de activación detallados.

## Procesar campos de datos de clientes {#render-customer-data-fields}

Utilice la variable `/authoring/testing/template/render` Punto final de API para visualizar cómo se establece la plantilla [campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) definido en la configuración de destino tendría el aspecto siguiente.

El extremo API genera valores aleatorios para los campos de datos del cliente y los devuelve en la respuesta. Esto le ayuda a validar la estructura semántica de los campos de datos del cliente, como los nombres de bloque o las rutas de carpeta.

Consulte la [documentación dedicada](file-based-render-template-api.md) para aprender a generar y visualizar valores para los campos de datos de los clientes.
