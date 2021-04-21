---
keywords: Experience Platform;inicio;temas populares;catálogo;protección de datos;lago de datos de cifrado
solution: Experience Platform
title: Protección de datos en Adobe Experience Platform
topic-legacy: data protection
description: Todos los datos que persisten en Data Lake se cifran, almacenan y administran en una cuenta aislada de Microsoft Azure Data Lake Storage que es única para su organización. El siguiente diagrama de flujo de proceso ilustra cómo el Experience Platform incorpora, procesa, cifra y persiste los datos.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Protección de datos en Adobe Experience Platform

Todos los datos introducidos y utilizados por Adobe Experience Platform se almacenan en el [!DNL Data Lake], un almacén de datos muy granular que contiene todos los datos administrados por [!DNL Platform], independientemente del origen o el formato de archivo. Todos los datos que persisten en [!DNL Data Lake] se cifran, almacenan y administran en una cuenta de almacenamiento [!DNL Microsoft Azure Data Lake] aislada que es única para su organización.

El siguiente diagrama de flujo de proceso ilustra cómo se introducen, procesan, cifran y mantienen los datos [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Para obtener más información sobre cómo se cifran los datos en reposo en [!DNL Data Lake Storage], consulte el documento sobre [cifrado de datos en Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Para obtener información sobre cómo se cifran los datos en reposo en [!DNL Cosmos DB], consulte el documento sobre el [cifrado de datos en Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).
