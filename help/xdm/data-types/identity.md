---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;identity;tipo de datos;tipo de datos;data-type;
solution: Experience Platform
title: Tipo de datos de identidad
description: Obtenga información sobre el tipo de datos XDM de identidad.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 4%

---

# [!UICONTROL Identidad] tipo de datos

[!UICONTROL Identidad] es un tipo de datos XDM estándar que se utiliza para distinguir claramente a las personas que interactúan con experiencias digitales. La identidad la establece un proveedor de identidad, al que se hace referencia en un `namespace` atributo. Dentro de cada `namespace`, la identidad es única.

<img src="../images/data-types/identity.png" width="550" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `namespace` | Objeto | Un objeto que contiene un único campo de cadena (`code`), que indica el área de nombres asociado con el proporcionado `id` atributo. |
| `authenticatedState` | Cadena | El estado autenticado para esta identidad en el momento del evento de experiencia observado. Consulte la [apéndice](#authenticatedState) para valores y definiciones aceptados. |
| `id` | Cadena | La identidad del consumidor en el área de nombres relacionada. |
| `primary` | Booleano | Indica si esta es la identidad principal del individuo. Cada individuo solo puede tener una identidad principal. |
| `xid` | Cadena | Cuando está presente, este valor representa un identificador de área de nombres cruzado que es único en todos los identificadores de ámbito de área de nombres en todas las áreas de nombres. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Apéndice

La siguiente sección contiene información adicional sobre [!UICONTROL Identidad] tipo de datos.

## Valores aceptados para authenticatedState {#authenticatedState}

En la tabla siguiente se describen los valores aceptados para `authenticatedState` y sus significados asociados:

| Valor | Descripción |
| --- | --- |
| `ambiguous` | El estado autenticado es ambiguo. |
| `authenticated` | El usuario se identificó mediante un inicio de sesión o una acción similar válida en el momento de la observación del evento. |
| `loggedOut` | El usuario se identificó mediante una acción de inicio de sesión en un momento anterior, pero no había iniciado sesión en el momento de la observación del evento. |
