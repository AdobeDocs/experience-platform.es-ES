---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: Explorar recursos XDM en la interfaz de usuario
description: En este tutorial se explican los pasos para explorar los esquemas, las clases, las mezclas y los tipos de datos existentes en la interfaz de usuario del Experience Platform.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 49d37cdf14bd03b62fe64116842bacd0f806e5ce
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# Explorar recursos XDM en la interfaz de usuario

En Adobe Experience Platform, todos los recursos del Modelo de datos de experiencia (XDM) se almacenan en el [!DNL Schema Library], incluidos los recursos estándar proporcionados por el Adobe y los recursos personalizados definidos por la organización. En la interfaz de usuario del Experience Platform, puede realizar la vista de la estructura y los campos de cualquier esquema, clase, mezcla o tipo de datos existente en el [!DNL Schema Library]. Esto resulta especialmente útil al planificar y preparar la ingestión de datos, ya que la interfaz de usuario proporciona información sobre los tipos de datos esperados y los casos de uso de cada campo que proporcionan estos recursos XDM.

En este tutorial se explican los pasos para explorar los esquemas, las clases, las mezclas y los tipos de datos existentes en la interfaz de usuario del Experience Platform.

## Buscar un recurso XDM {#lookup}

En la interfaz de usuario de la plataforma, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. El espacio de trabajo [!UICONTROL Esquemas] proporciona una ficha **[!UICONTROL Examinar]** para explorar todos los recursos XDM existentes en la organización, junto con fichas adicionales dedicadas a la exploración específica de **[!UICONTROL clases]**, **[!UICONTROL mezclas]** y tipos **** de datos.

![](../images/tutorials/explore/tabs.png)

En la ficha [!UICONTROL Examinar] , puede utilizar el icono de filtro (Imagen![de icono](../images/tutorials/explore/icon.png)de filtro) para mostrar los controles en el carril izquierdo y reducir los resultados de la lista.

Por ejemplo, para filtrar la lista para que solo muestre los tipos de datos estándar proporcionados por Adobe, seleccione **[!UICONTROL Tipo]** de datos y **[!UICONTROL Adobe]** en las secciones **[!UICONTROL Tipo]** y **[!UICONTROL Propietario]** , respectivamente.

La opción **[!UICONTROL Incluido en Perfil]** le permite filtrar los resultados para mostrar solo los recursos que se utilizan en esquemas que se han habilitado para su uso en el Perfil [del cliente en tiempo](../../profile/home.md)real.

![](../images/tutorials/explore/filter.png)

También puede utilizar la barra de búsqueda para reducir los resultados a los recursos cuyos nombres coincidan con la consulta de búsqueda.

![](../images/tutorials/explore/search.png)

Cuando encuentre el recurso que desea explorar, seleccione su nombre en la lista para vista de su estructura en el lienzo.

## Explorar un recurso XDM en el lienzo {#explore}

Una vez seleccionado un recurso, su estructura se abre en el lienzo.

![](../images/tutorials/explore/canvas.png)

Todos los campos de tipo de objeto que contienen subpropiedades se contraen de forma predeterminada cuando aparecen por primera vez en el lienzo. Para mostrar las subpropiedades de cualquier campo, seleccione el icono junto a su nombre.

![](../images/tutorials/explore/field-expand.png)

### Campos generados por el sistema {#system-fields}

Algunos campos de esquema van precedidos de un guión bajo, como `_repo` y `_id`. Representan marcadores de posición para los campos que el sistema generará automáticamente y asignará a medida que se ingrese datos.

Por lo tanto, la mayoría de estos campos deben excluirse de la estructura de los datos al realizar la ingesta en Platform, con la excepción principal del `_{TENANT_ID}` campo, en el que se deben asignar nombres a todos los campos XDM creados en la organización.

### Tipos de datos {#data-types}

Para cada campo mostrado en el lienzo, se muestra el tipo de datos correspondiente junto a su nombre, indicando de un vistazo el tipo de datos que ese campo espera para la ingestión.

Cualquier tipo de datos que se anexa con corchetes (`[]`) representa una matriz de ese tipo de datos en particular. Por ejemplo, un tipo de datos de **[!UICONTROL String]\[]** indica que el campo espera una matriz de valores de cadena. Un tipo de datos de Elemento **[!UICONTROL de]pago\[]** indica una matriz de objetos que se ajustan al tipo de datos de Elemento [!UICONTROL de] pago.

Si un campo de matriz se basa en un tipo de objeto, puede seleccionar su icono en el lienzo para mostrar los atributos esperados para cada elemento de matriz.

![](../images/tutorials/explore/array-type.png)

### [!UICONTROL Propiedades del campo] {#field-properties}

Al seleccionar el nombre de cualquier campo del lienzo, se actualiza el carril derecho para mostrar detalles sobre ese campo en Propiedades **[!UICONTROL de]** campo. Esto puede incluir una descripción del caso de uso previsto del campo, los valores predeterminados, los patrones, los formatos, si el campo es obligatorio o no, etc.

![](../images/tutorials/explore/field-properties.png)

Si el campo que está inspeccionando es un campo de enumeración, el carril derecho también mostrará los valores aceptables que el campo espera recibir.

![](../images/tutorials/explore/enum-field.png)

### Campos de identidad {#identity}

Al inspeccionar esquemas que contienen campos de identidad, estos campos se resaltan en el lienzo con un icono de huella digital (Imagen![de icono de](../images/tutorials/explore/identity-symbol.png)huella digital). Si selecciona el nombre del campo de identidad, puede vista información adicional como la Área de nombres [de](../../identity-service/namespaces.md) identidad y si el campo es o no la identidad principal del esquema.

![](../images/tutorials/explore/identity-field.png)

### Campos de relación {#relationship}

Los campos de relación también se resaltan de forma única en el lienzo, mostrando el nombre del esquema de destino al que hace referencia el campo. Si selecciona el nombre del campo de relación, puede vista la Área de nombres de identidad de la identidad principal del esquema de destino.

![](../images/tutorials/explore/relationship-field.png)

>[!NOTE]
>
>Consulte el tutorial sobre la [creación de una relación en la interfaz de usuario](./create-schema-ui.md) para obtener más información sobre el uso de relaciones en esquemas XDM.

## Pasos siguientes

Este documento explicaba cómo explorar los recursos XDM existentes en la interfaz de usuario del Experience Platform. Para obtener más información sobre las distintas funciones del espacio de trabajo de [!UICONTROL Esquemas] y [!DNL Schema Editor], consulte el tutorial [de creación de](./create-schema-ui.md)esquemas.