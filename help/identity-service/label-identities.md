---
keywords: Experience Platform;inicio;temas populares;identidades de etiqueta
title: Etiquetado de un campo como identidad en la IU
description: Los campos que contienen información de identificación personal (PII) se pueden etiquetar como campos de identidad. El servicio de identidad interpreta un valor proporcionado en un campo de identidad como una identidad. El área de nombres de la identidad se especifica como parte del etiquetado del campo.
hide: true
hidefromtoc: true
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 0d111241658b4014d1ca2e6013d21a4782d81be9
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# Etiquetado de un campo como identidad en la IU

Los campos que contienen información de identificación personal (PII) se pueden etiquetar como campos de identidad. [!DNL Identity Service] interpreta un valor proporcionado en un campo de identidad como una identidad. El área de nombres de la identidad se especifica como parte del etiquetado del campo.

Se deben cumplir los siguientes criterios para que un campo se etiquete como identidad:

* Solo se pueden utilizar campos de tipo cadena para la identidad
* Las identidades solo se reconocen en los datos de registros y series temporales
* Solo los campos PII deben marcarse como identidad. Elegir un campo que represente datos más genéricos resultaría en relaciones menos precisas y en posibles errores que accederían a identidades relacionadas desde el gráfico de identidades

Para obtener instrucciones sobre cómo etiquetar campos de identidad en la interfaz de usuario, consulte la guía sobre [definición de campos de identidad en la interfaz de usuario](../xdm/ui/fields/identity.md).

## Pasos siguientes

Para obtener más información sobre [!DNL Identity Service], consulte la [[!DNL Identity Service] información general](./home.md).
