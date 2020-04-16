---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: esquemas y descriptores XDM
topic: tutorial
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Trabajar con esquemas del modelo de datos de experiencia (XDM) y descriptores de relaciones

La estandarización y la interoperabilidad son conceptos clave que subyacen a Adobe Experience Platform. El modelo de datos de experiencia (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente. Los Esquemas son la forma estándar de describir los datos en la plataforma de experiencia, lo que permite reutilizar todos los datos que se ajustan a los esquemas sin conflictos en una organización e incluso compartir entre varias organizaciones. Para obtener más información sobre los esquemas XDM, lea la descripción general [del sistema](../xdm/home.md)XDM para obtener inicios.

## Creación de un esquema mediante el Registro de Esquemas

El Registro de Esquema proporciona una interfaz de usuario y una API RESTful desde la que puede realizar la vista y la gestión de todos los recursos en la biblioteca de Esquemas de Adobe Experience Platform. La biblioteca de Esquemas contiene los recursos que Adobe, los socios de la plataforma de experiencia y los proveedores cuyas aplicaciones utiliza, así como los recursos que define y guarda en el Registro de Esquema. Para aprender a crear esquemas para su organización, siga los tutoriales para [crear un esquema con la API](../xdm/tutorials/create-schema-api.md) del Registro de Esquemas o [crear un esquema con la interfaz](../xdm/tutorials/create-schema-ui.md)de usuario del Editor de Esquemas.

## Definir una relación entre dos esquemas

La capacidad de comprender las relaciones entre sus clientes y sus interacciones con su marca en diversos canales es una parte importante de Adobe Experience Platform. La definición de estas relaciones dentro de la estructura de los esquemas del Modelo de datos de experiencia (XDM) le permite obtener perspectivas complejas sobre los datos de sus clientes. Estos descriptores de relación se pueden definir mediante la API del Registro de Esquemas y la interfaz de usuario del Editor de Esquemas. Para obtener más información, consulte los tutoriales sobre la definición de relaciones entre dos esquemas [con la API](../xdm/tutorials/relationship-api.md) o [con la IU](../xdm/tutorials/relationship-ui.md).

## Creación de un esquema ad-hoc

En circunstancias específicas, puede que sea necesario crear un esquema de modelo de datos de experiencia (XDM) con campos a los que solo un conjunto de datos debe asignar un nombre para su uso. Esto se denomina esquema &quot;ad-hoc&quot;. Los esquemas específicos se utilizan en varios flujos de trabajo de [recopilación](../ingestion/home.md) de datos para la plataforma de experiencia, incluida la ingesta de archivos CSV y la creación de determinados tipos de conexiones [de](../sources/home.md)origen. La creación de un esquema ad-hoc se realiza mediante la API del Registro de Esquema y está pensada para utilizarse junto con otros tutoriales de la Plataforma de experiencia que requieran la creación de un esquema ad-hoc como parte de su flujo de trabajo. Para empezar a crear un esquema ad-hoc, consulte el tutorial para [crear un esquema ad-hoc mediante la API](../xdm/tutorials/ad-hoc.md).

## Pasos siguientes

Una vez que haya definido esquemas para su organización, puede empezar a crear conjuntos de datos en los que se pueden ingerir datos. Para empezar, consulte la siguiente documentación:

* [Introducción a los conjuntos de datos](../catalog/datasets/overview.md)
* [Información general sobre la inserción de datos](../ingestion/home.md)