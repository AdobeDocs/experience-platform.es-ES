---
title: Resumen de reglas de vinculación de gráficos de identidad
description: Obtenga información acerca de las reglas de vinculación de gráficos de identidad en Identity Service.
hide: true
hidefromtoc: true
badge: Alfa
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 20b8433cee719329bce562069c328adb906697a0
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Resumen de reglas de vinculación de gráficos de identidad

>[!IMPORTANT]
>
>Las reglas de vinculación de gráficos de identidad están actualmente en Alpha. La funcionalidad y la documentación están sujetas a cambios.

## Índice 

* [Información general](./overview.md)
* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Casos de ejemplo](./example-scenarios.md)
* [Servicio de identidad y perfil del cliente en tiempo real](identity-and-profile.md)
* [Lógica de vinculación de identidad](./identity-linking-logic.md)

Con el servicio de identidad de Adobe Experience Platform y el perfil del cliente en tiempo real, es fácil suponer que los datos se incorporan perfectamente y que todos los perfiles combinados representan a una sola persona individual a través de un identificador de persona, como un ID de CRM. Sin embargo, hay escenarios posibles en los que ciertos datos podrían intentar combinar varios perfiles dispares en un único perfil (&quot;colapso de perfil&quot;). Para evitar estas combinaciones no deseadas, puede utilizar las configuraciones proporcionadas mediante reglas de vinculación de gráficos de identidad y permitir una personalización precisa para los usuarios.

## Casos de ejemplo en los que podría producirse un colapso de perfil

* **Dispositivo compartido**: dispositivo compartido hace referencia a dispositivos utilizados por más de un individuo. Algunos ejemplos de dispositivos compartidos son tabletas, equipos de biblioteca y quioscos.
* **Correo electrónico y números de teléfono incorrectos**: Los números de correo electrónico y teléfono incorrectos hacen referencia a usuarios finales que registran información de contacto no válida, como &quot;prueba&quot;<span>@test.com&quot; para correo electrónico y &quot;+1-111-111-1111&quot; para número de teléfono.
* **Valores de identidad erróneos o incorrectos**: Los valores de identidad erróneos o incorrectos hacen referencia a valores de identidad no únicos que podrían combinar ID de CRM. Por ejemplo, aunque los IDFA deben tener 36 caracteres (32 caracteres alfanuméricos y cuatro guiones), hay escenarios en los que se puede introducir un IDFA con un valor de identidad &quot;user_null&quot;. Del mismo modo, los números de teléfono solo admiten caracteres numéricos, pero se puede introducir un área de nombres de teléfono con un valor de identidad &quot;no especificado&quot;.

Para obtener más información sobre casos de uso de reglas de vinculación de gráficos de identidad, lea el documento sobre [escenarios de ejemplo](./example-scenarios.md).

## Objetivos de reglas de vinculación de gráfico de identidad

Con las reglas de vinculación de gráficos de identidad puede:

* Cree un único gráfico de identidad o perfil combinado para cada usuario configurando áreas de nombres únicas (límites), lo que evitará que dos identificadores de persona diferentes se combinen en un gráfico de identidad.
* Asociar eventos autenticados en línea a la persona configurando prioridades

### Límites

Un área de nombres única es un identificador que representa a un individuo, como un ID de CRM, un ID de inicio de sesión y un correo electrónico con hash. Si un área de nombres se designa como única, un gráfico solo puede tener una identidad con ese área de nombres (`limit=1`). Esto evitará la combinación de dos identificadores de persona dispares dentro del mismo gráfico.

* Si no se configura un límite, esto podría dar como resultado combinaciones de gráficos no deseadas, como dos identidades con un área de nombres de ID de CRM en un gráfico.
* Si no se configura un límite, el gráfico puede agregar tantas áreas de nombres como sea necesario siempre y cuando el gráfico esté dentro de las barreras (50 identidades/gráfico).
* Si se configura un límite, el algoritmo de optimización de identidad garantizará que se aplique.

### Algoritmo de optimización de identidad

El algoritmo de optimización de identidad es una regla que garantiza que se apliquen los límites. El algoritmo respeta los vínculos más recientes y elimina los vínculos más antiguos para garantizar que un gráfico determinado se mantenga dentro de los límites definidos.

A continuación se muestra una lista de implicaciones del algoritmo en la asociación de eventos anónimos a identificadores conocidos:

* El ECID se asociará al último usuario autenticado si se cumplen las siguientes condiciones:
   * Si ECID (dispositivo compartido) combina los ID de CRM.
   * Si los límites están configurados para un solo ID de CRM.

Para obtener más información, lea el documento sobre [algoritmo de optimización de identidad](./identity-optimization-algorithm.md).

### Prioridad

>[!IMPORTANT]
>
>Actualmente, las prioridades de área de nombres no están disponibles para alfa.

Puede utilizar la prioridad del área de nombres para definir qué áreas de nombres son más importantes que otras. La jerarquía que establezca para sus áreas de nombres se utilizará para definir identidades principales y almacenar fragmentos de perfil. Si se establece la configuración de prioridad, ya no se utilizará la configuración de identidad principal del SDK web para determinar qué fragmentos de perfil se almacenan.

* Los límites y la prioridad son configuraciones independientes y lo hacen **no** se afectan mutuamente:
   * Límites es una configuración de gráfico de identidad en el servicio de identidad.
   * La prioridad es una configuración de fragmento de perfil en el Perfil del cliente en tiempo real.
   * La prioridad sí **no** afectan a las protecciones del sistema de gráficos de identidad.

>[!BEGINSHADEBOX]

**Ejemplo de prioridad de área de nombres**

Supongamos que ha configurado la siguiente prioridad para sus áreas de nombres:

1. ID de CRM: representa a un usuario.
2. IDFA: representa un dispositivo de hardware de Apple, como un iPhone y iPad.
3. GAID: representa un dispositivo de hardware de Google, como Google Pixel.
4. ECID: Representa un explorador web, como Firefox, Safari y Chrome.
5. AAID: Representa un explorador web.
Si ECID y AAID se envían simultáneamente, ambas identidades representan el mismo explorador web (duplicado).

Si se incorporan los siguientes eventos de experiencia en Experience Platform, los fragmentos de perfil se almacenan con el área de nombres con la prioridad más alta.

**Eventos autenticados:**

* Si el mapa de identidad contiene un ECID, un GAID y un ID de CRM, la información del evento se almacenará con el ID de CRM (identidad principal).
   * GAID representa un dispositivo de hardware Google (por ejemplo, Google Pixel), ECID representa un explorador web (por ejemplo, Google Chrome) y CRM ID representa un usuario autenticado.
   * Si el mapa de identidad contiene un ID de CRM, un ECID y un AAID, la información del evento se almacenará con el ID de CRM (identidad principal).

**Eventos no autenticados:**

* Si el mapa de identidad contiene un ECID, IDFA y AAID, la información del evento se almacenará con el IDFA (identidad principal).
   * IDFA representa un dispositivo de hardware Apple (por ejemplo, iPhone), ECID y AAID representan un explorador web (Safari).

>[!ENDSHADEBOX]

## Pasos siguientes

Para obtener más información sobre las reglas de vinculación de gráficos de identidad, lea la siguiente documentación:

* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Casos de ejemplo para configurar reglas de vinculación de gráficos de identidad](./example-scenarios.md)
* [Servicio de identidad y perfil del cliente en tiempo real](identity-and-profile.md)
* [Lógica de vinculación de identidad](./identity-linking-logic.md)
