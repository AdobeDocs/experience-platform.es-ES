---
title: Guía de configuración de reglas de vinculación de gráfico de identidad
description: Conozca los pasos recomendados a seguir al implementar sus datos con las configuraciones de reglas de vinculación de gráficos de identidad.
badge: Beta
source-git-commit: 72773f9ba5de4387c631bd1aa0c4e76b74e5f1dc
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 4%

---

# Guía de configuración de reglas de vinculación de gráfico de identidad

Lea este documento para obtener una guía paso a paso que puede seguir al implementar los datos con el servicio de identidad de Adobe Experience Platform.

Descripción paso a paso:

1. [Crear las áreas de nombres de identidad necesarias](#namespace)
2. [Utilice la herramienta de simulación de gráficos para familiarizarse con el algoritmo de optimización de identidad](#graph-simulation)
3. [Utilice la herramienta de configuración de identidad para designar las áreas de nombres únicas y configurar las clasificaciones de prioridad para las áreas de nombres](#identity-settings)
4. [Creación de un esquema de modelo de datos de experiencia (XDM)](#schema)
5. [Crear un conjunto de datos](#dataset)
6. [Ingesta de datos en Experience Platform](#ingest)

## Requisitos previos a la implementación

Antes de empezar, primero debe asegurarse de que los eventos autenticados en el sistema siempre contengan un identificador de persona.

## Definición de permisos {#set-permissions}

El primer paso en el proceso de implementación del servicio de identidad es garantizar que la cuenta de Experience Platform se añada a una función que esté aprovisionada con los permisos necesarios. El administrador puede configurar permisos para su cuenta navegando a la interfaz de usuario de permisos en Adobe Experience Cloud. A partir de ahí, la cuenta debe agregarse a una función con los siguientes permisos:

* [!UICONTROL Ver configuración de identidad]: aplique este permiso para poder ver áreas de nombres únicas y su prioridad en la página de exploración del área de nombres de identidad.
* [!UICONTROL Editar configuración de identidad]: aplique este permiso para poder editar y guardar la configuración de identidad.

Para obtener más información sobre los permisos, lea la [guía de permisos](../../access-control/abac/ui/permissions.md).

## Crear sus áreas de nombres de identidad {#namespace}

Si los datos lo requieren, primero debe crear los espacios de nombres adecuados para su organización. Para obtener información sobre cómo crear un área de nombres personalizada, lea la guía sobre [creación de un área de nombres personalizada en la interfaz de usuario](../features/namespaces.md#create-custom-namespaces).

## Uso de la herramienta de simulación de gráficos {#graph-simulation}

A continuación, vaya a la [herramienta de simulación de gráficos](./graph-simulation.md) en el área de trabajo de la interfaz de usuario del servicio de identidad. Puede utilizar la herramienta de simulación de gráficos para simular gráficos de identidad, creados con una variedad de diferentes configuraciones de área de nombres única y prioridad de área de nombres.

Mediante la creación de diferentes configuraciones, puede utilizar la herramienta de simulación de gráficos para aprender y comprender mejor cómo el algoritmo de optimización de identidad y determinadas configuraciones pueden afectar al comportamiento del gráfico.

## Configuración de la identidad {#identity-settings}

Una vez que tengas una mejor idea de cómo deseas que se comporte tu gráfico, ve a la [herramienta de configuración de identidad](./identity-settings-ui.md) en el área de trabajo de la interfaz de usuario del servicio de identidad.

Utilice la herramienta de configuración de identidad para designar las áreas de nombres únicas y configurar las áreas de nombres por orden de prioridad. Una vez que haya terminado de aplicar la configuración, debe esperar al menos seis horas antes de continuar con la ingesta de datos, ya que la nueva configuración tarda al menos seis horas en reflejarse en el servicio de identidad.

## Creación de un esquema XDM {#schema}

Una vez establecidas las áreas de nombres únicas y las prioridades del área de nombres, ahora puede continuar con la configuración necesaria para introducir los datos. En primer lugar, debe crear un esquema XDM. En función de los datos, es posible que tenga que crear un esquema tanto para XDM Individual Profile como para XDM ExperienceEvent.

Para introducir datos en el perfil del cliente en tiempo real, debe asegurarse de que el esquema contenga al menos un campo que se haya designado como identidad principal. Al establecer una identidad principal, puede habilitar un esquema determinado para la ingesta de perfiles.

Para obtener instrucciones sobre cómo crear un esquema, lea la guía sobre [creación de un esquema XDM en la interfaz de usuario](../../xdm/tutorials/create-schema-ui.md).

## Crear un conjunto de datos {#dataset}

A continuación, cree un conjunto de datos para proporcionar una estructura para los datos que va a introducir. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos trabajan en conjunto con esquemas y, para introducir datos en el Perfil del cliente en tiempo real, el conjunto de datos debe estar habilitado para la ingesta de perfiles. Para que el conjunto de datos esté habilitado para el perfil, debe hacer referencia a un esquema que esté habilitado para la ingesta de perfiles.

Para obtener instrucciones sobre cómo crear un conjunto de datos, lea la [guía de IU de conjuntos de datos](../../catalog/datasets/user-guide.md).

## Ingesta de datos {#ingest}

En este punto, debería tener lo siguiente:

* Los permisos necesarios para acceder a las funciones del servicio de identidad.
* Áreas de nombres para sus datos.
* Áreas de nombres únicas designadas y prioridades configuradas para sus áreas de nombres.
* Al menos un esquema XDM. (Según los datos y el caso de uso específico, es posible que deba crear esquemas de perfil y de evento de experiencia).
* Un conjunto de datos basado en el esquema.

Una vez que tenga todos los elementos enumerados arriba, puede empezar a ingerir los datos en Experience Platform. Puede realizar la ingesta de datos de varias formas diferentes. Puede utilizar los siguientes servicios para llevar los datos a Experience Platform:

* [Ingesta por lotes y streaming](../../ingestion/home.md)
* [Recopilación de datos en Experience Platform](../../collection/home.md)
* [fuentes de Experience Platform](../../sources/home.md)

>[!TIP]
>
>Una vez introducidos los datos, la carga de datos sin procesar del XDM no cambia. Es posible que siga viendo las configuraciones de identidad principales en la interfaz de usuario. Sin embargo, estas configuraciones se sobrescribirán con la configuración de identidad.

Para obtener cualquier comentario, use la opción **[!UICONTROL comentarios de Beta]** en el área de trabajo de la interfaz de usuario del servicio de identidad.