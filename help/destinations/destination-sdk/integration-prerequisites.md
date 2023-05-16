---
description: Para utilizar Destination SDK, una empresa asociada debe cumplir los requisitos previos enumerados en este documento.
title: Requisitos previos de integración
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Requisitos previos de integración

Para utilizar Destination SDK, asegúrese de cumplir los requisitos técnicos y de colaboración enumerados en las secciones siguientes.

## Requisitos previos técnicos y de API para destinos de flujo continuo {#streaming-prerequisites}

1. Tiene un extremo de API de REST para Adobe Experience Platform para entregar los siguientes tipos de datos a:
   * Información de pertenencia a segmentos;
   * Información de identidad del perfil;
   * (Opcional) Atributos adicionales para el enriquecimiento de perfiles.
2. El extremo de la API de REST es compatible con el token básico del portador o con los protocolos de autenticación de OAuth 2.0.
3. (Opcional) Tiene una API de creación, actualización o eliminación de segmentos o un extremo de API para la administración de metadatos programáticos.

## Requisitos previos técnicos para destinos de lote {#batch-prerequisites}

1. Tiene una ubicación de destino alojada en [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud]o un [!DNL Data Landing Zone], donde puede recibir archivos exportados fuera del Experience Platform.
2. Su plataforma de destino puede ingerir archivos en el formato configurado mediante la variable [opciones de formato de archivo](functionality/destination-server/file-formatting.md) en Destination SDK para destinos de lote.
3. (Opcional) Tiene un segmento crear, recuperar, actualizar o eliminar ([!DNL CRUD]) API o punto final de API para la administración de metadatos programáticos.

## Requisitos previos de la asociación {#partnership-prerequisites}

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que busca utilizar un Destination SDK, lea los requisitos de asociación para ISV e SI en la [sección obtener acceso](overview.md#get-access).
