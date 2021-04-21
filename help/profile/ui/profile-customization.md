---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;interfaz de usuario;IU;personalización;detalles del perfil;detalles
title: Personalización de detalles de perfil en la interfaz de usuario
description: 'Esta guía proporciona instrucciones paso a paso para personalizar la forma en que se muestran los datos del perfil del cliente en tiempo real en la interfaz de usuario de Adobe Experience Platform. '
topic-legacy: guide
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] personalización de detalles  {#profile-detail-customization}

En la interfaz de usuario de Adobe Experience Platform, puede ver e interactuar con datos [!DNL Real-time Customer Profile] en forma de perfiles de cliente. La información de perfil mostrada en la interfaz de usuario se ha combinado desde varios fragmentos de perfil para formar una sola vista de cada cliente individual. Esto incluye detalles como atributos básicos, identidades vinculadas y preferencias de canal. Los campos predeterminados que se muestran en los perfiles también se pueden cambiar en el nivel de organización para mostrar los atributos preferidos [!DNL Profile]. Esta guía proporciona instrucciones paso a paso para personalizar la forma en que se muestran los datos [!DNL Profile] en la interfaz de usuario de Platform.

Para obtener una guía completa de la interfaz de usuario de Perfiles, visite la [Guía de la interfaz de usuario del perfil](user-guide.md).

## Reordenar y cambiar el tamaño de las tarjetas {#reorder-and-resize-cards}

En la pestaña **[!UICONTROL Detail]** del perfil del cliente, puede seleccionar **[!UICONTROL Modify dashboard]** para cambiar el tamaño y reordenar las tarjetas existentes.

![](../images/profile-customization/profiles-modify-dashboard.png)

Después de modificar el tablero, puede reordenar las tarjetas seleccionando el título de la tarjeta y arrastrando y soltando las tarjetas en el orden deseado. También puede cambiar el tamaño de una tarjeta seleccionando el símbolo de ángulo en la esquina inferior derecha de la tarjeta (`⌟`) y arrastrando la tarjeta al tamaño deseado. En este ejemplo, se está cambiando el tamaño de la tarjeta **[!UICONTROL Basic attributes]**.

![](../images/profile-customization/profiles-resize-cards.png)

La tarjeta seleccionada se ajusta al tamaño deseado y las tarjetas que la rodean se cambian de posición de forma dinámica. Esto puede hacer que algunas tarjetas se muevan a filas adicionales, lo que requiere que se desplace hacia abajo para ver todas las tarjetas. Por ejemplo, cuando se cambia el tamaño de la tarjeta &quot;[!UICONTROL Basic attributes]&quot;, la tarjeta &quot;[!UICONTROL Linked identities]&quot; ya no está visible en la fila superior y ahora aparece en una nueva segunda fila dentro del perfil (no se muestra). Para devolver la tarjeta &quot;[!UICONTROL Linked identities]&quot; a la fila superior, puede arrastrarla y soltarla en la posición actual de la tarjeta &quot;[!UICONTROL Channel preferences]&quot;.

![](../images/profile-customization/profiles-card-resized.png)

## Editar y quitar tarjetas

Además de cambiar el tamaño y reordenar las tarjetas, puede editar el contenido de ciertas tarjetas y eliminar algunas del tablero por completo. Seleccione los puntos suspensivos (`...`) en la esquina superior derecha de la tarjeta para editarla o eliminarla. Se abre un menú desplegable con opciones para editar o quitar la tarjeta, según las propiedades de la tarjeta seleccionada.

>[!NOTE]
>
>No todas las tarjetas se pueden editar o eliminar. Esto se debe a que algunas tarjetas contienen información de solo lectura o obligatoria. Si una tarjeta no tiene elipses en la esquina superior derecha, contiene información de solo lectura Y necesaria y no se puede editar ni eliminar. Si una tarjeta tiene elipses en la esquina y si la selecciona solo muestra una opción para quitar la tarjeta, la información de la tarjeta es de solo lectura y no se puede editar.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Seleccione **[!UICONTROL Edit]** en la lista desplegable para abrir el espacio de trabajo **[!UICONTROL Edit widget]**, donde puede actualizar el título de la tarjeta, reordenar o eliminar los atributos visibles, o agregar atributos adicionales mediante el botón **[!UICONTROL Add attributes]**.

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## Añadir atributos {#add-attributes}

En la pantalla **[!UICONTROL Edit widget]**, seleccione **[!UICONTROL Add attributes]** en la esquina superior derecha de la tarjeta para empezar a añadir atributos a esa tarjeta.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

Cuando se abre el cuadro de diálogo **[!UICONTROL Select union schema field]**, la parte izquierda del cuadro de diálogo muestra el esquema de unión [!UICONTROL XDM Individual Profile] completo, con campos anidados debajo. Para obtener más información sobre los esquemas de unión, consulte la sección [esquemas de unión de la  [!DNL Profile] guía del usuario](user-guide.md#union-schema).

La sección **[!UICONTROL Selected Attributes]** del lado derecho del cuadro de diálogo muestra los atributos que están incluidos actualmente en la tarjeta que está editando. Aquí también puede eliminar y reordenar los atributos. Se muestra el número total de atributos seleccionados, así como el número máximo de atributos (20) que se pueden agregar a una sola tarjeta.

![](../images/profile-customization/profiles-select-field-before.png)

Puede seleccionar cualquiera de los campos de esquema de unión disponibles para personalizar los atributos en la tarjeta que esté editando. Los campos seleccionados se muestran con una marca de verificación junto a ellos y se añaden automáticamente a la lista de atributos seleccionados. Una vez añadidos todos los atributos que desea mostrar en la tarjeta, elija **[!UICONTROL Select]** para volver a la pantalla **[!UICONTROL Edit widget]**.

![](../images/profile-customization/profiles-select-field-after.png)

Cuando vuelva a la pantalla **[!UICONTROL Edit widget]** , la lista de atributos de la tarjeta debería actualizarse para reflejar sus opciones. Puede eliminar o reordenar los atributos de la tarjeta o editar el título de la tarjeta según sea necesario. Una vez completadas las ediciones, seleccione **[!UICONTROL Save]** para guardar los cambios.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

Después de guardar, volverá a la pestaña **[!UICONTROL Detail]**, donde se verán la tarjeta y los atributos actualizados.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Agregar una tarjeta nueva {#add-a-new-card}

Para personalizar aún más el aspecto de los perfiles dentro del Experience Platform, puede elegir añadir nuevas tarjetas al tablero y seleccionar los atributos que desea mostrar en esas tarjetas. Para empezar, seleccione **[!UICONTROL Modify dashboard]** en la pestaña **[!UICONTROL Detail]**.

![](../images/profile-customization/profiles-modify-dashboard.png)

A continuación, seleccione **[!UICONTROL Add widget]** en la esquina superior izquierda del tablero.

![](../images/profile-customization/profiles-add-widget.png)

Al elegir agregar una tarjeta nueva, se abre la pantalla **[!UICONTROL Edit widget]**, donde puede proporcionar un título para la tarjeta nueva y elegir los atributos que desea que muestre la tarjeta. Para empezar a añadir atributos a la tarjeta, seleccione **[!UICONTROL Add attributes]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

Cuando se abre el cuadro de diálogo **[!UICONTROL Select union schema field]**, la parte izquierda del cuadro de diálogo muestra el esquema de unión [!UICONTROL XDM Individual Profile] completo y la sección **[!UICONTROL Selected Attributes]** a la derecha del cuadro de diálogo muestra los atributos que seleccione para la tarjeta. Para obtener más información sobre la adición de atributos, consulte la sección [sobre la adición de atributos](#add-attributes) que aparece anteriormente en este documento.

Se muestra el número total de atributos seleccionados, así como el número máximo de atributos (20) que se pueden agregar a una sola tarjeta. También puede quitar y reordenar los atributos seleccionados desde esta pantalla. Una vez añadidos todos los atributos que desea mostrar en la tarjeta, elija **[!UICONTROL Select]** para volver a la pantalla **[!UICONTROL Edit widget]**.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

Cuando vuelva a la pantalla **[!UICONTROL Edit widget]** , la lista de atributos de la tarjeta debe reflejar sus opciones de la pantalla anterior. También puede reordenar y eliminar los atributos de la tarjeta según sea necesario.

Para guardar la nueva tarjeta, primero debe proporcionar un **[!UICONTROL Card title]**, luego podrá seleccionar **[!UICONTROL Save]** y completar el proceso de creación de la tarjeta.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

Después de guardar, volverá a la pestaña **[!UICONTROL Detail]** donde se verán la tarjeta y los atributos nuevos.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Restaurar tarjetas predeterminadas

Si en cualquier momento decide que desea restaurar las tarjetas predeterminadas que se han eliminado desde entonces, puede hacerlo de forma rápida y sencilla. Primero, seleccione **[!UICONTROL Modify dashboard]** y luego seleccione **[!UICONTROL Restore default cards]**. Una vez que las tarjetas predeterminadas están visibles, puede seleccionar **[!UICONTROL Save]** para guardar los cambios o seleccionar **[!UICONTROL Cancel]** si no desea restaurar las tarjetas predeterminadas.

![](../images/profile-customization/profiles-restore-default.png)

## Pasos siguientes

Al seguir este documento, debería poder actualizar la vista de perfil de su organización, lo que incluye agregar y eliminar tarjetas, editar los detalles y atributos de las tarjetas y reordenar y cambiar el tamaño de las tarjetas. Para obtener más información sobre cómo trabajar con datos [!DNL Profile] en la interfaz de usuario del Experience Platform, consulte la [[!DNL Profile] guía del usuario](user-guide.md).
