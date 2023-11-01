---
solution: Experience Platform
title: Introducción
description: Obtenga información sobre cómo empezar a utilizar la funcionalidad de manuales de tácticas de casos de uso.
badgeBeta: label="Beta" type="Informative"
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 100%

---

# (Beta) Introducción

>[!AVAILABILITY]
>
>Actualmente, esta funcionalidad está en versión beta y no está disponible para todos los usuarios. La documentación y las funcionalidades están sujetas a cambios.

## Creación de una zona protegida de desarrollo {#create-development-sandbox}

Para empezar y obtener acceso a la funcionalidad [[!UICONTROL Manuales de tácticas de casos de uso]](/help/use-case-playbooks/playbooks/overview.md), [cree una nueva zona protegida de desarrollo](/help/sandboxes/ui/user-guide.md#create) (asegúrese de no seleccionar una zona protegida de producción) con el nombre (no el título) que contiene `-ucp` o `-UCP` en el sufijo, como se muestra a continuación.

![Creación de una zona protegida de desarrollo para manuales de tácticas de casos de uso](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Ahora debería ver [!UICONTROL Manuales de tácticas] en el carril izquierdo debajo de [!UICONTROL Manuales de tácticas de casos de uso] o en [!UICONTROL Área de experto en marketing].

![Manuales de tácticas de casos de uso en la IU después de crear una zona protegida.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Si no ve [!UICONTROL Manuales de tácticas] en el carril izquierdo, como se muestra arriba, utilice este vínculo `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` para ir directamente allí. En el vínculo, `<YOUR_ORG>` es el nombre de su organización y `<YOUR_SANDBOX_NAME>` es el nombre de la zona protegida de desarrollo que ha creado.

### Configuración de zona protegida para usuarios de Adobe Journey Optimizer {#sandbox-configuration-journey-optimizer}

Si su organización tiene licencia para [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es), tendrá que configurar los ajustes preestablecidos de canal en su zona protegida, que definen los parámetros técnicos necesarios para sus mensajes. [Obtenga información sobre cómo configurar superficies de canal en Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=es).

## Conceda a su equipo los permisos de acceso necesarios {#grant-access-permissions}

Para empezar con [!UICONTROL Manuales de tácticas de casos de uso], los miembros de su equipo de operaciones de marketing necesitan los permisos adecuados. Puede conceder permisos a su equipo de este modo:

* Los integrantes del equipo de operaciones de marketing que solo deseen examinar los manuales de tácticas pueden obtener permiso de **lectura**.
* Los integrantes del equipo de operaciones de marketing que deseen crear instancias a partir de manuales de tácticas pueden obtener los siguientes permisos de **lectura y escritura**.

## Pasos siguientes {#next-steps}

Después de leer este documento, ya sabe cómo empezar a usar los [!UICONTROL Manuales de tácticas de casos de uso]. A continuación, lea cómo [descubrir el manual de tácticas adecuado](/help/use-case-playbooks/playbooks/discover.md) para usted y luego [crear instancias a partir de él](/help/use-case-playbooks/playbooks/create-share-reuse.md).
