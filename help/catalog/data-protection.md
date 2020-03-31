---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Protección de datos en Adobe Experience Platform
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716

---


# Protección de datos en Adobe Experience Platform

Todos los datos que Adobe Experience Platform ingesta y utiliza se almacenan en Data Lake, un almacén de datos muy granular que contiene todos los datos administrados por Platform, independientemente del origen o el formato de archivo. Todos los datos que persisten en Data Lake se cifran, almacenan y administran en una cuenta de Almacenamiento aislada de Microsoft Azure Data Lake que sea única para su organización.

El siguiente diagrama de flujo de proceso ilustra cómo la plataforma de experiencia transfiere, procesa, cifra y mantiene los datos:

![](images/data-protection/flow.png)

Para obtener más información sobre cómo se cifran los datos en reposo en el Almacenamiento de Data Lake, consulte el documento sobre el cifrado de [datos en el Almacenamiento](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)de Azure Data Lake. Para obtener información sobre cómo se cifran los datos en reposo en Cosmos DB, consulte el documento sobre el cifrado de [datos en Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).