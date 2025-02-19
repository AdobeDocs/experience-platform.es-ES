---
title: Utilice etiquetas de acceso para administrar el acceso de los usuarios a los flujos de datos de destino
description: Obtenga información sobre cómo utilizar las etiquetas de acceso para administrar el acceso de los usuarios a los flujos de datos de destino, de modo que solo un subconjunto de usuarios de su organización obtenga acceso a flujos de datos de destino específicos.
role: Developer, Admin, User
exl-id: 85944720-8551-491c-8991-dd9668beb0ca
source-git-commit: e1b8ca463146d300b48257304778a82aa745df73
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---

# Utilice etiquetas de acceso para administrar el acceso de los usuarios a los flujos de datos de destino

Como parte de la funcionalidad [[!UICONTROL control de acceso basado en atributos]](overview.md) de Real-Time CDP, ahora puede aplicar etiquetas de acceso a [flujos de datos de destino](../../dataflows/ui/monitor-destinations.md). De este modo, puede asegurarse de que solo un subconjunto de usuarios de su organización obtenga acceso a flujos de datos de destino específicos.

Cuando se agrega una etiqueta de acceso a un destino determinado, solo los usuarios que tienen acceso a una función que tiene esa etiqueta asignada pueden ver y editar ese flujo de datos de destino. Si un flujo de datos de destino no está marcado con etiquetas, es visible para todos los usuarios que pertenecen a su organización.

Lea esta página para comprender casos de uso de ejemplo, requisitos previos para poder aplicar etiquetas de acceso a flujos de datos de destino y otras llamadas importantes al utilizar esta funcionalidad.

## Requisitos previos {#prerequisites}

Tenga en cuenta los siguientes requisitos previos para completar antes de empezar a utilizar esta funcionalidad. Para familiarizarse con el [!UICONTROL control de acceso basado en atributos], Adobe también recomienda leer los siguientes artículos:

* [Información general de control de acceso basado en atributos](/help/access-control/abac/overview.md)
* [Guía completa de control de acceso basado en atributos](/help/access-control/abac/end-to-end-guide.md)

### Acceso a la IU de permisos {#access-permissions-ui}

[!UICONTROL Permisos] es el área de Experience Cloud donde los administradores pueden definir roles de usuario y directivas para administrar permisos para características y objetos dentro de una aplicación de producto. Lea la [sección de permisos](/help/access-control/abac/end-to-end-guide.md#permissions) para comenzar.

### Crear funciones, etiquetas y asignar usuarios {#create-roles-labels-assign-users}

Después de obtener acceso a la interfaz de usuario de [!UICONTROL permissions], usted o un miembro de su equipo deben configurar funciones y agregarles las etiquetas necesarias. Por último, los usuarios que deben acceder a los recursos etiquetados con las etiquetas específicas deben añadirse a la función. Consulte las siguientes secciones de documentación:

* [Crear una nueva función](/help/access-control/abac/ui/roles.md)
* [Adición de etiquetas a un rol](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [Adición de usuarios a una función](/help/access-control/ui/users.md)

### Crear flujos de datos de destino {#create-dataflow}

Primero debe conectarse al destino deseado y crear un flujo de datos para exportar los datos, antes de poder aplicar etiquetas de acceso al flujo de datos.

Lea las guías sobre [conectarse a un destino](/help/destinations/ui/connect-destination.md) y [activar datos en el destino](/help/destinations/ui/activation-overview.md). A continuación, seleccione el destino deseado en el [catálogo de conectores disponibles](/help/destinations/catalog/overview.md).

## Ya disponible: Aplicar etiquetas de acceso a otros recursos de Experience Platform {#apply-labels-other-resources}

Aunque esta versión le permite conceder a los usuarios acceso a nivel de objeto a flujos de datos de destino específicos, la funcionalidad para conceder control de acceso a nivel de objeto ya está disponible de forma general para otros recursos de Experience Platform, como [audiencias](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## Ejemplo de caso de uso {#use-case-example}

Con el control de acceso de nivel de objeto para destinos, limite equipos específicos de especialistas en marketing para obtener acceso únicamente a sus destinos específicos. Por ejemplo, si su organización tiene datos de clientes en varias ubicaciones geográficas, como Estados Unidos y el Reino Unido, puede limitar un equipo de marketing para que vea y edite los flujos de datos solo de la ubicación de EE. UU., y otro equipo de marketing para que vea y edite los flujos de datos de la ubicación de Reino Unido.

## Aplicar etiquetas de acceso a flujos de datos de destino {#apply-labels-to-destination-dataflow}

Para aplicar etiquetas de acceso a un flujo de datos específico:

1. Vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y busque el flujo de datos de destino para el cual desea limitar el acceso de los usuarios.
1. Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Nombre] y use el control ![Editar detalles](/help/images/icons/key.png) **[!UICONTROL Aplicar etiquetas de acceso]** para agregar nuevas etiquetas y administrar las etiquetas existentes para el flujo de datos.
   ![Seleccione Aplicar etiquetas de acceso en la vista Examinar del área de trabajo de destinos.](/help/access-control/images/olac/apply-access-labels.png)
1. Seleccione las etiquetas que desee agregar al flujo de datos de destino y seleccione **[!UICONTROL Guardar]**.
   ![Seleccione las etiquetas de acceso en que deben aplicarse al flujo de datos de destino.](/help/access-control/images/olac/view-access-labels.png)
1. Observe cómo el flujo de datos ahora muestra una etiqueta de acceso en la interfaz de usuario.
   ![Vista de varios flujos de datos de destino con el flujo de datos seleccionado y que muestran una etiqueta de acceso.](/help/access-control/images/olac/dataflow-with-access-label.png)

Si un flujo de datos de destino no está marcado con ninguna etiqueta, es visible para todos los usuarios. Si el flujo de datos está marcado con una o más etiquetas de acceso, solo es visible para los usuarios que pertenecen a una función que tiene la misma etiqueta o combinación de etiquetas.

Puede añadir etiquetas estándar y personalizadas a los flujos de datos de destino. Después de agregar una etiqueta a los flujos de datos de destino:

* Los usuarios asignados a funciones con acceso a la misma etiqueta pueden ver el flujo de datos con la nueva etiqueta en la interfaz de usuario. Pueden ver y editar el flujo de datos de destino en la interfaz de usuario o a través de las API.

* Los usuarios *que no son* asignados a roles con acceso a la misma etiqueta no tienen acceso al flujo de datos de destino para verlo o editarlo en la interfaz de usuario o a través de API.

## Llamadas y elementos importantes que se deben conocer {#important-callouts}

Actualmente, las etiquetas de acceso solo se pueden aplicar a flujos de datos existentes. Esto significa que debe crear un flujo de datos a un destino antes de poder aplicar etiquetas de acceso.

No puede aplicar una etiqueta de acceso a un flujo de datos de destino si no tiene acceso a esa etiqueta.

Al agregar varias etiquetas a un flujo de datos de destino, los usuarios que deban poder ver y editar el flujo de datos deben agregarse a una función con al menos la misma combinación de etiquetas. Por ejemplo, si aplica las etiquetas C1, I2 y otra etiqueta personalizada a un flujo de datos de destino, solo los usuarios añadidos a funciones con acceso a la combinación de estas tres etiquetas pueden ver y editar este flujo de datos de destino específico.

>[!NOTE]
>
> Al buscar flujos de datos de destino mediante el cuadro de búsqueda en la parte superior de la interfaz de usuario de Experience Platform, los resultados pueden incluir flujos de datos de destino que las etiquetas de acceso de usuario no permiten ver. Este comportamiento se corregirá en una actualización futura.

![Diagrama de Venn que muestra cómo solo ciertos usuarios tienen acceso a destinos con varias etiquetas aplicadas.](/help/access-control/images/olac/multiple-labels-venn.png)

## Pasos siguientes {#next-steps}

Al seguir los pasos de este documento, ahora sabe cómo aplicar etiquetas de acceso a los flujos de datos de destino para que solo un subconjunto de usuarios de su organización obtenga acceso a flujos de datos de destino específicos.

A continuación, puede obtener más información acerca de otras funcionalidades admitidas por [!UICONTROL control de acceso basado en atributos] al activar datos en destinos. Por ejemplo, puede limitar el acceso de los usuarios a [ver y activar solo campos específicos](/help/access-control/abac/overview.md#destinations).
