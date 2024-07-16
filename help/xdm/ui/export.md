---
solution: Experience Platform
title: Exportación de esquemas XDM en la IU
description: Obtenga información sobre cómo exportar un esquema existente a una zona protegida u organización diferente en la interfaz de usuario de Adobe Experience Platform.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: 0f0842c1d14ce42453b09bf97e1f3690448f6e9a
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 11%

---

# Exportación de esquemas XDM en la IU {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="Copiar estructura JSON"
>abstract="Genere una carga útil de exportación para el esquema elegido copiando la estructura JSON en el portapapeles. Utilice esta función para exportar los detalles de cualquier esquema de la biblioteca de esquemas. Este JSON exportado puede utilizarse para importar el esquema y cualquier recurso relacionado en una zona protegida u organización distinta. Esto hace que compartir y reutilizar esquemas entre diferentes entornos sea sencillo y eficaz."

Todos los recursos de la biblioteca de esquemas están contenidos en una zona protegida específica de una organización. En algunos casos, es posible que desee compartir recursos del Modelo de datos de experiencia (XDM) entre entornos limitados y organizaciones.

Para resolver esta necesidad, el área de trabajo [!UICONTROL Schemas] de la interfaz de usuario de Adobe Experience Platform le permite generar una carga útil de exportación para cualquier esquema de la biblioteca de esquemas. Esta carga útil se puede utilizar en una llamada a la API de Registro de esquemas para importar el esquema (y todos los recursos dependientes) en una organización y zona protegida de destino.

>[!NOTE]
>
>También puede utilizar la API de Registro de esquemas para exportar otros recursos además de esquemas, incluidas clases, grupos de campos de esquema y tipos de datos. Consulte la [guía de extremo de exportación](../api/export.md) para obtener más información.

## Requisitos previos

Aunque la IU de Platform le permite exportar recursos XDM, debe utilizar la API de Registro de esquemas para importar esos recursos en otras zonas protegidas u organizaciones para completar el flujo de trabajo. Consulte la guía sobre [introducción a la API de Registro de esquemas](../api/getting-started.md) para obtener información importante sobre los encabezados de autenticación requeridos antes de seguir esta guía.

## Generación de una carga útil de exportación {#generate-export-payload}

Las cargas útiles de exportación se pueden generar en la interfaz de usuario de Platform desde el panel de detalles de la pestaña [!UICONTROL Examinar] o directamente desde el lienzo del esquema en el Editor de esquemas.

Para generar una carga útil de exportación, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. En el área de trabajo [!UICONTROL Esquemas], seleccione la fila del esquema que desea exportar para mostrar los detalles del esquema en la barra lateral derecha.

>[!TIP]
>
>Consulte la guía [Exploración de recursos XDM](./explore.md) para obtener más información sobre cómo encontrar el recurso XDM que está buscando.

A continuación, seleccione el icono **[!UICONTROL Copiar JSON]** (![Copiar icono](../images/ui/export/icon.png)) de las opciones disponibles.

![Se resaltó el área de trabajo de esquemas con una fila de esquema y [!UICONTROL Copiar a JSON].](../images/ui/export/copy-json.png)

Esto copia una carga útil JSON en el portapapeles, generada en función de la estructura de esquema. Para el esquema &quot;[!DNL Loyalty Members]&quot; mostrado arriba, se genera el siguiente JSON:

+++Seleccione para ampliar una carga útil JSON de ejemplo

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

+++

La carga útil también se puede copiar seleccionando [!UICONTROL Más] en la parte superior derecha del Editor de esquemas. Un menú desplegable proporciona dos opciones: [!UICONTROL Copiar estructura JSON] y [!UICONTROL Eliminar esquema].

>[!NOTE]
>
>Un esquema no se puede eliminar cuando está habilitado para el perfil o tiene conjuntos de datos asociados.

![Se ha resaltado el editor de esquemas con [!UICONTROL Más] y [!UICONTROL Copiar a JSON].](../images/ui/export/schema-editor-copy-json.png)

La carga útil adopta la forma de una matriz, y cada elemento de matriz es un objeto que representa un recurso XDM personalizado que se va a exportar. En el ejemplo anterior, se incluyen el grupo de campos personalizados [!DNL Loyalty details] y el esquema [!DNL Loyalty Members]. Los recursos principales empleados por el esquema no se incluyen en la exportación, ya que estos recursos están disponibles en todas las zonas protegidas y organizaciones.

Tenga en cuenta que cada instancia del ID de inquilino de su organización aparece como `<XDM_TENANTID_PLACEHOLDER>` en la carga útil. Estos marcadores de posición se reemplazarán automáticamente con el valor de ID de inquilino adecuado según dónde importe el esquema en el siguiente paso.

## Importe el recurso mediante la API {#import-resource-with-api}

Una vez que haya copiado el JSON de exportación para el esquema, puede utilizarlo como carga para una solicitud de POST al extremo `/rpc/import` en la API de Registro de esquemas. Consulte la [guía de extremo de importación](../api/import.md) para obtener detalles sobre cómo configurar la llamada para enviar el esquema a la organización y zona protegida deseadas.

## Pasos siguientes

Al seguir esta guía, ha exportado correctamente un esquema XDM a una organización o zona protegida diferente. Para obtener más información sobre las capacidades de la interfaz de usuario de [!UICONTROL Schemas], consulte la descripción general de la interfaz de usuario de [[!UICONTROL Schemas]](./overview.md).
