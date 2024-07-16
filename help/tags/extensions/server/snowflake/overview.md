---
title: Resumen del Snowflake
description: Obtenga información acerca del Snowflake para reenvío de eventos en Adobe Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Información general de [!DNL Snowflake]

[[!DNL Snowflake]](https://www.snowflake.com/en/) es un almacén de datos en la nube que puede almacenar y analizar todos sus registros de datos en un solo lugar. Se puede utilizar para el almacenamiento de datos, los lagos de datos, la ingeniería de datos, la ciencia de datos, el desarrollo de aplicaciones de datos y el uso compartido y consumo seguros de datos en tiempo real o compartidos.

[!DNL Snowflake] se basa en Amazon Web Service (AWS), Microsoft Azure (Azure) y Google Cloud Platform (GCP).

![Diagrama que muestra la arquitectura de datos [!DNL Snowflake].](../../../images/extensions/server/snowflake/snowflake.png)

## Integración con nuestro Snowflake

Una cuenta de Snowflake puede alojarse en cualquiera de las siguientes plataformas de nube:

- [Amazon Web Service ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] es una plataforma de computación en la nube que ofrece una amplia variedad de servicios, como computación distribuida, almacenamiento de bases de datos, entrega de contenido y servicios de integración de software como servicio (SaaS) para la administración de la relación con los clientes (CRM) y la planificación de recursos empresariales (ERP).

Consulte [[!DNL AWS] descripción general](../aws/overview.md) para obtener más información sobre cómo instalar la extensión y configurar las reglas de reenvío de eventos.

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] es una plataforma de computación en la nube y un portal en línea que le permite acceder y administrar los servicios en la nube y los recursos proporcionados por Microsoft.

Consulte [[!DNL Azure] descripción general](../azure/overview.md) para obtener más información sobre cómo instalar la extensión y configurar las reglas de reenvío de eventos.

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] es una plataforma de computación en la nube que ofrece una amplia variedad de servicios, como computación distribuida, almacenamiento de bases de datos, entrega de contenido y servicios de integración de software como servicio (SaaS) para la administración de la relación con los clientes (CRM) y la planificación de recursos empresariales (ERP).

Consulte [[!DNL Google Cloud Platform] descripción general](../google-cloud-platform/overview.md) para obtener más información sobre cómo instalar la extensión y configurar las reglas de reenvío de eventos.

Nuestras extensiones nativas de reenvío de eventos [[!DNL AWS]](../aws/overview.md), [[!DNL Azure]](../azure/overview.md) y [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md) permiten a los clientes recopilar, enriquecer y reenviar sus datos de evento del lado del servidor en tiempo real a sus servicios en la nube para que los consuma [!DNL Snowflake]. Consulte lo siguiente:

![Diagrama de informe de [!DNL Snowflake] que muestra el vínculo entre [!DNL AWS] y [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## Pasos siguientes

Esta guía proporciona información general sobre [!DNL Snowflake] y el uso de [!DNL AWS] y [!DNL Azure] extensiones de reenvío de eventos.

Para obtener más información sobre las capacidades de reenvío de eventos de [!DNL AWS] y [!DNL Azure] en Experience Platform, consulte [[!DNL AWS] descripción general de la extensión](../aws/overview.md) y [[!DNL Azure] descripción general de la extensión](../azure/overview.md).
