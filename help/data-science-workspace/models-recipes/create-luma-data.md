---
keywords: Experience Platform;datos web de luma;Data Science Workspace;temas populares;recetas;datos de demostración;datos web de demostración;datos de luma
solution: Experience Platform
title: Creación de los esquemas y conjuntos de datos web de Luma
type: Tutorial
description: Este tutorial proporciona los requisitos previos y los recursos necesarios para el modelo de tendencia de demostración de Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Creación de esquemas y conjuntos de datos del modelo de tendencia de Luma

Este tutorial le proporciona los requisitos previos y los recursos necesarios para todos los demás [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] tutoriales. Una vez completados, los siguientes esquemas y conjuntos de datos estarán disponibles para usted y su organización.

**Esquemas:**

- Esquema de datos web de Luma
- Esquema de resultados de puntuación del modelo de tendencia

**Conjuntos de datos:**

- Conjunto de datos web de Luma
- Conjunto de datos de formación del modelo de tendencia
- Conjunto de datos de puntuación del modelo de tendencia
- Conjunto de datos de resultados de puntuación del modelo de tendencia

## Descargar los recursos {#assets}

El siguiente tutorial utiliza un modelo de tendencia de compra de Luma personalizado. Antes de continuar, [descargar los recursos necesarios](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) carpeta zip. Esta carpeta contiene:

- El portátil modelo de tendencia a la compra
- Un bloc de notas utilizado para introducir datos en un conjunto de datos de formación y puntuación (un subconjunto de los datos web de Luma)
- Archivo JSON de demostración que contiene los datos web de 730 000 usuarios de Luma
- Un portátil opcional EDA (análisis de datos exploratorios) de Python 3 que se puede utilizar para ayudar a comprender los datos y el modelo web.

>[!NOTE]
>
> Puede utilizar su propio esquema y datos para cualquiera de los tutoriales. Sin embargo, el modelo de demostración proporcionado en los recursos no funciona a menos que se proporcionen los archivos de configuración y el archivo de requisitos adecuados. Este modelo de tendencia de demostración se diseñó para trabajar con datos web de Luma.

### Creación del esquema de datos web de Luma e ingesta de datos

Para crear un modelo, debe tener un conjunto de datos en Platform que se utilice para entrenar y puntuar el modelo. El siguiente tutorial de vídeo de la [Curso de Data Science Workspace](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw&amp;lang=es) le explica cómo crear el esquema de Luma e ingerir los datos utilizados por el modelo de tendencia de compra.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Cree los conjuntos de datos de formación, puntuación y resultados de puntuación

Para ejecutar el bloc de notas del generador de fórmulas o utilizar la API para entrenar y puntuar un modelo, debe especificar los conjuntos de datos y los esquemas que se utilizan para la formación/puntuación. El siguiente tutorial de vídeo le guía a través de la configuración de los conjuntos de datos de formación, puntuación y resultados de puntuación, así como el esquema de resultados de puntuación utilizado en el modelo de tendencia de compra de Luma.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente los esquemas y conjuntos de datos necesarios para el modelo de tendencia de Luma. Ya está listo para continuar con el siguiente tutorial y crear el modelo con [bloc de notas del generador de fórmulas](../jupyterlab/create-a-model.md) tutorial.

Además, puede explorar los datos mediante el bloc de notas de análisis exploratorio de datos (EDA) proporcionado. Este bloc de notas se puede utilizar para comprender mejor los patrones de los datos de Luma, comprobar la sanidad de los datos y resumir los datos relevantes para el modelo de tendencia predictiva. Para obtener más información sobre Análisis de datos exploratorios, visite la [Documentación de EDA](../jupyterlab/eda-notebook.md).
