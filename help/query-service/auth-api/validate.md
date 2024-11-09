---
keywords: Experience Platform; seguridad; acceso ip; validación; guía de API; servicio de consultas; verificación de IP
title: Extremo de validación de IP
description: Obtenga información sobre cómo validar el acceso IP para zonas protegidas en el servicio de consultas mediante el punto final de la API de validación IP.
role: Developer
source-git-commit: ad1b6d8449a2a3ca9c8422e70769d12e33d8e255
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---

# Extremo de validación de IP

Utilice el punto final de la API de validación IP para comprobar si una dirección IP especificada puede acceder a una zona protegida designada en el servicio de consultas. Esta comprobación confirma si se aplican restricciones de acceso o si se permite a una dirección IP acceder a los datos dentro de una zona protegida.

## Validar IP para acceso a zonas protegidas {#validate-ip-for-sandbox-access}

Utilice el punto final de validación de IP para comprobar si una dirección IP determinada tiene permiso para acceder a los datos de la zona protegida especificada. Si no se configura ninguna restricción IP para la zona protegida, se permiten todas las direcciones IP de forma predeterminada. Si existen restricciones IP o CIDR, esta API verifica si la dirección IP especificada coincide con algún intervalo configurado.

>[!NOTE]
>
>Puede acceder a este extremo con **tokens de usuario** o **tokens de servicio**. No se necesitan requisitos de función específicos.

**Formato de API**

```http
POST /security/validate/ip-access
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con un booleano que indica si la IP está permitida.

>[!NOTE]
>
>El campo `isAllowed` de la respuesta devuelve `true` si la IP proporcionada tiene permiso para acceder a la zona protegida y `false` en caso contrario. Esta API admite la validación dinámica del acceso y garantiza el cumplimiento de la seguridad en los entornos de zonas protegidas.

```json
{
"isAllowed": true
}
```
