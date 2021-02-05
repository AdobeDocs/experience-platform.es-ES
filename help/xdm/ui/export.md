---
solution: Experience Platform
title: Exportación de Esquemas XDM en la interfaz de usuario
description: Obtenga información sobre cómo exportar un esquema existente a un entorno limitado diferente o a una organización de IMS en la interfaz de usuario de Adobe Experience Platform.
topic: user guide
type: Tutorial
translation-type: tm+mt
source-git-commit: 2d6e833db7cd79135e6da4c68c9dca8cbed09ce4
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Exportación de esquemas XDM en la interfaz de usuario

Todos los recursos de la biblioteca de Esquemas están contenidos en un entorno limitado específico de una organización de IMS. En algunos casos, es posible que desee compartir recursos del Modelo de datos de experiencia (XDM) entre entornos limitados y organizaciones IMS.

Para satisfacer esta necesidad, el espacio de trabajo [!UICONTROL Esquemas] de la interfaz de usuario de Adobe Experience Platform le permite generar una carga útil de exportación para cualquier esquema de la biblioteca de Esquemas. Esta carga útil se puede utilizar en una llamada a la API del Registro de Esquema para importar el esquema (y todos los recursos dependientes) en un entorno limitado de destinatario y en una organización de IMS.

>[!NOTE]
>
>También puede utilizar la API del Registro de Esquema para exportar otros recursos además de esquemas, como clases, mezclas y tipos de datos. Consulte la guía de los [extremos de exportación e importación](../api/export-import.md) para obtener más información.

## Requisitos previos

Aunque la interfaz de usuario de la plataforma le permite exportar recursos XDM, debe utilizar la API del Registro de Esquema para importar esos recursos en otros entornos limitados u organizaciones IMS para completar el flujo de trabajo. Consulte la guía [Introducción a la API del Registro de Esquema](../api/getting-started.md) para obtener información importante sobre los encabezados de autenticación requeridos antes de seguir esta guía.

## Generar una carga útil de exportación

En la interfaz de usuario de la plataforma, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. Dentro del espacio de trabajo [!UICONTROL Esquemas], localice el esquema que desea exportar y ábralo en [!DNL Schema Editor].

>[!TIP]
>
>Consulte la guía sobre [exploración de recursos XDM](./explore.md) para obtener detalles sobre cómo encontrar el recurso XDM que está buscando.

Una vez abierto el esquema, seleccione el icono **[!UICONTROL Copiar JSON]** (![Copiar icono](../images/ui/export/icon.png)) en la parte superior derecha del lienzo.

![](../images/ui/export/copy-json.png)

Esto copia una carga útil JSON en el portapapeles, generada en función de la estructura de esquema. Para el esquema &quot;[!DNL Loyalty Members]&quot; mostrado arriba, se genera el siguiente JSON:

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

La carga útil adopta la forma de una matriz, y cada elemento de la matriz es un objeto que representa un recurso XDM personalizado que se va a exportar. En el ejemplo anterior, se incluyen la mezcla personalizada &quot;[!DNL Loyalty details]&quot; y el esquema &quot;[!DNL Loyalty Members]&quot;. Los recursos básicos empleados por el esquema no se incluyen en la exportación, ya que estos recursos están disponibles en todos los entornos limitados y en todas las organizaciones de IMS.

Tenga en cuenta que cada instancia del ID de inquilino de su organización aparece como `<XDM_TENANTID_PLACEHOLDER>` en la carga útil. Estos marcadores de posición se reemplazarán automáticamente con el valor de ID de inquilino correspondiente, según el lugar donde se exporte el esquema en el paso siguiente.

## Importar el recurso mediante la API

Una vez copiado el JSON de exportación para el esquema, puede utilizarlo como carga útil para una solicitud de POST al extremo `/import` de la API del Registro de Esquema. Consulte la sección sobre [importación de un recurso XDM en la API](../api/export-import.md#import) para obtener más información sobre cómo configurar la llamada para enviar el esquema a la organización y el entorno limitado de IMS correctos.

## Pasos siguientes

Siguiendo esta guía, se ha exportado correctamente un esquema XDM a una organización IMS o un simulador de pruebas diferentes. Para obtener más información sobre las funciones de la interfaz de usuario [!UICONTROL Esquemas], consulte la [[!UICONTROL información general de la interfaz de usuario de ] Esquemas](./overview.md).