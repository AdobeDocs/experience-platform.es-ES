---
solution: Experience Platform
title: Exportar esquemas XDM en la interfaz de usuario
description: Obtenga información sobre cómo exportar un esquema existente a un simulador para pruebas o una organización IMS diferente en la interfaz de usuario de Adobe Experience Platform.
topic-legacy: user guide
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Exportar esquemas XDM en la interfaz de usuario

Todos los recursos de la biblioteca de esquemas están contenidos en un simulador de pruebas específico de una organización de IMS. En algunos casos, es posible que desee compartir recursos del Modelo de datos de experiencia (XDM) entre entornos limitados y organizaciones IMS.

Para satisfacer esta necesidad, el espacio de trabajo [!UICONTROL Schemas] en la interfaz de usuario de Adobe Experience Platform le permite generar una carga útil de exportación para cualquier esquema dentro de la biblioteca de esquemas. Esta carga útil se puede utilizar en una llamada a la API del Registro de esquemas para importar el esquema (y todos los recursos dependientes) en un entorno limitado de destino y en una organización de IMS.

>[!NOTE]
>
>También puede utilizar la API del Registro de esquemas para exportar otros recursos además de esquemas, como clases, grupos de campos de esquema y tipos de datos. Consulte la guía de [export/import endpoints](../api/export-import.md) para obtener más información.

## Requisitos previos

Aunque la interfaz de usuario de Platform le permite exportar recursos XDM, debe utilizar la API del Registro de esquemas para importar esos recursos en otros entornos limitados u organizaciones IMS para completar el flujo de trabajo. Consulte la guía [Introducción a la API del Registro de esquemas](../api/getting-started.md) para obtener información importante sobre los encabezados de autenticación necesarios antes de seguir esta guía.

## Generar una carga útil de exportación

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Schemas]** en el panel de navegación izquierdo. Dentro del espacio de trabajo [!UICONTROL Schemas], busque el esquema que desea exportar y ábralo en [!DNL Schema Editor].

>[!TIP]
>
>Consulte la guía sobre [exploración de recursos XDM](./explore.md) para obtener más información sobre cómo encontrar el recurso XDM que está buscando.

Una vez que haya abierto el esquema, seleccione el icono **[!UICONTROL Copy JSON]** (![Copiar icono](../images/ui/export/icon.png)) en la parte superior derecha del lienzo.

![](../images/ui/export/copy-json.png)

Esto copia una carga útil JSON en el portapapeles, generada según la estructura del esquema. Para el esquema &quot;[!DNL Loyalty Members]&quot; mostrado arriba, se genera el siguiente JSON:

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/fieldgroups/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.fieldgroups.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "fieldgroups",
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
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/fieldgroups/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/fieldgroups/profile-consents",
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
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/fieldgroups/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/fieldgroups/profile-consents"
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

La carga útil adopta la forma de una matriz, y cada elemento de matriz es un objeto que representa un recurso XDM personalizado que se va a exportar. En el ejemplo anterior, se incluyen el grupo de campos personalizados &quot;[!DNL Loyalty details]&quot; y el esquema &quot;[!DNL Loyalty Members]&quot;. Los recursos principales empleados por el esquema no se incluyen en la exportación, ya que estos recursos están disponibles en todos los entornos limitados y en las organizaciones de IMS.

Tenga en cuenta que cada instancia del ID de inquilino de su organización aparece como `<XDM_TENANTID_PLACEHOLDER>` en la carga útil. Estos marcadores de posición se sustituirán automáticamente por el valor de ID de inquilino correspondiente, según el lugar de importación del esquema en el paso siguiente.

## Importación del recurso mediante la API

Una vez copiado el JSON de exportación para el esquema, puede utilizarlo como carga útil para una solicitud de POST al extremo `/import` en la API del Registro de esquemas. Consulte la sección sobre [importación de un recurso XDM en la API](../api/export-import.md#import) para obtener más información sobre cómo configurar la llamada para enviar el esquema a la organización y el entorno limitado de IMS deseados.

## Pasos siguientes

Al seguir esta guía, ha exportado correctamente un esquema XDM a una organización o simulador de pruebas IMS diferente. Para obtener más información sobre las capacidades de la [!UICONTROL Schemas] interfaz de usuario, consulte la [[!UICONTROL Schemas] información general de la interfaz de usuario](./overview.md).
