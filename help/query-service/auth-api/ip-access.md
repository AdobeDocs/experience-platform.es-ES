---
keywords: Experience Platform; seguridad; acceso ip; QS-Auth; guía de API; servicio de consulta; intervalos de IP
title: Punto final de acceso IP
description: Obtenga información sobre cómo administrar intervalos de IP para el acceso a zonas protegidas en el servicio de consultas mediante el punto final de la API de acceso IP.
role: Developer
exl-id: fc15ab50-c125-4f00-a311-81fd41697c7d
source-git-commit: d0f4a295928b000b6091172800e453d79dc44e3a
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 5%

---

# Extremo de acceso IP

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes que han adquirido el complemento Data Distiller. Para obtener más información, contacte con su representante de Adobe.

Para proteger el acceso a los datos dentro de una zona protegida del servicio de consulta especificada, utilice el extremo de acceso IP para administrar los intervalos de IP permitidos. Puede utilizar esta API para recuperar, configurar o eliminar intervalos de IP asociados al ID de su organización.

Puede realizar las siguientes acciones con la API de acceso IP:

- **Recuperar todos los rangos de IP**
- **Establecer nuevos intervalos de IP**
- **Eliminar intervalos de IP existentes**

Este documento describe las solicitudes y respuestas que puede realizar y recibir desde el extremo `/security/ip-access`.

>[!NOTE]
>
>Debe tener un token de usuario para llamar a esta API. Consulte la [guía de introducción](./getting-started.md) para obtener información sobre cómo adquirir los valores necesarios para cada uno de los encabezados.

## Recuperar todos los intervalos de IP {#fetch-all-ip-ranges}

Recupere una lista de todos los rangos de IP configurados para su zona protegida. Si no se establece ningún intervalo de IP, todas las IP se permiten de forma predeterminada y la respuesta devuelve una lista vacía en `allowedIpRanges`.

**Formato de API**

```http
GET /security/ip-access
```

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de los intervalos de IP permitidos de la zona protegida.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

La siguiente tabla proporciona una descripción y un ejemplo de las propiedades del esquema de respuesta:

| Propiedad | Descripción | Ejemplo |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | ID de organización de la zona protegida. | `{ORG_ID}` |
| `sandboxName` | Nombre de la zona protegida donde se aplican las restricciones IP. | `prod` |
| `channel` | El modo de acceso para restricciones de IP. Actualmente el único valor aceptado es `data_distiller`. Este valor significa que las restricciones IP se aplican a conexiones PSQL o JDBC. | `data_distiller` |
| `allowedIpRanges` | Lista de direcciones IP permitidas en formato CIDR o IP fija. Cada entrada puede incluir una descripción opcional. | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>El campo `allowedIpRanges` puede incluir dos tipos de especificaciones de IP: <br><ul><li>**CIDR**: Notación CIDR estándar (por ejemplo, `"136.23.110.0/23"`) para definir rangos de IP.</li><li>**IP fija**: IP únicas para permisos de acceso individuales (por ejemplo, `"101.10.1.1"`).</li></ul>

## Establecer nuevos intervalos de IP

Sobrescriba los intervalos de IP existentes configurando una nueva lista para la zona protegida. Esta operación requiere una lista completa de intervalos de IP, incluidos los que permanecen sin cambios.

**Formato de API**

```http
PUT /security/ip-access
```

**Solicitud**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de los intervalos de IP recién configurados.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## Eliminar intervalos de IP {#delete-ip-ranges}

Elimine todos los intervalos de IP configurados para la zona protegida. Esta acción elimina los rangos de IP y devuelve la lista de IP eliminadas.

>[!NOTE]
>
>La operación de eliminación se aplica al identificador de organización (`imsOrg`) y afecta a todos los rangos de IP configurados para la zona protegida.

**Formato de API**

```http
DELETE /security/ip-access
```

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de los intervalos de IP eliminados.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```
