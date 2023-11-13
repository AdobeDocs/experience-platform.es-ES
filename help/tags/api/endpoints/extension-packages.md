---
title: Extremo de paquetes de extensiones
description: Aprenda a realizar llamadas al extremo /extension_packages en la API de Reactor.
exl-id: a91c6f32-6c72-4118-a43f-2bd8ef50709f
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 70%

---

# Extremo de paquetes de extensiones

>[!WARNING]
>
>La implementación del extremo `/extension_packages` está en proceso de cambio a medida que se añaden, eliminan y vuelven a trabajar las funciones.

Un paquete de extensiones representa una [extensión](./extensions.md) creada por un desarrollador de extensiones. Un paquete de extensiones define capacidades adicionales que se pueden poner a disposición de los usuarios de etiquetas. Normalmente, estas capacidades se presentan en forma de [componentes de regla](./rule-components.md) (eventos, condiciones y acciones) y [elementos de datos](./data-elements.md), pero también pueden incluir módulos principales y módulos compartidos.

Los paquetes de extensiones se muestran en el catálogo de extensiones dentro de la IU de recopilación de datos y la IU de Adobe Experience Platform para que los usuarios los instalen. Para añadir un paquete de extensiones a una propiedad, se crea una extensión con un vínculo al paquete de extensiones.

Un paquete de extensiones pertenece a la [empresa](./companies.md) del desarrollador que lo creó.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [API de Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

Además de comprender cómo se realizan llamadas a la API de Reactor, también es importante comprender cómo se ejecuta un paquete de extensión `status` y `availability` Los atributos de afectan a las acciones que puede realizar en ellos. Estas se explican en las secciones siguientes.

### Estado

Los paquetes de extensión tienen tres estados potenciales: `pending`, `succeeded`, y `failed`.

| Estado | Descripción |
| --- | --- |
| `pending` | Cuando se crea un paquete de extensiones, su `status` se establece en `pending`. Esto indica que el sistema recibió la información del paquete de extensión y que comenzará a procesarse. Paquetes de extensión con un estado de `pending` no están disponibles para su uso. |
| `succeeded` | El estado de un paquete de extensiones se actualiza a `succeeded` si completa correctamente el procesamiento. |
| `failed` | El estado de un paquete de extensiones se actualiza a `failed` si finaliza el procesamiento sin éxito. Un paquete de extensiones con un estado de `failed` puede actualizarse hasta que el procesamiento se realice correctamente. Paquetes de extensión con un estado de `failed` no están disponibles para su uso. |

### Disponibilidad

Hay niveles de disponibilidad para un paquete de extensión: `development`, `private`, y `public`.

| Disponibilidad | Descripción |
| --- | --- |
| `development` | Un paquete de extensiones en `development` solo está visible para la compañía que lo posee y está disponible dentro de ella. Además, solo se puede utilizar en propiedades configuradas para el desarrollo de extensiones. |
| `private` | A `private` El paquete de extensiones solo es visible para la compañía que lo posee y solo se puede instalar en propiedades de la compañía. |
| `public` | A `public` el paquete de extensiones es visible y está disponible para todas las empresas y propiedades. |

>[!NOTE]
>
>Cuando se crea un paquete de extensiones, `availability` se establece en `development`. Una vez finalizada la prueba, puede realizar la transición del paquete de extensión a `private` o `public`.

## Recuperación de una lista de paquetes de extensión {#list}

Puede recuperar una lista de paquetes de extensiones realizando una petición GET a `/extension_packages`.

**Formato de API**

```http
GET /extension_packages
```

>[!NOTE]
>
>Mediante parámetros de consulta, los paquetes de extensiones enumerados se pueden filtrar según los siguientes atributos:<ul><li>`archive`</li><li>`created_at`</li><li>`name`</li><li>`stage`</li><li>`token`</li><li>`updated_at`</li></ul>Consulte la guía de [respuestas de filtrado](../guides/filtering.md) para obtener más información.

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de paquetes de extensiones.

```json
{
  "data": [
    {
      "id": "EP6860e2485de2413ea9b295d6f5321ad3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP6860e2485de2413ea9b295d6f5321ad3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:32.694Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944710",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:35.754Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP6860e2485de2413ea9b295d6f5321ad3"
      }
    },
    {
      "id": "EP1b173c8316954e0986e5a405b4e715e3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP1b173c8316954e0986e5a405b4e715e3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:34.632Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944712",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:36.655Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP1b173c8316954e0986e5a405b4e715e3"
      }
    },
    {
      "id": "EPb8eca81769a64af3892af5202a57ce15",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EPb8eca81769a64af3892af5202a57ce15",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T18:32:29.271Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604946740",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T18:32:43.710Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EPb8eca81769a64af3892af5202a57ce15"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 3
    }
  }
}
```

## Búsqueda de un paquete de extensiones {#lookup}

Puede buscar un paquete de extensiones proporcionando su ID en la ruta de una petición GET.

**Formato de API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | El `id` del paquete de extensiones que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del paquete de extensiones, incluidos los recursos delegados como `actions`, `conditions`, `data_elements`, etc. La respuesta de ejemplo siguiente se ha truncado para el espacio.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Creación de un paquete de extensiones {#create}

Los paquetes de extensiones se crean mediante una herramienta de andamiaje de Node.js y se guardan en el equipo local antes de enviarse a la API de Reactor. Para obtener más información sobre la configuración de un paquete de extensiones, consulte la guía sobre [introducción al desarrollo de extensiones](../../extension-dev/getting-started.md).

Una vez creado el archivo del paquete de extensiones, puede enviarlo a la API de React mediante una petición POST.

**Formato de API**

```http
POST /extension_packages
```

**Solicitud**

La siguiente solicitud crea un nuevo paquete de extensiones. Se hace referencia a la ruta local al archivo del paquete que se está cargando como datos de formulario (`package`) y, por lo tanto, este punto final requiere un encabezado `Content-Type` de `multipart/form-data`.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del paquete de extensiones recién creado.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Actualización de un paquete de extensiones {#update}

Puede actualizar un paquete de extensiones incluyendo su ID en la ruta de una petición del PATCH.

**Formato de API**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | El `id` del paquete de extensiones que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

Al igual que con [la creación de un paquete de extensiones](#create), se debe cargar una versión local del paquete actualizado a través de los datos del formulario.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del paquete de extensiones actualizado.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Liberación en privado de un paquete de extensiones {#private-release}

Una vez que haya completado la prueba del paquete de extensiones, puede publicarlo en privado. Esto lo hace disponible para cualquier propiedad de su empresa.

Una vez que haya salido en privado, puede iniciar el proceso de publicación rellenando el [formulario de solicitud de versión pública](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest).

**Formato de API**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | El `id` del paquete de extensiones que desea publicar de forma privada. |

{style="table-layout:auto"}

**Solicitud**

Se logra una versión privada al proporcionar un `action` con un valor de `release_private` en el `meta` de los datos de solicitud.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "meta": {
            "action": "release_private"
          },
          "id": "EP27e9323eb585411fae6086fc78a3b70b",
          "type": "extension_packages"
        }
      }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del paquete de extensiones.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Suspensión de un paquete de extensiones {#discontinue}

Puede suspender un paquete de extensiones estableciendo su atributo `discontinued` en `true` mediante una petición PATCH.

**Formato de API**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | El `id` del paquete de extensiones que desea suspender. |

{style="table-layout:auto"}

**Solicitud**

Se logra una versión privada al proporcionar un `action` con un valor de `release_private` en el `meta` de los datos de solicitud.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "discontinued": true
          },
          "id": "EP5705a5d99aba406692e0ac666fcab160",
          "type": "extension_packages"
        }
      }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del paquete de extensiones.

```json
{
  "data": {
    "id": "EP5705a5d99aba406692e0ac666fcab160",
    "type": "extension_packages",
    "attributes": {
      "actions": [

      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP5705a5d99aba406692e0ac666fcab160",
      "conditions": [

      ],
      "configuration": null,
      "created_at": "2020-12-14T17:39:36.932Z",
      "data_elements": [

      ],
      "description": "Provides nothing.",
      "discontinued": true,
      "display_name": "Kessel Template Test",
      "events": [

      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "test-1607967575",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-12-14T17:39:43.883Z",
      "version": "1.0.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP5705a5d99aba406692e0ac666fcab160"
    }
  }
}
```

## Enumeración de las versiones de un paquete de extensiones

Puede enumerar las versiones de un paquete de extensiones añadiendo `/versions` a la ruta de una solicitud de búsqueda.

**Formato de API**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/versions
```

| Parámetro | Descripción |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | El `id` del paquete de extensiones cuyas versiones desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172/versions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de versiones anteriores del paquete de extensiones. Se ha omitido una respuesta de ejemplo para el espacio.
