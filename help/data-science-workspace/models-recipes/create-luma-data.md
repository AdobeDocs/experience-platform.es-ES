---
keywords: Experience Platform;datos web de luma;Data Science Workspace;temas populares;fórmulas;datos de demostración;datos web de demostración;datos de luma
solution: Experience Platform
title: Creación de esquemas web y conjuntos de datos de Luma
type: Tutorial
description: Este tutorial le proporciona los requisitos previos y los recursos necesarios para el modelo de propensión de demostración de Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Creación de esquemas y conjuntos de datos del modelo de propensión de Luma

Este tutorial le proporciona los requisitos previos y los recursos necesarios para el resto de [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] tutoriales. Una vez finalizado, los siguientes esquemas y conjuntos de datos estarán disponibles para usted y su organización.

**Esquemas:**

- esquema de datos web de Luma
- Esquema de resultados de puntuación del modelo de propensión

**Conjuntos de datos:**

- Conjunto de datos web de Luma
- Conjunto de datos de capacitación del modelo de propensión
- Conjunto de datos de puntuación del modelo de propensión
- Conjunto de datos de resultados de puntuación del modelo de propensión

## Descargar los recursos {#assets}

El siguiente tutorial utiliza un modelo de propensión de compra de Luma personalizado. Antes de continuar, [descargar los recursos necesarios](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) carpeta zip. Esta carpeta contiene:

- El bloc de notas del modelo de propensión de compra
- Un bloc de notas que se utiliza para introducir datos en un conjunto de datos de capacitación y puntuación (un subconjunto de datos web de Luma)
- Archivo JSON de demostración que contiene los datos web de 730 000 usuarios de Luma
- Un bloc de notas opcional Python 3 EDA (análisis de datos exploratorios) que puede utilizarse para ayudar a comprender los datos y el modelo web.

>[!NOTE]
>
> Puede utilizar su propio esquema y datos para cualquiera de los tutoriales. Sin embargo, el modelo de demostración proporcionado en los recursos no funciona a menos que se proporcione el archivo de configuración y requisitos adecuado. Este modelo de propensión de demostración se ha diseñado para trabajar con datos web de Luma.

### Crear el esquema de datos web de Luma e introducir los datos

Para crear un modelo, debe tener un conjunto de datos en Platform que se utilice para entrenar y puntuar el modelo. El siguiente tutorial de vídeo de la sección [Curso de Data Science Workspace](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw&amp;lang=es) lo acompaña durante la creación del esquema de Luma y la ingesta de los datos utilizados por el modelo de propensión de compra.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Crear conjuntos de datos de resultados de capacitación, puntuación y puntuación

Para ejecutar el bloc de notas del generador de fórmulas o utilizar la API para entrenar y puntuar un modelo, debe especificar los conjuntos de datos y los esquemas que se utilizan para la formación/puntuación. El siguiente tutorial de vídeo le explica cómo configurar los conjuntos de datos de resultados de capacitación, puntuación y puntuación, así como el esquema de resultados de puntuación utilizado en el modelo de propensión de compra de Luma.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente los esquemas y conjuntos de datos necesarios para el modelo de propensión de Luma. Ya está listo para continuar con el siguiente tutorial y crear el modelo con el [portátil del generador de fórmulas](../jupyterlab/create-a-model.md) tutorial.

Además, puede explorar los datos mediante el bloc de notas de Análisis de datos exploratorios (EDA) que se proporciona. Este bloc de notas se puede utilizar para ayudar a comprender los patrones de los datos de Luma, comprobar la solidez de los datos y resumir los datos relevantes para el modelo de propensión predictiva. Para obtener más información sobre el análisis de datos exploratorios, visite [Documentación de EDA](../jupyterlab/eda-notebook.md).
