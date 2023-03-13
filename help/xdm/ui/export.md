---
solution: Experience Platform
title: Exportación de esquemas XDM en la IU
description: Obtenga información sobre cómo exportar un esquema existente a una zona protegida u organización de IMS diferente en la interfaz de usuario de Adobe Experience Platform.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Exportación de esquemas XDM en la IU

Todos los recursos de la biblioteca de esquemas están en una zona protegida específica de una organización de IMS. En algunos casos, es posible que desee compartir recursos del Modelo de datos de experiencia (XDM) entre entornos limitados y organizaciones IMS.

Para resolver esta necesidad, la variable [!UICONTROL Esquemas] El espacio de trabajo de en la IU de Adobe Experience Platform permite generar una carga útil de exportación para cualquier esquema de en la Biblioteca de esquemas. Esta carga útil se puede utilizar en una llamada a la API de Registro de esquemas para importar el esquema (y todos los recursos dependientes) en una zona protegida de destino y una organización de IMS.

>[!NOTE]
>
>También puede utilizar la API de Registro de esquemas para exportar otros recursos además de esquemas, incluidas clases, grupos de campos de esquema y tipos de datos. Consulte la [guía de extremo de exportación](../api/export.md) para obtener más información.

## Requisitos previos

Aunque la IU de Platform le permite exportar recursos XDM, debe utilizar la API de Registro de esquemas para importar esos recursos en otras zonas protegidas u organizaciones IMS para completar el flujo de trabajo. Consulte la guía de [Introducción a la API de Registro de esquemas](../api/getting-started.md) para obtener información importante acerca de los encabezados de autenticación necesarios antes de seguir esta guía.

## Generación de una carga útil de exportación

En la IU de Platform, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. Dentro de [!UICONTROL Esquemas] espacio de trabajo, busque el esquema que desea exportar y ábralo en [!DNL Schema Editor].

>[!TIP]
>
>Consulte la guía de [exploración de recursos XDM](./explore.md) para obtener más información sobre cómo encontrar el recurso XDM que está buscando.

Una vez abierto el esquema, seleccione la opción **[!UICONTROL Copiar JSON]** icono (![Icono Copiar](../images/ui/export/icon.png)), en la parte superior derecha del lienzo.

![](../images/ui/export/copy-json.png)

Esto copia una carga útil JSON en el portapapeles, generada en función de la estructura de esquema. Para el &quot;[!DNL Loyalty Members]&quot; como se muestra arriba, se genera el siguiente JSON:

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "enum": [
                      "platinum",
                      "gold",
                      "silver",
                      "bronze"
                    ],
                    "meta:enum": {
                      "platinum": "Platinum",
                      "gold": "Gold",
                      "silver": "Silver",
                      "bronze": "Bronze"
                    },
                    "meta:xdmType": "string"
                  }
                },
                "meta:xdmType": "object"
              }
            },
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

La carga útil adopta la forma de una matriz, y cada elemento de matriz es un objeto que representa un recurso XDM personalizado que se va a exportar. En el ejemplo anterior, la variable &quot;[!DNL Loyalty details]&quot; grupo de campos personalizados y &quot;[!DNL Loyalty Members]Se incluyen los esquemas &quot;. Los recursos principales empleados por el esquema no se incluyen en la exportación, ya que estos recursos están disponibles en todas las zonas protegidas y organizaciones de IMS.

Tenga en cuenta que cada instancia del ID de inquilino de su organización aparece como `<XDM_TENANTID_PLACEHOLDER>` en la carga útil. Estos marcadores de posición se reemplazarán automáticamente con el valor de ID de inquilino adecuado según dónde importe el esquema en el siguiente paso.

## Importe el recurso mediante la API

Una vez copiado el JSON de exportación para el esquema, puede utilizarlo como carga útil para una solicitud de POST a `/rpc/import` en la API de Registro de esquemas. Consulte la [guía de importar extremo](../api/import.md) para obtener más información sobre cómo configurar la llamada para enviar el esquema a la organización de IMS y a la zona protegida deseados.

## Pasos siguientes

Al seguir esta guía, ha exportado correctamente un esquema XDM a una organización de IMS o zona protegida diferente. Para obtener más información sobre las capacidades de [!UICONTROL Esquemas] IU, consulte la [[!UICONTROL Esquemas] Información general de IU](./overview.md).
