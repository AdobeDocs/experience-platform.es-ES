---
solution: Experience Platform
title: Introducción
description: Obtenga información sobre cómo empezar a utilizar la funcionalidad de libros de reproducción de casos de uso.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 297dc9d6252d401f805fa5ebb5cf5111910286cf
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 8%

---


# (Beta) Introducción

>[!AVAILABILITY]
>
>Actualmente, esta funcionalidad está en versión beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

## Creación de una zona protegida de desarrollo {#create-development-sandbox}

Para empezar y obtener acceso a la [[!UICONTROL Manuales de casos de uso]](/help/use-case-playbooks/playbooks/overview.md) funcionalidad, [crear una nueva zona protegida de desarrollo](/help/sandboxes/ui/user-guide.md#create) (asegúrese de no seleccionar una zona protegida de producción) con el nombre (no el título) que contiene `-ucp` o `-UCP` en el sufijo, como se muestra a continuación.

![Creación de una zona protegida de desarrollo para libros de reproducción de casos de uso](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Ahora debería ver [!UICONTROL Manuales] en el carril izquierdo debajo de [!UICONTROL Manuales de casos de uso] o en [!UICONTROL Área de marketing].

![Libros de casos de uso en la IU después de crear una zona protegida.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Si no ve [!UICONTROL Manuales] en el carril izquierdo, como se muestra arriba, utilice este vínculo `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` para ir directamente allí. En el vínculo, `<YOUR_ORG>` es el nombre de su organización y `<YOUR_SANDBOX_NAME>` es el nombre de la zona protegida de desarrollo que ha creado.

### Configuración de zona protegida para usuarios de Adobe Journey Optimizer {#sandbox-configuration-journey-optimizer}

Si su organización tiene licencia para [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es), tendrá que configurar los ajustes preestablecidos de canal en su zona protegida, que definen los parámetros técnicos necesarios para sus mensajes. [Obtenga información sobre cómo configurar superficies de canal en Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=es).

## Conceda a su equipo los permisos de acceso necesarios {#grant-access-permissions}

Para empezar con [!UICONTROL Manuales de casos de uso]Sin embargo, los miembros de su equipo de operaciones de marketing necesitan los permisos adecuados. Puede conceder permisos de este modo a su equipo:

* Los miembros del equipo de operaciones de marketing que solo deseen examinar los libros de reproducción pueden obtener **leer** permiso.
* Los miembros del equipo de operaciones de marketing que deseen crear instancias a partir de libros de reproducción pueden obtener lo siguiente **leer y escribir** permisos.

## Pasos siguientes {#next-steps}

Después de leer este documento, ya sabe cómo empezar a usar [!UICONTROL Manuales de casos de uso]. A continuación, lea cómo [descubra el manual adecuado](/help/use-case-playbooks/playbooks/discover.md) para ti y luego [crear instancias a partir de él](/help/use-case-playbooks/playbooks/create-share-reuse.md).
