---
title: Notas de la versión de Adobe Experience Platform de noviembre de 2021
description: Notas de la versión de noviembre de 2021 de Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 12%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 17 de noviembre de 2021**

## Nuevas funciones

Nuevas funciones de Adobe Experience Platform:

- [Real-Time Customer Data Platform edición B2B](#B2B)
- [(Beta) Active los segmentos de audiencia en destinos por lotes a través de la API de activación ad hoc](#ad-hoc-activation)

## Actualizaciones de funciones existentes

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Inteligencia artificial aplicada a la atribución](#attribution-ai)
- [Inteligencia artificial aplicada al cliente](#customer-ai)

### Real-Time Customer Data Platform edición B2B {#B2B}

**Fecha de la versión: 12 de noviembre de 2021**

Real-Time CDP B2B Edition, que se creó en Real-time Customer Data Platform (Real-Time CDP), está diseñado específicamente para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse a audiencias específicas con precisión y captar esas audiencias en todos los canales disponibles.

Se han realizado mejoras en una variedad de funciones de Adobe Experience Platform que distinguen a Real-Time CDP B2B Edition de su homólogo B2C. Entre ellos se incluyen mejoras en el Experience Data Model (XDM) para casos de uso B2B, actualizaciones en la resolución de identidades y la segmentación de perfiles, así como un conector creado a medida y un destino para Marketo Engage. El conector Marketo permite a las marcas B2B conectar sus datos de participación B2B líderes del sector con información de comportamiento para fomentar posibles clientes y mejorar las operaciones de marketing basadas en cuentas.

-[Nuevas ediciones B2B y B2P](#editions)
-[Nuevos conectores de origen y destino de datos de Marketo](#marketo)
-[XDM B2B estándar](#XDM)

### Nuevas ediciones B2B y B2P {#editions}

Se pueden adquirir nuevas ediciones B2B y B2P que aportan datos y funcionalidad B2B tanto a los productos de Real-Time CDP como a los de Platform Activation.

Para obtener más información sobre Real-Time CDP B2B Edition, consulte la [descripción general](../../rtcdp/overview.md).

### Nuevos conectores de origen y destino de datos de Marketo {#marketo}

Los nuevos conectores de origen y destino de datos de Marketo transmiten los datos de Marketo a las audiencias de Platform y Platform de nuevo a Marketo. Disponible para todos los usuarios de Platform.

| Función | Descripción |
|----------|-------------|
| Conector de origen del Marketo Engage | El [Conector de origen del Marketo Engage](../../sources/connectors/adobe-applications/marketo/marketo.md) permite a los especialistas en marketing introducir sin problemas datos de una o más instancias de Marketo en su instancia de Adobe Experience Platform y proporciona una solución completa para la administración de posibles clientes y los especialistas en marketing B2B. |
| Destino del Marketo Engage | El [Marketo destination](../../destinations/catalog/adobe/marketo-engage.md) permite a los especialistas en marketing insertar segmentos creados en Adobe Experience Platform en Marketo, donde aparecerán como listas estáticas. |

### XDM B2B estándar {#XDM}

Las clases XDM estándar B2B, los grupos de campos y los tipos de datos están disponibles para todos los usuarios de Platform.

| Función | Descripción |
|-----------|--------------|
| Clases XDM B2B estándar | Real-time Customer Data Platform B2B Edition proporciona varios XDM estándar que capturan detalles sobre entidades de datos B2B esenciales, como cuentas, oportunidades, campañas y más. |

Consulte la [Esquemas en Real-time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md) para obtener más información sobre la captura de entidades de datos B2B.

### (Beta) Active los segmentos de audiencia en destinos por lotes a través de la API de activación ad hoc {#ad-hoc-activation}

La API de activación ad hoc permite a los especialistas en marketing activar mediante programación segmentos de audiencia en destinos de forma rápida y eficaz en situaciones en las que se requiera la activación inmediata. La activación de audiencias ad hoc solo es compatible con [destinos basados en archivos por lotes](../../destinations/destination-types.md#file-based) y está actualmente en fase beta. Para obtener más información, consulte la [Documentación de la API de activación ad hoc](../../destinations/api/ad-hoc-activation-api.md).

### Inteligencia artificial aplicada a la atribución {#attribution-ai}

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

| Función | Descripción |
|-----------|---------------|
| Compatibilidad con varios conjuntos de datos | Ahora, Attribution AI puede introducir fácilmente varios conjuntos de datos directamente en la interfaz de usuario sin necesidad de asignar y unir cada conjunto de datos. Esta nueva capacidad de ahorro de tiempo proporciona puntuaciones más potentes y precisas con datos más completos de varios conjuntos de datos. |
| Asignación de campos de campaña y canal de medios | Attribution AI ahora admite la asignación de campos de campaña y canal de medios. La asignación de canales de medios entre conjuntos de datos mejora las perspectivas derivadas de la Attribution AI y ayuda a proporcionar resultados más claros y fáciles de interpretar. |

Para obtener más información sobre Attribution AI, consulte la [documentación de Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Inteligencia artificial aplicada al cliente {#customer-ai}

La inteligencia artificial aplicada al cliente disponible en Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades comerciales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.

**Funciones actualizadas**

| Función | Descripción |
|-----------|-------------|
| Compatibilidad con varios conjuntos de datos | La inteligencia artificial aplicada al cliente ahora puede introducir fácilmente varios conjuntos de datos directamente en la interfaz de usuario sin necesidad de asignar y unir cada conjunto de datos. Esta nueva capacidad de ahorro de tiempo proporciona puntuaciones más potentes y precisas con datos más completos de varios conjuntos de datos. |
| Atributos de perfil personalizados | La inteligencia artificial aplicada al cliente ahora admite la definición de campos de conjuntos de datos de perfil personalizados (con marcas de tiempo) en los datos, además de los campos de evento estándar. El uso de esta opción le permite agregar atributos de perfil adicionales que considere influyentes, lo que puede mejorar la calidad del modelo y proporcionar resultados más precisos. |

Para obtener más información sobre Customer AI, consulte la [Documentación de Customer AI](../../intelligent-services/customer-ai/overview.md).
