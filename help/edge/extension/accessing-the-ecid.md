---
title: Acceso al ECID
description: Obtenga información sobre cómo acceder al ID de Experience Cloud (ECID) en las etiquetas de Adobe Experience Platform
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 5%

---


# Acceso al ECID

La variable [!DNL Experience Cloud ID (ECID)] es un identificador de Experience Cloud persistente que puede ayudarle a identificar a los visitantes del sitio web. En determinadas circunstancias, como el envío del identificador a una plataforma de terceros, es posible que necesite acceder a la variable [!DNL ECID].

Para acceder a la [!DNL ECID] dentro de las etiquetas , siga los pasos a continuación:

1. Asegúrese de que la propiedad esté configurada con [secuenciación de componentes de regla](../../tags/ui/managing-resources/rules.md#sequencing) activada.
2. Crear una regla nueva.
3. Agregue un [!UICONTROL Biblioteca cargada] a la regla.
4. Agregue un [!UICONTROL Condición personalizada] acción a la regla, con el siguiente código (suponiendo que el nombre que ha configurado para la instancia de SDK sea `alloy`):

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. Guarde la regla.

Ahora debería poder acceder al [!DNL ECID] en reglas posteriores, usar `%ECID%` o `_satellite.getVar("ECID")`, similar a cómo se accede a cualquier otro elemento de datos.
