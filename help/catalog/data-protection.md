---
keywords: Experience Platform;inicio;temas populares;catálogo;protección de datos;lago de datos de cifrado
solution: Experience Platform
title: Protección de datos en Adobe Experience Platform
topic: data protection
description: Todos los datos que persisten en Data Lake se cifran, almacenan y administran en una cuenta de Almacenamiento aislada de Microsoft Azure Data Lake que sea única para su organización. El siguiente diagrama de flujo de proceso ilustra cómo el Experience Platform ingesta, procesa, cifra y persiste los datos.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Protección de datos en Adobe Experience Platform

Todos los datos que Adobe Experience Platform ingesta y utiliza se almacenan en [!DNL Data Lake], un almacén de datos altamente granular que contiene todos los datos administrados por [!DNL Platform], independientemente del origen o el formato de archivo. Todos los datos que persisten en [!DNL Data Lake] se cifran, almacenan y administran en una cuenta de Almacenamiento [!DNL Microsoft Azure Data Lake] aislada que es única para su organización.

El siguiente diagrama de flujo de proceso muestra cómo [!DNL Experience Platform] ingesta, procesa, cifra y persiste los datos:

![](images/data-protection/flow.png)

Para obtener más información sobre cómo se cifran los datos en reposo en [!DNL Data Lake Storage], consulte el documento sobre [cifrado de datos en el Almacenamiento de Azure Data Lake](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Para obtener información sobre cómo se cifran los datos en reposo en [!DNL Cosmos DB], consulte el documento sobre [cifrado de datos en Base de datos Cosmos de Azure](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).