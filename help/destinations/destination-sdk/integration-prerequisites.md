---
description: Para utilizar Destination SDK, una empresa asociada debe cumplir los requisitos previos enumerados en este documento.
title: Requisitos previos de integración
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Requisitos previos de integración

Para utilizar Destination SDK, asegúrese de cumplir los requisitos técnicos y de asociación que se enumeran en las secciones siguientes.

## Requisitos técnicos/API previos para destinos de flujo continuo {#streaming-prerequisites}

1. Tiene un extremo de API de REST para que Adobe Experience Platform envíe los siguientes tipos de datos a:
   * Información de pertenencia a audiencias;
   * Información de identidad del perfil;
   * (Opcional) Atributos adicionales para el enriquecimiento de perfiles.
2. El extremo de la API de REST admite los protocolos de autenticación básicos, token de portador o OAuth 2.0.
3. (Opcional) Tiene una API de creación, actualización o eliminación de audiencia o un extremo de API para la administración de metadatos mediante programación.

## Requisitos técnicos previos para destinos por lotes {#batch-prerequisites}

1. Tiene una ubicación de destino hospedada en [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud] o un(a) [!DNL Data Landing Zone] privado(a), donde puede recibir archivos exportados fuera del Experience Platform.
2. Su plataforma de destino puede ingerir archivos en el formato configurado a través de [opciones de formato de archivo](functionality/destination-server/file-formatting.md) en el Destination SDK para destinos por lotes.
3. (Opcional) Tiene una API de creación/recuperación/actualización/eliminación de audiencia ([!DNL CRUD]) o un extremo de API para la administración de metadatos mediante programación.

## Requisitos previos de asociación {#partnership-prerequisites}

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que desea utilizar un Destination SDK, lea los requisitos de asociación para ISV y SI en la [sección de obtención de acceso](overview.md#get-access).
