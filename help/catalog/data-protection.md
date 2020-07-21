---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Protección de datos en Adobe Experience Platform
topic: data protection
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Protección de datos en Adobe Experience Platform

Todos los datos que Adobe Experience Platform ingesta y utiliza se almacenan en el [!DNL Data Lake], un almacén de datos altamente granular que contiene todos los datos administrados por [!DNL Platform], independientemente del origen o el formato de archivo. Todos los datos persistentes en el [!DNL Data Lake] se cifran, almacenan y administran en una cuenta de [!DNL Microsoft Azure Data Lake] Almacenamiento aislada que es única para su organización.

El siguiente diagrama de flujo de proceso ilustra cómo se ingieren, procesan, cifran y mantienen los datos [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Para obtener más información sobre cómo se cifran los datos en reposo en [!DNL Data Lake Storage], consulte el documento sobre el cifrado de [datos en Azure Data Lake Almacenamiento](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Para obtener información sobre cómo se cifran los datos en reposo en [!DNL Cosmos DB], consulte el documento sobre el cifrado de [datos en Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).