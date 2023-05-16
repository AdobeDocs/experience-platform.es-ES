---
description: Esta página trata el formato de mensaje y la transformación del perfil en los datos exportados de Adobe Experience Platform a los destinos.
title: Formato del mensaje
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---


# Formato del mensaje

## Requisitos previos - Conceptos de Adobe Experience Platform {#prerequisites}

Para comprender el formato de mensaje y la configuración de perfil y el proceso de transformación en el lado del Adobe, familiarícese con los siguientes conceptos de Experience Platform:

* **Modelo de datos de experiencia (XDM)**. [Información general de XDM](../../../../xdm/home.md) y  [Cómo crear un esquema XDM en Adobe Experience Platform](../../../../xdm/tutorials/create-schema-ui.md).
* **Clase**. [Crear y editar clases en la interfaz de usuario](../../../../xdm/ui/resources/classes.md).
* **Mapa de identidades**. El mapa de identidad representa un mapa de todas las identidades de los usuarios finales en Adobe Experience Platform. Consulte `xdm:identityMap` en el [Diccionario de campo XDM](../../../../xdm/schema/field-dictionary.md).
* **SegmentMembership**. La variable [segmentMembership](../../../../xdm/schema/field-dictionary.md) El atributo XDM informa de los segmentos a los que pertenece un perfil. Para los tres valores diferentes de la variable `status` , lea la documentación en [Grupo de campos de esquema Detalles de pertenencia a segmentos](../../../../xdm/field-groups/profile/segmentation.md).

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí (solo los pasos 1 y 2 del diagrama a continuación) |

## Información general {#overview}

Esta página trata el formato de mensaje y la transformación del perfil en los datos exportados de Adobe Experience Platform a los destinos.

Adobe Experience Platform exporta datos a un número significativo de destinos, en varios formatos de datos. Algunos ejemplos de tipos de destino son plataformas publicitarias (Google), redes sociales (Facebook) y ubicaciones de almacenamiento en la nube (Amazon S3, Azure Event Hubs).

El Experience Platform puede ajustar el formato de mensaje de los perfiles exportados para que coincidan con el formato esperado de su parte. Para comprender esta personalización, son importantes los siguientes conceptos:

* El esquema XDM de origen (1) y destino (2) en Adobe Experience Platform
* El formato de mensaje esperado en el lado del socio (3) y
* La capa de transformación entre el esquema XDM y el formato de mensaje esperado, que puede definir creando un [plantilla de transformación de mensaje](#using-templating).

![Transformación de esquema a JSON](../../assets/functionality/destination-server/transformations-3-steps.png)

El Experience Platform utiliza esquemas XDM para describir la estructura de los datos de una manera consistente y reutilizable.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Esquema XDM de origen (1)**: Este elemento hace referencia al esquema que utilizan los clientes en Experience Platform. En Experience Platform, en la variable [paso de asignación](../../../ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino, los clientes asignan campos desde su esquema XDM al esquema de destino del destino (2).

**Esquema XDM de Target (2)**: En función del esquema estándar JSON (3) del formato esperado de su destino y los atributos que su destino pueda interpretar, puede definir atributos e identidades de perfil en el esquema XDM de destino. Puede hacerlo en la configuración de destinos, en la [schemaConfig](../../functionality/destination-configuration/schema-configuration.md) y [identityNamespaces](../../functionality/destination-configuration/identity-namespace-configuration.md) objetos.

**Esquema estándar JSON de los atributos de perfil de destino (3)**: Este ejemplo representa un [esquema JSON](https://json-schema.org/learn/miscellaneous-examples.html) de todos los atributos de perfil que admite su plataforma y sus tipos (por ejemplo: objeto, cadena, matriz). Los campos de ejemplo con los que podría ser compatible su destino podrían ser `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`, etc. Necesita un [plantilla de transformación de mensaje](#using-templating) para adaptar los datos exportados fuera del Experience Platform al formato esperado.

Basándose en las transformaciones de esquema descritas anteriormente, así es como cambia una configuración de perfil entre el esquema XDM de origen y un esquema de muestra en el lado del socio:

![Ejemplo de mensaje de transformación](../../assets/functionality/destination-server/transformations-with-examples.png)

## Introducción: transformación de tres atributos básicos {#getting-started}

Para demostrar el proceso de transformación del perfil, el ejemplo siguiente utiliza tres atributos de perfil comunes en Adobe Experience Platform: **nombre**, **apellido** y **dirección de correo electrónico**.

>[!NOTE]
>
>El cliente asigna los atributos del esquema XDM de origen al esquema XDM de socio en la interfaz de usuario de Adobe Experience Platform, en la variable **Asignación** del [activar flujo de trabajo de destino](../../../ui/activate-segment-streaming-destinations.md#mapping).

Supongamos que su plataforma puede recibir un formato de mensaje como:

```shell
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

Teniendo en cuenta el formato de mensaje, las transformaciones correspondientes son las siguientes:

| Atributo en el esquema XDM del socio en el lado del Adobe | Transformación | Atributo en mensaje HTTP de su lado |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Estructura del perfil en el Experience Platform {#profile-structure}

Para comprender los ejemplos que se muestran más abajo en la página, es importante conocer la estructura de un perfil en Experience Platform.

Los perfiles tienen tres secciones:

* `segmentMembership` (siempre presente en un perfil)
   * esta sección contiene todos los segmentos que están presentes en el perfil. Los segmentos pueden tener uno de estos dos estados: `realized` o `exited`.
* `identityMap` (siempre presente en un perfil)
   * esta sección contiene todas las identidades presentes en el perfil (correo electrónico, Google GAID, Apple IDFA, etc.) y que el usuario asignó para exportar en el flujo de trabajo de activación.
* (en función de la configuración de destino, estos pueden estar presentes en el perfil). También hay una ligera diferencia entre los atributos predefinidos y los atributos de forma libre:
   * para *atributos de forma libre*, que contienen un `.value` ruta si el atributo está presente en el perfil (consulte la `lastName` del ejemplo 1). Si no están presentes en el perfil, no contendrán la variable `.value` ruta (consulte `firstName` del ejemplo 1).
   * para *atributos predefinidos*, no contienen un `.value` ruta. Todos los atributos asignados que están presentes en un perfil estarán presentes en el mapa de atributos. Los que no están presentes (consulte el Ejemplo 2 - la `firstName` no existe en el perfil).

Consulte a continuación dos ejemplos de perfiles en Experience Platform:

### Ejemplo 1 con `segmentMembership`, `identityMap` y atributos para atributos de forma libre {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "firstName": {
    },
    "lastName": {
      "value": "lastName"
    }
  }
}
```

### Ejemplo 2 con `segmentMembership`, `identityMap` y atributos para atributos predefinidos {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "lastName": "lastName"
  }
}
```

## Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a segmentos {#using-templating}

usos del Adobe [Plantillas pegables](https://pebbletemplates.io/), un idioma de plantilla similar a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), para transformar los campos del esquema XDM de Experience Platform en un formato compatible con el destino.

Esta sección proporciona varios ejemplos de cómo se realizan estas transformaciones: desde el esquema XDM de entrada, a través de la plantilla y la salida a formatos de carga útil aceptados por el destino. Los ejemplos siguientes se presentan con una complejidad creciente, como se indica a continuación:

1. Ejemplos de transformación simples. Aprenda cómo funciona la plantilla con transformaciones sencillas para [Atributos de perfil](#attributes), [Pertenencia a segmentos](#segment-membership)y [Identidad](#identities) campos.
2. Se han aumentado los ejemplos de complejidad de las plantillas que combinan los campos anteriores: [Crear una plantilla que envíe segmentos e identidades](./message-format.md#segments-and-identities) y [Cree una plantilla que envíe segmentos, identidades y atributos de perfil](#segments-identities-attributes).
3. Plantillas que incluyen la clave de agregación. Cuando utilice [agregación configurable](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) en la configuración de destino, el Experience Platform agrupa los perfiles exportados a su destino según criterios como ID de segmento, estado del segmento o áreas de nombres de identidad.

### Atributos de perfil {#attributes}

Para transformar los atributos de perfil exportados a su destino, consulte los ejemplos de código y JSON a continuación.

>[!IMPORTANT]
>
>Para obtener una lista de todos los atributos de perfil disponibles en Adobe Experience Platform, consulte la [Diccionario de campo XDM](../../../../xdm/schema/field-dictionary.md).


**Entrada**

Perfil 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

Perfil 2:

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**Plantilla**

>[!IMPORTANT]
>
>Para todas las plantillas que utilice, debe omitir los caracteres ilegales, como las comillas dobles `""` antes de insertar el [plantilla](../../functionality/destination-server/templating-specs.md) en el [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obtener más información sobre cómo escapar entre comillas dobles, consulte el capítulo 9 en la sección [JSON estándar](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### Inscripción a segmento {#segment-membership}

La variable [segmentMembership](../../../../xdm/schema/field-dictionary.md) El atributo XDM informa de los segmentos a los que pertenece un perfil.
Para los tres valores diferentes de la variable `status` , lea la documentación en [Grupo de campos de esquema Detalles de pertenencia a segmentos](../../../../xdm/field-groups/profile/segmentation.md).

**Entrada**

Perfil 1:

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

Perfil 2:

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "realized"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**Plantilla**

>[!IMPORTANT]
>
>Para todas las plantillas que utilice, debe omitir los caracteres ilegales, como las comillas dobles `""` antes de insertar el [plantilla](../../functionality/destination-server/templating-specs.md) en el [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obtener más información sobre cómo escapar entre comillas dobles, consulte el capítulo 9 en la sección [JSON estándar](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).


```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### Identidades {#identities}

Para obtener información sobre las identidades en el Experience Platform, consulte la [Información general del área de nombres de identidad](../../../../identity-service/namespaces.md).

**Entrada**

Perfil 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

Perfil 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**Plantilla**

>[!IMPORTANT]
>
>Para todas las plantillas que utilice, debe omitir los caracteres ilegales, como las comillas dobles `""` antes de insertar el [plantilla](../../functionality/destination-server/templating-specs.md) en el [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obtener más información sobre cómo escapar entre comillas dobles, consulte el capítulo 9 en la sección [JSON estándar](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```

### Crear una plantilla que envíe segmentos e identidades {#segments-and-identities}

Esta sección proporciona un ejemplo de una transformación utilizada comúnmente entre el esquema de Adobe XDM y el esquema de destino del socio.
El ejemplo siguiente muestra cómo transformar el formato de pertenencia e identidades de segmentos y mostrarlo en su destino.

**Entrada**

Perfil 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Perfil 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**Plantilla**

>[!IMPORTANT]
>
>Para todas las plantillas que utilice, debe omitir los caracteres ilegales, como las comillas dobles `""` antes de insertar el [plantilla](../../functionality/destination-server/templating-specs.md) en el [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obtener más información sobre cómo escapar entre comillas dobles, consulte el capítulo 9 en la sección [JSON estándar](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering segments by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**

La variable `json` a continuación, representa los datos exportados desde Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Cree una plantilla que envíe segmentos, identidades y atributos de perfil {#segments-identities-attributes}

Esta sección proporciona un ejemplo de una transformación utilizada comúnmente entre el esquema de Adobe XDM y el esquema de destino del socio.

Otro caso de uso común es la exportación de datos que contienen pertenencia a segmentos e identidades (por ejemplo: dirección de correo electrónico, número de teléfono, ID de publicidad) y atributos de perfil. Para exportar los datos de esta forma, consulte el ejemplo siguiente:

**Entrada**

Perfil 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Perfil 2:

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**Plantilla**

>[!IMPORTANT]
>
>Para todas las plantillas que utilice, debe omitir los caracteres ilegales, como las comillas dobles `""` antes de insertar el [plantilla](../../functionality/destination-server/templating-specs.md) en el [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obtener más información sobre cómo escapar entre comillas dobles, consulte el capítulo 9 en la sección [JSON estándar](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**Resultado**

La variable `json` a continuación, representa los datos exportados desde Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Incluya la clave de agregación en la plantilla para acceder a los perfiles exportados agrupados por varios criterios {#template-aggregation-key}

Cuando utilice [agregación configurable](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) en la configuración de destino, puede agrupar los perfiles exportados a su destino según criterios como ID de segmento, alias de segmento, pertenencia a segmentos o áreas de nombres de identidad.

En la plantilla de transformación de mensajes, puede acceder a las claves de agregación mencionadas anteriormente, como se muestra en los ejemplos de las secciones siguientes. Utilice las claves de agregación para estructurar el mensaje HTTP exportado fuera del Experience Platform de modo que coincida con el formato y los límites de velocidad esperados por el destino.

#### Utilizar la clave de agregación de ID de segmento en la plantilla {#aggregation-key-segment-id}

Si usa [agregación configurable](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) y establezca `includeSegmentId` como true, los perfiles de los mensajes HTTP exportados a su destino se agrupan por ID de segmento. Consulte a continuación cómo puede acceder al ID de segmento en la plantilla.

**Entrada**

Considere los cuatro perfiles siguientes, donde:

* los dos primeros forman parte del segmento con el ID de segmento `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* el tercer perfil forma parte del segmento con el ID de segmento `8f812592-3f06-416b-bd50-e7831848a31a`
* el cuarto perfil forma parte de los dos segmentos anteriores.

Perfil 1:

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Perfil 2:

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Perfil 3:

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         }
      }
   }
}
```

Perfil 4:

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

**Plantilla**

>[!IMPORTANT]
>
>Para todas las plantillas que utilice, debe omitir los caracteres ilegales, como las comillas dobles `""` antes de insertar el [plantilla](../../functionality/destination-server/templating-specs.md) en el [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obtener más información sobre cómo escapar entre comillas dobles, consulte el capítulo 9 en la sección [JSON estándar](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Aviso a continuación: `audienceId` se utiliza en la plantilla para acceder a los ID de segmento. Este ejemplo asume que se utiliza `audienceId` para la pertenencia a segmentos en su taxonomía de destino. En su lugar, puede utilizar cualquier otro nombre de campo, según su propia taxonomía.

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultado**

Cuando se exportan a su destino, los perfiles se dividen en dos grupos, según su ID de segmento.

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione"
      },
      {
         "firstName":"Harry"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

#### Utilizar la clave de agregación de alias de segmento en la plantilla {#aggregation-key-segment-alias}

Si usa [agregación configurable](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) y establezca `includeSegmentId` como true, también puede acceder al alias del segmento en la plantilla.

Añada la línea siguiente a la plantilla para acceder a los perfiles exportados agrupados por alias de segmento.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Utilizar la clave de agregación del estado del segmento en la plantilla {#aggregation-key-segment-status}

Si usa [agregación configurable](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) y establezca `includeSegmentId` y `includeSegmentStatus` como true, puede acceder al estado del segmento en la plantilla. De este modo, puede agrupar perfiles en los mensajes HTTP exportados a su destino en función de si se deben añadir o eliminar perfiles de segmentos.

Los valores posibles son:

* realizado
* existente
* exitado

Añada la línea siguiente a la plantilla para añadir o eliminar perfiles de segmentos, según los valores anteriores:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Utilizar la clave de agregación del área de nombres de identidad en la plantilla {#aggregation-key-identity}

A continuación se muestra un ejemplo en el que la variable [agregación configurable](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) en la configuración de destino se configura para agregar perfiles exportados por áreas de nombres de identidad, en el formulario `"namespaces": ["email", "phone"]` y `"namespaces": ["GAID", "IDFA"]`. Consulte la `groups` en el [crear configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md) documentación para obtener más información sobre la agrupación.

**Entrada**

Perfil 1:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ],
      "IDFA":[
         {
            "id":"AEBE52E7-03EE-455A-B3C4-E57283966239"
         }
      ],
      "GAID":[
         {
            "id":"e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         }
      ]
   }
}
```

Perfil 2:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ],
      "IDFA":[
         {
            "id":"134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         }
      ],
      "GAID":[
         {
            "id":"47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         }
      ]
   }
}
```

**Plantilla**

>[!IMPORTANT]
>
>Para todas las plantillas que utilice, debe omitir los caracteres ilegales, como las comillas dobles `""` antes de insertar el [plantilla](../../functionality/destination-server/templating-specs.md) en el [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Para obtener más información sobre cómo escapar entre comillas dobles, consulte el capítulo 9 en la sección [JSON estándar](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Observe que `input.aggregationKey.identityNamespaces` se utiliza en la plantilla siguiente

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**Resultado**

Cuando se exportan al destino, los perfiles se dividen en dos grupos, según sus áreas de nombres de identidad. El correo electrónico y el teléfono están en un grupo, mientras que GAID y IDFA están en otro.

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

```json
{
   "profiles":[
      {
         "IDFA":[
            "AEBE52E7-03EE-455A-B3C4-E57283966239"
         ],
         "GAID":[
            "e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         ]
      },
      {
         "IDFA":[
            "134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         ],
         "GAID":[
            "47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         ]
      }
   ]
}
```

#### Utilizar la clave de agregación en una plantilla de URL {#aggregation-key-url-template}

Según el caso de uso, también puede utilizar las claves de agregación que se describen aquí en una URL, como se muestra a continuación:

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Referencia: Contexto y funciones utilizadas en las plantillas de transformación {#reference}

El contexto proporcionado a la plantilla contiene `input`  (los perfiles o datos que se exportan en esta llamada) y `destination` (datos sobre el destino al que envía los datos ese Adobe, válidos para todos los perfiles).

En la tabla siguiente se describen las funciones de los ejemplos anteriores.

| Función | Descripción |
|---------|----------|
| `input.profile` | El perfil, representado como un [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Sigue el esquema XDM de socio mencionado anteriormente en esta página. |
| `destination.segmentAliases` | Asigne ID de segmentos en el espacio de nombres de Adobe Experience Platform para segmentar alias en el sistema del socio. |
| `destination.segmentNames` | Asigne nombres de segmento en el espacio de nombres de Adobe Experience Platform a nombres de segmento en el sistema del socio. |
| `addedSegments(listOfSegments)` | Devuelve solo los segmentos que tienen estado `realized`. |
| `removedSegments(listOfSegments)` | Devuelve solo los segmentos que tienen estado `exited`. |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo se transforman los datos exportados fuera del Experience Platform. A continuación, lea las páginas siguientes para completar sus conocimientos sobre la creación de plantillas de transformación de mensajes para su destino:

* [Creación y prueba de una plantilla de transformación de mensaje](../../testing-api/streaming-destinations/create-template.md)
* [Operaciones de API de plantilla de procesamiento](../../testing-api/streaming-destinations/render-template-api.md)
* [Funciones de transformación admitidas en el Destination SDK](../destination-server/supported-functions.md)

Para obtener más información sobre los otros componentes del servidor de destino, consulte los siguientes artículos:

* [Especificaciones del servidor para los destinos creados con el Destination SDK](server-specs.md)
* [Plantillas de especificaciones](templating-specs.md)
* [Configuración de formato de archivo](file-formatting.md)