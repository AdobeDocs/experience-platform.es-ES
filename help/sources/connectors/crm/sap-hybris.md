---
title: Resumen de origen de SAP Hybris
description: Aprenda a conectar SAP Hybris a Adobe Experience Platform mediante API o la interfaz de usuario.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 32e2c13dcdbf2f13b4025354dfc50f5ccaf5f664
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 3%

---

# [!DNL SAP Hybris]

>[!NOTE]
>
>El [!DNL SAP Hybris] el origen está en versión beta. Consulte la [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

[[!DNL SAP Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), una solución de plataforma de comercio electrónico basada en la nube para empresas B2B y B2C está disponible como parte del catálogo de productos de SAP Customer Experience. [[!DNL SAP] Facturación de suscripción](https://www.sap.com/products/financial-management/subscription-billing.html) es un producto incluido en la cartera de productos y permite una administración completa del ciclo de vida de las suscripciones con experiencias de venta y pago simplificadas mediante integraciones estandarizadas.

El [!DNL SAP Hybris] fuente permite introducir información de clientes y contactos en Platform desde el [[!DNL SAP] Facturación de suscripción](https://www.sap.com/products/financial-management/subscription-billing.html) Extremos de API de socios comerciales a continuación:

* [Clientes](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contactos](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Además, si [!DNL SAP Hybris] se ejecuta para recuperar los datos del cliente, la variable [Relaciones cliente-contacto](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) También se llama a la API para recuperar la información de contacto del cliente.

## LISTA DE PERMITIDOS de direcciones IP {#ip-allow-list}

Es posible que sea necesario agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Requisitos previos {#prerequisites}

Antes de que pueda traer su [!DNL SAP Hybris] datos al Experience Platform, primero debe asegurarse de que dispone de lo siguiente:

* A [!DNL SAP Subscription Billing] cuenta. Si todavía no tiene una cuenta de facturación válida, póngase en contacto con su [!DNL SAP] administrador de cuentas. Consulte la [[!DNL SAP] Configuración de plataforma](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) para obtener más información.

* [!DNL SAP] clave de servicio. El [!DNL SAP] clave de servicio le permite acceder al [!DNL SAP Subscription Billing] API a través del Experience Platform. [!DNL SAP Hybris] requiere lo siguiente:
   * ID del cliente
   * Secreto de cliente
   * URL. El patrón de URL es el siguiente: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Este valor se utilizará más adelante para obtener valores para `region` y `tokenEndpoint` cuando usted [Crear conexión base](../../tutorials/api/create/crm/sap-hybris.md#base-connection) mediante la API o cuando [Conecte su [!DNL SAP Hybris] account](../../tutorials/ui/create/crm/sap-hybris.md#connect-account) mediante la IU de Platform.

+++Seleccione para ver un ejemplo de la clave de servicio

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## Pasos siguientes

La siguiente documentación proporciona información sobre cómo conectarse [!DNL SAP Hybris] Vaya a Platform mediante las API o la interfaz de usuario de:

* [Crear una conexión de origen y un flujo de datos para traer [!DNL SAP Hybris] datos a Platform mediante API](../../tutorials/api/create/crm/sap-hybris.md).
* [Conecte su [!DNL SAP Hybris] cuenta de al Experience Platform mediante la interfaz de usuario de](../../tutorials/ui/create/crm/sap-hybris.md).
* [Crear un flujo de datos para una fuente CRM mediante la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
