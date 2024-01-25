---
title: Guía de implementación del servicio de ID
description: Descubra cómo se procesan los datos proporcionados a Adobe Experience Platform antes de que el servicio de identidad los utilice para crear gráficos de identidad.
source-git-commit: f1273c1deac32559e214d1d99d10f6ca25fe4264
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Guía de implementación del servicio de ID

Este documento proporciona información sobre cómo se procesan los datos proporcionados a Adobe Experience Platform antes de que el servicio de identidad los utilice para crear un gráfico de identidad para un cliente determinado.

## Decidir sobre los campos de identidad

Según la estrategia de recopilación de datos empresariales, los campos de datos que etiquete como identidades determinan qué datos se incluyen en el mapa de identidad. Para obtener el máximo beneficio de Experience Platform y las identidades de cliente más completas posibles, debe cargar datos en línea y sin conexión.

* Los datos en línea son datos que describen la presencia y el comportamiento en línea, como nombres de usuario y direcciones de correo electrónico.

* Los datos sin conexión hacen referencia a datos que no están directamente relacionados con la presencia en línea, como los ID de sistemas CRM. Este tipo de datos hace que sus identidades sean más sólidas y admite la cohesión de los datos en sus distintos sistemas.

## Crear áreas de nombres de identidad adicionales

Aunque Experience Platform ofrece una variedad de áreas de nombres estándar, es posible que necesite crear áreas de nombres adicionales para categorizar correctamente sus identidades. Para obtener más información, lea la guía de [crear áreas de nombres personalizadas para su organización](./features/namespaces.md).

>[!NOTE]
>
>Las áreas de nombres de identidad son un calificador para identidades. Como resultado, una vez creada una Área de nombres, no se puede eliminar.

## Incluir datos de identidad en el modelo de datos de experiencia (XDM)

Como marco estandarizado mediante el cual Experience Platform organiza los datos de los clientes, el modelo de datos de experiencia (XDM) permite que los datos se compartan y entiendan entre los Experience Platform y otros servicios que interactúan con Experience Platform. Para obtener más información, lea la [Información general del sistema XDM](../xdm/home.md).

Tanto los esquemas de registros como los de series temporales proporcionan los medios para incluir los datos de identidad. A medida que se incorporan los datos, el gráfico de identidad creará nuevas relaciones entre fragmentos de datos de diferentes áreas de nombres si se encuentran para compartir datos de identidad comunes.

## Etiquetado de campos XDM como identidad

Cualquier campo de tipo `string` en los esquemas que implementan las clases XDM de registro o de serie temporal se pueden etiquetar como un campo de identidad. Como resultado, todos los datos introducidos en ese campo se considerarían datos de identidad.

Los campos de identidad también permiten la vinculación de identidades si comparten datos PII comunes.
Por ejemplo, al etiquetar los campos de número de teléfono como campos de identidad, el servicio de identidad grafica automáticamente las relaciones con las otras personas que utilizan el mismo número de teléfono.

>[!NOTE]
>
>* Los campos de tipo matriz y mapa no son compatibles y no se pueden marcar y etiquetar como campos de identidad.
>* El área de nombres de las identidades resultantes se proporciona en el momento en que se etiqueta el campo.

Para obtener más información, lea la guía en [definición de campos de identidad en la IU](../xdm/ui/fields/identity.md).

## Configuración de un conjunto de datos para el servicio de identidad

Durante el proceso de introducción por streaming, el servicio de identidad extrae automáticamente los datos de identidad de los datos de registros y series temporales. Sin embargo, para poder ingerir los datos, deben habilitarse para el servicio de identidad. Lea el tutorial sobre  [Configuración de un conjunto de datos para el perfil del cliente en tiempo real y el servicio de identidad mediante API](../profile/tutorials/dataset-configuration.md) para obtener más información.

## Ingesta de datos en el servicio de identidad

El servicio de identidad consume datos compatibles con XDM enviados al Experience Platform por [ingesta por lotes](../ingestion/batch-ingestion/overview.md) o [ingesta por streaming](../ingestion/streaming-ingestion/overview.md).

El siguiente vídeo tiene como objetivo ayudarle a comprender el servicio de identidad. Este vídeo muestra cómo etiquetar campos de datos como identidades, ingerir datos de identidad y luego verificar que los datos hayan llegado al gráfico privado del servicio de identidad de Adobe Experience Platform.

>[!WARNING]
>
>La interfaz de usuario del Experience Platform que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)