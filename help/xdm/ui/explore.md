---
keywords: Experience Platform;inicio;temas populares;interfaz de usuario;IU;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;explorar;clase;grupo de campos;tipo de datos;esquema;
solution: Experience Platform
title: Explorar recursos de esquema en la interfaz de usuario
description: Obtenga información sobre cómo explorar esquemas, clases, grupos de campos de esquema y tipos de datos existentes en la interfaz de usuario del Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# Explorar los recursos de esquema en la interfaz de usuario

En Adobe Experience Platform, todos los recursos de esquema del Modelo de datos de experiencia (XDM) se almacenan en la variable [!DNL Schema Library], incluidos los recursos estándar proporcionados por el Adobe y los recursos personalizados definidos por su organización. En la interfaz de usuario del Experience Platform, puede ver la estructura y los campos de cualquier esquema, clase, grupo de campos o tipo de datos existente en la [!DNL Schema Library]. Esto resulta especialmente útil a la hora de planificar y preparar el consumo de datos, ya que la interfaz de usuario proporciona información sobre los tipos de datos esperados y los casos de uso de cada campo proporcionados por estos recursos XDM.

Este tutorial trata los pasos para explorar los esquemas, clases, grupos de campos y tipos de datos existentes en la interfaz de usuario del Experience Platform.

## Buscar un recurso de esquema {#lookup}

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. La variable [!UICONTROL Esquemas] workspace proporciona un **[!UICONTROL Examinar]** para explorar todos los esquemas de su organización, junto con pestañas dedicadas adicionales para explorar **[!UICONTROL Clases]**, **[!UICONTROL Grupos de campo]** y **[!UICONTROL Tipos de datos]** respectivamente.

![](../images/ui/explore/tabs.png)

El icono de filtro (![Icono de filtro Imagen](../images/ui/explore/icon.png)) muestra los controles del carril izquierdo para reducir los resultados de la lista. Los controles mostrados difieren según el tipo de recurso que se enumera.

Por ejemplo, para filtrar la lista y mostrar solo los tipos de datos estándar proporcionados por el Adobe, seleccione **[!UICONTROL DataType]** y **[!UICONTROL Adobe]** en el **[!UICONTROL Tipo]** y **[!UICONTROL Propietario]** secciones, respectivamente.

La variable **[!UICONTROL Incluido en el perfil]** alternar le permite filtrar los resultados para mostrar solo los recursos que se utilizan en esquemas que se han habilitado para usar en [Perfil del cliente en tiempo real](../../profile/home.md).

![](../images/ui/explore/filter.png)

Al enumerar recursos en la **[!UICONTROL Clases]**, **[!UICONTROL Grupos de campo]** o **[!UICONTROL Tipos de datos]** fichas, puede seleccionar **[!UICONTROL Adobe]** para mostrar solo recursos estándar o **[!UICONTROL Cliente]** para mostrar solo los recursos creados por su organización.

![](../images/ui/explore/filter-data-type.png)

También puede utilizar la barra de búsqueda para reducir aún más los resultados.

![](../images/ui/explore/search.png)

Los recursos mostrados en los resultados de búsqueda se ordenan primero por coincidencias de título y, a continuación, por coincidencias de descripción. A su vez, cuantas más coincidencias de palabras haya en cualquiera de estas categorías, más alto aparecerá el recurso en la lista.

Cuando encuentre el recurso que desea explorar, seleccione su nombre en la lista para ver su estructura en el lienzo.

## Explorar un recurso XDM en el lienzo {#explore}

Una vez seleccionado un recurso, su estructura se abre en el lienzo.

![](../images/ui/explore/canvas.png)

Todos los campos de tipo objeto que contienen subpropiedades se contraen de forma predeterminada cuando aparecen por primera vez en el lienzo. Para mostrar las subpropiedades de cualquier campo, seleccione el icono junto a su nombre.

![](../images/ui/explore/field-expand.png)

### Campos generados por el sistema {#system-fields}

Algunos nombres de campo van precedidos de un guión bajo, como `_repo` y `_id`. Representan marcadores de posición para campos que el sistema generará automáticamente y asignará a medida que se introduzcan datos.

Como tal, la mayoría de estos campos deben excluirse de la estructura de los datos al ingerir en Platform. La principal excepción a esta regla es la [`_{TENANT_ID}` field](../api/getting-started.md#know-your-tenant_id), en el que todos los campos XDM creados en su organización deben tener un espacio de nombres.

### Tipos de datos {#data-types}

Para cada campo mostrado en el lienzo, su tipo de datos correspondiente se muestra junto a su nombre, indicando de un vistazo el tipo de datos que ese campo espera para ingestión.

![](../images/ui/explore/data-types.png)

Cualquier tipo de datos que se añada con corchetes (`[]`) representa una matriz de ese tipo de datos concreto. Por ejemplo, un tipo de datos de **[!UICONTROL Cadena]\[]** indica que el campo espera una matriz de valores de cadena. Un tipo de datos de **[!UICONTROL Artículo de pago]\[]** indica una matriz de objetos que se ajustan a la variable [!UICONTROL Artículo de pago] tipo de datos.

Si un campo de matriz se basa en un tipo de objeto, puede seleccionar su icono en el lienzo para mostrar los atributos esperados para cada elemento de matriz.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Propiedades del campo] {#field-properties}

Cuando selecciona el nombre de cualquier campo del lienzo, el carril derecho se actualiza para mostrar detalles sobre ese campo en **[!UICONTROL Propiedades del campo]**. Esto puede incluir una descripción del caso de uso previsto del campo, valores predeterminados, patrones, formatos, si el campo es obligatorio o no, y más.

![](../images/ui/explore/field-properties.png)

Si el campo que está inspeccionando es un campo de enumeración, el carril derecho también mostrará los valores aceptables que el campo espera recibir.

![](../images/ui/explore/enum-field.png)

### Campos de identidad {#identity}

Al inspeccionar esquemas que contienen campos de identidad, estos campos se enumeran en el carril izquierdo debajo del grupo de clases o campos que los proporciona al esquema. Seleccione el nombre del campo de identidad en el carril izquierdo para mostrar el campo en el lienzo, independientemente de la profundidad con la que esté anidado.

Los campos de identidad se resaltan en el lienzo con un icono de huella (![Icono de huella digital Imagen](../images/ui/explore/identity-symbol.png)). Si selecciona el nombre del campo de identidad, puede ver información adicional como la variable [área de nombres de identidad](../../identity-service/namespaces.md) y si el campo es o no la identidad principal del esquema.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consulte la guía de [definición de campos de identidad](./fields/identity.md) para obtener más información sobre los campos de identidad y su relación con los servicios de Platform descendentes.

### Campos de relación {#relationship}

Si está inspeccionando un esquema que contiene un campo de relación, el campo aparece en el carril izquierdo debajo de **[!UICONTROL Relaciones]**. Seleccione el nombre del campo de relación en el carril izquierdo para mostrar el campo en el lienzo, independientemente de la profundidad con la que esté anidado.

Los campos de relación también se resaltan de forma única en el lienzo, mostrando el nombre del esquema de referencia al que está vinculado el campo. Si selecciona el nombre del campo de relación, puede ver el área de nombres de identidad de la identidad principal del esquema de referencia en el carril derecho.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Consulte el tutorial en [creación de una relación en la interfaz de usuario](../tutorials/relationship-ui.md) para obtener más información sobre el uso de relaciones en esquemas XDM.

## Pasos siguientes

Este documento trata sobre cómo explorar los recursos XDM existentes en la interfaz de usuario del Experience Platform. Para obtener más información sobre las distintas funciones de la variable [!UICONTROL Esquemas] espacio de trabajo y [!DNL Schema Editor], consulte la [[!UICONTROL Esquemas] información general del espacio de trabajo](./overview.md).
