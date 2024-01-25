---
title: Punto final de API de conversión de esquema a plantilla CSV
description: El extremo /rpc/csv2schema de la API de Registro de esquemas le permite utilizar plantillas CSV para crear automáticamente esquemas XDM (Experience Data Model).
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 5%

---

# Punto final de API de conversión de esquema a plantilla CSV

El `/rpc/csv2schema` punto final en la [!DNL Schema Registry] API permite crear automáticamente un esquema del Modelo de datos de experiencia (XDM) utilizando un archivo CSV como plantilla. Con este punto de conexión, puede crear plantillas para importar campos de esquema por lotes y reducir el trabajo manual de la API o la IU.

## Introducción

El `/rpc/csv2schema` El punto final forma parte de la variable [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Adobe Experience Platform.

El `/rpc/csv2schema` El extremo forma parte de las llamadas a procedimientos remotos (RPC) compatibles con [!DNL Schema Registry]. A diferencia de otros extremos de [!DNL Schema Registry] API, los extremos RPC no requieren encabezados adicionales como `Accept` o `Content-Type`, y no use un `CONTAINER_ID`. En su lugar, deben utilizar la variable `/rpc` , como se muestra en las llamadas de API siguientes.

## Requisitos del archivo CSV

Para utilizar este punto de conexión, primero debe crear un archivo CSV con los encabezados de columna adecuados y los valores correspondientes. Algunas columnas son obligatorias, mientras que el resto son opcionales. En la tabla siguiente se describen estas columnas y su función en la construcción de esquemas.

| Posición del encabezado CSV | Nombre del encabezado CSV | Obligatorio/Opcional | Descripción |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Opcional | Cuando se incluye y se establece en `true`, indica que el campo no está listo para la carga de API y que se debe ignorar. |
| 2 | `isCustom` | Requerido | Indica si el campo es un campo personalizado o no. |
| 3 | `fieldGroupId` | Opcional | El ID del grupo de campos al que se debe asociar un campo personalizado. |
| 4 | `fieldGroupName` | (Ver descripción) | Nombre del grupo de campos al que se asocia este campo.<br><br>Opcional para campos personalizados que no amplían los campos estándar existentes. Si se deja en blanco, el sistema asignará automáticamente un nombre.<br><br>Necesario para campos estándar o campos personalizados que amplían los grupos de campos estándar, que se utiliza para consultar la variable `fieldGroupId`. |
| 5 | `fieldPath` | Requerido | Ruta de notación de puntos XED completa del campo. Para incluir todos los campos de un grupo de campos estándar (como se indica en `fieldGroupName`), establezca el valor en `ALL`. |
| 6 | `displayName` | Opcional | Título o nombre descriptivo para mostrar del campo. También puede ser un alias para el título, si existe. |
| 7 | `fieldDescription` | Opcional | Una descripción para el campo. También puede ser un alias para la descripción si existe. |
| 8 | `dataType` | (Ver descripción) | Indica el [tipo de datos básico](../schema/field-constraints.md#basic-types) para el campo. Necesario para todos los campos personalizados.<br><br>If `dataType` se establece en `object`, bien `properties` o `$ref` también debe definirse para la misma fila, pero no para ambas. |
| 9 | `isRequired` | Opcional | Indica si el campo es necesario para la ingesta de datos. |
| 10 | `isArray` | Opcional | Indica si el campo es una matriz de los indicados `dataType`. |
| 11 | `isIdentity` | Opcional | Indica si el campo es de identidad. |
| 12 | `identityNamespace` | Obligatorio si `isIdentity` is true | El [área de nombres de identidad](../../identity-service/features/namespaces.md) para el campo de identidad. |
| 13 | `isPrimaryIdentity` | Opcional | Indica si el campo es la identidad principal del esquema. |
| 14 | `minimum` | Opcional | (Solo para campos numéricos) El valor mínimo del campo. |
| 15 | `maximum` | Opcional | (Solo para campos numéricos) El valor máximo del campo. |
| 16 | `enum` | Opcional | Una lista de valores de enumeración para el campo, expresada como una matriz (por ejemplo, `[value1,value2,value3]`). |
| 17 | `stringPattern` | Opcional | (Solo para campos de cadena) Un patrón regex que el valor de cadena debe coincidir para pasar la validación durante la ingesta de datos. |
| 18 | `format` | Opcional | (Solo para campos de cadena) El formato del campo de cadena. |
| 19 | `minLength` | Opcional | (Solo para campos de cadena) La longitud mínima del campo de cadena. |
| 20 | `maxLength` | Opcional | (Solo para campos de cadena) La longitud máxima del campo de cadena. |
| 21 | `properties` | (Ver descripción) | Obligatorio si `dataType` se establece en `object` y `$ref` no está definida. Esto define el cuerpo del objeto como una cadena JSON (por ejemplo, `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (Ver descripción) | Obligatorio si `dataType` se establece en `object` y `properties` no está definida. Esto define la variable `$id` del objeto al que se hace referencia para el tipo de objeto (por ejemplo, `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | Opcional | Cuándo `isIgnored` se establece en `true`, esta columna se utiliza para proporcionar la información de encabezado del esquema. |

{style="table-layout:auto"}

Consulte lo siguiente [Plantilla CSV](../assets/sample-csv-template.csv) para determinar el formato que debe aplicarse al archivo CSV.

## Creación de una carga útil de exportación a partir de un archivo CSV

Una vez configurada la plantilla CSV, puede enviar el archivo al `/rpc/csv2schema` y convertirlo en una carga útil de exportación.

**Formato de API**

```http
POST /rpc/csv2schema
```

**Solicitud**

La carga útil de la solicitud debe utilizar datos de formulario como formato. A continuación, se muestran los campos de formulario requeridos.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| Propiedad | Descripción |
| --- | --- |
| `csv-file` | La ruta a la plantilla CSV almacenada en el equipo local. |
| `schema-class-id` | El `$id` del XDM [clase](../schema/composition.md#class) que este esquema empleará. |
| `schema-name` | Un nombre para mostrar para el esquema. |
| `schema-description` | Una descripción del esquema. |

**Respuesta**

Una respuesta correcta devuelve una carga útil de exportación generada a partir del archivo CSV. La carga útil adopta la forma de una matriz y cada elemento de matriz es un objeto que representa un componente XDM dependiente para el esquema. Seleccione la sección siguiente para ver un ejemplo completo de una carga útil de exportación generada a partir de un archivo CSV.

+++ Carga útil de respuesta de ejemplo

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## Importar la carga útil del esquema

Después de generar la carga útil de exportación desde el archivo CSV, puede enviar esa carga útil a `/rpc/import` extremo para generar el esquema.

Consulte la [guía de importar extremo](./import.md) para obtener más información sobre cómo generar esquemas a partir de cargas útiles de exportación.
