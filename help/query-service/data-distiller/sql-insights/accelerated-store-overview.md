---
title: Información general sobre almacenamiento acelerado
description: Aprenda a utilizar el almacén acelerado en Adobe Experience Platform para obtener perspectivas rápidas basadas en SQL mediante datos agregados. Esta página describe su uso previsto, las restricciones en los datos de identidad e inteligencia empresarial, y las prácticas recomendadas para garantizar el cumplimiento de las políticas de gobernanza de datos de Adobe.
source-git-commit: 5e8dccf91e8c83b4734b363539cfb911b5c2ae29
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# Información general sobre la tienda acelerada

El almacén acelerado en Adobe Experience Platform es una capa de almacenamiento optimizada para el rendimiento disponible a través del SKU de Data Distiller. Está diseñado para contener conjuntos de datos preagregados, lo que permite obtener perspectivas y procesamientos de tableros rápidos y basados en SQL.

Este documento describe cómo utilizar correctamente el almacén acelerado, explica por qué los conjuntos de datos agregados están exentos de los procesos de higiene de datos estándar y destaca que los datos de identidad no deben almacenarse. Para cumplir con las directrices de Adobe, debe adherirse a las políticas de gobernanza de datos y a las restricciones de uso descritas en este documento.

## Funcionalidades clave {#key-capabilities}

La tienda acelerada está diseñada específicamente para el rendimiento y la eficacia. Permite optimizar los flujos de trabajo de consultas e informes centrándose en los datos agregados. La lista siguiente resalta sus funcionalidades principales:

- Proporcionar paneles y widgets de alto rendimiento mediante consultas SQL
- Almacenar conjuntos de datos preagregados diseñados para perspectivas recurrentes
- Compatibilidad con la creación de modelos de datos personalizados para casos de uso de informes

## Uso previsto {#intended-use}

El almacén acelerado está diseñado **únicamente** para almacenar datos agregados que permiten una visualización y un tablero optimizados. Su arquitectura no está pensada para admitir cargas de trabajo complejas, como el procesamiento de inteligencia empresarial o el almacenamiento de datos.

>[!IMPORTANT]
>
>El almacenamiento acelerado no sustituye al lago de datos ni a una solución de almacenamiento de uso general.

## Restricciones de uso {#usage-restrictions}

Para garantizar el cumplimiento del modelo de control de datos y los términos de licencia de Adobe, se aplican las siguientes restricciones:

- **No almacenar datos de evento sin procesar**
- **No almacenar datos de identidad**
- **No almacene información de identificación personal (PII)**, como direcciones de correo electrónico, datos de atención médica o identificadores de clientes
- **No use el almacén acelerado para replicar todo el lago de datos**

Solo se pueden almacenar en el almacén acelerado datos agregados no identificables. Los conjuntos de datos agregados no se pueden analizar mediante ingeniería inversa para revelar los datos de origen originales, lo que los exime de los procesos de higiene de datos centralizados de Experience Platform.

## Gobernanza y cumplimiento {#governance-and-compliance}

El uso del almacén acelerado fuera de su propósito previsto puede poner a su organización en riesgo de violar los límites del acuerdo de licencia y la gobernanza de datos de Adobe. Si se producen incidentes de control de datos debido a patrones de uso no admitidos, su organización asume la responsabilidad total.

Adobe no se hace responsable de las consecuencias derivadas del uso indebido de esta función.

Para obtener más información sobre cómo administrar los datos de forma responsable en Experience Platform, consulta [Gobernanza, privacidad y seguridad en Experience Platform](../../../landing/governance-privacy-security/overview.md). Esta página describe los servicios y las herramientas que le ayudan a controlar los datos de la experiencia de acuerdo con las políticas empresariales, los requisitos legales y los estándares de desarrollo. Para obtener vínculos a instrucciones más detalladas sobre el etiquetado de uso y la aplicación de políticas, visite la [Información general sobre la administración de datos](../../../data-governance/home.md).

## Prácticas recomendadas {#best-practices}

Para garantizar un uso eficiente y conforme de la tienda acelerada, siga estas prácticas recomendadas:

- Utilice conjuntos de datos derivados para crear tablas preagregadas específicamente adaptadas a sus necesidades de tablero
- Evite utilizar el almacén acelerado como ubicación de ensayo o de copia de seguridad para conjuntos de datos sin procesar
- Revise regularmente su uso para garantizar la alineación con las protecciones recomendadas por Adobe

## Pasos siguientes

Al leer este documento, ha aprendido qué es el almacén acelerado, su uso previsto para los datos agregados en situaciones de creación de informes y las reglas de gobernanza que deben seguirse para garantizar un uso compatible. Para profundizar en su comprensión y aplicar estas directrices de forma eficaz, explore los siguientes recursos:

- [Información general de SQL Insights](./overview.md): Descubra cómo SQL Insights habilita la creación de informes optimizados para el rendimiento mediante conjuntos de datos agregados.
- [Enviar consultas aceleradas](./send-accelerated-queries.md): Aprenda a ejecutar consultas en el almacén acelerado para activar paneles y widgets.
- [Gobernanza e higiene de los datos](../../data-governance/overview.md): revise las políticas de higiene de los datos y las directrices de gobernanza de Adobe para garantizar que se cumpla con el uso.
