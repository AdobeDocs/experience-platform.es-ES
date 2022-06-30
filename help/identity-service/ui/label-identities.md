---
keywords: Experience Platform;inicio;temas populares;identidades de etiquetas
title: Etiquetado de campos como identidad en la interfaz de usuario
description: Los campos que contienen información de identificación personal (PII) pueden etiquetarse como campos de identidad. El servicio de identidad interpreta un valor proporcionado en un campo de identidad como una identidad. El área de nombres de la identidad se especifica como parte del etiquetado del campo.
source-git-commit: ae51c9bd07944f26be2809a6d15f9d9e8c2fd5a1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Etiquetado de un campo como identidad en la interfaz de usuario

Los campos que contienen información de identificación personal (PII) pueden etiquetarse como campos de identidad. Un valor proporcionado en un campo de identidad se interpreta como una identidad por [!DNL Identity Service]. El área de nombres de la identidad se especifica como parte del etiquetado del campo.

Se deben cumplir los siguientes criterios para que un campo se etiquete como identidad:

* Solo se pueden utilizar campos de tipo cadena para la identidad
* Las identidades solo se reconocen en los datos de registros y series temporales
* Solo los campos PII deben marcarse como identidad. La selección de un campo que represente datos más genéricos resultaría en relaciones menos precisas y posibles errores al acceder a identidades relacionadas desde el gráfico de identidad

Para obtener instrucciones sobre cómo etiquetar campos de identidad en la interfaz de usuario, consulte la guía de [definición de campos de identidad en la interfaz de usuario](../../xdm/ui/fields/identity.md).

## Pasos siguientes

Para obtener más información, consulte [!DNL Identity Service], consulte la [[!DNL Identity Service] información general](../home.md).
