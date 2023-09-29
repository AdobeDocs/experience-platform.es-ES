---
keywords: Experience Platform;inicio;temas populares;iu;IU;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;explorar;clase;grupo de campos;tipo de datos;esquema;
solution: Experience Platform
title: Exploración de los recursos de esquema en la IU
description: Aprenda a explorar esquemas, clases, grupos de campos de esquema y tipos de datos existentes en la interfaz de usuario de Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: f08aa017b7f971a54197b95023e9331832ecb7f1
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# Exploración de recursos de esquema en la IU

En Adobe Experience Platform, todos los recursos de esquema del Modelo de datos de experiencia (XDM) se almacenan en la variable [!DNL Schema Library], incluidos los recursos estándar proporcionados por los Adobes y los recursos personalizados definidos por su organización. En la interfaz de usuario del Experience Platform, puede ver la estructura y los campos de cualquier esquema, clase, grupo de campos o tipo de datos existente en la variable [!DNL Schema Library]. Esto resulta especialmente útil a la hora de planificar y preparar la ingesta de datos, ya que la interfaz de usuario proporciona información sobre los tipos de datos esperados y los casos de uso de cada campo proporcionado por estos recursos XDM.

Este tutorial explica los pasos para explorar los esquemas, las clases, los grupos de campos y los tipos de datos existentes en la interfaz de usuario de Experience Platform.

## Búsqueda de un recurso de esquema {#lookup}

En la IU de Platform, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. El [!UICONTROL Esquemas] workspace proporciona un **[!UICONTROL Examinar]** para explorar todos los esquemas de la organización, junto con pestañas dedicadas adicionales para explorar **[!UICONTROL Clases]**, **[!UICONTROL Grupos de campos]**, y **[!UICONTROL Tipos de datos]** respectivamente.

![](../images/ui/explore/tabs.png)

El icono de filtro (![Imagen del icono de filtro](../images/ui/explore/icon.png)) revela los controles en el carril izquierdo para reducir los resultados enumerados. Los controles mostrados difieren según el tipo de recurso que se enumere.

Por ejemplo, para filtrar la lista de modo que solo muestre los tipos de datos estándar proporcionados por Adobe, seleccione **[!UICONTROL Tipo de datos]** y **[!UICONTROL Adobe]** en el **[!UICONTROL Tipo]** y **[!UICONTROL Propietario]** secciones, respectivamente.

El **[!UICONTROL Incluido en el perfil]** permite filtrar los resultados para mostrar solo los recursos que se utilizan en esquemas que se han habilitado para su uso en [Perfil del cliente en tiempo real](../../profile/home.md). El **[!UICONTROL Mostrar esquemas ad hoc]** alternar filtra la lista de esquemas creados con campos que tienen un espacio de nombres para su uso exclusivo en un único conjunto de datos.

![El [!UICONTROL Esquemas] workspace [!UICONTROL Examinar] pestaña con el panel filtros resaltado.](../images/ui/explore/filter.png)

Al enumerar recursos en **[!UICONTROL Clases]**, **[!UICONTROL Grupos de campos]**, o **[!UICONTROL Tipos de datos]** pestañas, puede seleccionar **[!UICONTROL Adobe]** para mostrar solo los recursos estándar o **[!UICONTROL Cliente]** para mostrar solo los recursos creados por su organización.

![](../images/ui/explore/filter-data-type.png)

También puede utilizar la barra de búsqueda para reducir aún más los resultados.

![](../images/ui/explore/search.png)

Los recursos mostrados en los resultados de búsqueda se ordenan primero por coincidencias de título y luego por coincidencias de descripción. A su vez, cuanto más coincidan las palabras en cualquiera de estas categorías, más alto aparecerá el recurso en la lista.

Cuando haya encontrado el recurso que desea explorar, seleccione su nombre en la lista para ver su estructura en el lienzo.

## Exploración de un recurso XDM en el lienzo {#explore}

Una vez seleccionado un recurso, su estructura se abre en el lienzo.

![](../images/ui/explore/canvas.png)

Todos los campos de tipo de objeto que contienen subpropiedades se contraen de forma predeterminada la primera vez que aparecen en el lienzo. Para mostrar las subpropiedades de cualquier campo, seleccione el icono junto a su nombre.

![](../images/ui/explore/field-expand.png)

### Campos generados por el sistema {#system-fields}

Algunos nombres de campo van precedidos de un guion bajo, como `_repo` y `_id`. Representan marcadores de posición para campos que el sistema generará y asignará automáticamente a medida que se incorporen los datos.

Como tal, la mayoría de estos campos deben excluirse de la estructura de los datos al ingerirlos en Platform. La principal excepción a esta regla es la [`_{TENANT_ID}` campo](../api/getting-started.md#know-your-tenant_id), en los que todos los campos XDM creados en su organización deben tener un espacio de nombres.

### Tipos de datos {#data-types}

Para cada campo que se muestra en el lienzo, su tipo de datos correspondiente se muestra junto a su nombre, lo que indica de un vistazo el tipo de datos que ese campo espera para la ingesta.

![](../images/ui/explore/data-types.png)

Cualquier tipo de datos anexado con corchetes (`[]`) representa una matriz de ese tipo de datos en particular. Por ejemplo, un tipo de datos de **[!UICONTROL Cadena]\[]** indica que el campo espera una matriz de valores de cadena. Un tipo de datos de **[!UICONTROL Elemento de pago]\[]** indica una matriz de objetos que se ajustan a [!UICONTROL Elemento de pago] tipo de datos.

Si un campo de matriz se basa en un tipo de objeto, puede seleccionar su icono en el lienzo para mostrar los atributos esperados para cada elemento de matriz.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Propiedades del campo] {#field-properties}

Al seleccionar el nombre de cualquier campo en el lienzo, el carril derecho se actualiza para mostrar detalles sobre ese campo en **[!UICONTROL Propiedades del campo]**. Esto puede incluir una descripción del caso de uso previsto del campo, los valores predeterminados, los patrones, los formatos, si el campo es obligatorio o no, y más.

![](../images/ui/explore/field-properties.png)

Si el campo que está inspeccionando es un campo de enumeración, el carril derecho también mostrará los valores aceptables que el campo espera recibir.

![](../images/ui/explore/enum-field.png)

### Campos de identidad {#identity}

Al inspeccionar esquemas que contienen campos de identidad, estos campos se enumeran en el carril izquierdo bajo la clase o el grupo de campos que los proporciona al esquema. Seleccione el nombre del campo de identidad en el carril izquierdo para mostrar el campo en el lienzo, independientemente de la profundidad con que esté anidado.

Los campos de identidad se resaltan en el lienzo con un icono de huella digital (![Imagen del icono de huella digital](../images/ui/explore/identity-symbol.png)). Si selecciona el nombre del campo de identidad, puede ver información adicional como la [área de nombres de identidad](../../identity-service/namespaces.md) y si el campo es o no la identidad principal del esquema.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consulte la guía de [definición de campos de identidad](./fields/identity.md) para obtener más información sobre los campos de identidad y su relación con los servicios de Platform secundarios.

### Campos de relación {#relationship}

Si está inspeccionando un esquema que contiene un campo de relación, el campo se mostrará en el carril izquierdo debajo de **[!UICONTROL Relaciones]**. Seleccione el nombre del campo de relación en el carril izquierdo para mostrar el campo en el lienzo, independientemente de la profundidad con que esté anidado.

Los campos de relación también se resaltan de forma exclusiva en el lienzo, mostrando el nombre del esquema de referencia al que está vinculado el campo. Si selecciona el nombre del campo de relación, puede ver el área de nombres de identidad de la identidad principal del esquema de referencia en el carril derecho.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Consulte el tutorial sobre [creación de una relación en la IU](../tutorials/relationship-ui.md) para obtener más información sobre el uso de relaciones en esquemas XDM.

## Pasos siguientes

En este documento se explica cómo explorar los recursos XDM existentes en la interfaz de usuario de Experience Platform. Para obtener más información sobre las distintas características de [!UICONTROL Esquemas] workspace y [!DNL Schema Editor], consulte la [[!UICONTROL Esquemas] información general de workspace](./overview.md).
