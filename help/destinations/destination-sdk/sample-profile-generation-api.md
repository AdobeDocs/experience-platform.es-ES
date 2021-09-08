---
description: En esta página se enumeran y describen todas las operaciones de API que puede realizar con el extremo de API `/authoring/sample-profiles`, para generar perfiles de muestra y utilizarlos en las pruebas de destino.
title: Ejemplos de operaciones de API de generación de perfiles
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 2%

---

# Ejemplos de operaciones de API de generación de perfiles {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**Punto final** de API:  `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Esta página enumera y describe todas las operaciones de API que puede realizar con el extremo de API `/authoring/sample-profiles` .

Este extremo de API le permite generar perfiles de muestra para usar:
* Al probar una plantilla de transformación de mensaje. Obtenga más información en [Crear y probar una plantilla de transformación de mensaje](./create-template.md).
* Al probar si el destino está configurado correctamente. Obtenga más información en [Pruebe la configuración de destino](./test-destination.md).

Puede generar perfiles de ejemplo basados en el esquema de origen XDM de Adobe o en el esquema de destino admitido por el destino. Para comprender la diferencia entre el esquema de origen XDM de Adobe y el esquema de destino, lea el artículo [Message format](./message-format.md).

## Introducción a las operaciones de API de generación de perfiles de ejemplo {#get-started}

Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino necesario y los encabezados necesarios.

## Generación de perfiles de muestra basados en el esquema de origen {#generate-sample-profiles-source-schema}

Puede generar perfiles de muestra basados en el esquema de origen realizando una solicitud de GET al extremo `authoring/sample-profiles/` y proporcionando el ID de una instancia de destino que ha creado en función de la configuración de destino que desea probar.

>[!TIP]
>
>* Obtenga el ID de instancia de destino que debe usar aquí desde la dirección URL al examinar una conexión con su destino.
   >![Imagen de la interfaz de usuario de cómo obtener el ID de instancia de destino](./assets/get-destination-instance-id.png)


**Formato de API**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Parámetro de consulta | Descripción |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | El ID de la instancia de destino en función de la cual está generando perfiles de muestra. |
| `{COUNT}` | *Opcional*. Número de perfiles de muestra que está generando. El parámetro puede tomar valores entre `1 - 1000`. <br> Si no se especifica el parámetro count , el número predeterminado de perfiles generados se determina mediante el  `maxUsersPerRequest` valor de la configuración [ del servidor de ](./destination-server-api.md#create)destino. Si no se define esta propiedad, el Adobe generará un perfil de muestra. |


**Solicitud**

La siguiente solicitud genera perfiles de muestra, configurados por los parámetros de consulta `{DESTINATION_INSTANCE_ID}` y `{COUNT}` .

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el número especificado de perfiles de muestra, con pertenencia a segmentos, identidades y atributos de perfil que corresponden al esquema XDM de origen.

>[!TIP]
>
> La respuesta solo devuelve la pertenencia a segmentos, las identidades y los atributos de perfil que se utilizan en la instancia de destino. Incluso si el esquema de origen tiene otros campos, estos se ignoran.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| Propiedad | Descripción |
| -------- | ----------- |
| `segmentMembership` | Un objeto map que describe las suscripciones a segmentos del individuo. Para obtener más información sobre `segmentMembership`, lea [Detalles de pertenencia a segmentos](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Marca de fecha y hora de la última vez que este perfil cumplía los requisitos para el segmento. |
| `xdm:status` | Indica si la pertenencia al segmento se ha realizado como parte de la solicitud actual. Se aceptan los siguientes valores: <ul><li>`existing`: El perfil ya formaba parte del segmento antes de la solicitud y continúa manteniendo su pertenencia.</li><li>`realized`: El perfil está introduciendo el segmento como parte de la solicitud actual.</li><li>`exited`: El perfil sale del segmento como parte de la solicitud actual.</li></ul> |
| `identityMap` | Campo de tipo asignación que describe los distintos valores de identidad de un individuo, junto con sus áreas de nombres asociadas. Para obtener más información sobre `identityMap`, lea [Base de la composición del esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |


## Generación de perfiles de muestra basados en el esquema de destino {#generate-sample-profiles-target-schema}

Puede generar perfiles de ejemplo basados en el esquema de destino que realice una solicitud de GET al extremo `authoring/sample-profiles/` y proporcione el ID de destino de la configuración de destino en función del cual esté creando la plantilla.

>[!TIP]
>
>* El ID de destino que debe usar aquí es el `instanceId` que corresponde a una configuración de destino creada con el extremo `/destinations` . Consulte la [referencia de la API de configuración de destino](./destination-configuration-api.md#retrieve-list).


**Formato de API**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Parámetro de consulta | Descripción |
| -------- | ----------- |
| `{DESTINATION_ID}` | El ID de la configuración de destino en función del cual está generando perfiles de muestra. |
| `{COUNT}` | *Opcional*. Número de perfiles de muestra que está generando. El parámetro puede tomar valores entre `1 - 1000`. <br> Si no se especifica el parámetro count , el número predeterminado de perfiles generados se determina mediante el  `maxUsersPerRequest` valor de la configuración [ del servidor de ](./destination-server-api.md#create)destino. Si no se define esta propiedad, el Adobe generará un perfil de muestra. |

**Solicitud**

La siguiente solicitud genera perfiles de muestra, configurados por los parámetros de consulta `{DESTINATION_ID}` y `{COUNT}` .

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el número especificado de perfiles de muestra, con pertenencia a segmentos, identidades y atributos de perfil que corresponden al esquema XDM de destino.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## Gestión de errores de API {#api-error-handling}

Los extremos de la API del SDK de destino siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte los [códigos de estado de API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) y [errores de encabezado de solicitud](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo generar perfiles de muestra para usarlos al [probar una plantilla de transformación de mensaje](./create-template.md) o al [probar si su destino está configurado correctamente](./test-destination.md).