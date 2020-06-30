---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Etiquetar un campo como identidad
topic: api guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 1%

---


# Etiquetar un campo como identidad

Los campos que contienen información de identificación personal (PII) pueden etiquetarse como campos de identidad. Un valor proporcionado en un campo de identidad se interpreta como una identidad por [!DNL Identity Service]. La Área de nombres de la identidad se especifica como parte del etiquetado del campo.

Se deben cumplir los siguientes criterios para que un campo se etiquete como identidad:

- Solo se pueden usar campos de tipo de cadena para la identidad
- Las identidades solo se reconocen en los datos de registros y series temporales
- Solo los campos PII deben marcarse como identidad. Si se elige un campo que representa datos más genéricos, las relaciones serán menos precisas y se producirán posibles errores al acceder a identidades relacionadas desde el gráfico de identidad

Para obtener instrucciones sobre cómo utilizar la API del Registro de Esquema para etiquetar un campo como identidad, visite [Crear un descriptor](../../xdm/api/descriptors.md).

## Pasos siguientes

Continúe con el siguiente tutorial sobre las identidades del clúster de [lista](./list-cluster-identites.md)