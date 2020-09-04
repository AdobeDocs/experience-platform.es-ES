---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consent;Consent
solution: Adobe Experience Platform
title: Información general sobre la combinación de privacidad
description: La combinación de privacidad y preferencias de marketing (consentimiento) es una combinación de modelo de datos de experiencia (XDM) destinada a admitir la recopilación de permisos y preferencias de usuario generadas por CMP y otras fuentes de los clientes. El presente documento abarca la estructura y el uso previsto de los diversos campos proporcionados por la mezcla.
topic: guide
translation-type: tm+mt
source-git-commit: 172710c62b6f60de74e05364edb1191fbba0ff64
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 1%

---


# [!DNL Privacy Consent] información general de la mezcla

La [!DNL Privacy/Marketing Preferences (Consent)] mezcla (denominada en lo sucesivo &quot;[!DNL Privacy Consent] mezcla&quot;) es una mezcla [!DNL Experience Data Model] (XDM) destinada a apoyar la recopilación de permisos y preferencias de usuario generados por los CMP y otras fuentes de los clientes. El presente documento abarca la estructura y el uso previsto de los diversos campos proporcionados por la mezcla.

## Requisitos previos {#prerequisites}

Este documento requiere una comprensión práctica de [!DNL Experience Data Model] (XDM) y el uso de los esquemas en [!DNL Experience Platform]. Revise la siguiente documentación antes de continuar:

* [Descripción general del sistema XDM](http://www.adobe.com/go/xdm-home-en)
* [Conceptos básicos de la composición de esquemas](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Ejemplo de esquema {#schema}

>[!NOTE]
>
>El ejemplo siguiente ilustra la estructura de los datos que se envían [!DNL Platform] a través de la [!DNL Privacy Consent] mezcla, para dar contexto a la siguiente sección de este documento, en la que se explican los principales campos proporcionados por la mezcla. En el [apéndice](#full-schema) figura un ejemplo completo de la estructura del esquema con fines de referencia.

El siguiente JSON muestra un ejemplo del tipo de datos que puede procesar la [!DNL Privacy Consent] mezcla. En la siguiente sección se proporciona información sobre el uso específico de cada uno de estos campos.

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## Campos {#fields}

Las secciones que figuran a continuación abarcan el uso de cada uno de los principales campos proporcionados por la [!DNL Privacy Consent] mezcla y la forma en que deben estructurarse sus subcampos.

### xdm:privacyOptOuts {#privacyOptOuts}

`xdm:privacyOptOuts` es una matriz que representa la configuración general de exclusión seleccionada por el cliente. Se pueden incluir varios objetos en esta matriz, cada uno de los cuales representa un tipo de exclusión específico y las preferencias que el cliente ha seleccionado para ese tipo.

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:optOutType` | Tipo de exclusión. Consulte el [apéndice](#optOutType-values) para conocer los valores y las definiciones aceptados. |
| `xdm:optOutValue` | La preferencia seleccionada que el cliente ha elegido para este tipo de exclusión en particular. Consulte el [apéndice](#choice-optOutValue-values) para conocer los valores y las definiciones aceptados. |
| `xdm:timestamp` | Marca de hora ISO 8601 del momento en que se cambió la preferencia de exclusión, si corresponde. |
| `xdm:basisOfProcessing` | Indica la base relacionada con la privacidad mediante la cual se deben recopilar y procesar los datos. De forma predeterminada, este campo se establece en `consent`, lo que indica que los datos sólo deben procesarse si el usuario ha dado su consentimiento (como se refleja en `xdm:optOutValue`).<br><br>En algunas circunstancias, no se ha pedido a los clientes que den su consentimiento para el procesamiento de datos. `xdm:basisOfProcessing` debe incluirse en el objeto de exclusión en estos casos, indicando el motivo por el que no se proporcionó un mensaje de consentimiento. Consulte el [apéndice](#basisOfProcessing-values) para conocer los valores y las definiciones aceptados. |

### xdm:personalizationPreferences {#personalizationPreferences}

`xdm:personalizationPreferences` captura las preferencias de los clientes con respecto a las formas en que se pueden utilizar sus datos para la personalización. Los usuarios pueden exclusión casos de uso de personalización específicos o exclusión la personalización por completo.

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` no cubre casos de uso de la mercadotecnia. Por ejemplo, si un cliente exclusión la personalización de los mensajes de correo electrónico, no dejará de recibir mensajes. Más bien, los correos electrónicos que reciben son genéricos y no están basados en su perfil.
>
>En el mismo ejemplo, si un cliente exclusión la mercadotecnia por correo electrónico (a través de `xdm:marketingPreferences`, según se explica en la [siguiente sección](#marketingPreferences)), ese cliente no recibirá ningún correo electrónico, aunque se permita la personalización del correo electrónico.

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:default` | Los datos proporcionados en este objeto representan las preferencias del cliente para la personalización en su conjunto. |
| `xdm:details` | Matriz de objetos, uno para cada tipo de personalización específica para la que el cliente ha proporcionado preferencias. |
| `xdm:choice` | La preferencia de consentimiento proporcionado por el cliente para la personalización en general, o un tipo de personalización específico, dependiendo de si se proporciona en `xdm:default` o `xdm:details`, respectivamente. Consulte el [apéndice](#choice-optOutValue-values) para conocer los valores y las definiciones aceptados. |
| `xdm:type` | Los objetos de la `xdm:details` matriz deben proporcionar este campo para indicar el caso de uso de personalización específico para el que el cliente proporciona los datos de consentimiento. Consulte el [apéndice](#type-values) para conocer los valores y las definiciones aceptados. |
| `xdm:timestamp` | Marca de hora ISO 8601 del momento en que se cambió la preferencia de exclusión, si corresponde. |
| `xdm:basisOfProcessing` | Indica la base relacionada con la privacidad mediante la cual se deben recopilar y procesar los datos. De forma predeterminada, este campo se establece en `consent`, lo que indica que los datos sólo deben procesarse si el usuario ha dado su consentimiento (como se refleja en `xdm:choice`).<br><br>En algunas circunstancias, no se ha pedido a los clientes que den su consentimiento para la personalización. `xdm:basisOfProcessing` debe incluirse en el objeto de exclusión en estos casos, indicando el motivo por el que no se proporcionó un mensaje de consentimiento. Consulte el [apéndice](#basisOfProcessing-values) para conocer los valores y las definiciones aceptados. |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` captura las preferencias del cliente con respecto a los fines de mercadotecnia para los que se pueden utilizar sus datos. Los usuarios pueden exclusión casos específicos de uso de mercadotecnia o exclusión completamente la mercadotecnia directa.

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:default` | Los datos proporcionados en este objeto representan las preferencias del cliente para la mercadotecnia directa en su conjunto. |
| `xdm:details` | Una matriz de objetos, uno para cada caso de uso de mercadotecnia específico para el que el cliente ha proporcionado preferencias. |
| `xdm:choice` | La preferencia de consentimiento proporcionado por el cliente para la mercadotecnia en general, o un caso de uso de mercadotecnia específico, dependiendo de si se proporciona en `xdm:default` o `xdm:details`, respectivamente. Consulte el [apéndice](#choice-optOutValue-values) para conocer los valores y las definiciones aceptados. |
| `xdm:subscriptions` | Objeto cuyas claves representan suscripciones específicas de la compañía, como listas de correo o newsletters. Cada objeto de suscripción debe a su vez contener un `xdm:choice` valor para la suscripción en cuestión. |
| `xdm:type` | Los objetos de la `xdm:details` matriz deben proporcionar este campo para indicar el caso de uso de marketing específico para el que el cliente proporciona los datos de consentimiento. Consulte el [apéndice](#type-values) para conocer los valores y las definiciones aceptados. |
| `xdm:timestamp` | Marca de hora ISO 8601 del momento en que se cambió la preferencia de exclusión, si corresponde. |
| `xdm:basisOfProcessing` | Indica la base relacionada con la privacidad mediante la cual se deben recopilar y procesar los datos. De forma predeterminada, este campo se establece en `consent`, lo que indica que los datos sólo deben procesarse si el usuario ha dado su consentimiento (como se refleja en `xdm:choice`).<br><br>En algunas circunstancias, no se ha pedido a los clientes que den su consentimiento para la mercadotecnia directa. `xdm:basisOfProcessing` debe incluirse en el objeto de exclusión en estos casos, indicando el motivo por el que no se proporcionó un mensaje de consentimiento. Consulte el [apéndice](#basisOfProcessing-values) para conocer los valores y las definiciones aceptados. |

## Ingesta de datos de consentimiento mediante la mezcla {#ingest}

Para utilizar la [!DNL Privacy Consent] combinación para ingerir datos de consentimiento de sus clientes, debe agregar la mezcla a un esquema nuevo o existente y crear un conjunto de datos basado en ese esquema.

Consulte el tutorial sobre la [creación de un esquema en la interfaz de usuario](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) para ver los pasos para agregar mezclas a un esquema. La[!DNL  Privacy Consent] mezcla es compatible con esquemas basados en las clases [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent].

Una vez creado un esquema que contiene la [!DNL Privacy Consent] mezcla, consulte la sección sobre la [creación de un conjunto de datos](../../catalog/datasets/user-guide.md#create) en la guía del usuario del conjunto de datos, siguiendo los pasos para crear un conjunto de datos con un esquema existente.

>[!IMPORTANT]
>
>Si desea enviar datos de consentimiento a [!DNL Real-time Customer Profile], es necesario crear un esquema [!DNL Profile]-activado basado en la [!DNL XDM Individual Profile] clase que contiene la [!DNL Privacy Consent] mezcla. El conjunto de datos que cree en función de ese esquema también debe estar habilitado para [!DNL Profile]. Consulte los tutoriales anteriores para ver los pasos específicos relacionados con [!DNL Real-time Customer Profile] los requisitos.

## Apéndice {#appendix}

En las secciones que figuran a continuación se proporciona información de referencia adicional sobre la [!DNL Privacy Consent] mezcla.

### Valores aceptados para xdm:optOutType {#optOutType-values}

La siguiente tabla describe los valores aceptados para `xdm:optOutType`:

| Valor | Descripción |
| --- | --- |
| `general_opt_out` | Los datos no se pueden usar para ningún propósito. Esto generalmente bloquea la recopilación de datos, excepto cuando la base del procesamiento no es &quot;consentimiento&quot;.<br><br>Al utilizar este tipo de exclusión, los valores aceptados `in` y `out` obtienen el siguiente significado contextual:<ul><li>`in`:: El usuario **ha dado su consentimiento** para que sus datos se utilicen para el procesamiento general.</li><li>`out`:: El usuario **no da su consentimiento** para que sus datos se utilicen para el procesamiento general.</li></ul>Consulte la tabla de valores [aceptados para xdm:optOutValue](#choice-optOutValue-values) para obtener más información. |
| `anonymous_analysis` | Los datos no se pueden utilizar para métricas web genéricas que no requieren ningún tipo de ID de usuario, como el número de veces que se vio una página en particular. |
| `device_linking` | Los datos de un dispositivo utilizado por un visitante no se pueden combinar con los datos de otro dispositivo utilizado por ese mismo visitante. Los dispositivos se vinculan mediante técnicas como un nombre de usuario o una dirección de correo electrónico comunes, a menudo mediante la cooperación entre dispositivos de Adobe o un gráfico de dispositivos privados. |
| `pseudonymous_analysis` | Los datos no se pueden utilizar para métricas web proporcionadas por Adobe Analytics, que requiere ID seudónimos para identificar las rutas que toman los usuarios a través de un sitio web (como un informe de visitas en el orden previsto), para establecer sesiones y con fines de atribución. |
| `sales_sharing_opt_out` | Los datos no se pueden usar con fines de venta ni compartir con terceros.<br><br>Al utilizar este tipo de exclusión, los valores aceptados `in` y `out` obtienen el siguiente significado contextual:<ul><li>`in`:: El usuario **ha dado su consentimiento** para que sus datos se utilicen con fines de venta y uso compartido.</li><li>`out`:: El usuario **no da su consentimiento** para que sus datos se utilicen con fines de venta y uso compartido.</li></ul>Consulte la tabla de valores [aceptados para xdm:optOutValue](#choice-optOutValue-values) para obtener más información. |

### Valores aceptados para xdm:baseOfProcessing {#basisOfProcessing-values}

La siguiente tabla describe los valores aceptados para `xdm:basisOfProcessing`:

| Valor | Descripción |
| --- | --- |
| `consent` **(Predeterminado)** | Se permite la recopilación de datos para el propósito especificado, dado que el individuo ha proporcionado un permiso explícito. Es el valor predeterminado de `xdm:basisOfProcessing` si no se proporciona ningún otro valor. <br><br>**IMPORTANTE**: Los valores para `xdm:choice` y `xdm:optOutValue` solo se respetan cuando `xdm:basisOfProcessing` se establece en `consent`. Si se utiliza cualquiera de los demás valores descritos en esta tabla `xdm:basisOfProcessing` en su lugar, se ignoran las opciones de consentimiento del individuo. |
| `compliance` | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones jurídicas de la empresa. |
| `contract` | La recopilación de datos con el fin especificado es necesaria para cumplir las obligaciones contractuales con la persona. |
| `legitimate_interest` | El interés legítimo de las empresas en recopilar y procesar estos datos con el fin especificado es mayor que el daño potencial que supone para la persona. |
| `public_interest` | La recopilación de datos con el fin especificado es necesaria para llevar a cabo una tarea de interés público o en el ejercicio de la autoridad oficial. |
| `vital_interest` | La recopilación de datos con el fin especificado es necesaria para proteger los intereses vitales de la persona. |

### Valores aceptados para xdm:choice y xdm:optOutValue {#choice-optOutValue-values}

La siguiente tabla describe los valores aceptados para `xdm:choice` y `xdm:optOutValue`:

| Valor | Descripción |
| --- | --- |
| `pending` | El sistema aún no ha recibido información sobre la preferencia de consentimiento del cliente. Puede utilizarse para la primera página de un sitio web mientras se obtiene el consentimiento. También puede utilizarse para indicar que el consentimiento se &quot;asume&quot;, en lugar de proporcionarse explícitamente. |
| `in` | El usuario ha adhesión a la preferencia de consentimiento. En otras palabras, **consienten** en utilizar sus datos como se indica en la preferencia de consentimiento en cuestión. |
| `out` | El usuario ha exclusión la preferencia de consentimiento. En otras palabras, **no consienten** en utilizar sus datos como se indica en la preferencia de consentimiento en cuestión. |
| `not_applicable` | La preferencia de consentimiento en cuestión no se aplica al cliente. |
| `not_provided` | El cliente no ha proporcionado ninguna información de consentimiento-preferencia. |
| `unknown` | Se desconoce la información de preferencias de consentimiento del cliente. |

### Valores aceptados para xdm:type {#type-values}

La siguiente tabla describe los valores aceptados para `xdm:type`:

| Valor | Descripción |
| --- | --- |
| `ads` | Publicidades que se pueden ver desde sitios web no relacionados. |
| `content` | Contenido que aparece en el sitio web. |
| `customer_support` | Datos relacionados con la asistencia al cliente. |
| `email` | Mensajes de correo electrónico. |
| `iot` | Datos relacionados con el &quot;internet de las cosas&quot; (IoT). |
| `in_app_messages` | Mensajes en la aplicación. |
| `in_home` | Mensajes en casa. |
| `in_store` | Mensajes en la tienda. |
| `in_vehicle` | Mensajes en el vehículo. |
| `offers` | Ofertas especiales. |
| `phone_calls` | Datos relacionados con las interacciones de llamadas telefónicas. |
| `push_notifications` | Notificaciones push. |
| `sms` | Mensajes SMS. |
| `social_media` | Contenido de los medios sociales. |
| `snail_mail` | Mensajes enviados a través del envío postal convencional. |
| `third_party_content` | Contenido o artículos mostrados en el sitio web que son proporcionados por una entidad no relacionada. |
| `third_party_offers` | Ofertas o publicidades que se muestran en el sitio web de servicios publicitarios de una entidad no relacionada. |

### Esquema [!DNL Privacy Consent] completo {#full-schema}

El siguiente JSON representa el [!DNL Privacy Consent] esquema completo tal como aparece en el Registro de Esquemas:

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```
