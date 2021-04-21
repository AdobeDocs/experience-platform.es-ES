---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Esquemas y descriptores XDM
topic-legacy: tutorial
type: Tutorial
description: La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. Experience Data Model (XDM), impulsado por el Adobe, es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente. Los esquemas son la forma estándar de describir los datos en Experience Platform, lo que permite que todos los datos que se ajustan a los esquemas se puedan reutilizar sin conflictos en una organización e incluso compartir entre varias organizaciones.
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Trabajar con esquemas [!DNL Experience Data Model] (XDM) y descriptores de relaciones

La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente. Los esquemas son la forma estándar de describir los datos en [!DNL Experience Platform], lo que permite reutilizar todos los datos que se ajustan a los esquemas sin conflictos en una organización e incluso compartirlos entre varias organizaciones. Para obtener más información sobre los esquemas XDM, comience leyendo la [información general del sistema XDM](../xdm/home.md).

## Creación de un esquema mediante el Registro de esquemas

El Registro de esquemas proporciona una interfaz de usuario y una API RESTful desde la que puede ver y administrar todos los recursos de la Biblioteca de esquemas de Adobe Experience Platform. La Biblioteca de esquemas contiene recursos que están disponibles para usted por Adobe, [!DNL Experience Platform] socios y proveedores cuyas aplicaciones utiliza, así como recursos que define y guarda en el Registro de esquemas. Para aprender a crear esquemas para su organización, siga los tutoriales para [crear un esquema con la API del Registro de esquemas](../xdm/tutorials/create-schema-api.md) o [crear un esquema con la interfaz de usuario del Editor de esquemas](../xdm/tutorials/create-schema-ui.md).

## Definir una relación entre dos esquemas

La capacidad de comprender las relaciones entre los clientes y sus interacciones con la marca a través de varios canales es una parte importante de Adobe Experience Platform. La definición de estas relaciones dentro de la estructura de los esquemas [!DNL Experience Data Model] (XDM) le permite obtener perspectivas complejas sobre los datos de sus clientes. Estos descriptores de relación se pueden definir mediante la API del Registro de esquemas y la IU del Editor de esquemas. Para obtener más información, consulte los tutoriales para definir relaciones entre dos esquemas [mediante la API](../xdm/tutorials/relationship-api.md) o [mediante la IU](../xdm/tutorials/relationship-ui.md).

## Crear un esquema ad hoc

En circunstancias específicas, puede ser necesario crear un esquema [!DNL Experience Data Model] (XDM) con campos a los que solo se les asigna un nombre para su uso mediante un único conjunto de datos. Esto se denomina esquema &quot;ad-hoc&quot;. Los esquemas específicos se utilizan en varios flujos de trabajo de [ingesta de datos](../ingestion/home.md) para [!DNL Experience Platform], incluida la ingesta de archivos CSV y la creación de ciertos tipos de [conexiones de origen](../sources/home.md). La creación de un esquema ad-hoc se realiza mediante la API del Registro de esquemas y está pensada para utilizarse junto con otros tutoriales [!DNL Experience Platform] que requieran la creación de un esquema ad-hoc como parte de su flujo de trabajo. Para empezar a crear un esquema ad-hoc, consulte el tutorial para [crear un esquema ad-hoc con la API](../xdm/tutorials/ad-hoc.md).

## Pasos siguientes

Una vez que haya definido esquemas para su organización, puede empezar a crear conjuntos de datos en los que se puedan introducir datos. Para empezar, consulte la siguiente documentación:

* [Información general sobre conjuntos de datos](../catalog/datasets/overview.md)
* [Información general sobre la ingesta de datos](../ingestion/home.md)
