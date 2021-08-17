---
title: 'Acceso al ECID '
description: Extensión del SDK web de Adobe Experience Platform que aprovecha el ECID en las etiquetas
source-git-commit: befe1efa884706165b8d65803d06f6370a8a60f2
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 5%

---


# Acceso al ECID

El [!DNL Experience Cloud Identity (ECID)] es un identificador persistente para un visitante del sitio web. En determinadas circunstancias, es posible que prefiera acceder al ECID (para enviarlo a un tercero, por ejemplo).

Para acceder al ECID dentro de las etiquetas, Adobe recomienda lo siguiente:

1. Asegúrese de que la propiedad esté configurada con [secuenciación de componentes de regla](../../tags/ui/managing-resources/rules.md#sequencing) habilitada.
1. Crear una regla nueva.
1. Agregue un evento [!UICONTROL Library Loaded] a la regla.
1. Agregue una acción [!UICONTROL Condición personalizada] a la regla con el siguiente código (suponiendo que el nombre que ha configurado para la instancia del SDK sea `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Guarde la regla.

A continuación, debe poder acceder al ECID en reglas posteriores que utilicen `%ECID%` o `_satellite.getVar("ECID")` como lo haría con cualquier otro elemento de datos.
