---
keywords: Experience Platform;inicio;temas populares;servicio de identidad;servicio de identidad;dispositivos compartidos;dispositivos compartidos
title: Información general sobre dispositivos compartidos (Beta)
description: La detección de dispositivos compartidos identifica a diferentes usuarios autenticados del mismo dispositivo, lo que permite una representación más precisa de los datos del cliente en los gráficos de identidad
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 75362c67e1a8a31a449cb4c9dd618515325d36f0
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 0%

---

# Resumen de Detección de dispositivos compartidos (Beta)

>[!IMPORTANT]
>
>La variable [!DNL Shared Device Detection] está en versión beta. Sus características y documentación están sujetas a cambios.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.

[!DNL Shared Device] hace referencia a dispositivos que utilizan más de una persona. Algunos ejemplos de un dispositivo compartido son tabletas, equipos de biblioteca y quioscos. A través de [!DNL Shared Device Detection] , se puede impedir que distintos usuarios del mismo dispositivo se fusionen en una sola identidad, lo que permite una representación más precisa de un individuo.

con [!DNL Shared Device Detection] puede:

* Crear gráficos de identidad independientes para distintos usuarios del mismo dispositivo;
* Impedir la mezcla de datos de diferentes personas utilizando el mismo dispositivo;
* Genere una vista más limpia y precisa de sus clientes.

>[!TIP]
>
>Configuraciones para [!DNL Shared Device Detection] debe completarse antes de habilitar el perfil para el conjunto de datos, ya que ya no puede revisar la configuración una vez que se generan los gráficos en [!DNL Identity Service].

## Introducción a [!DNL Shared Device Detection]

Uso de [!DNL Shared Device Detection] requiere una comprensión de los distintos servicios de Platform implicados. Antes de comenzar a trabajar con [!DNL Shared Device Detection], consulte la documentación de los siguientes servicios:

* [[!DNL Identity Service]](../home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
   * [Visor de gráficos de identidad](./identity-graph-viewer.md): Visualice e interactúe con el visualizador de gráficos de identidad para comprender mejor cómo se vinculan las identidades de los clientes y de qué manera.
   * [Espacios de nombres de identidad](../namespaces.md): Consulte los componentes de una identidad completa y cómo los espacios de nombres de identidad permiten distinguir el contexto y el tipo de una identidad.

## Explicación [!DNL Shared Device Detection]

Es importante comprender la siguiente terminología al trabajar con
[!DNL Shared Device Detection]. Consulte la siguiente tabla para obtener una lista de términos esenciales para comprender [!DNL Shared Device Detection].

### Terminología

| Términos | Definición |
| --- | --- |
| Dispositivo compartido | Un dispositivo compartido es cualquier dispositivo utilizado por más de una persona. Algunos ejemplos de dispositivos compartidos son tabletas, equipos de biblioteca y quioscos. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] hace referencia a una configuración que permite separar los datos de distintos usuarios del mismo dispositivo. |
| Área de nombres de identidad compartida | El área de nombres de identidad compartida representa el dispositivo que podrían utilizar varios usuarios. El área de nombres de identidad compartida suele ser el ECID, pero se puede establecer en otros ID de dispositivo. |
| Espacio de nombres de identidad de usuario | El área de nombres de identidad de usuario representa el usuario autenticado (con sesión iniciada) de un dispositivo compartido. |
| Último usuario autenticado | El último usuario autenticado representa al usuario que inició sesión por última vez en un dispositivo, si varias cuentas están iniciando sesión en un dispositivo. |

{style=&quot;table-layout:auto&quot;}

[!DNL Shared Device Detection] funciona estableciendo dos áreas de nombres: el **Área de nombres de identidad compartida** y **Espacio de nombres de identidad de usuario**.

* El área de nombres de identidad compartida representa el dispositivo que podrían utilizar varios usuarios. Adobe recomienda que los clientes utilicen ECID como identificador de dispositivo compartido.
* El área de nombres de identidad de usuario está asignado al área de nombres de identidad que corresponde al ID de inicio de sesión de un usuario; puede ser el ID de CRM, la dirección de correo electrónico, el correo electrónico con hash o el número de teléfono del usuario.

Un dispositivo compartido, como una tableta, tiene una sola **Área de nombres de identidad compartida**. Por otro lado, cada usuario de un dispositivo compartido tiene su propia designación **Espacio de nombres de identidad de usuario** que corresponde a sus respectivos ID de inicio de sesión. Por ejemplo, una tableta que Kevin y Nora comparten para uso de comercio electrónico tiene su propio ECID de `1234`, mientras que Kevin tiene su propio espacio de nombres de identidad de usuario asignado a su `kevin@email.com` cuenta y Nora tiene su propio espacio de nombres de identidad de usuario asignado a su `nora@email.com` cuenta.

[!DNL Shared Device Detection] puede hacer distinciones entre varios usuarios del mismo dispositivo vinculando el área de nombres de identidad compartida (por ejemplo, ECID) con el último espacio de nombres de identidad de usuario del usuario autenticado (ID de inicio de sesión).

### Envío de datos de identidad a un gráfico de identidad

Considere el siguiente ejemplo para ayudarle a comprender cómo [!DNL Shared Device Detection] funciona:

>[!NOTE]
>
>En este diagrama, el área de nombres de identidad compartida se configura en ECID y el área de nombres de identidad de usuario se configura en CRM ID.

![diagrama](../images/shared-device/diagram.png)

* Kevin y Nora comparten una tableta para visitar un sitio web de comercio electrónico. Sin embargo, ambos tienen sus propias cuentas independientes que cada uno utiliza para navegar y comprar en línea;
   * Como dispositivo compartido, la tableta tiene un ECID correspondiente, que representa el ID de cookie del explorador web de la tableta;
* Supongamos que Kevin usa el comprimido y **inicia sesión** a su cuenta de comercio electrónico para buscar auriculares, esto significa que Kevin&#39;s CRM ID (**Espacio de nombres de identidad de usuario**) ahora está vinculado al ECID de la tableta (**Área de nombres de identidad compartida**). Los datos de navegación de la tableta ahora se incorporan con el gráfico de identidad de Kevin.
   * Si Kevin **cierre de sesión** y Nora utiliza el comprimido y **inicia sesión** a su propia cuenta y compra una cámara, su CRM ID ahora está vinculado al ECID de la tableta. Por lo tanto, los datos de navegación de la tableta se incorporan ahora con el gráfico de identidad de Nora.
   * Si Nora **no cierra la sesión** y Kevin usa la tableta, pero **no inicia sesión**, los datos de navegación de la tableta se siguen incorporando a Nora, ya que sigue siendo la usuaria autenticada y su ID de CRM sigue vinculado al ECID de la tableta.
   * Si Nora **cierra sesión** y Kevin usa la tableta, pero **no inicia sesión**, entonces los datos de navegación de la tableta siguen incorporados con el gráfico de identidad de Nora, porque como **último usuario autenticado**, su ID de CRM permanece vinculado al ECID de la tableta.
   * Si Kevin **inicia sesión** de nuevo, su ID de CRM ahora se vincula al ECID de la tableta, ya que ahora es el último usuario autenticado y los datos de navegación de la tableta ahora se incorporan con este gráfico de identidad.

### Cómo [!DNL Profile Service] combina fragmentos de perfil con [!DNL Shared Device Detection] enabled

[!DNL Profile Service] toma nota de los fragmentos de perfil y los perfiles combinados. Cada perfil de cliente individual está compuesto por varios fragmentos de perfil que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con la marca a través de varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan a Platform, se combinan para crear un perfil único para ese cliente.

When [!DNL Shared Device Detection] está habilitado, [!DNL Profile] define la identidad principal del fragmento de perfil en función de si el evento de experiencia está autenticado o no

Un **evento de experiencia autenticada** es una acción completada por un usuario mientras iniciaba sesión en un dispositivo. Para los eventos de experiencia autenticados, la identidad principal es la **Espacio de nombres de identidad de usuario** (ID de inicio de sesión). Un **evento de experiencia no autenticada** es una acción completada por un usuario que no ha iniciado sesión en un dispositivo. Para los eventos de experiencia no autenticados, la identidad principal es la **Área de nombres de identidad compartida** (ECID).

Para obtener más información, consulte la  [[!DNL Real-time Customer Profile] información general](../../profile/home.md).

## Interfaz de usuario de dispositivos compartidos

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Identidades]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Configuración de identidad]**.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

La variable [!UICONTROL Configuración de dispositivos compartidos] , lo que le proporciona una interfaz para configurar los dispositivos compartidos de los datos. La configuración del dispositivo compartido está deshabilitada de forma predeterminada.

Cuando está habilitada, la configuración de dispositivos compartidos permite separar los datos de diferentes usuarios del mismo dispositivo entre sí. Esta configuración permite una representación más limpia y precisa de los gráficos de identidad, en los que las identidades de usuario del mismo dispositivo no se combinan.

Select **[!UICONTROL Habilitar]** para comenzar a modificar la configuración del dispositivo compartido.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

La variable [!UICONTROL Área de nombres de identidad compartida] y [!UICONTROL Espacio de nombres de identidad de usuario] , que le permite modificar los espacios de nombres de identidad que desea utilizar.

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL Área de nombres de identidad compartida] representa un solo dispositivo que utilizan varios usuarios diferentes. Este espacio de nombres siempre está establecido en **[!UICONTROL ECID]** porque todos los usuarios de Platform utilizan **[!UICONTROL ECID]** como identificador del explorador web.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

La variable [!UICONTROL Espacio de nombres de identidad de usuario] le permite identificar diferentes usuarios del mismo dispositivo e impedir que los datos se combinen en el mismo gráfico de identidad.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

Seleccione el **[!UICONTROL Espacio de nombres de identidad de usuario]** barra de búsqueda e introduzca un área de nombres de identidad o seleccione un área de nombres de identidad en el menú desplegable.

>[!TIP]
>
>La variable [!UICONTROL Espacio de nombres de identidad de usuario] debe asignarse al área de nombres de identidad que corresponda al ID de inicio de sesión del usuario final. Las opciones incluyen ID de cliente, correo electrónico y correo electrónico con hash.

![correos electrónicos](../images/shared-device/emails.png)

Una vez que haya configurado el [!UICONTROL Configuración de dispositivo compartido], seleccione **[!UICONTROL Guardar]**.

![guardar](../images/shared-device/save.png)

Aparece una ventana emergente que le solicita que confirme la selección. Select **[!UICONTROL Sí]** para completar la configuración.

![confirm](../images/shared-device/confirm.png)
