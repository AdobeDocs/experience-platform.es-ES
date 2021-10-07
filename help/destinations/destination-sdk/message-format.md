---
description: Utilice el contenido de esta página junto con el resto de las opciones de configuración para los destinos de socio. Esta página trata el formato de mensajería de los datos exportados desde Adobe Experience Platform a los destinos, mientras que la otra página trata aspectos específicos sobre cómo conectar y autenticarse en el destino.
seo-description: Use the content on this page together with the rest of the configuration options for partner destinations. This page addresses the messaging format of data exported from Adobe Experience Platform to destinations, while the other page addresses specifics about connecting and authenticating to your destination.
seo-title: Message format
title: Formato del mensaje
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: c328293cf710ad8a2ddd2e52cb01c86d29c0b569
workflow-type: tm+mt
source-wordcount: '1995'
ht-degree: 2%

---

# Formato del mensaje

## Requisitos previos - Conceptos de Adobe Experience Platform {#prerequisites}

Para comprender el proceso en el lado del Adobe, familiarícese con los siguientes conceptos de Experience Platform:

* **Modelo de datos de experiencia (XDM)**. [Información general ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es) de XDM y   [Cómo crear un esquema de XDM en Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **Clase**. [Cree y edite clases en la interfaz de usuario](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **Mapa de identidades**. El mapa de identidad representa un mapa de todas las identidades de los usuarios finales en Adobe Experience Platform. Consulte `xdm:identityMap` en el [diccionario del campo XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. El atributo [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM informa de los segmentos a los que pertenece un perfil. Para los tres valores diferentes del campo `status`, lea la documentación del grupo de campos [Segment Membership Details schema group](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Información general {#overview}

Utilice el contenido de esta página junto con el resto de las [opciones de configuración para destinos de socio](./configuration-options.md). Esta página trata el formato de mensajería de los datos exportados desde Adobe Experience Platform a los destinos, mientras que la otra página trata aspectos específicos sobre cómo conectar y autenticarse en el destino.

Adobe Experience Platform exporta datos a un número significativo de destinos, en varios formatos de datos. Algunos ejemplos de tipos de destino son plataformas publicitarias (Google), redes sociales (Facebook), ubicaciones de almacenamiento en la nube (Amazon S3, centros de eventos de Azure).

El Experience Platform puede ajustar el formato de mensaje exportado para que coincida con el formato esperado de su parte. Para comprender esta personalización, son importantes los siguientes conceptos:
* El esquema XDM de origen (1) y destino (2) en Adobe Experience Platform
* El formato de mensaje esperado en el lado del socio (3) y
* La capa de transformación entre el esquema XDM y el formato de mensaje esperado, que puede definir creando una [plantilla de transformación de mensaje](./message-format.md#using-templating).

![Transformación de esquema a JSON](./assets/transformations-3-steps.png)

El Experience Platform utiliza esquemas XDM para describir la estructura de los datos de una manera consistente y reutilizable.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Esquema XDM de origen (1)**: Este elemento hace referencia al esquema que utilizan los clientes en Experience Platform. En Experience Platform, en el [paso de asignación](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) del flujo de trabajo de activación de destino, los clientes asignarían campos desde su esquema de origen al esquema de destino del destino (2).

**Esquema XDM de Target (2)**: En función del esquema estándar JSON (3) del formato esperado del destino, puede definir atributos e identidades de perfil en el esquema XDM de destino. Puede hacerlo en la configuración de destinos, en los objetos [schemaConfig](./destination-configuration.md#schema-configuration) y [identityNamespaces](./destination-configuration.md#identities-and-attributes).

**Esquema estándar JSON de los atributos de perfil de destino (3)**: Este elemento representa un  [esquema ](https://json-schema.org/learn/miscellaneous-examples.html) JSON de todos los atributos de perfil que admite su plataforma y sus tipos (por ejemplo: objeto, cadena, matriz). Los campos de ejemplo que su destino podría admitir son `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`, etc. Necesita una [plantilla de transformación de mensajes](./message-format.md#using-templating) para adaptar los datos exportados fuera del Experience Platform al formato esperado.

Basándose en las transformaciones de esquema descritas anteriormente, así es como cambia la estructura de un mensaje entre el esquema XDM de origen y un esquema de muestra en el lado del socio:

![Ejemplo de mensaje de transformación](./assets/transformations-with-examples.png)

<br> 


## Introducción: transformación de tres atributos básicos {#getting-started}

Para demostrar el proceso de transformación, el ejemplo siguiente utiliza tres atributos de perfil comunes en Adobe Experience Platform: **nombre**, **apellidos** y **dirección de correo electrónico**.

>[!NOTE]
>
>El cliente asigna los atributos del esquema XDM de origen al esquema XDM de socio en la interfaz de usuario de Adobe Experience Platform, en el paso **Mapping** del [activate destination workflow](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

Supongamos que su plataforma puede recibir un formato de mensaje como:

```curl
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

## Uso de un idioma de plantilla para las transformaciones de identidad, atributos y pertenencia a segmentos {#using-templating}

Adobe utiliza un lenguaje de plantilla similar a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) para transformar los campos del esquema XDM en un formato compatible con el destino.

En esta sección se proporcionan varios ejemplos de cómo se realizan estas transformaciones, desde el esquema XDM de entrada hasta la plantilla y la salida a los formatos de carga útil aceptados por el destino. Los ejemplos siguientes se ordenan por complejidad creciente, de la siguiente manera:

1. Ejemplos de transformación simples. Aprenda cómo funciona la plantilla con transformaciones simples para los campos [Atributos de perfil](./message-format.md#attributes), [Pertenencia a segmento](./message-format.md#segment-membership) y [Identidad](./message-format.md#identities).
2. Se han aumentado los ejemplos de complejidad de las plantillas que combinan los campos anteriores: [Cree una plantilla que envíe segmentos e identidades](./message-format.md#segments-and-identities) y [Cree una plantilla que envíe segmentos, identidades y atributos de perfil](./message-format.md#segments-identities-attributes).
3. Plantillas que incluyen la clave de agregación. Cuando se utiliza [agregación configurable](./destination-configuration.md#configurable-aggregation) en la configuración de destino, el Experience Platform agrupa los perfiles exportados a su destino según criterios como ID de segmento, estado del segmento o áreas de nombres de identidad.

### Atributos de perfil {#attributes}

Para transformar los atributos de perfil exportados a su destino, consulte los ejemplos de código y JSON a continuación.

>[!IMPORTANT]
>
>Para obtener una lista de todos los atributos de perfil disponibles en Adobe Experience Platform, consulte el [diccionario de campos XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).


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
>Para todas las plantillas que utilice, debe omitir los caracteres no permitidos, como las comillas dobles `""` antes de insertar la plantilla en la [configuración del servidor de destino](./server-and-template-configuration.md#template-specs). Para obtener más información sobre cómo omitir las comillas dobles, consulte el capítulo 9 en el [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### Pertenencia a segmentos {#segment-membership}

El atributo [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM informa de los segmentos a los que pertenece un perfil.
Para los tres valores diferentes del campo `status`, lea la documentación del grupo de campos [Segment Membership Details schema group](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

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
        "status": "existing"
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
        "status": "existing"
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
>Para todas las plantillas que utilice, debe omitir los caracteres no permitidos, como las comillas dobles `""` antes de insertar la plantilla en la [configuración del servidor de destino](./server-and-template-configuration.md#template-specs). Para obtener más información sobre cómo omitir las comillas dobles, consulte el capítulo 9 en el [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

Para obtener información sobre las identidades en el Experience Platform, consulte la [descripción general del área de nombres de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=es).

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
>Para todas las plantillas que utilice, debe omitir los caracteres no permitidos, como las comillas dobles `""` antes de insertar la plantilla en la [configuración del servidor de destino](./server-and-template-configuration.md#template-specs). Para obtener más información sobre cómo omitir las comillas dobles, consulte el capítulo 9 en el [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
              "status": "existing"
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
>Para todas las plantillas que utilice, debe omitir los caracteres no permitidos, como las comillas dobles `""` antes de insertar la plantilla en la [configuración del servidor de destino](./server-and-template-configuration.md#template-specs). Para obtener más información sobre cómo omitir las comillas dobles, consulte el capítulo 9 en el [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

El `json` siguiente representa los datos exportados fuera de Adobe Experience Platform.

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
              "status": "existing"
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
>Para todas las plantillas que utilice, debe omitir los caracteres no permitidos, como las comillas dobles `""` antes de insertar la plantilla en la [configuración del servidor de destino](./server-and-template-configuration.md#template-specs). Para obtener más información sobre cómo omitir las comillas dobles, consulte el capítulo 9 en el [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

El `json` siguiente representa los datos exportados fuera de Adobe Experience Platform.

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

Cuando utiliza [agregación configurable](./destination-configuration.md#configurable-aggregation) en la configuración de destino, puede agrupar los perfiles exportados a su destino según criterios como ID de segmento, alias de segmento, pertenencia a segmentos o áreas de nombres de identidad.

En la plantilla de transformación de mensajes, puede acceder a las claves de agregación mencionadas anteriormente, como se muestra en los ejemplos de las secciones siguientes. Utilice las claves de agregación para estructurar el mensaje HTTP exportado fuera del Experience Platform de modo que coincida con el formato y los límites de velocidad esperados por el destino.

#### Utilizar la clave de agregación de ID de segmento en la plantilla {#aggregation-key-segment-id}

Si utiliza [agregación configurable](./destination-configuration.md#configurable-aggregation) y establece `includeSegmentId` como verdadero, los perfiles de los mensajes HTTP exportados a su destino se agrupan por ID de segmento. Consulte a continuación cómo puede acceder al ID de segmento en la plantilla.

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
            "status":"existing"
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
            "status":"existing"
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
            "status":"existing"
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
            "status":"existing"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

**Plantilla**

>[!IMPORTANT]
>
>Para todas las plantillas que utilice, debe omitir los caracteres no permitidos, como las comillas dobles `""` antes de insertar la plantilla en la [configuración del servidor de destino](./server-and-template-configuration.md#template-specs). Para obtener más información sobre cómo omitir las comillas dobles, consulte el capítulo 9 en el [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Observe a continuación cómo se utiliza `audienceId` en la plantilla para acceder a los ID de segmento. En este ejemplo se asume que utiliza `audienceId` para la pertenencia a segmentos en su taxonomía de destino. En su lugar, puede utilizar cualquier otro nombre de campo, según su propia taxonomía.

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

Si utiliza [agregación configurable](./destination-configuration.md#configurable-aggregation) y establece `includeSegmentId` como verdadero, también puede acceder a los alias de segmento en la plantilla.

Añada la línea siguiente a la plantilla para acceder a los perfiles exportados agrupados por alias de segmento.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Utilizar la clave de agregación del estado del segmento en la plantilla {#aggregation-key-segment-status}

Si utiliza [agregación configurable](./destination-configuration.md#configurable-aggregation) y establece `includeSegmentId` y `includeSegmentStatus` como verdadero, puede acceder al estado del segmento en la plantilla. De este modo, puede agrupar perfiles en los mensajes HTTP exportados a su destino en función de si se deben añadir o eliminar perfiles de segmentos.

Los valores posibles son:

* realizado
* existente
* exitado

Añada la línea siguiente a la plantilla para añadir o eliminar perfiles de segmentos, según los valores anteriores:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Utilizar la clave de agregación del área de nombres de identidad en la plantilla {#aggregation-key-identity}

A continuación, se muestra un ejemplo en el que la [agregación configurable](./destination-configuration.md#configurable-aggregation) de la configuración de destino se configura para agregar perfiles exportados por áreas de nombres de identidad, en el formulario `"namespaces": ["email", "phone"]` y `"namespaces": ["GAID", "IDFA"]`. Consulte el parámetro `groups` en la [referencia de la API de configuración de destino](./destination-configuration-api.md) para obtener más información sobre esta agrupación.

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
>Para todas las plantillas que utilice, debe omitir los caracteres no permitidos, como las comillas dobles `""` antes de insertar la plantilla en la [configuración del servidor de destino](./server-and-template-configuration.md#template-specs). Para obtener más información sobre cómo omitir las comillas dobles, consulte el capítulo 9 en el [JSON standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

El contexto proporcionado a la plantilla contiene `input` (los perfiles/datos que se exportan en esta llamada) y `destination` (datos sobre el destino al que ese Adobe envía datos, válidos para todos los perfiles).

En la tabla siguiente se describen las funciones de los ejemplos anteriores.

| Función | Descripción |
|---------|----------|
| `input.profile` | El perfil, representado como [JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Sigue el esquema XDM de socio mencionado anteriormente en esta página. |
| `destination.segmentAliases` | Asigne ID de segmentos en el espacio de nombres de Adobe Experience Platform para segmentar alias en el sistema del socio. |
| `destination.segmentNames` | Asigne nombres de segmento en el espacio de nombres de Adobe Experience Platform a nombres de segmento en el sistema del socio. |
| `addedSegments(listOfSegments)` | Devuelve solo los segmentos que tienen estado `realized` o `existing`. |
| `removedSegments(listOfSegments)` | Devuelve solo los segmentos que tienen estado `exited`. |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
