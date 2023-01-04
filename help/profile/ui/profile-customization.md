---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;interfaz de usuario;IU;personalización;detalles del perfil;detalles
title: Personalización de detalles de perfil en la interfaz de usuario
description: Esta guía proporciona instrucciones paso a paso para personalizar la forma en que se muestran los datos del perfil del cliente en tiempo real en la interfaz de usuario de Adobe Experience Platform.
topic-legacy: guide
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] personalización de detalles {#profile-detail-customization}

En la interfaz de usuario de Adobe Experience Platform, puede ver e interactuar con [!DNL Real-Time Customer Profile] datos en forma de perfiles de cliente. La información de perfil mostrada en la interfaz de usuario se ha combinado desde varios fragmentos de perfil para formar una sola vista de cada cliente individual. Esto incluye detalles como atributos básicos, identidades vinculadas y preferencias de canal. Los campos predeterminados que se muestran en los perfiles también se pueden cambiar en el nivel de organización para que se muestren los preferidos [!DNL Profile] atributos. Esta guía proporciona instrucciones paso a paso para personalizar la forma en que [!DNL Profile] los datos se muestran en la interfaz de usuario de Platform.

Para obtener una guía completa de la interfaz de usuario de Perfiles, visite el [Guía de la interfaz de usuario del perfil](user-guide.md).

## Reordenar y cambiar el tamaño de las tarjetas {#reorder-and-resize-cards}

En el **[!UICONTROL Detalle]** del perfil del cliente, puede seleccionar **[!UICONTROL Personalización de los detalles de perfil]** para cambiar el tamaño y reordenar las tarjetas existentes.

![El botón Personalizar detalles del perfil se resalta en el panel Perfil.](../images/profile-customization/customize-profile-details.png)

Después de modificar el tablero, puede reordenar las tarjetas seleccionando el título de la tarjeta y arrastrando y soltando las tarjetas en el orden deseado. También puede cambiar el tamaño de una tarjeta seleccionando el símbolo de ángulo en la esquina inferior derecha de la tarjeta (`⌟`) y arrastrando la tarjeta al tamaño deseado. En este ejemplo, la variable **[!UICONTROL Atributos básicos]** se está cambiando el tamaño de la tarjeta.

![El botón Cambiar tamaño se resalta en la tarjeta Atributos básicos .](../images/profile-customization/resize.png)

La tarjeta seleccionada se ajusta al tamaño deseado y las tarjetas que la rodean se cambian de posición de forma dinámica. Esto puede hacer que algunas tarjetas se muevan a filas adicionales, lo que requiere que se desplace hacia abajo para ver todas las tarjetas. Por ejemplo, cuando la variable[!UICONTROL Atributos básicos]&quot; se cambia el tamaño de la tarjeta &quot;[!UICONTROL Identidades vinculadas]&quot; ya no está visible en la fila superior y ahora aparece en una segunda fila dentro del perfil (no se muestra). Para devolver el &quot;[!UICONTROL Identidades vinculadas]&quot; a la fila superior, puede arrastrarla y soltarla en la posición actual del &quot;[!UICONTROL Preferencias de canal]&quot;.

![Se resalta una tarjeta de nuevo tamaño.](../images/profile-customization/resized.png)

## Editar y quitar tarjetas

Además de cambiar el tamaño y reordenar las tarjetas, puede editar el contenido de ciertas tarjetas y eliminar algunas del tablero por completo. Seleccione los puntos suspensivos (`...`) en la esquina superior derecha de la tarjeta para editarla o eliminarla. Se abre un menú desplegable con opciones para editar o quitar la tarjeta, según las propiedades de la tarjeta seleccionada.

>[!NOTE]
>
>No todas las tarjetas se pueden editar o eliminar. Esto se debe a que algunas tarjetas contienen información de solo lectura o obligatoria. Si una tarjeta no tiene elipses en la esquina superior derecha, contiene información de solo lectura Y necesaria y no se puede editar ni eliminar. Si una tarjeta tiene elipses en la esquina y si la selecciona solo muestra una opción para quitar la tarjeta, la información de la tarjeta es de solo lectura y no se puede editar.

![Se resalta la lista desplegable editar tarjeta . Esto incluye opciones para editar o eliminar la tarjeta.](../images/profile-customization/edit-card.png)

Select **[!UICONTROL Editar]** en el menú desplegable para abrir **[!UICONTROL Editar utilidad]** espacio de trabajo, donde puede actualizar el título de la tarjeta, reordenar o eliminar los atributos visibles o agregar atributos adicionales utilizando la variable **[!UICONTROL Añadir atributos]** botón.

![Se muestra la tarjeta Atributos básicos .](../images/profile-customization/basic-attributes.png)

## Añadir atributos {#add-attributes}

En el **[!UICONTROL Editar utilidad]** pantalla, seleccionar **[!UICONTROL Añadir atributos]** en la esquina superior derecha de la tarjeta para empezar a añadir atributos a esa tarjeta.

![Se resalta el botón Añadir atributos de la tarjeta Atributos básicos .](../images/profile-customization/add-attributes.png)

Cuando la variable **[!UICONTROL Seleccionar campo de esquema de unión]** se abre el cuadro de diálogo, el lado izquierdo del cuadro de diálogo muestra la [!UICONTROL Perfil individual XDM] esquema de unión, con campos anidados debajo. Para obtener más información sobre los esquemas de unión, consulte la [sección de esquemas de unión del [!DNL Profile] guía del usuario](user-guide.md#union-schema).

La variable **[!UICONTROL Atributos seleccionados]** a la derecha del cuadro de diálogo, se muestran los atributos que están actualmente incluidos en la tarjeta que está editando. Aquí también puede eliminar y reordenar los atributos. Se muestra el número total de atributos seleccionados, así como el número máximo de atributos (20) que se pueden agregar a una sola tarjeta.

![Se resaltan los atributos que actualmente conforman los atributos de la tarjeta.](../images/profile-customization/select-before.png)

Puede seleccionar cualquiera de los campos de esquema de unión disponibles para personalizar los atributos en la tarjeta que esté editando. Los campos seleccionados se muestran con una marca de verificación junto a ellos y se añaden automáticamente a la lista de atributos seleccionados. Una vez añadidos todos los atributos que desea mostrar en la tarjeta, elija **[!UICONTROL Select]** para volver a la **[!UICONTROL Editar utilidad]** en el Navegador.

![Se resaltan los atributos recién añadidos.](../images/profile-customization/select-after.png)

Cuando vuelva a la **[!UICONTROL Editar utilidad]** , la lista de atributos de la tarjeta debería actualizarse para reflejar sus opciones. Puede eliminar o reordenar los atributos de la tarjeta o editar el título de la tarjeta según sea necesario. Una vez completadas las ediciones, seleccione **[!UICONTROL Guardar]** para guardar los cambios.

![Los atributos recién añadidos se muestran en la tarjeta editada.](../images/profile-customization/new-attributes.png)

Después de guardar, volverá a la **[!UICONTROL Detalle]** en la que se ven la tarjeta y los atributos actualizados.

![Los atributos recién añadidos se muestran en la tarjeta del panel Perfil .](../images/profile-customization/added-attributes.png)

## Agregar una tarjeta nueva {#add-a-new-card}

Para personalizar aún más el aspecto de los perfiles dentro del Experience Platform, puede elegir añadir nuevas tarjetas al tablero y seleccionar los atributos que desea mostrar en esas tarjetas. Para empezar, seleccione **[!UICONTROL Modificar tablero]** en el **[!UICONTROL Detalle]** pestaña .

![Se resalta el botón Personalizar detalles del perfil.](../images/profile-customization/customize-profile-details.png)

A continuación, seleccione **[!UICONTROL Agregar utilidad]** en la esquina superior izquierda del panel.

![Se resalta el botón Agregar utilidad.](../images/profile-customization/add-widget.png)

Si elige agregar una tarjeta nueva, se abre el **[!UICONTROL Editar utilidad]** , donde puede proporcionar un título para la nueva tarjeta y elegir los atributos que desea que muestre la tarjeta. Para empezar a añadir atributos a la tarjeta, seleccione **[!UICONTROL Añadir atributos]**.

![Se muestra una nueva tarjeta de utilidad en blanco en la pantalla Editar utilidad.](../images/profile-customization/edit-widget.png)

Cuando la variable **[!UICONTROL Seleccionar campo de esquema de unión]** se abre el cuadro de diálogo, el lado izquierdo del cuadro de diálogo muestra la [!UICONTROL Perfil individual XDM] esquema de unión y **[!UICONTROL Atributos seleccionados]** a la derecha del cuadro de diálogo se muestran los atributos que seleccione para la tarjeta. Para obtener más información sobre la adición de atributos, consulte la [sección sobre adición de atributos](#add-attributes) que aparece anteriormente en este documento.

Se muestra el número total de atributos seleccionados, así como el número máximo de atributos (20) que se pueden agregar a una sola tarjeta. También puede quitar y reordenar los atributos seleccionados desde esta pantalla. Una vez que haya añadido todos los atributos que desea mostrar en la tarjeta, elija **[!UICONTROL Select]** para volver a la **[!UICONTROL Editar utilidad]** en el Navegador.

![Los campos que agregue a la tarjeta se resaltarán.](../images/profile-customization/add-widget-attributes.png)

Cuando vuelva a la **[!UICONTROL Editar utilidad]** , la lista de atributos de la tarjeta debe reflejar sus opciones de la pantalla anterior. También puede reordenar y eliminar los atributos de la tarjeta según sea necesario.

Para guardar la tarjeta nueva, primero debe proporcionar una **[!UICONTROL Título de la tarjeta]**, podrá seleccionar **[!UICONTROL Guardar]** y complete el proceso de creación de tarjetas.

![La nueva utilidad se previsualiza en la pantalla Editar utilidad .](../images/profile-customization/new-widget.png)

Después de guardar, volverá a la **[!UICONTROL Detalle]** en la que se ven la tarjeta y los atributos nuevos.

![El nuevo widget se agrega al panel Perfil.](../images/profile-customization/added-widget.png)

## Restaurar tarjetas predeterminadas

Si en cualquier momento decide que desea restaurar las tarjetas predeterminadas que se han eliminado desde entonces, puede hacerlo de forma rápida y sencilla. Primero, seleccione **[!UICONTROL Modificar tablero]** y, a continuación, seleccione **[!UICONTROL Restaurar tarjetas predeterminadas]**. Una vez que las tarjetas predeterminadas estén visibles, puede seleccionar **[!UICONTROL Guardar]** para guardar los cambios o seleccionar **[!UICONTROL Cancelar]** si no desea restaurar las tarjetas predeterminadas.

![El botón Restaurar tarjetas predeterminadas se resalta en el panel Perfil.](../images/profile-customization/restore-default.png)

## Pasos siguientes

Al seguir este documento, debería poder actualizar la vista de perfil de su organización, lo que incluye agregar y eliminar tarjetas, editar los detalles y atributos de las tarjetas y reordenar y cambiar el tamaño de las tarjetas. Para obtener más información sobre cómo trabajar con [!DNL Profile] en la interfaz de usuario del Experience Platform, consulte la [[!DNL Profile] guía del usuario](user-guide.md).
