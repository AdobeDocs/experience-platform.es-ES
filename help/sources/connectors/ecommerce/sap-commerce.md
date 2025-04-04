---
title: Información general sobre SAP Commerce Source
description: Obtenga información sobre cómo conectar SAP Commerce a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 3%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>El origen [!DNL SAP Commerce] está en la versión beta. Consulte la [descripción general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), una solución de plataforma de comercio electrónico basada en la nube para empresas B2B y B2C está disponible como parte del portafolio de experiencias del cliente de SAP. [[!DNL SAP] Facturación de suscripción](https://www.sap.com/products/financial-management/subscription-billing.html) es un producto del portafolio y permite administrar por completo el ciclo de vida de la suscripción con experiencias de pago y venta simplificadas mediante integraciones estandarizadas.

La fuente [!DNL SAP Commerce] le permite introducir información de clientes y contactos en Experience Platform desde los extremos de la API de [[!DNL SAP] Facturación de suscripción](https://www.sap.com/products/financial-management/subscription-billing.html) Socios comerciales a continuación:

* [Clientes](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contactos](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Además, si se ejecuta [!DNL SAP Commerce] para recuperar datos de clientes, también se llama a la API [Relaciones entre el cliente y el contacto](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) para recuperar la información de contacto del cliente.

## LISTA DE PERMITIDOS de direcciones IP {#ip-allow-list}

Es posible que sea necesario agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Requisitos previos {#prerequisites}

Para poder llevar los datos de [!DNL SAP Commerce] a Experience Platform, primero debe asegurarse de que dispone de lo siguiente:

* Una cuenta de [!DNL SAP Subscription Billing]. Si todavía no tiene una cuenta de facturación válida, comuníquese con el administrador de cuentas de [!DNL SAP]. Consulte el documento [[!DNL SAP] Configuración de la plataforma](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) para obtener más información.

* Clave de servicio [!DNL SAP]. La clave de servicio [!DNL SAP] le permite acceder a la API [!DNL SAP Subscription Billing] a través de Experience Platform. [!DNL SAP Commerce] requiere lo siguiente:
   * ID de cliente
   * Secreto del cliente
   * URL. El patrón de la dirección URL es el siguiente: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Este valor se usará más adelante para obtener valores para `region` y `tokenEndpoint` al [crear conexión base](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) mediante la API o al [conectar su [!DNL SAP Commerce] cuenta](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) a través de la interfaz de usuario de Experience Platform.

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

La siguiente documentación proporciona información sobre cómo conectar [!DNL SAP Commerce] a Experience Platform mediante API o la interfaz de usuario:

* [Cree una conexión de origen y un flujo de datos para llevar [!DNL SAP Commerce] datos a Experience Platform mediante las API](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Conecta tu cuenta de  [!DNL SAP Commerce] a Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Creación de un flujo de datos para una fuente mediante la interfaz de usuario](../../tutorials/ui/dataflow/ecommerce.md)
