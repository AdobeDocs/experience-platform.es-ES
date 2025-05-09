---
title: Información de seguridad de la capa de transporte (TLS)
description: Información acerca de las versiones TLS y los cifrados que se utilizan
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 236c5a11f40490fc7ee536358fb146027fe64545
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 25%

---

# Información de seguridad de la capa de transporte (TLS)

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Para obtener una referencia consolidada de los cambios terminológicos, consulte el documento [actualizaciones de términos](../../term-updates.md).

Seguridad de la capa de transporte (TLS) es un protocolo criptográfico que proporciona seguridad de extremo a extremo para los datos enviados entre aplicaciones a través de Internet. Para obtener información más detallada sobre TLS, lea la [documentación básica de TLS](https://www.internetsociety.org/deploy360/tls/basics/).

Las etiquetas de Adobe Experience Platform son un sistema de administración de etiquetas diseñado para cargar dinámicamente scripts en su sitio web. TLS asegura la comunicación entre el host de Adobe `assets.adobedtm.com` y el sitio web cuando se cargan estos scripts.

Hay varias versiones TLS disponibles y admite una serie de cifrados diferentes. No todas las versiones y cifrados son los mismos, ya que algunas se consideran menos o más seguras que otras.

## Versiones y cifrados TLS compatibles

Actualmente, la opción de host de Adobe admite las siguientes versiones y cifrados TLS:

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### Alojamiento propio

Si está [alojando su biblioteca](../publishing/hosts/self-hosting-libraries.md) por su cuenta, las versiones TLS admitidas serán determinadas por su propio servicio de alojamiento.
