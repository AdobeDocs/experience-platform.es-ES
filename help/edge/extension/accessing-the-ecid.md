---
title: 'Acceso al ECID '
description: Extensión del SDK web de Adobe Experience Platform que aprovecha ECID en Adobe Experience Platform Launch
source-git-commit: 3002036d7366e2f7310aa62e53c7c391d9ff7a07
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---


# Acceso al ECID

El [!DNL Experience Cloud Identity (ECID)] es un identificador persistente para un visitante del sitio web. En determinadas circunstancias, es posible que prefiera acceder al ECID (para enviarlo a un tercero, por ejemplo).

Para acceder al ECID dentro de Adobe Experience Platform Launch, Adobe recomienda lo siguiente:

1. Asegúrese de que la propiedad esté configurada con [secuenciación de componentes de regla](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing) habilitada.
1. Crear una regla nueva.
1. Agregue un evento [!UICONTROL Library Loaded] a la regla.
1. Agregue una acción [!UICONTROL Custom Condition] a la regla con el siguiente código (suponiendo que el nombre que ha configurado para la instancia del SDK sea `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Guarde la regla.

A continuación, debe poder acceder al ECID en reglas posteriores que utilicen `%ECID%` o `_satellite.getVar("ECID")` como lo haría con cualquier otro elemento de datos.
