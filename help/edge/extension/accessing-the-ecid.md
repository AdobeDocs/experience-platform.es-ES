---
title: Acceso al ECID
description: Extensión de SDK web de Adobe Experience Platform que aprovecha ECID en etiquetas
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 5%

---

# Acceso al ECID

El [!DNL Experience Cloud Identity (ECID)] es un identificador persistente para un visitante del sitio web. En determinadas circunstancias, es posible que prefiera acceder al ECID (para enviarlo a un tercero, por ejemplo).

Para acceder al ECID dentro de las etiquetas, Adobe recomienda lo siguiente:

1. Asegúrese de que la propiedad esté configurada con [Secuencia de componentes de regla](../../tags/ui/managing-resources/rules.md#sequencing) activado.
1. Crear una regla nueva.
1. Añadir un [!UICONTROL Library Loaded] a la regla.
1. Añadir un [!UICONTROL Condición personalizada] acción a la regla con el siguiente código (suponiendo que el nombre configurado para la instancia del SDK sea `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Guarde la regla.

A continuación, debe poder acceder al ECID en reglas posteriores utilizando `%ECID%` o `_satellite.getVar("ECID")` como lo haría con cualquier otro elemento de datos.
