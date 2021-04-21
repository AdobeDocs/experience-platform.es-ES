---
keywords: Experience Platform;inicio;temas populares;identidades de etiquetas
solution: Experience Platform
title: Etiquetado de campos como identidad
topic-legacy: api guide
description: Los campos que contienen información de identificación personal (PII) pueden etiquetarse como campos de identidad. El servicio de identidad interpreta un valor proporcionado en un campo de identidad como una identidad. El área de nombres de la identidad se especifica como parte del etiquetado del campo.
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Etiquetado de un campo como identidad

Los campos que contienen información de identificación personal (PII) pueden etiquetarse como campos de identidad. [!DNL Identity Service] interpreta un valor proporcionado en un campo de identidad como una identidad. El área de nombres de la identidad se especifica como parte del etiquetado del campo.

Se deben cumplir los siguientes criterios para que un campo se etiquete como identidad:

- Solo se pueden utilizar campos de tipo cadena para la identidad
- Las identidades solo se reconocen en los datos de registros y series temporales
- Solo los campos PII deben marcarse como identidad. La selección de un campo que represente datos más genéricos resultaría en relaciones menos precisas y posibles errores al acceder a identidades relacionadas desde el gráfico de identidad

Para obtener instrucciones sobre cómo utilizar la API del Registro de esquemas para etiquetar un campo como identidad, visite la [guía de extremo de descriptores](../../xdm/api/descriptors.md#create).

## Pasos siguientes

Continúe con el siguiente tutorial para [list cluster identities](./list-cluster-identites.md)
