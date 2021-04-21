---
keywords: Experience Platform;inicio;temas populares;iu;IU;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;explorar;clase;mezcla;tipo de datos;esquema;
solution: Experience Platform
title: Explorar recursos XDM en la interfaz de usuario
description: Aprenda a explorar los esquemas, clases, mezclas y tipos de datos existentes en la interfaz de usuario del Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Explorar los recursos XDM en la interfaz de usuario

En Adobe Experience Platform, todos los recursos del Modelo de datos de experiencia (XDM) se almacenan en [!DNL Schema Library], incluidos los recursos estándar proporcionados por el Adobe y los recursos personalizados definidos por su organización. En la interfaz de usuario del Experience Platform, puede ver la estructura y los campos de cualquier esquema, clase, mezcla o tipo de datos existente en [!DNL Schema Library]. Esto resulta especialmente útil a la hora de planificar y preparar el consumo de datos, ya que la interfaz de usuario proporciona información sobre los tipos de datos esperados y los casos de uso de cada campo proporcionados por estos recursos XDM.

Este tutorial trata los pasos para explorar los esquemas, clases, mezclas y tipos de datos existentes en la interfaz de usuario del Experience Platform.

## Buscar un recurso XDM {#lookup}

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Schemas]** en el panel de navegación izquierdo. El espacio de trabajo [!UICONTROL Schemas] proporciona una pestaña **[!UICONTROL Browse]** para explorar todos los recursos XDM existentes en su organización, junto con pestañas dedicadas adicionales para explorar **[!UICONTROL Classes]**, **[!UICONTROL Mixins]** y **[!UICONTROL Data types]** específicamente.

![](../images/ui/explore/tabs.png)

En la pestaña [!UICONTROL Browse], puede utilizar el icono de filtro (![Imagen de icono de filtro](../images/ui/explore/icon.png)) para mostrar los controles en el carril izquierdo y reducir los resultados de la lista.

Por ejemplo, para filtrar la lista y mostrar solo los tipos de datos estándar proporcionados por el Adobe, seleccione **[!UICONTROL Datatype]** y **[!UICONTROL Adobe]** en las secciones **[!UICONTROL Type]** y **[!UICONTROL Owner]**, respectivamente.

La opción **[!UICONTROL Included in Profile]** le permite filtrar los resultados para mostrar solo los recursos que se utilizan en esquemas que se han habilitado para su uso en [Perfil del cliente en tiempo real](../../profile/home.md).

![](../images/ui/explore/filter.png)

También puede utilizar la barra de búsqueda para reducir aún más los resultados. Al buscar un término, los elementos principales representan recursos cuyos nombres coinciden con la consulta de búsqueda. Debajo de estos elementos, en **[!UICONTROL Standard Fields]**, se enumerarán todos los recursos que contengan campos que coincidan con la consulta. Esto le permite buscar recursos XDM en función del tipo de datos que contienen, sin tener que saber previamente el nombre del recurso.

![](../images/ui/explore/search.png)

Cuando encuentre el recurso que desea explorar, seleccione su nombre en la lista para ver su estructura en el lienzo.

## Explorar un recurso XDM en el lienzo {#explore}

Una vez seleccionado un recurso, su estructura se abre en el lienzo.

![](../images/ui/explore/canvas.png)

Todos los campos de tipo objeto que contienen subpropiedades se contraen de forma predeterminada cuando aparecen por primera vez en el lienzo. Para mostrar las subpropiedades de cualquier campo, seleccione el icono junto a su nombre.

![](../images/ui/explore/field-expand.png)

### Campos generados por el sistema {#system-fields}

Algunos nombres de campo van precedidos de un guión bajo, como `_repo` y `_id`. Representan marcadores de posición para campos que el sistema generará automáticamente y asignará a medida que se introduzcan datos.

Como tal, la mayoría de estos campos deben excluirse de la estructura de los datos al ingerir en Platform. La excepción principal a esta regla es el campo [`_{TENANT_ID}`](../api/getting-started.md#know-your-tenant_id), en el que todos los campos XDM creados en su organización deben tener un espacio de nombres.

### Tipos de datos {#data-types}

Para cada campo mostrado en el lienzo, su tipo de datos correspondiente se muestra junto a su nombre, indicando de un vistazo el tipo de datos que ese campo espera para ingestión.

![](../images/ui/explore/data-types.png)

Cualquier tipo de datos que se anexa con corchetes (`[]`) representa una matriz de ese tipo de datos concreto. Por ejemplo, un tipo de datos de **[!UICONTROL String]\[]** indica que el campo espera una matriz de valores de cadena. Un tipo de datos **[!UICONTROL Payment Item]\[]** indica una matriz de objetos que se ajustan al tipo de datos [!UICONTROL Payment Item].

Si un campo de matriz se basa en un tipo de objeto, puede seleccionar su icono en el lienzo para mostrar los atributos esperados para cada elemento de matriz.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

Cuando selecciona el nombre de cualquier campo del lienzo, el carril derecho se actualiza para mostrar detalles sobre ese campo en **[!UICONTROL Field properties]**. Esto puede incluir una descripción del caso de uso previsto del campo, valores predeterminados, patrones, formatos, si el campo es obligatorio o no, y más.

![](../images/ui/explore/field-properties.png)

Si el campo que está inspeccionando es un campo de enumeración, el carril derecho también mostrará los valores aceptables que el campo espera recibir.

![](../images/ui/explore/enum-field.png)

### Campos de identidad {#identity}

Al inspeccionar esquemas que contienen campos de identidad, estos campos se enumeran en el carril izquierdo debajo de la clase o mezcla que los proporciona al esquema. Seleccione el nombre del campo de identidad en el carril izquierdo para mostrar el campo en el lienzo, independientemente de la profundidad con la que esté anidado.

Los campos de identidad se resaltan en el lienzo con un icono de huella (![Imagen de icono de huella digital](../images/ui/explore/identity-symbol.png)). Si selecciona el nombre del campo de identidad, puede ver información adicional como el [espacio de nombres de identidad](../../identity-service/namespaces.md) y si el campo es o no la identidad principal del esquema.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consulte la guía sobre [definición de campos de identidad](./fields/identity.md) para obtener más información sobre los campos de identidad y su relación con los servicios de Platform descendentes.

### Campos de relación {#relationship}

Si está inspeccionando un esquema que contiene un campo de relación, el campo aparece en el carril izquierdo debajo de **[!UICONTROL Relationships]**. Seleccione el nombre del campo de relación en el carril izquierdo para mostrar el campo en el lienzo, independientemente de la profundidad con la que esté anidado.

Los campos de relación también se resaltan de forma única en el lienzo, mostrando el nombre del esquema de destino al que hace referencia el campo. Si selecciona el nombre del campo de relación, puede ver el área de nombres de identidad de la identidad principal del esquema de destino en el carril derecho.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Consulte el tutorial sobre la [creación de una relación en la interfaz de usuario](../tutorials/create-schema-ui.md) para obtener más información sobre el uso de relaciones en esquemas XDM.

## Pasos siguientes

Este documento trata sobre cómo explorar los recursos XDM existentes en la interfaz de usuario del Experience Platform. Para obtener más información sobre las distintas funciones del espacio de trabajo [!UICONTROL Schemas] y [!DNL Schema Editor], consulte la [[!UICONTROL Schemas] descripción general del espacio de trabajo](./overview.md).
