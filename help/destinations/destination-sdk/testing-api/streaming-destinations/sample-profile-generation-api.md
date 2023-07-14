---
description: Aprenda a utilizar la API de prueba de destino para generar perfiles de muestra para su destino de flujo continuo, que puede utilizar en las pruebas de destino.
title: Generar perfiles de muestra basados en un esquema de origen
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 2%

---


# Generar perfiles de muestra basados en un esquema de origen {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**Extremo de API**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Esta página enumera y describe todas las operaciones de API que puede realizar con la variable `/authoring/sample-profiles` Extremo de API.

## Generar diferentes tipos de perfiles para diferentes API {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Utilice este extremo de API para generar perfiles de muestra para dos casos de uso independientes. Puede:
>* generar perfiles para utilizarlos al [creación y prueba de una plantilla de transformación de mensajes](create-template.md) - mediante *ID de destino* como parámetro de consulta.
>* generar perfiles para utilizarlos al realizar llamadas a [compruebe si el destino está configurado correctamente](streaming-destination-testing-overview.md) - mediante *ID de instancia de destino* como parámetro de consulta.

Puede generar perfiles de muestra basados en el esquema de origen XDM de Adobe (para utilizarlo al probar el destino) o el esquema de destino admitido por el destino (para utilizarlo al crear la plantilla). Para comprender la diferencia entre el esquema de origen XDM de Adobe y el esquema de destino, lea la sección de información general del [Formato del mensaje](../../functionality/destination-server/message-format.md) artículo.

Tenga en cuenta que los propósitos para los que se pueden utilizar los perfiles de muestra no son intercambiables. Perfiles generados en función de la variable *ID de destino* solo se puede utilizar para crear las plantillas de transformación de mensajes y los perfiles generados en función de la variable *ID de instancia de destino* solo se puede usar para probar el punto final de destino.

## Introducción a las operaciones de API de generación de perfiles de muestra {#get-started}

Antes de continuar, consulte la [guía de introducción](../../getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Generar perfiles de muestra basados en el esquema de origen para utilizarlos al probar el destino {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Agregue los perfiles de muestra generados aquí a las llamadas HTTP cuando [prueba del destino](streaming-destination-testing-overview.md).

Puede generar perfiles de muestra basados en el esquema de origen realizando una solicitud de GET al `authoring/sample-profiles/` y proporciona el ID de una instancia de destino que ha creado en función de la configuración de destino que desea probar.

Para obtener el ID de una instancia de destino, primero debe crear una conexión en la interfaz de usuario de Experience Platform a su destino antes de intentar probar el destino. Lea el [activar tutorial de destino](../../../ui/activation-overview.md) y consulte la sugerencia siguiente sobre cómo obtener el ID de instancia de destinos que se utiliza para esta API.

>[!IMPORTANT]
>
>* Para utilizar esta API, debe tener una conexión existente con el destino en la interfaz de usuario de Experience Platform. Leer [conectar con destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) y [activación de perfiles y audiencias en un destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) para obtener más información.
> * Después de establecer la conexión con su destino, obtenga el ID de instancia de destino que debe utilizar en las llamadas API a este extremo cuando [exploración de una conexión con su destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
>![Imagen de interfaz de usuario cómo obtener el ID de instancia de destino](../../assets/testing-api/get-destination-instance-id.png)

**Formato de API**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Parámetro de consulta | Descripción |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | El ID de la instancia de destino en función de la cual está generando perfiles de muestra. |
| `{COUNT}` | *Opcional*. El número de perfiles de muestra que está generando. El parámetro puede tomar valores entre `1 - 1000`. <br> Si no se especifica el parámetro de recuento, el número predeterminado de perfiles generados se determina mediante la variable `maxUsersPerRequest` valor en [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Si no se define esta propiedad, el Adobe generará un perfil de muestra. |

{style="table-layout:auto"}


**Solicitud**

La siguiente solicitud genera perfiles de ejemplo, configurados por el `{DESTINATION_INSTANCE_ID}` y `{COUNT}` parámetros de consulta.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el número especificado de perfiles de muestra, con pertenencia a audiencia, identidades y atributos de perfil que corresponden al esquema XDM de origen.

>[!TIP]
>
> La respuesta solo devuelve la pertenencia a audiencias, identidades y atributos de perfil que se utilizan en la instancia de destino. Aunque el esquema de origen tenga otros campos, estos se ignoran.

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
| `segmentMembership` | Un objeto map que describe las pertenencias de audiencia del individuo. Para obtener más información sobre `segmentMembership`, lea [Detalles de pertenencia a audiencia](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Una marca de tiempo de la última vez que este perfil se clasificó para el segmento. |
| `xdm:status` | Campo de cadena que indica si el abono a audiencia se ha realizado como parte de la solicitud actual. Se aceptan los siguientes valores: <ul><li>`realized`: el perfil forma parte del segmento.</li><li>`exited`: el perfil se está saliendo de la audiencia como parte de la solicitud actual.</li></ul> |
| `identityMap` | Campo de tipo mapa que describe los distintos valores de identidad de un individuo, junto con sus áreas de nombres asociadas. Para obtener más información sobre `identityMap`, lea [Base de composición del esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style="table-layout:auto"}

## Generar perfiles de muestra basados en el esquema de destinatario para utilizarlos al crear una plantilla de transformación de mensajes {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Utilice los perfiles de muestra generados aquí al crear la plantilla, en la [paso de plantilla de procesamiento](render-template-api.md#multiple-profiles-with-body).

Puede generar perfiles de muestra basados en el esquema de destinatario realizando una solicitud a la GET `authoring/sample-profiles/` y proporcionar el ID de destino de la configuración de destino en función de la que esté creando la plantilla.

>[!TIP]
>
>* El ID de destino que debe utilizar aquí es el `instanceId` que corresponde a una configuración de destino, creada con la variable `/destinations` punto final. Consulte [recuperar una configuración de destino](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) para obtener más información.

**Formato de API**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Parámetro de consulta | Descripción |
| -------- | ----------- |
| `{DESTINATION_ID}` | El ID de la configuración de destino en función de la cual está generando perfiles de muestra. |
| `{COUNT}` | *Opcional*. El número de perfiles de muestra que está generando. El parámetro puede tomar valores entre `1 - 1000`. <br> Si no se especifica el parámetro de recuento, el número predeterminado de perfiles generados se determina mediante la variable `maxUsersPerRequest` valor en [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Si no se define esta propiedad, el Adobe generará un perfil de muestra. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud genera perfiles de ejemplo, configurados por el `{DESTINATION_ID}` y `{COUNT}` parámetros de consulta.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el número especificado de perfiles de muestra, con pertenencia a audiencia, identidades y atributos de perfil que corresponden al esquema XDM de destino.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
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
                    "status": "realized"
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
                    "status": "realized"
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

## Administración de errores de API {#api-error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo generar perfiles de muestra para utilizarlos cuando [prueba de una plantilla de transformación de mensajes](create-template.md) o cuando [prueba de si el destino está configurado correctamente](streaming-destination-testing-overview.md).
