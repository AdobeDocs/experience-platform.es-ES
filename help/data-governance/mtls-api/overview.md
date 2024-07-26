---
title: Guía de API de MTLS
description: Aprenda a utilizar la API del servicio mTLS para recuperar y comprobar de forma segura los certificados públicos emitidos por el Adobe.
role: Developer
source-git-commit: f805d03ff2cd3a4f84ca8068023d83986f8bdfbb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Información general de API del servicio MTLS

Utilice la API del servicio MTLS para recuperar de forma segura los certificados públicos emitidos por el Adobe para las aplicaciones de su organización. Esta API garantiza que los intercambios de datos entre sus clientes y Adobe Experience Platform estén autenticados y cifrados, lo que proporciona un nivel adicional de seguridad. Al verificar externamente la autenticidad de los certificados, puede mejorar la confianza y proteger la información confidencial.

## Certificado público

Un certificado público es un documento digital que se utiliza para autenticar la identidad de un servidor o cliente en comunicaciones seguras. En el contexto de la API del servicio mTLS, estos certificados garantizan que los intercambios de datos con Adobe Experience Platform se autentican y cifran. La recuperación y verificación de estos certificados a través de la API confirma su autenticidad, lo que mejora la seguridad y fiabilidad de sus transacciones de datos y protege la información confidencial. Para obtener información sobre cómo recuperar el certificado público, consulte la [guía de extremo](./public-certificate-endpoint.md) para obtener información sobre cómo realizar llamadas.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API del servicio MTLS, lea la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y mucho más.
