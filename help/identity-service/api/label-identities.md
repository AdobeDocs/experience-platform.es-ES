---
keywords: Experience Platform;inicio;temas populares;identidades de etiqueta
solution: Experience Platform
title: Etiquetado de un campo como identidad
description: Los campos que contienen información de identificación personal (PII) se pueden etiquetar como campos de identidad. El servicio de identidad interpreta un valor proporcionado en un campo de identidad como una identidad. El área de nombres de la identidad se especifica como parte del etiquetado del campo.
role: Developer
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Etiquetado de un campo como identidad

Los campos que contienen información de identificación personal (PII) se pueden etiquetar como campos de identidad. Un valor proporcionado en un campo de identidad se interpreta como una identidad por [!DNL Identity Service]. El área de nombres de la identidad se especifica como parte del etiquetado del campo.

Se deben cumplir los siguientes criterios para que un campo se etiquete como identidad:

- Solo se pueden utilizar campos de tipo cadena para la identidad
- Las identidades solo se reconocen en los datos de registros y series temporales
- Solo los campos PII deben marcarse como identidad. Elegir un campo que represente datos más genéricos resultaría en relaciones menos precisas y en posibles errores que accederían a identidades relacionadas desde el gráfico de identidades

Para obtener instrucciones sobre cómo utilizar la API de Registro de esquemas para etiquetar un campo como identidad, visite [guía de extremo de descriptores](../../xdm/api/descriptors.md#create).

## Pasos siguientes

Continúe con el siguiente tutorial para [enumerar identidades de clúster](./list-cluster-identites.md)
