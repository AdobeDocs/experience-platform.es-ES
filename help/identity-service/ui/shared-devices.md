---
keywords: Experience Platform;inicio;temas populares;servicio de identidad;servicio de identidad;dispositivos compartidos;dispositivos compartidos
solution: Experience Platform
title: Información general sobre dispositivos compartidos (Beta)
topic-legacy: tutorial
description: La detección de dispositivos compartidos identifica a diferentes usuarios autenticados del mismo dispositivo, lo que permite una representación más precisa de los datos del cliente en los gráficos de identidad
hide: true
hidefromtoc: true
source-git-commit: 1cdab6ce71c748ae174700ce50f50b143e46b40f
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Resumen de Detección de dispositivos compartidos (Beta)

>[!IMPORTANT]
>
>La función [!DNL Shared Device Detection] está en versión beta. Sus características y documentación están sujetas a cambios.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales y impactantes en tiempo real.

[!DNL Shared Device] hace referencia a dispositivos que utilizan más de una persona. Algunos ejemplos de un dispositivo compartido son tabletas, equipos de biblioteca y quioscos. A través de la función [!DNL Shared Device Detection], se puede impedir que distintos usuarios del mismo dispositivo se fusionen en una sola identidad, lo que permite una representación más precisa de un individuo.

Con [!DNL Shared Device Detection] puede:

* Crear gráficos de identidad independientes para distintos usuarios del mismo dispositivo;
* Impedir la mezcla de datos de diferentes personas utilizando el mismo dispositivo;
* Genere una vista más limpia y precisa de sus clientes.

>[!TIP]
>
>Las configuraciones para [!DNL Shared Device Detection] deben completarse antes de habilitar Perfil para conjunto de datos porque ya no puede revisar la configuración una vez que se generan los gráficos en [!DNL Identity Service].

## Primeros pasos

Trabajar con [!DNL Shared Device Detection] requiere comprender los distintos servicios de Platform involucrados. Antes de comenzar a trabajar con [!DNL Shared Device Detection], revise la documentación de los siguientes servicios:

* [[!DNL Identity Service]](../home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
   * [Visor](./identity-graph-viewer.md) de gráficos de identidad: Visualice e interactúe con el visualizador de gráficos de identidad para comprender mejor cómo se vinculan las identidades de los clientes y de qué manera.
   * [Espacios de nombres](../namespaces.md) de identidad: Consulte los componentes de una identidad completa y cómo los espacios de nombres de identidad permiten distinguir el contexto y el tipo de una identidad.

### Terminología

La siguiente tabla contiene una lista de términos que son esenciales para comprender [!DNL Shared Device Detection]:

| Términos | Definición |
| --- | --- |
| Dispositivo compartido | Un dispositivo compartido es cualquier dispositivo utilizado por más de una persona. Algunos ejemplos de dispositivos compartidos son tabletas, equipos de biblioteca y quioscos. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] hace referencia a una configuración que permite separar los datos de distintos usuarios del mismo dispositivo. |
| [!UICONTROL Área de nombres de identidad compartida] | Se utiliza un [!UICONTROL Área de nombres de identidad compartida] para representar un único dispositivo compartido por varios usuarios diferentes. |
| [!UICONTROL Espacio de nombres de identidad de usuario] | Se utiliza un [!UICONTROL espacio de nombres de identidad de usuario] para representar al usuario autenticado o registrado de un dispositivo compartido. |

## Interfaz de usuario de dispositivos compartidos

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Identities]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Identity settings]**.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

Aparece la página [!UICONTROL Configuración de dispositivos compartidos], que proporciona una interfaz para configurar los dispositivos compartidos de sus datos. La configuración del dispositivo compartido está deshabilitada de forma predeterminada.

Cuando está habilitada, la configuración de dispositivos compartidos permite separar los datos de diferentes usuarios del mismo dispositivo entre sí. Esta configuración permite una representación más limpia y precisa de los gráficos de identidad, en los que las identidades de usuario del mismo dispositivo no se combinan.

Seleccione **[!UICONTROL Habilitar]** para comenzar a modificar la configuración del dispositivo compartido.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

Aparecen las opciones de configuración [!UICONTROL Área de nombres de identidad compartida] y [!UICONTROL Área de nombres de identidad de usuario] , lo que permite modificar los espacios de nombres de identidad que desea utilizar.

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL Shared Identity ] Namespacerepresenta un único dispositivo que utilizan varios usuarios diferentes. Este espacio de nombres siempre se establece en **[!UICONTROL ECID]** porque todos los usuarios de Platform utilizan **[!UICONTROL ECID]** como identificador del explorador web.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

El [!UICONTROL espacio de nombres de identidad de usuario] permite identificar a distintos usuarios del mismo dispositivo e impedir que los datos se combinen en el mismo gráfico de identidad.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

Seleccione la barra de búsqueda **[!UICONTROL User Identity Namespace]** e introduzca un área de nombres de identidad o seleccione un área de nombres de identidad en el menú desplegable.

>[!TIP]
>
>El [!UICONTROL área de nombres de identidad de usuario] debe asignarse al área de nombres de identidad que corresponda al ID de inicio de sesión del usuario final. Las opciones incluyen ID de cliente, correo electrónico y correo electrónico con hash.

![correos electrónicos](../images/shared-device/emails.png)

Una vez que haya configurado la [!UICONTROL Configuración de dispositivo compartido], seleccione **[!UICONTROL Guardar]**.

![guardar](../images/shared-device/save.png)

Aparece una ventana emergente que le solicita que confirme la selección. Seleccione **[!UICONTROL Yes]** para completar la configuración.

![confirm](../images/shared-device/confirm.png)
