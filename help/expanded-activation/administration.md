---
title: Administración expandida de cuentas de activación
description: Obtenga información sobre cómo realizar tareas administrativas en la cuenta de activación expandida, como monitorizar el uso de licencias y asignar los permisos correctos.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Administración de cuentas

Para introducir audiencias de Audience Manager y activarlas en medios sociales y publicitarios, primero debe crear una cuenta de usuario de activación expandida y asignar la cuenta a la función de permiso correcta.

En esta página se explica cómo crear una cuenta de usuario en el Admin Console y cómo asignar los permisos correctos para la activación expandida.

## Creación de cuentas de usuario {#create-users}

Antes de usar [!DNL Audience Manager Expanded Activation], debe crear una cuenta de usuario.

Para crear una cuenta de usuario para [!DNL Expanded Activation], siga las instrucciones sobre la administración de usuarios desde el [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/manage-users-individually.html) documentación.

## Agregar usuarios a la función de permiso {#permissions}

Después de crear una cuenta de usuario, debe agregarla al [!DNL Expanded Activation] función de permiso, en [!DNL Expanded Activation] interfaz de usuario.

Ir a **[!UICONTROL Administration]** -> **[!UICONTROL Permisos]** -> **[!UICONTROL Funciones]** y seleccione la opción **[!UICONTROL Función predeterminada de activación expandida]**.

![Imagen de la interfaz de usuario de Activation expandida que muestra la página Funciones.](assets/expanded-activation-role.png)

Vaya a la **[!UICONTROL Usuarios]** y seleccione **[!UICONTROL Agregar usuarios]**.

![Imagen de la interfaz de usuario de Activation expandida que muestra la página Usuarios.](assets/add-users.png)

Seleccione el usuario recién creado de la lista disponible y seleccione **[!UICONTROL Guardar]**.

![Imagen de la interfaz de usuario de Activation expandida que muestra la página Agregar usuarios.](assets/add-user.png)

La cuenta de usuario ahora se crea y se asigna a la función correcta. Ya está listo para acceder a la **[!UICONTROL Activación expandida]** interfaz de usuario.

## Monitorización del uso de licencias {#license-usage}

Su [!DNL Audience Manager Expanded Activation] El contrato especifica el número máximo de correos electrónicos con hash que puede introducir en su cuenta.

Para encontrar esta información, vaya a la **[!UICONTROL Administration]** -> **[!UICONTROL Uso de licencias]** página.

![Imagen de la interfaz de usuario de Activation expandida que muestra la pantalla de uso de licencias.](assets/license-usage.png)

En esta página puede encontrar la siguiente información:

* **[!UICONTROL Product]**: el producto de Adobe para el que tiene licencia. Esto siempre será **[!UICONTROL Activación expandida de Audience Manager]**.
* **[!UICONTROL Métrica principal]**: Nombre de la métrica de la que se está realizando un seguimiento para su uso. Esto siempre será **[!UICONTROL Audiencia a la que dirigirse]**.
* **[!UICONTROL Cantidad de licencia]**: El número máximo de correos electrónicos con hash que tiene licencia para introducir.

  >[!TIP]
  >
  >La ingesta de correos electrónicos con hash se realiza mediante [Conector de origen del Audience Manager](../sources/connectors/adobe-applications/audience-manager.md). Consulte la documentación sobre [cómo activar audiencias](activate-audiences.md) para obtener más información.

* **[!UICONTROL Uso]**: el número de correos electrónicos con hash que ha introducido.
* **[!UICONTROL % de uso]**: el porcentaje del importe de la licencia que ha utilizado.

Para obtener más información sobre el uso de licencias en Experience Platform, consulte la [documentación de uso de licencias](../dashboards/guides/license-usage.md).

## Pasos siguientes {#next-steps}

Ahora que ha configurado al menos una cuenta de usuario con el acceso correcto a la activación expandida, puede empezar a utilizar la cuenta para lo siguiente [activar audiencias](activate-audiences.md).
