---
solution: Experience Platform
title: Introducción a los manuales de casos de uso
description: Obtenga información sobre cómo empezar a utilizar la funcionalidad de manuales de tácticas de casos de uso.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 703c84e61af105bc3933e4750a3cb27df8ac19fe
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 14%

---


# Introducción 

Aprenda a configurar su cuenta para libros de reproducción de casos de uso, diseñados para Real-time Customer Data Platform y Adobe Journey Optimizer si no se configura automáticamente. Los tres pasos de configuración principales son:

* Creación de una zona protegida
* Configuración de permisos de usuario
* Configuración de las superficies de canal de Journey Optimizer para notificaciones por correo electrónico, push y SMS (si planea utilizar libros de reproducción de Journey Optimizer)

Para acceder a una amplia galería de libros de casos de uso en la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Libros de reproducción]** en el panel de navegación izquierdo. Lea la documentación sobre cómo [navegar por los manuales de casos de uso](../playbooks/navigate.md) y comience con una [zona protegida inspiradora](../playbooks/navigate.md).

## Configuración de libros de casos de uso: tutorial en vídeo {#video}

Vea este vídeo para conocer los pasos necesarios para crear su zona protegida, configurar permisos y configurar superficies de canal para notificaciones por correo electrónico, push y SMS en Journey Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3449829?learn=on&captions=spa)

## Creación de una zona protegida de desarrollo {#create-development-sandbox}

Los libros de casos de uso utilizan un tipo especial de zona protegida de desarrollo. Para empezar y obtener acceso a la funcionalidad [[!UICONTROL Manuales de tácticas de casos de uso]](/help/use-case-playbooks/playbooks/overview.md), [cree una nueva zona protegida de desarrollo](/help/sandboxes/ui/user-guide.md#create) (asegúrese de no seleccionar una zona protegida de producción) con el nombre (no el título) que contiene `-ucp` o `-UCP` en el sufijo, como se muestra a continuación.

>[!IMPORTANT]
>
>Cuando cree una nueva zona protegida de desarrollo, asegúrese de que el nombre contenga `-ucp` o `-UCP` en el sufijo.


![Creación de una zona protegida de desarrollo para manuales de tácticas de casos de uso](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Ahora debería ver [!UICONTROL Libros de reproducción] en el carril izquierdo bajo [!UICONTROL Libros de reproducción de casos de uso].

![Manuales de tácticas de casos de uso en la IU después de crear una zona protegida.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Si no ve [!UICONTROL Manuales de tácticas] en el carril izquierdo, como se muestra arriba, utilice este vínculo `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` para ir directamente allí. En el vínculo, `<YOUR_ORG>` es el nombre de su organización y `<YOUR_SANDBOX_NAME>` es el nombre de la zona protegida de desarrollo que ha creado.

## Conceda a su equipo los permisos de acceso necesarios {#grant-access-permissions}

Para empezar a usar [!UICONTROL Casos de uso de libros], los miembros de su equipo de marketing necesitan los permisos adecuados para poder ver la lista de libros de reproducción creados o crearlos ellos mismos.

**Permisos necesarios**

Para agregar los permisos necesarios, en la interfaz de usuario de Permisos, incluya la nueva zona protegida del libro de casos de uso en [funciones que ya ha configurado](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role), incluidas las utilizadas para otras zonas protegidas de desarrollo.

![Ya se ha configurado la zona protegida del libro de estrategias para las funciones](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Configurar un rol para libros de reproducción:**

También podría considerar agregar nuevas funciones con [los permisos necesarios](/help/access-control/home.md#sandboxes-and-permissions).

[Configure una función nueva](/help/access-control/abac/ui/permissions.md) con los permisos necesarios para las tareas esenciales del manual de implementación. Cree una función y añádale la nueva zona protegida, como se muestra a continuación.

![Crear un rol y agregarlo a la zona protegida](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Permisos para instancias de libros de reproducción**

Como parte de los libros de reproducción de casos de uso, creará varios recursos, como esquemas, audiencias, destinos y recorridos. Usted y otros usuarios necesitarán los permisos adecuados para crear estos objetos.

**Permisos para esquemas**

Para crear y administrar esquemas, utilice los permisos de modelado de datos; **[!UICONTROL Administrar esquemas]**, **[!UICONTROL Ver esquemas]**, **[!UICONTROL Administrar relaciones]**, **[!UICONTROL Administrar metadatos de identidad]**

**Permisos para destinos**

Para crear y administrar destinos, use los permisos de Destinos; **[!UICONTROL Administrar]**, **[!UICONTROL Destinos]**, **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Activar segmento sin asignación]**, **[!UICONTROL Administrar y activar destino de conjunto de datos]**, **[!UICONTROL Creación de destinos]**.

**Permisos para recorridos**

Para crear y administrar recorridos, use los permisos de Recorridos; **[!UICONTROL Administrar Recorridos]**, **[!UICONTROL Ver Recorridos]**, **[!UICONTROL Ver informe de Recorridos]**, **[!UICONTROL Administrar Recorridos]**, **[!UICONTROL Eventos]**, **[!UICONTROL Fuentes de datos y acciones]**, **[!UICONTROL Ver Recorridos]**, **[!UICONTROL Eventos]**, **[!UICONTROL Fuentes de datos y acciones, Recorridos de Publish]**.

La siguiente imagen muestra una instantánea de los permisos recomendados para que los usuarios vean, creen y administren libros de reproducción y los recursos generados por libros de reproducción.

![Instantánea de todos los elementos de permiso necesarios para crear todas las instancias de los libros de reproducción](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Agregar usuarios al rol**

Una vez que haya [creado una nueva función](/help/access-control/abac/ui/permissions.md#managing-users-for-role) como se menciona arriba, agréguese como usuario a ella. Si crea una función con acceso limitado para otro conjunto de usuarios con acceso de solo vista, incluya solo los elementos de vista necesarios asociados con estos permisos.

## Configuración de zonas protegidas y superficies de canal en Journey Optimizer {#configure-channel-surfaces}

Si su organización tiene licencia para [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es) y quiere usar los libros de reproducción diseñados para Journey Optimizer, deberá configurar los ajustes preestablecidos de canal en su zona protegida, que definen los parámetros técnicos necesarios para sus mensajes. [Obtenga información sobre cómo configurar superficies de canal en Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=es).

Para crear instancias de libros de reproducción en Journey Optimizer, debe configurar las superficies de canal para las notificaciones por correo electrónico, push y SMS.

### Superficie del canal de correo electrónico

Vaya a `Channels` en la interfaz de Journey Optimizer. Configure subdominios y grupos de IP independientes para los correos electrónicos de marketing y la mensajería transaccional, si no están configurados ya. Estas son las prácticas recomendadas para garantizar que los mensajes transaccionales, como los correos electrónicos de confirmación de pedidos, lleguen a sus clientes. Escriba nombres, direcciones de correo electrónico y configuraciones adicionales. Seleccione **Enviar** en la parte superior derecha de la página para crear la superficie del canal de marketing. Lea la documentación sobre [cómo configurar las superficies de canal de correo electrónico](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html?lang=es).

### Superficie del canal SMS

Para crear una superficie de canal SMS, primero cree una credencial de API de SMS y seleccione el proveedor preferido (por ejemplo, Sinch). Asigne un nombre a la superficie del canal SMS (por ejemplo, Marketing SMS), seleccione la configuración e introduzca un número de remitente. Seleccione **Enviar** en la parte superior derecha de la página para guardar la superficie del canal SMS. Lea la documentación sobre [cómo configurar las superficies de canal de SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=es#message-preset-sms).

Configure también canales para libros de reproducción que contengan mensajes transaccionales como confirmaciones de pedidos.

### Superficie del canal push

Confirme que las configuraciones de canal se hayan realizado desde la interfaz de Experience Platform o de Recopilación de datos. Este es el aspecto de las configuraciones de canal en el entorno de recopilación de datos.

<!-- ![Channel configurations in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

A continuación, seleccione el canal, las plataformas y las aplicaciones que ha visto en las configuraciones de canal. Seleccione **Enviar** para crear la superficie del canal push.

Lea la documentación sobre [cómo configurar las superficies de los canales push](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html?lang=es).

## Pasos siguientes {#next-steps}

Ahora que ha seguido todos los pasos de este documento, debería haber creado una zona protegida de desarrollo con libros de casos de uso disponibles en el panel de navegación izquierdo. Ahora también sabe cómo conceder a los integrantes del equipo los permisos necesarios para ver y administrar libros de reproducción y generar recursos. Como paso siguiente, lee cómo [elegir el libro de estrategias correcto](/help/use-case-playbooks/playbooks/choose.md) para ti y luego [crear instancias a partir de él](/help/use-case-playbooks/playbooks/create-share-reuse.md).
