---
keywords: Experience Platform;inicio;temas populares;identidades de etiqueta
solution: Experience Platform
title: Etiquetar un campo como identidad
topic: api guide
description: Los campos que contienen información de identificación personal (PII) pueden etiquetarse como campos de identidad. El servicio de identidad interpreta un valor proporcionado en un campo de identidad como una identidad. La Área de nombres de la identidad se especifica como parte del etiquetado del campo.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# Etiquetado de un campo como identidad

Los campos que contienen información de identificación personal (PII) pueden etiquetarse como campos de identidad. Un valor proporcionado en un campo de identidad se interpreta como una identidad por [!DNL Identity Service]. La Área de nombres de la identidad se especifica como parte del etiquetado del campo.

Se deben cumplir los siguientes criterios para que un campo se etiquete como identidad:

- Solo se pueden usar campos de tipo de cadena para la identidad
- Las identidades solo se reconocen en los datos de registros y series temporales
- Solo los campos PII deben marcarse como identidad. Si se elige un campo que representa datos más genéricos, las relaciones serán menos precisas y se producirán posibles errores al acceder a identidades relacionadas desde el gráfico de identidad

Para obtener instrucciones sobre cómo utilizar la API del Registro de Esquema para etiquetar un campo como identidad, visite [guía de extremo de descriptores](../../xdm/api/descriptors.md#create).

## Pasos siguientes

Continúe con el siguiente tutorial para [identidades de clúster de lista](./list-cluster-identites.md)