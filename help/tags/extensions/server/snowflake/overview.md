---
title: Resumen del Snowflake
description: Obtenga información acerca del Snowflake para reenvío de eventos en Adobe Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# Información general del [!DNL Snowflake]

[[!DNL Snowflake]](https://www.snowflake.com/en/) es un almacén de datos en la nube que puede almacenar y analizar todos los registros de datos en un solo lugar. Se puede utilizar para el almacenamiento de datos, los lagos de datos, la ingeniería de datos, la ciencia de datos, el desarrollo de aplicaciones de datos y el uso compartido y consumo seguros de datos en tiempo real o compartidos.

[!DNL Snowflake] se basa en Amazon Web Service (AWS), Microsoft Azure (Azure) y Google Cloud Platform (GCP).

![Un diagrama que muestra el [!DNL Snowflake] arquitectura de datos.](../../../images/extensions/server/snowflake/snowflake.png)

## Integración con nuestro Snowflake

Una cuenta de Snowflake puede alojarse en cualquiera de las siguientes plataformas de nube:

- [AMAZON WEB SERVICE ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] es una plataforma de computación en la nube que ofrece una amplia variedad de servicios, como computación distribuida, almacenamiento de bases de datos, entrega de contenido y servicios de integración de software como servicio (SaaS) para la administración de la relación con los clientes (CRM) y la planificación de recursos empresariales (ERP).

Consulte la [[!DNL AWS] descripción general](../aws/overview.md) para obtener más información sobre la instalación de la extensión y la configuración de reglas de reenvío de eventos.

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] es una plataforma de cloud computing y un portal en línea que le permite acceder y administrar los servicios y recursos en la nube que proporciona Microsoft.

Consulte la [[!DNL Azure] descripción general](../azure/overview.md) para obtener más información sobre la instalación de la extensión y la configuración de reglas de reenvío de eventos.

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] es una plataforma de computación en la nube que ofrece una amplia variedad de servicios, como computación distribuida, almacenamiento de bases de datos, entrega de contenido y servicios de integración de software como servicio (SaaS) para la administración de la relación con los clientes (CRM) y la planificación de recursos empresariales (ERP).

Consulte la [[!DNL Google Cloud Platform] descripción general](../google-cloud-platform/overview.md) para obtener más información sobre la instalación de la extensión y la configuración de reglas de reenvío de eventos.

Nuestro nativo [[!DNL AWS]](../aws/overview.md), [[!DNL Azure]](../azure/overview.md), y [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md) las extensiones de reenvío de eventos permiten a los clientes recopilar, enriquecer y reenviar sus datos de evento del lado del servidor en tiempo real a sus servicios en la nube para que los consuma [!DNL Snowflake]. Vea lo siguiente:

![El [!DNL Snowflake] diagrama del sistema de informes que muestra el vínculo entre [!DNL AWS] y [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## Pasos siguientes

Esta guía proporciona una descripción general de [!DNL Snowflake] y el uso de [!DNL AWS] y [!DNL Azure] extensiones de reenvío de eventos.

Para obtener más información sobre [!DNL AWS] y [!DNL Azure] funciones de reenvío de eventos en Experience Platform, consulte las [[!DNL AWS] información general sobre extensiones](../aws/overview.md) y el [[!DNL Azure] información general sobre extensiones](../azure/overview.md).
