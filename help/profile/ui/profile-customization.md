---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;interfaz de usuario;interfaz de usuario;personalización;detalles del perfil;detalles
title: Personalización de los detalles del perfil en la IU de
description: Esta guía proporciona instrucciones paso a paso para personalizar la forma en que se muestran los datos del perfil del cliente en tiempo real en la interfaz de usuario de Adobe Experience Platform.
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 69ac6d3f98675df11183082ecbbb49d18ddb57af
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] personalización de detalles {#profile-detail-customization}

En la interfaz de usuario de Adobe Experience Platform, puede ver e interactuar con [!DNL Real-Time Customer Profile] datos en forma de perfiles de cliente. La información de perfil mostrada en la interfaz de usuario de se ha combinado a partir de varios fragmentos de perfil para formar una sola vista de cada cliente individual. Esto incluye detalles como atributos básicos, identidades vinculadas y preferencias de canal. Los campos predeterminados que se muestran en los perfiles también se pueden cambiar a nivel organizativo para mostrar los campos preferidos [!DNL Profile] atributos. Esta guía proporciona instrucciones paso a paso para personalizar la forma en que [!DNL Profile] Los datos de se muestran en la IU de Platform.

Para obtener una guía completa de la interfaz de usuario de perfiles, visite la [Guía de IU de perfil](user-guide.md).

## Reordenar y cambiar el tamaño de las tarjetas {#reorder-and-resize-cards}

Desde el **[!UICONTROL Detalle]** del perfil del cliente, puede seleccionar **[!UICONTROL Personalizar detalles del perfil]** para redimensionar y reordenar las tarjetas existentes.

![El botón Personalizar detalles del perfil aparece resaltado en el panel Perfil.](../images/profile-customization/customize-profile-details.png)

Después de elegir modificar el panel, puede reordenar las tarjetas seleccionando el título de la tarjeta y arrastrando y soltando las tarjetas en el orden deseado. También puede cambiar el tamaño de una tarjeta seleccionando el símbolo de ángulo en la esquina inferior derecha de la tarjeta (`⌟`) y arrastrando la tarjeta al tamaño deseado. En este ejemplo, la variable **[!UICONTROL Atributos básicos]** se está cambiando el tamaño de la tarjeta.

![El botón Cambiar tamaño se resalta dentro de la tarjeta Atributos básicos.](../images/profile-customization/resize.png)

La tarjeta seleccionada se ajusta al tamaño deseado y las tarjetas adyacentes se cambian de posición de forma dinámica. Esto puede hacer que algunas tarjetas se muevan a filas adicionales, lo que requiere que se desplace hacia abajo para ver todas las tarjetas. Por ejemplo, cuando la variable &quot;[!UICONTROL Atributos básicos]La tarjeta &quot; cambia de tamaño a &quot;[!UICONTROL Identidades vinculadas]&quot; ya no está visible en la fila superior y ahora aparece en una nueva segunda fila dentro del perfil (no se muestra). Para devolver &quot;[!UICONTROL Identidades vinculadas]&quot; en la fila superior, puede arrastrarla y soltarla en la posición actual de la &quot;[!UICONTROL Preferencias de canal]&quot;.

![Se resaltará una tarjeta cuyo tamaño se haya cambiado.](../images/profile-customization/resized.png)

## Editar y eliminar tarjetas

Además de cambiar el tamaño y reordenar las tarjetas, puede editar el contenido de determinadas tarjetas y quitar algunas tarjetas del panel por completo. Seleccione los puntos suspensivos (`...`) en la esquina superior derecha de la tarjeta para editarla o quitarla. Se abrirá una lista desplegable con opciones para editar o quitar la tarjeta, según las propiedades de la tarjeta seleccionada.

>[!NOTE]
>
>No todas las tarjetas se pueden editar o eliminar. Esto se debe a que algunas tarjetas contienen información de solo lectura o necesaria. Si una tarjeta no tiene puntos suspensivos en la esquina superior derecha, contiene información de solo lectura Y necesaria, y no se puede editar ni eliminar. Si una tarjeta tiene puntos suspensivos en la esquina y, al seleccionarla, solo se muestra una opción para quitar la tarjeta, la información de la tarjeta es de solo lectura y no se puede editar.

![Se resaltará la lista desplegable Editar tarjeta. Esto incluye opciones para editar o quitar la tarjeta.](../images/profile-customization/edit-card.png)

Seleccionar **[!UICONTROL Editar]** en el menú desplegable para abrir **[!UICONTROL Editar widget]** espacio de trabajo, donde puede actualizar el título de la tarjeta, reordenar o quitar los atributos visibles o agregar atributos adicionales mediante el **[!UICONTROL Añadir atributos]** botón.

![Se muestra la tarjeta Atributos básicos.](../images/profile-customization/basic-attributes.png)

## Añadir atributos {#add-attributes}

Desde el **[!UICONTROL Editar widget]** pantalla, seleccione **[!UICONTROL Añadir atributos]** situado en la esquina superior derecha de la tarjeta para empezar a añadir atributos a la misma.

![El botón Agregar atributos dentro de la tarjeta Atributos básicos está resaltado.](../images/profile-customization/add-attributes.png)

Si la variable **[!UICONTROL Seleccionar campo de esquema de unión]** se abre, el lado izquierdo del cuadro de diálogo muestra el [!UICONTROL Perfil individual de XDM] esquema de unión, con campos anidados debajo. Para obtener más información sobre los esquemas de unión, consulte la [sección de esquemas de unión de [!DNL Profile] guía del usuario](user-guide.md#union-schema).

El **[!UICONTROL Atributos seleccionados]** en la parte derecha del cuadro de diálogo se muestran los atributos que están incluidos actualmente en la tarjeta que está editando. Aquí también puede quitar y reordenar atributos. Se muestra el número total de atributos seleccionados, así como el número máximo de atributos (20) que se pueden agregar a una sola tarjeta.

![Se resaltan los atributos que actualmente conforman los atributos de la tarjeta.](../images/profile-customization/select-before.png)

Puede seleccionar cualquiera de los campos de esquema de unión disponibles para personalizar los atributos de la tarjeta que está editando. Al seleccionar los campos, puede elegir ver el nombre de la ruta de archivo o el nombre para mostrar. Para cambiar entre estas dos pantallas, seleccione la **[!UICONTROL Mostrar nombres para mostrar]** alternar.

![El [!UICONTROL Mostrar nombres para mostrar] La opción se resalta en la página Detalles del perfil.](../images/profile-customization/show-display-names.png)

Los campos seleccionados se muestran con una marca de verificación junto a ellos y se añaden automáticamente a la lista de atributos seleccionados. Una vez añadidos todos los atributos que desea que se muestren en la tarjeta, elija **[!UICONTROL Seleccionar]** para volver a la **[!UICONTROL Editar widget]** pantalla.

![Se resaltan los atributos recién añadidos.](../images/profile-customization/select-after.png)

Cuando vuelva a la **[!UICONTROL Editar widget]** , la lista de atributos de la tarjeta debe actualizarse para reflejar sus opciones. Puede quitar o reordenar los atributos de la tarjeta o editar el título de la tarjeta según sea necesario. Una vez finalizadas las ediciones, seleccione **[!UICONTROL Guardar]** para guardar los cambios.

![Los atributos recién añadidos se muestran en la tarjeta editada.](../images/profile-customization/new-attributes.png)

Después de guardar, volverá a la **[!UICONTROL Detalle]** pestaña donde están visibles la tarjeta y los atributos actualizados.

![Los atributos recién agregados se muestran en la tarjeta dentro del panel Perfil.](../images/profile-customization/added-attributes.png)

## Añadir una tarjeta nueva {#add-a-new-card}

Para personalizar aún más el aspecto de los perfiles dentro de Experience Platform, puede seleccionar añadir nuevas tarjetas al panel y seleccionar los atributos que desee mostrar en esas tarjetas. Para empezar, seleccione **[!UICONTROL Modificar tablero]** en el **[!UICONTROL Detalle]** pestaña.

![Se resalta el botón Personalizar detalles del perfil.](../images/profile-customization/customize-profile-details.png)

A continuación, seleccione **[!UICONTROL Añadir widget]** en la esquina superior izquierda del panel.

![Se resaltará el botón Añadir widget.](../images/profile-customization/add-widget.png)

Si elige añadir una tarjeta nueva, se abre el **[!UICONTROL Editar widget]** pantalla donde puede proporcionar un título para la nueva tarjeta y elegir los atributos que desea que muestre la tarjeta. Para empezar a añadir atributos a la tarjeta, seleccione **[!UICONTROL Añadir atributos]**.

![Se mostrará una nueva tarjeta widget en blanco en la pantalla Editar widget.](../images/profile-customization/edit-widget.png)

Si la variable **[!UICONTROL Seleccionar campo de esquema de unión]** se abre, el lado izquierdo del cuadro de diálogo muestra el [!UICONTROL Perfil individual de XDM] esquema de unión y **[!UICONTROL Atributos seleccionados]** en la parte derecha del cuadro de diálogo se muestran los atributos que ha seleccionado para la tarjeta. Para obtener más información sobre cómo añadir atributos, consulte [sobre agregar atributos](#add-attributes) que aparece anteriormente en este documento.

Se muestra el número total de atributos seleccionados, así como el número máximo de atributos (20) que se pueden agregar a una sola tarjeta. También puede quitar y reordenar los atributos seleccionados de esta pantalla. Una vez añadidos todos los atributos que desee visualizar en la tarjeta, elija **[!UICONTROL Seleccionar]** para volver a la **[!UICONTROL Editar widget]** pantalla.

![Los campos que agregue a la tarjeta se resaltarán.](../images/profile-customization/add-widget-attributes.png)

Cuando vuelva a la **[!UICONTROL Editar widget]** , la lista de atributos de la tarjeta debe reflejar sus opciones de la pantalla anterior. También puede reordenar y quitar atributos de tarjeta según sea necesario.

Para guardar la nueva tarjeta, primero debe proporcionar un **[!UICONTROL Título de tarjeta]**, a continuación, podrá seleccionar **[!UICONTROL Guardar]** y complete el proceso de creación de la tarjeta.

![El nuevo widget se previsualiza en la pantalla Editar widget.](../images/profile-customization/new-widget.png)

Después de guardar, volverá a la **[!UICONTROL Detalle]** pestaña donde están visibles la nueva tarjeta y los atributos.

![El nuevo widget se agregará al tablero de perfiles.](../images/profile-customization/added-widget.png)

## Restaurar tarjetas predeterminadas

Si en cualquier momento decide que desea restaurar las tarjetas predeterminadas que se han eliminado desde entonces, tiene la capacidad de hacerlo de forma rápida y sencilla. Primero, seleccione **[!UICONTROL Modificar tablero]**, luego seleccione **[!UICONTROL Restaurar tarjetas predeterminadas]**. Una vez que las tarjetas predeterminadas estén visibles, puede seleccionar **[!UICONTROL Guardar]** para guardar los cambios o seleccione **[!UICONTROL Cancelar]** si no desea restaurar las tarjetas predeterminadas.

![El botón Restaurar tarjetas predeterminadas está resaltado en el panel Perfil.](../images/profile-customization/restore-default.png)

## Pasos siguientes

Al seguir este documento, debería poder actualizar la vista de perfil de su organización, lo que incluye agregar y eliminar tarjetas, editar detalles y atributos de tarjetas, y reordenar y cambiar el tamaño de las tarjetas. Para obtener más información sobre cómo trabajar con [!DNL Profile] en la interfaz de usuario del Experience Platform, consulte la [[!DNL Profile] guía del usuario](user-guide.md).
