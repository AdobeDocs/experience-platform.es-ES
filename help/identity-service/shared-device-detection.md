---
keywords: Experience Platform;inicio;temas populares;servicio de identidad;servicio de identidad;dispositivos compartidos;Dispositivos compartidos
title: Información general sobre dispositivos compartidos (Beta)
description: La detección de dispositivos compartidos identifica diferentes usuarios autenticados del mismo dispositivo, lo que permite una representación más precisa de los datos del cliente en los gráficos de identidad
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 0%

---

# Información general sobre la detección de dispositivos compartidos (Beta)

>[!IMPORTANT]
>
>La característica [!DNL Shared Device Detection] se encuentra en la versión beta. Sus funciones y documentación están sujetas a cambios.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

[!DNL Shared Device] hace referencia a dispositivos que utilizan más de un individuo. Algunos ejemplos de dispositivos compartidos son tabletas, equipos de biblioteca y quioscos. A través de la característica [!DNL Shared Device Detection], se puede evitar que distintos usuarios del mismo dispositivo se combinen en una sola identidad, lo que permite una representación más precisa de un individuo.

Con [!DNL Shared Device Detection] puede:

* Crear gráficos de identidad independientes para distintos usuarios del mismo dispositivo.
* Impedir la mezcla de datos de distintas personas utilizando el mismo dispositivo;
* Genere una visión más limpia y precisa de sus clientes.

>[!TIP]
>
>Las configuraciones de [!DNL Shared Device Detection] deben completarse antes de habilitar el perfil para el conjunto de datos, porque ya no podrá revisar la configuración una vez que se generen los gráficos en [!DNL Identity Service].

## Introducción a [!DNL Shared Device Detection]

Trabajar con [!DNL Shared Device Detection] requiere una comprensión de los distintos servicios de plataforma implicados. Antes de comenzar a trabajar con [!DNL Shared Device Detection], revise la documentación de los siguientes servicios:

* [[!DNL Identity Service]](./home.md): obtenga una mejor vista de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
   * [Visor de gráficos de identidad](./features/identity-graph-viewer.md): visualice e interactúe con el visor de gráficos de identidad para comprender mejor cómo se vinculan las identidades de los clientes y de qué maneras.
   * [Áreas de nombres de identidad](./features/namespaces.md): vea los componentes de una identidad completa y cómo las áreas de nombres de identidad le permiten distinguir el contexto y el tipo de una identidad.

## Explicación [!DNL Shared Device Detection]

Es importante entender la siguiente terminología al trabajar con
[!DNL Shared Device Detection]. Consulte la tabla siguiente para obtener una lista de los términos esenciales para comprender [!DNL Shared Device Detection].

### Terminología

| Términos | Definición |
| --- | --- |
| Dispositivo compartido | Un dispositivo compartido es cualquier dispositivo que utilice más de un individuo. Algunos ejemplos de dispositivos compartidos son tabletas, equipos de biblioteca y quioscos. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] hace referencia a una configuración que permite separar datos de distintos usuarios del mismo dispositivo. |
| Área de nombres de identidad compartida | El área de nombres de identidad compartida representa el dispositivo que varios usuarios podrían usar. El área de nombres de identidad compartida suele ser el ECID, pero se puede establecer en otros ID de dispositivo. |
| Área de nombres de identidad de usuario | El área de nombres de identidad del usuario representa al usuario autenticado (que ha iniciado sesión) de un dispositivo compartido. |
| Último usuario autenticado | El último usuario autenticado representa al usuario que inició sesión por última vez en un dispositivo, si este lo están iniciando varias cuentas. |

{style="table-layout:auto"}

[!DNL Shared Device Detection] funciona estableciendo dos áreas de nombres: el **Área de nombres de identidad compartida** y el **Área de nombres de identidad de usuario**.

* El área de nombres de identidad compartida representa el dispositivo que varios usuarios podrían usar. El Adobe recomienda que los clientes utilicen ECID como identificador de dispositivo compartido.
* El área de nombres de identidad del usuario está asignada al área de nombres de identidad que corresponde al ID de inicio de sesión de un usuario; puede ser el CRMID, la dirección de correo electrónico, el correo electrónico con hash o el número de teléfono de un usuario.

Un dispositivo compartido, como una tableta, tiene un solo **Área de nombres de identidad compartida**. Por otro lado, cada usuario de un dispositivo compartido tiene su propio **espacio de nombres de identidad de usuario** designado que corresponde con sus respectivos ID de inicio de sesión. Por ejemplo, una tableta que Kevin y Nora comparten para uso en comercio electrónico tiene su propio ECID de `1234`, mientras que Kevin tiene su propia área de nombres de identidad de usuario asignada a su cuenta de `kevin@email.com` y Nora tiene su propia área de nombres de identidad de usuario asignada a su cuenta de `nora@email.com`.

[!DNL Shared Device Detection] puede hacer distinciones entre varios usuarios del mismo dispositivo vinculando el área de nombres de identidad compartida (por ejemplo, ECID) con el último área de nombres de identidad de usuario del usuario autenticado (ID de inicio de sesión).

### Envío de datos de identidad a un gráfico de identidad

Considere el siguiente ejemplo para comprender mejor cómo funciona [!DNL Shared Device Detection]:

>[!NOTE]
>
>En este diagrama, el área de nombres de identidad compartida se configura como ECID y el área de nombres de identidad de usuario se configura como CRMID.

![diagrama](./images/shared-device/diagram.png)

* Kevin y Nora comparten una tableta para visitar un sitio web de comercio electrónico. Sin embargo, ambos tienen sus propias cuentas independientes que cada uno utiliza para navegar y comprar en línea;
   * Como dispositivo compartido, la tableta tiene un ECID correspondiente, que representa el ID de cookie del explorador web de la tableta;
* Supongamos que Kevin usa la tableta y **inicia sesión** en su cuenta de comercio electrónico para buscar auriculares, lo que significa que el CRMID de Kevin (**Área de nombres de identidad de usuario**) ahora está vinculado con el ECID de la tableta (**Área de nombres de identidad compartida**). Los datos de navegación de la tableta ahora están incorporados con el gráfico de identidad de Kevin.
   * Si Kevin **cierra la sesión** y Nora usa la tableta y **inicia sesión** en su propia cuenta y compra una cámara, entonces su CRMID ahora está vinculado al ECID de la tableta. Por lo tanto, los datos de navegación de la tableta ahora están incorporados con el gráfico de identidad de Nora.
   * Si Nora **no cierra la sesión** y Kevin usa la tableta, pero **no inicia la sesión**, entonces los datos de navegación de la tableta aún se incorporan con Nora, porque ella permanece como el usuario autenticado y su CRMID sigue vinculado al ECID de la tableta.
   * Si Nora **cierra la sesión** y Kevin usa la tableta, pero **no inicia la sesión**, entonces los datos de navegación de la tableta aún se incorporan con el gráfico de identidad de Nora, porque como **último usuario autenticado**, su CRMID permanece vinculado con el ECID de la tableta.
   * Si Kevin **inicia sesión** de nuevo, su CRMID ahora se vincula al ECID de la tableta, porque ahora es el último usuario autenticado y los datos de navegación de la tableta ahora se incorporan con su gráfico de identidad.

### Cómo [!DNL Profile Service] combina fragmentos de perfil con [!DNL Shared Device Detection] habilitado

[!DNL Profile Service] toma nota de los fragmentos de perfil y de los perfiles combinados. Cada perfil de cliente individual está compuesto por varios fragmentos de perfil que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con su marca en varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan en Platform, se combinan para crear un único perfil para ese cliente.

Cuando [!DNL Shared Device Detection] está habilitado, [!DNL Profile] define la identidad principal del fragmento de perfil en función de si el evento de experiencia está autenticado o no

Un **evento de experiencia autenticada** es una acción completada por un usuario que inició sesión en un dispositivo. Para los eventos de experiencia autenticados, la identidad principal es el **Área de nombres de identidad del usuario** (ID de inicio de sesión). Un **evento de experiencia no autenticado** es una acción completada por un usuario que no ha iniciado sesión en un dispositivo. Para los eventos de experiencia no autenticados, la identidad principal es el **Área de nombres de identidad compartida** (ECID).

Para obtener más información, consulte [[!DNL Real-Time Customer Profile] descripción general](../profile/home.md).

## IU de dispositivos compartidos

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Identidades]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Configuración de identidad]**.

![tablero de identidad](./images/shared-device/identity-dashboard.png)

Aparecerá la página [!UICONTROL Configuración de dispositivos compartidos], que le proporcionará una interfaz para configurar la configuración de dispositivos compartidos para sus datos. La configuración de dispositivos compartidos está deshabilitada de forma predeterminada.

Cuando está habilitada, la configuración de dispositivos compartidos permite separar datos de distintos usuarios del mismo dispositivo. Esta configuración permite una representación más limpia y precisa de los gráficos de identidad, donde las identidades de los usuarios del mismo dispositivo no se combinan.

Seleccione **[!UICONTROL Habilitar]** para empezar a modificar la configuración del dispositivo compartido.

![enable-shared-device](./images/shared-device/enable-shared-device.png)

Aparecen las opciones de configuración [!UICONTROL Área de nombres de identidad compartida] y [!UICONTROL Área de nombres de identidad de usuario], que le permiten modificar las áreas de nombres de identidad que desea utilizar.

![set-namespaces](./images/shared-device/set-namespaces.png)

[!UICONTROL Área de nombres de identidad compartida] representa un solo dispositivo que utilizan varios usuarios diferentes. Este área de nombres siempre está establecida en **[!UICONTROL ECID]** porque todos los usuarios de Platform utilizan **[!UICONTROL ECID]** como identificador del explorador web.

![área de nombres de identidad compartida](./images/shared-device/shared-identity-namespace.png)

El [!UICONTROL espacio de nombres de identidad de usuario] le permite identificar a distintos usuarios del mismo dispositivo e impedir que los datos se combinen en el mismo gráfico de identidad.

![área de nombres de identidad de usuario](./images/shared-device/user-identity-namespace.png)

Seleccione la barra de búsqueda **[!UICONTROL Área de nombres de identidad de usuario]** y escriba un área de nombres de identidad o seleccione un área de nombres de identidad en el menú desplegable.

>[!TIP]
>
>El [!UICONTROL espacio de nombres de identidad de usuario] debe asignarse al área de nombres de identidad que corresponde al identificador de inicio de sesión del usuario final. Las opciones incluyen ID de cliente, correo electrónico y correo electrónico con hash.

![correos electrónicos](./images/shared-device/emails.png)

Una vez que hayas configurado tu [!UICONTROL Configuración de dispositivo compartido], selecciona **[!UICONTROL Guardar]**.

![guardar](./images/shared-device/save.png)

Aparece una ventana emergente que le solicita que confirme la selección. Seleccione **[!UICONTROL Sí]** para completar la configuración.

![confirmar](./images/shared-device/confirm.png)
