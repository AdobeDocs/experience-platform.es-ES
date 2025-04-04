---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;perfil unificado;perfil unificado;perfil unificado;perfil unificado;rtcp;habilitar perfil;habilitar perfil;esquema de unión;UNION PROFILE;perfil de unión
title: Guía de IU de Esquema de unión
type: Documentation
description: En la interfaz de usuario (IU) de Adobe Experience Platform puede ver fácilmente cualquier esquema de unión dentro de su organización y previsualizar los campos, identidades, relaciones y esquemas de contribución para una clase específica. Esta guía proporciona información detallada sobre cómo ver y explorar esquemas de unión mediante la interfaz de usuario de Experience Platform.
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 0%

---

# Guía de IU de [!UICONTROL Union schema]

En la interfaz de usuario (IU) de Adobe Experience Platform puede ver fácilmente cualquier esquema de unión dentro de su organización y previsualizar los campos, identidades, relaciones y esquemas de contribución para una clase específica. Esta guía proporciona información detallada sobre cómo ver y explorar esquemas de unión mediante la interfaz de usuario de Experience Platform.

## Introducción

Esta guía de interfaz de usuario requiere una comprensión de los distintos servicios de [!DNL Experience Platform] implicados en la administración de los datos del perfil del cliente en tiempo real. Antes de leer esta guía o de trabajar en la interfaz de usuario de, consulte la documentación de los siguientes servicios:

* [[!DNL Real-Time Customer Profile]](../home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [[!DNL Identity Service]](../../identity-service/home.md): habilita [!DNL Real-Time Customer Profile] al unir identidades de orígenes de datos dispares a medida que se incorporan en [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.

## Explicación de los esquemas de unión

El Perfil del cliente en tiempo real permite crear perfiles sólidos y centralizados que contienen atributos del cliente y eventos con marca de tiempo para cada interacción de clientes en todos los sistemas integrados con Adobe Experience Platform. El formato y la estructura de estos datos los proporcionan los esquemas XDM (Experience Data Model), cada uno de los cuales se basa en una clase XDM y contiene campos compatibles con esa clase.

Los esquemas se pueden crear para varios casos de uso, haciendo referencia a la misma clase pero conteniendo campos específicos de su uso. Cuando un esquema está habilitado para Perfil, pasa a formar parte de un esquema de unión. Es decir, los esquemas de unión están compuestos por varios esquemas que comparten la misma clase y que se han habilitado para Perfil. El esquema de unión permite ver una amalgamación de todos los campos contenidos en esquemas que comparten la misma clase. El perfil del cliente en tiempo real utiliza el esquema de unión para crear una vista holística de cada cliente individual.

El trabajo con esquemas de unión requiere una comprensión profunda de los esquemas XDM. Para obtener más información, comience por leer los [conceptos básicos de la composición de esquemas](../../xdm/schema/composition.md).

## Ver esquemas de unión

Para navegar a esquemas de unión en la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Perfiles]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Esquema de unión]**. Se abre la pestaña [!UICONTROL Esquema de unión] para mostrar el esquema de unión de la clase seleccionada actualmente.

![Se muestra la página Esquema de unión, con la ficha Perfil y Esquema de unión resaltadas.](../images/union-schema/landing.png)

## Seleccionar una clase

Para mostrar el esquema de unión de una clase XDM específica, seleccione la clase en la lista desplegable **[!UICONTROL Clase]**. Debido a que no todas las clases tienen esquemas de unión, solo las clases con esquemas de unión (es decir, las clases con esquemas que se han habilitado para el perfil) están disponibles en el desplegable.

Una vez seleccionada una clase, el esquema que se muestra se actualiza para reflejar el esquema de unión de la clase seleccionada. Por ejemplo, puede seleccionar **[!UICONTROL Perfil individual de XDM]** para ver el esquema de unión de esa clase.

![Se resalta un menú desplegable que contiene las clases del esquema de unión.](../images/union-schema/class.png)

## Explorar esquemas de unión

Puede explorar el esquema de unión desplazándose hacia arriba y hacia abajo para ver la estructura completa del esquema y seleccionando un corchete angular derecho (`>`) para expandir los campos anidados.

![Se ha expandido un conjunto de campos anidados dentro del esquema de unión.](../images/union-schema/explore.png)

Seleccione cualquier campo para ver sus detalles, incluidos el nombre para mostrar, el tipo de datos, la descripción, la ruta, la fecha de creación y la fecha de la última modificación. También puede ver una lista de esquemas colaboradores que contienen el campo seleccionado.

![Se resalta un campo de esquema de unión. Los detalles sobre el campo resaltado se muestran en la barra lateral derecha.](../images/union-schema/explore-field.png)

Al seleccionar el nombre de un esquema colaborador, se muestran los nombres de los conjuntos de datos relacionados con ese esquema que están introduciendo datos en el campo seleccionado. Cada nombre del conjunto de datos aparece como un vínculo. Al seleccionar el nombre de un conjunto de datos, se abre la pestaña de actividad de dicho conjunto de datos en una nueva ventana.

Para obtener más información sobre los conjuntos de datos, incluida la visualización de la actividad y los datos del conjunto de datos en la interfaz de usuario, visite la [guía de IU de conjuntos de datos](../../catalog/datasets/user-guide.md).

![Se resalta la lista de conjuntos de datos relacionados con el esquema.](../images/union-schema/datasets.png)

## Ver esquemas colaboradores

También puede ver qué esquemas específicos están contribuyendo al esquema de unión seleccionando **[!UICONTROL Todos los esquemas que contribuyen]** para expandir la lista de esquemas. Según la clase que haya seleccionado y el número de esquemas que su organización haya creado en Experience Platform, puede ser una lista corta que contenga un solo esquema o una lista larga que contenga muchos esquemas.

![Se resalta la lista de esquemas que contribuyen al esquema de unión.](../images/union-schema/contributing-schemas.png)

Al seleccionar el nombre de un esquema específico, se resaltan los campos del esquema de unión que forman parte del esquema seleccionado. Después de seleccionar un esquema, el esquema de unión aparece atenuado con barras negras que indican los campos que forman parte del esquema colaborador.

![El esquema de contribución seleccionado está resaltado. Los campos que forman parte del esquema de contribución permanecen en negro, mientras que los campos que no forman parte del esquema de contribución aparecen atenuados.](../images/union-schema/select-schema.png)

## Ver identidades

A través de la interfaz de usuario puede ver una lista de identidades incluidas en el esquema de unión seleccionando **[!UICONTROL Identidades]** para expandir la lista.

![Se resaltan las identidades que pertenecen al esquema de unión.](../images/union-schema/identities.png)

Si se selecciona una identidad individual en la lista, el esquema mostrado se actualiza automáticamente según sea necesario para mostrar el campo de identidad. Esto podría incluir la expansión de varios campos si el campo de identidad está anidado.

El campo de identidad se resalta dentro del esquema de unión y los detalles de la identidad se muestran en la parte derecha de la pantalla. Los detalles incluyen una lista de esquemas colaboradores que contienen el campo de identidad y puede explorar en profundidad para encontrar vínculos a los conjuntos de datos relacionados con ese esquema que están introduciendo datos en el campo de identidad seleccionado.

![La identidad seleccionada está resaltada. Los detalles sobre la identidad seleccionada se muestran en la barra lateral derecha.](../images/union-schema/select-identity.png)

## Ver relaciones

La interfaz de usuario del esquema de unión también permite ver las relaciones que se han definido para los esquemas en función de la clase de esquema seleccionada. La definición de una relación es una forma de conectar dos esquemas que pertenecen a clases diferentes para obtener perspectivas más complejas en los datos del cliente.

Si se han establecido relaciones para la clase seleccionada, al seleccionar **[!UICONTROL Relaciones]** se muestra una lista de campos utilizados para crear relaciones. No todos los esquemas utilizan o necesitan relaciones definidas, por lo que es común que la sección de relaciones no contenga campos.

Para obtener más información acerca de las relaciones de esquema, incluido cómo definirlas mediante la interfaz de usuario, visite [este documento sobre las relaciones de esquema](../../xdm/tutorials/relationship-ui.md).

![Se resaltan las relaciones que pertenecen al esquema de unión.](../images/union-schema/relationships.png)

Si se selecciona un campo de relación de la lista, el esquema mostrado se actualizará según sea necesario para mostrar el campo de relación resaltado. Esto podría incluir la expansión de varios campos si el campo de relación está anidado.

![La relación seleccionada está resaltada. El campo correspondiente para la relación también está resaltado.](../images/union-schema/select-relationship.png)

## Pasos siguientes

Al leer esta guía, ahora sabe cómo ver y navegar por esquemas de unión mediante la interfaz de usuario de [!DNL Experience Platform]. Para obtener más información sobre los esquemas, incluido cómo se utilizan en Experience Platform, comience por leer la [descripción general del sistema XDM](../../xdm/home.md).
