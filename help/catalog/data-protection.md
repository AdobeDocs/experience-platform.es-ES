---
keywords: Experience Platform;home;popular topics;catalog;data protection;encryption data lake
solution: Experience Platform
title: Protección de datos en Adobe Experience Platform
topic: data protection
description: Todos los datos que persisten en Data Lake se cifran, almacenan y administran en una cuenta de Almacenamiento aislada de Microsoft Azure Data Lake que sea única para su organización. El siguiente diagrama de flujo de proceso ilustra cómo el Experience Platform ingesta, procesa, cifra y persiste los datos.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Protección de datos en Adobe Experience Platform

Todos los datos que Adobe Experience Platform ingesta y utiliza se almacenan en el [!DNL Data Lake], un almacén de datos muy granular que contiene todos los datos administrados por [!DNL Platform], independientemente del origen o el formato de archivo. Todos los datos persistentes en el [!DNL Data Lake] se cifran, almacenan y administran en una cuenta de [!DNL Microsoft Azure Data Lake] Almacenamiento aislada que es única para su organización.

El siguiente diagrama de flujo de proceso ilustra cómo se ingieren, procesan, cifran y mantienen los datos [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Para obtener más información sobre cómo se cifran los datos en reposo en [!DNL Data Lake Storage], consulte el documento sobre el cifrado de [datos en Azure Data Lake Almacenamiento](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Para obtener información sobre cómo se cifran los datos en reposo en [!DNL Cosmos DB], consulte el documento sobre el cifrado de [datos en Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).