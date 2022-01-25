---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
source-git-commit: 49fd8615353a4029b0e98ba90e8438f8ff512e7b
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 12%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 26 de enero de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Preparación de datos](#data-prep)
- [Entornos aislados](#sandboxes)
- [Servicio de segmentación](#segmentation)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Experiencia de asignación consolidada | La nueva interfaz de asignación en la interfaz de usuario de Platform le ofrece una experiencia de asignación coherente para aprovechar las recomendaciones de asignación inteligente, configurar manualmente las reglas de asignación y depurar cualquier error que se produzca en los conjuntos de asignación. Para obtener más información, consulte la [[!DNL Data Prep] Guía de la interfaz de usuario](../../data-prep/home.md). |

Para obtener más información, consulte [!DNL Data Prep], consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Entornos aislados {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. A menudo, las empresas ejecutan varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, asegurando al mismo tiempo el cumplimiento de las normas operacionales. Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

| Función | Descripción |
| --- | --- |
| Mejoras en la interfaz de usuario de los Simuladores para pruebas | El indicador del simulador para pruebas ahora está integrado en el encabezado de todas las aplicaciones de interfaz de usuario de Platform. El indicador del simulador de pruebas muestra el nombre, la región y el tipo del simulador de pruebas, y también le permite acceder a un menú desplegable para alternar entre entornos limitados. Para obtener más información, consulte la [guía de la interfaz de usuario de sandbox](../../sandboxes/ui/user-guide.md). |

Para obtener más información sobre los entornos limitados, consulte la [información general sobre los entornos limitados](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

| Función | Descripción |
| --- | --- |
| Coincidencia de segmentos | Segment Match es un servicio de colaboración de datos que permite a dos o más usuarios de Platform intercambiar datos, en función de identificadores comunes, de forma segura, regulada y compatible con la privacidad. Para obtener más información, consulte la [Información general sobre la coincidencia de segmentos](../../segmentation/ui/segment-match/overview.md). |

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md).
