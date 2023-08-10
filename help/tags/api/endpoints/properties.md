---
title: Extremo de propiedades
description: Aprenda a realizar llamadas al extremo /properties en la API de Reactor.
exl-id: 7830c519-312f-4f73-b3f5-64ab0420d902
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 98%

---

# Extremo de propiedades

Una propiedad es una construcción de contenedor que sostiene la mayoría de los demás recursos disponibles en la API de Reactor. Las propiedades se administran mediante programación usando el extremo `/properties`.

En la jerarquía de recursos, una propiedad es la propietaria de lo siguiente:

* [Versiones](./builds.md)
* [Llamadas](./callbacks.md)
* [Elementos de datos](./data-elements.md)
* [Entornos](./environments.md)
* [Extensiones](./extensions.md)
* [Hosts](./properties.md)
* [Bibliotecas](./libraries.md)
* [Regla componentes](./rule-components.md)
* [Reglas](./rules.md)

Una propiedad pertenece a exactamente una [compañía](./companies.md). Una compañía puede tener muchas propiedades.

Para obtener más información general acerca de las propiedades y su función en la administración de etiquetas, consulte la descripción general de [compañías y propiedades](../../ui/administration/companies-and-properties.md).

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [API de Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Recuperación de una lista de propiedades {#list}

Puede recuperar una lista de propiedades pertenecientes a la compañía incluyendo el ID de la empresa en la ruta de una petición GET.

**Formato de API**

```http
GET /companies/{COMPANY_ID}/properties
```

| Parámetro | Descripción |
| --- | --- |
| `COMPANY_ID` | El `id` de la compañía que posee las propiedades que desea enumerar. |

{style="table-layout:auto"}

>[!NOTE]
>
>Mediante parámetros de consulta, las propiedades enumeradas se pueden filtrar según los atributos siguientes:<ul><li>`copying`</li><li>`created_at`</li><li>`enabled`</li><li>`name`</li><li>`platform`</li><li>`token`</li><li>`updated_at`</li></ul>Consulte la guía de [filtrado de respuestas](../guides/filtering.md) para obtener más información.

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de propiedades para la compañía especificada.

```json
{
  "data": [
    {
      "id": "PR29e066628dcf4ba0a16780b2e339821c",
      "type": "properties",
      "attributes": {
        "created_at": "2020-12-14T17:51:28.215Z",
        "enabled": true,
        "name": "Kessel Example Property",
        "updated_at": "2020-12-14T17:51:28.215Z",
        "platform": "web",
        "development": false,
        "token": "30a138ca7f5b",
        "domains": [
          "example.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments",
        "extensions": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions",
        "rules": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules",
        "self": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c"
      },
      "meta": {
        "rights": [
          "approve",
          "develop",
          "manage_environments",
          "manage_extensions",
          "publish"
        ]
      }
    },
    {
      "id": "PR0c559a62480142a7b9be4a118d1a0448",
      "type": "properties",
      "attributes": {
        "created_at": "2020-08-14T15:29:34.241Z",
        "enabled": true,
        "name": "new prop",
        "updated_at": "2020-08-14T15:29:34.241Z",
        "platform": "web",
        "development": true,
        "token": "b6cee01dedb7",
        "domains": [
          "google.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments",
        "extensions": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions",
        "rules": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules",
        "self": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448"
      },
      "meta": {
        "rights": [
          "approve",
          "develop",
          "manage_environments",
          "manage_extensions",
          "publish"
        ]
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

## Búsqueda de una propiedad {#lookup}

Puede buscar una propiedad proporcionando su ID en la ruta de una petición GET.

**Formato de API**

```http
GET /properties/{PROPERTY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `PROPERTY_ID` | El `id` de la propiedad que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la propiedad.

```json
{
  "data": {
    "id": "PR48ade10e6acf4385ba96214e9f5d31e1",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:18.725Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:18.725Z",
      "platform": "web",
      "development": false,
      "token": "c54ba5e843e6",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments",
      "extensions": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions",
      "rules": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules",
      "self": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## Crear una propiedad {#create}

Puede crear una nueva propiedad realizando una petición POST.

**Formato de API**

```http
POST /company/{COMPANY_ID}/properties
```

| Parámetro | Descripción |
| --- | --- |
| `COMPANY_ID` | El `id` de la compañía en la que está definiendo la propiedad. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud crea una nueva propiedad para la propiedad especificada. La llamada también asocia la propiedad con una extensión existente a través de la propiedad `relationships`. Consulte la guía de [relaciones](../guides/relationships.md) para obtener más información.

```shell
curl -X POST \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Example Property",
            "platform": "web"
            "domains": [
              "example.com"
            ],
            "privacy": "gdpr",
            "rule_component_sequencing_enabled": false,
            "ssl_enabled": false,
            "undefined_vars_return_empty": true
          },
          "type": "properties"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `attributes.name` | **(Obligatorio)** Un nombre legible en lenguaje natural para la propiedad. |
| `attributes.platform` | **(Obligatorio)** La plataforma de la propiedad. Puede ser `web` para propiedades web o `mobile` o `edge` para propiedades móviles. |
| `attributes.domains` | **(Necesario para propiedades web)** Una matriz de dominios URL de la propiedad. |
| `attributes.development` | Un booleano que indica si se trata de una propiedad de desarrollo. |
| `attributes.privacy` | Una cadena que puede utilizarse para hacer referencia a consideraciones relacionadas con la privacidad para la propiedad. |
| `attributes.rule_component_sequencing_enabled` | Un booleano para saber si la secuenciación de componentes de regla debe habilitarse para esta propiedad. |
| `attributes.ssl_enabled` | Un booleano para saber si la capa de sockets seguros (SSL) debe estar habilitada para esta propiedad. |
| `attributes.undefined_vars_return_empty` | Un booleano para saber si las variables indefinidas deben devolverse como vacías para esta propiedad. |
| `type` | Tipo de recurso que se actualiza. Para este extremo, el valor debe ser `properties`. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles de la propiedad recién creada.

```json
{
  "data": {
    "id": "PR505e39de0d0042d1b22321e7767edb4d",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:31:31.579Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:31:31.579Z",
      "platform": "web",
      "development": false,
      "token": "a969ffc6f872",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments",
      "extensions": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions",
      "rules": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules",
      "self": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## Actualización de una propiedad {#update}

Puede actualizar una propiedad incluyendo su ID en la ruta de una petición PATCH.

**Formato de API**

```http
PATCH /properties/{PROPERTY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `PROPERTY_ID` | El `id` de la propiedad que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud actualiza `name` y `domains` para una propiedad existente.

```shell
curl -X PATCH \
  https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Property B",
            "domains": [
              "example.com"
            ]
          },
          "id": "PR541dbb24bad54dceb04710d7a9e7a740",
          "type": "properties"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `attributes` | Un objeto cuyas propiedades representan los atributos que se van a actualizar para la propiedad. Los siguientes atributos se pueden actualizar para una propiedad: <ul><li>`development`</li><li>`domains`</li><li>`name`</li><li>`platform`</li><li>`privacy`</li><li>`rule_component_sequencing_enabled`</li><li>`ssl_enabled`</li><li>`undefined_vars_return_empty`</li></ul> |
| `id` | El `id` de la propiedad que desea actualizar. Debe coincidir con el valor `{PROPERTY_ID}` proporcionado en la ruta de solicitud. |
| `type` | Tipo de recurso que se actualiza. Para este extremo, el valor debe ser `properties`. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles de la propiedad actualizada.

```json
{
  "data": {
    "id": "PR541dbb24bad54dceb04710d7a9e7a740",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:37.386Z",
      "enabled": true,
      "name": "Kessel Property B",
      "updated_at": "2020-12-14T17:51:43.062Z",
      "platform": "web",
      "development": false,
      "token": "3f2d8630a8d3",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments",
      "extensions": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions",
      "rules": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules",
      "self": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## Eliminar una propiedad

Puede eliminar una propiedad incluyendo su ID en la ruta de una petición DELETE.

**Formato de API**

```http
DELETE /properties/{PROPERTY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `PROPERTY_ID` | El `id` de la propiedad que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X DELETE \
  https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) sin cuerpo de respuesta, lo que indica que la propiedad se ha eliminado.

## Administración de notas de una propiedad {#notes}

Las propiedades son recursos “anotables”, lo que significa que puede crear y recuperar notas basadas en texto en cada recurso individual. Consulte la [guía de extremo de notas](./notes.md) para obtener más información sobre cómo administrar notas para propiedades y otros recursos compatibles.

## Recuperación de recursos relacionados para una propiedad {#related}

Las siguientes llamadas muestran cómo recuperar los recursos relacionados para una propiedad. Cuando [busca una propiedad](#lookup), estas relaciones se enumeran en la propiedad `relationships`.

Consulte la [guía de relaciones](../guides/relationships.md) para obtener más información sobre las relaciones en la API de Reactor.

### Enumeración de las llamadas de retorno relacionadas para una propiedad {#callbacks}

Puede enumerar las [llamadas de retorno](./callbacks.md) registradas en una propiedad añadiendo `/callbacks` a la ruta de una solicitud de consulta.

**Formato de API**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El `id` de la propiedad cuyas llamadas de retorno desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de llamadas de retorno que son propiedad de la propiedad especificada.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Enumeración de los elementos de datos relacionados para una propiedad {#data-elements}

Puede enumerar los [elementos de datos](./data-elements.md) que son propiedad de una propiedad adjuntando `/data_elements` a la ruta de una solicitud de consulta.

**Formato de API**

```http
GET  /properties/{PROPERTY_ID}/data_elements
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El `id` de la propiedad cuyos elementos de datos desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de elementos de datos que son propiedad de la propiedad especificada.

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:36:08 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Enumeración de los entornos relacionados para una propiedad {#environments}

Puede enumerar los [entornos](./environments.md) que son propiedad de una propiedad adjuntando `/environments` a la ruta de una solicitud de consulta.

**Formato de API**

```http
GET  /properties/{PROPERTY_ID}/environments
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El `id` de la propiedad cuyos entornos desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de entornos que son propiedad de la propiedad especificada.

```json
{
  "data": [
    {
      "id": "ENbe322acb4fc64dfdb603254ffe98b5d3",
      "type": "environments",
      "attributes": {
        "archive": false,
        "created_at": "2020-12-14T17:38:51.047Z",
        "library_path": "f9fd106ab399/cb29d726b35e",
        "library_name": "launch-c0331746ae03-development.min.js",
        "library_entry_points": [
          {
            "library_name": "launch-c0331746ae03-development.min.js",
            "minified": true,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.min.js"
            ],
            "license_path": "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
          },
          {
            "library_name": "launch-c0331746ae03-development.js",
            "minified": false,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
            ]
          }
        ],
        "name": "Development Environment A",
        "path": "https://assets.adobedtm.com/staging",
        "stage": "development",
        "updated_at": "2020-12-14T17:38:51.047Z",
        "status": "succeeded",
        "token": "c0331746ae03"
      },
      "relationships": {
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/library"
          },
          "data": null
        },
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/builds"
          }
        },
        "host": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/host",
            "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/relationships/host"
          },
          "data": {
            "id": "HTc5cae9ce1e3943aab185bdba939f98bd",
            "type": "hosts"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/property"
          },
          "data": {
            "id": "PR06c9196bc57048dd8ff169c27baeeca8",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8",
        "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3"
      },
      "meta": {
        "archive_encrypted": false
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Enumeración de las extensiones relacionadas para una propiedad {#extensions}

Puede enumerar las [extensiones](./extensions.md) que son propiedad de una propiedad adjuntando `/extensions` a la ruta de una solicitud de consulta.

**Formato de API**

```http
GET  /properties/{PROPERTY_ID}/extensions
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El `id` de la propiedad cuyas extensiones desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de extensiones que son propiedad de la propiedad especificada.

```json
{
  "data": [
    {
      "id": "EXd9d80c87afb6432ba823a58d3e78299b",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:40:21.000Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:40:21.000Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/property"
          },
          "data": {
            "id": "PRee071cb5b7794f42b74c913e1ad2e325",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/origin"
          },
          "data": {
            "id": "EXd9d80c87afb6432ba823a58d3e78299b",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325",
        "origin": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "self": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Enumeración de los hosts relacionados para una propiedad {#hosts}

Puede enumerar los [hosts](./hosts.md) que utiliza una propiedad añadiendo `/hosts` a la ruta de una solicitud de consulta.

**Formato de API**

```http
GET  /properties/{PROPERTY_ID}/hosts
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El `id` de la propiedad cuyos hosts desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de hosts que utiliza una propiedad especificada.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Enumeración de las reglas relacionadas para una propiedad {#rules}

Puede enumerar las [reglas](./rules.md) que utiliza una propiedad añadiendo `/rules` a la ruta de una solicitud de consulta.

**Formato de API**

```http
GET  /properties/{PROPERTY_ID}/rules
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El `id` de la propiedad cuyas reglas desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de reglas que usa una propiedad especificada.

```json
{
  "data": [
    {
      "id": "RL8429f3fee98b44c68f7a538e68e21747",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:56:44.109Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:56:44.109Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/property"
          },
          "data": {
            "id": "PR41f64d2a9d9b4862b0582c5ff6a07504",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/origin"
          },
          "data": {
            "id": "RL8429f3fee98b44c68f7a538e68e21747",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504",
        "origin": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "self": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "rule_components": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### Búsqueda de la compañía relacionada de una propiedad {#company}

Puede consultar la compañía propietaria de una propiedad adjuntando `/company` a la ruta de una solicitud de consulta.

**Formato de API**

```http
GET /properties/{PROPERTY_ID}/company
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El `id` de la propiedad cuya compañía desea buscar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/HT5d90148e72224224aac9bc0b01498b84/company \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la compañía de la propiedad especificada.

```json
{
  "data": {
    "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.711Z",
      "name": "Reactor QE",
      "org_id": "08364A825824E04F0A494115@AdobeOrg",
      "updated_at": "2020-08-13T17:13:30.711Z",
      "token": "f9fd106ab399",
      "cjm_enabled": true,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "properties": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties",
        "manage_app_configurations"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ]
      }
    }
  }
}
```
