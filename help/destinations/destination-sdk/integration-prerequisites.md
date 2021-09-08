---
description: Para utilizar el SDK de destino, una empresa asociada debe cumplir los requisitos previos enumerados en este documento.
title: Requisitos previos de integración
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Requisitos previos de integración

Para utilizar el SDK de destino, asegúrese de cumplir los requisitos previos técnicos y de asociación enumerados en las secciones siguientes.

## Requisitos previos técnicos y de API

1. Tiene un extremo de API de REST para Adobe Experience Platform para entregar los siguientes tipos de datos a:
   * Información de pertenencia a segmentos;
   * Información de identidad del perfil;
   * (Opcional) Atributos adicionales para el enriquecimiento de perfiles.
2. El extremo de la API de REST admite la autenticación del portador de tokens de API o el protocolo de autenticación de OAuth 2.0.
3. (Opcional) Tiene una API de creación, actualización o eliminación de segmentos o un extremo de API para la administración de metadatos programáticos.

## Requisitos previos de la asociación

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que desea utilizar el SDK de destino, lea los requisitos de asociación para los ISV y los SI en la sección [obtener acceso](./overview.md#get-access).
