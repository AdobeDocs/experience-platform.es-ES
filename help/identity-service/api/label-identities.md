---
keywords: Experience Platform;inicio;temas populares;identidades de etiquetas
solution: Experience Platform
title: Etiquetado de campos como identidad
description: Los campos que contienen información de identificación personal (PII) pueden etiquetarse como campos de identidad. El servicio de identidad interpreta un valor proporcionado en un campo de identidad como una identidad. El área de nombres de la identidad se especifica como parte del etiquetado del campo.
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Etiquetado de un campo como identidad

Los campos que contienen información de identificación personal (PII) pueden etiquetarse como campos de identidad. Un valor proporcionado en un campo de identidad se interpreta como una identidad por [!DNL Identity Service]. El área de nombres de la identidad se especifica como parte del etiquetado del campo.

Se deben cumplir los siguientes criterios para que un campo se etiquete como identidad:

- Solo se pueden utilizar campos de tipo cadena para la identidad
- Las identidades solo se reconocen en los datos de registros y series temporales
- Solo los campos PII deben marcarse como identidad. La selección de un campo que represente datos más genéricos resultaría en relaciones menos precisas y posibles errores al acceder a identidades relacionadas desde el gráfico de identidad

Para obtener instrucciones sobre cómo utilizar la API del Registro de esquemas para etiquetar un campo como identidad, visite [guía de extremo de descriptores](../../xdm/api/descriptors.md#create).

## Pasos siguientes

Continúe con el siguiente tutorial a [enumerar identidades de clúster](./list-cluster-identites.md)
