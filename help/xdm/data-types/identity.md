---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;identidad;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de identidad
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de identidad.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 2%

---

# [!UICONTROL Identity] tipo de datos

[!UICONTROL Identity] es un tipo de datos XDM estándar que se utiliza para distinguir claramente a las personas que interactúan con experiencias digitales. La identidad la establece un proveedor de identidad, al que se hace referencia en un atributo `namespace`. Dentro de cada `namespace`, la identidad es única.

<img src="../images/data-types/identity.png" width="550" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `namespace` | Objeto | Un objeto que contiene un solo campo de cadena (`code`), que indica el área de nombres asociado al atributo proporcionado `id`. |
| `authenticatedState` | Cadena | El estado autenticado para esta identidad en el momento del evento de experiencia observado. Consulte el [apéndice](#authenticatedState) para conocer los valores y definiciones aceptados. |
| `id` | Cadena | La identidad del consumidor en el área de nombres relacionada. |
| `primary` | Booleano | Indica si esta es la identidad principal del individuo. Cada individuo solo puede tener una identidad principal. |
| `xid` | Cadena | Cuando está presente, este valor representa un identificador de área de nombres cruzada que es único en todos los identificadores de ámbito de área de nombres en todos los espacios de nombres. |

Para obtener más información sobre la mezcla, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Apéndice

La siguiente sección contiene información adicional sobre el tipo de datos [!UICONTROL Identity].

## Valores aceptados para authenticationState {#authenticatedState}

La siguiente tabla describe los valores aceptados para `authenticatedState` y sus significados asociados:

| Valor | Descripción |
| --- | --- |
| `ambiguous` | El estado autenticado es ambiguo. |
| `authenticated` | El usuario se identificó mediante un inicio de sesión o una acción similar que era válida en el momento de la observación del evento. |
| `loggedOut` | El usuario se identificó mediante una acción de inicio de sesión en algún momento anterior, pero no se inició sesión en el momento de la observación del evento. |
