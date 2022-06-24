---
title: Plantilla CSV a extremo de la API de conversión de esquema
description: El extremo /rpc/csv2schema de la API del Registro de esquemas permite utilizar plantillas CSV para crear automáticamente esquemas del Modelo de datos de experiencias (XDM).
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: b4c186c8c40d1372fb5011f49979523e1201fb0b
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 6%

---

# Plantilla CSV a extremo de la API de conversión de esquema

La variable `/rpc/csv2schema` en la variable [!DNL Schema Registry] La API le permite crear automáticamente un esquema del Modelo de datos de experiencia (XDM) con un archivo CSV como plantilla. Con este extremo, puede crear plantillas para importar de forma masiva campos de esquema y reducir el trabajo manual de API o IU.

## Primeros pasos

La variable `/rpc/csv2schema` es parte de la variable [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Adobe Experience Platform.

La variable `/rpc/csv2schema` el extremo es parte de las llamadas a procedimientos remotos (RPC) que son compatibles con la variable [!DNL Schema Registry]. A diferencia de otros extremos en la variable [!DNL Schema Registry] Los extremos de API y RPC no requieren encabezados adicionales como `Accept` o `Content-Type`y no use un `CONTAINER_ID`. En su lugar, deben usar la variable `/rpc` como se muestra en las llamadas de API a continuación.

## Requisitos de archivo CSV

Para utilizar este extremo, primero debe crear un archivo CSV con los encabezados de columna adecuados y los valores correspondientes. Algunas columnas son obligatorias, mientras que el resto son opcionales. En la tabla siguiente se describen estas columnas y su función en la construcción del esquema.

| Posición del encabezado CSV | Nombre del encabezado CSV | Obligatorio/Opcional | Descripción |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Opcional | Cuando se incluye y se establece en `true`, indica que el campo no está listo para la carga de la API y debe ignorarse. |
| 2 | `isCustom` | Requerido | Indica si el campo es un campo personalizado o no. |
| 3 | `fieldGroupId` | Opcional | Se debe asociar el ID del grupo de campos a un campo personalizado. |
| 4 | `fieldGroupName` | (Consulte la descripción) | Nombre del grupo de campos al que se va a asociar este campo.<br><br>Opcional para campos personalizados que no amplíen los campos estándar existentes. Si se deja en blanco, el sistema asignará automáticamente el nombre.<br><br>Necesario para campos estándar o campos personalizados que amplían grupos de campos estándar, que se utilizan para consultar la variable `fieldGroupId`. |
| 5 | `fieldPath` | Requerido | Ruta de notación de puntos XED completa para el campo. Para incluir todos los campos de un grupo de campos estándar (como se indica en `fieldGroupName`), establezca el valor en `ALL`. |
| 6 | `displayName` | Opcional | Título o nombre descriptivo del campo. También puede ser un alias para el título si existe uno. |
| 7 | `fieldDescription` | Opcional | Descripción del campo. También puede ser un alias para la descripción si existe uno. |
| 8 | `dataType` | (Consulte la descripción) | Indica la variable [tipo de datos básico](../schema/field-constraints.md#basic-types) para el campo . Necesario para todos los campos personalizados.<br><br>If `dataType` está configurado como `object`, ya sea `properties` o `$ref` también debe definirse para la misma fila, pero no para ambas. |
| 9 | `isRequired` | Opcional | Indica si el campo es necesario para la ingesta de datos. |
| 10 | `isArray` | Opcional | Indica si el campo es una matriz de sus indicadas `dataType`. |
| 11 | `isIdentity` | Opcional | Indica si el campo es de identidad. |
| 12 | `identityNamespace` | Requerido si `isIdentity` es verdadero | La variable [área de nombres de identidad](../../identity-service/namespaces.md) para el campo de identidad. |
| 13 | `isPrimaryIdentity` | Opcional | Indica si el campo es la identidad principal del esquema. |
| 14 | `minimum` | Opcional | (Solo para campos numéricos) El valor mínimo del campo. |
| 15 | `maximum` | Opcional | (Solo para campos numéricos) El valor máximo del campo. |
| 16 | `enum` | Opcional | Una lista de valores de enumeración para el campo, expresados como una matriz (por ejemplo, `[value1,value2,value3]`). |
| 17 | `stringPattern` | Opcional | (Solo para campos de cadena) Un patrón regex que el valor de cadena debe coincidir para pasar la validación durante el consumo de datos. |
| 18 | `format` | Opcional | (Solo para campos de cadena) El formato del campo de cadena. |
| 19 | `minLength` | Opcional | (Solo para campos de cadena) La longitud mínima del campo de cadena. |
| 20 | `maxLength` | Opcional | (Solo para campos de cadena) La longitud máxima del campo de cadena. |
| 21 | `properties` | (Consulte la descripción) | Requerido si `dataType` está configurado como `object` y `$ref` no está definida. Esto define el cuerpo del objeto como una cadena JSON (p. ej. `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (Consulte la descripción) | Requerido si `dataType` está configurado como `object` y `properties` no está definida. Define el `$id` del objeto al que se hace referencia para el tipo de objeto (p. ej. `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | Opcional | When `isIgnored` está configurado como `true`, esta columna se utiliza para proporcionar la información de encabezado del esquema. |

{style=&quot;table-layout:auto&quot;}

Consulte lo siguiente [Plantilla CSV](../assets/sample-csv-template.csv) para determinar cómo debe formatearse el archivo CSV.

## Creación de una carga útil de exportación a partir de un archivo CSV

Una vez configurada la plantilla CSV, puede enviar el archivo a la `/rpc/csv2schema` y conviértala en una carga útil de exportación.

**Formato de API**

```http
POST /rpc/csv2schema
```

**Solicitud**

La carga útil de la solicitud debe utilizar los datos del formulario como su formato. A continuación se muestran los campos de formulario necesarios.

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
| `schema-class-id` | La variable `$id` del XDM [class](../schema/composition.md#class) que empleará este esquema. |
| `schema-name` | Un nombre para mostrar para el esquema. |
| `schema-description` | Descripción del esquema. |

**Respuesta**

Una respuesta correcta devuelve una carga útil de exportación generada a partir del archivo CSV. La carga útil toma una forma de matriz y cada elemento de matriz es un objeto que representa un componente XDM dependiente para el esquema. Seleccione la sección siguiente para ver un ejemplo completo de una carga útil de exportación generada a partir de un archivo CSV.

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

## Importación de la carga útil de esquema

Después de generar la carga útil de exportación desde el archivo CSV, puede enviar esa carga útil a la variable `/rpc/import` para generar el esquema.

Consulte la [guía de extremo de importación](./import.md) para obtener más información sobre cómo generar esquemas a partir de cargas de exportación.
