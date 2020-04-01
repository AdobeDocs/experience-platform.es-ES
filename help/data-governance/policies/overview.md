---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Información general sobre las directivas de uso de datos
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842

---


# Información general sobre las directivas de uso de datos

Para que las etiquetas de uso de datos admitan de manera efectiva el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las directivas de uso de datos son reglas que describen los tipos de acciones de marketing que puede realizar o que tienen restricciones para realizar en los datos de la plataforma de experiencia.

Un ejemplo de una acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si existe una política que indica que determinados tipos de datos, como Información de identificación personal (PII), no se pueden exportar y se ha aplicado una etiqueta &quot;I&quot; (Datos de identidad) al conjunto de datos, recibirá una respuesta del Servicio de directivas que le indicará que se ha violado una política de uso de datos.

## Cómo crear y trabajar con políticas de uso de datos

Una vez aplicadas las etiquetas de uso de datos, los administradores de datos pueden crear políticas mediante la API [del servicio de directivas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE.

Como administrador de datos, puede utilizar la API de servicio de directivas para administrar y evaluar las políticas relacionadas con las acciones de marketing que se realizan en datos que contienen etiquetas DULE. Mediante la API, puede crear y actualizar políticas, determinar el estado de una política y trabajar con acciones de marketing para evaluar si una acción específica infringe una política de uso de datos.

Dentro de la API de servicio de directivas, todas las directivas y acciones de marketing se denominan `core` o `custom` recursos. `core` los recursos son definidos y mantenidos por Adobe, mientras que `custom` los recursos son creados y mantenidos por clientes individuales. Por lo tanto, los `custom` recursos son únicos y visibles únicamente para la organización que los creó.

Para obtener más información sobre cómo realizar las operaciones clave proporcionadas por la API de servicio de directivas DULE, consulte la guía [para desarrolladores de](../api/getting-started.md)Policy Service. Para obtener instrucciones paso a paso sobre cómo trabajar con políticas DULE, consulte el tutorial sobre la [creación y evaluación de políticas](create.md)DULE.