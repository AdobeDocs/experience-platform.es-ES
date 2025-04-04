---
title: Crear una conexión de origen de SAP Commerce en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de SAP Commerce mediante la interfaz de usuario de Adobe Experience Platform.
badge: Beta
exl-id: 6484e51c-77cd-4dbd-9c68-0a4e3372da33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL SAP Commerce] en la interfaz de usuario

>[!NOTE]
>
>El origen [!DNL SAP Commerce] está en la versión beta. Consulte la [descripción general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

El siguiente tutorial lo acompañará durante los pasos para crear una conexión de origen de [!DNL SAP Commerce] con el fin de obtener contactos y datos de clientes de [[!DNL SAP] Facturación de suscripción](https://www.sap.com/products/financial-management/subscription-billing.html) mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL SAP Commerce] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/ecommerce.md).

### Recopilar credenciales necesarias {#gather-credentials}

Para conectar [!DNL SAP Commerce] a Experience Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| ID de cliente | El valor de `clientId` de la clave de servicio. |
| Secreto del cliente | El valor de `clientSecret` de la clave de servicio. |
| Extremo de token | El valor de `url` de la clave de servicio será similar a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Región | Su ubicación del centro de datos. La región está presente en `url` y tiene un valor similar a `eu10` o `us10`. Por ejemplo, si `url` es `https://eu10.revenue.cloud.sap/api`, necesitará `eu10`. |

Para obtener más información, consulte la [[!DNL SAP Commerce] documentación](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

### Creación de un esquema de Experience Platform {#create-platform-schema}

Antes de crear una conexión de origen de [!DNL SAP Commerce], también debe asegurarse de crear primero un esquema de Experience Platform para utilizarlo en el origen. Consulte el tutorial de [creación de un esquema de Experience Platform](../../../../../xdm/schema/composition.md) para ver los pasos detallados sobre cómo crear un esquema.

Expanda la siguiente sección para ver un esquema de ejemplo.

+++ Ver ejemplo de esquema

```
{
  "_extconndev": {
    "addresses": [
      {
        "addressUUID": "{ADDRESS_UUID}",
        "city": "Burnaby",
        "country": "Canada",
        "email": "chandni@acme.com",
        "houseNumber": "27",
        "isDefault": false,
        "phone": "123-456-7890",
        "postalCode": "V3J 1X9",
        "state": "British Columbia",
        "street": "Beresford"
      }
    ],
    "changedAt": "1687204041",
    "changedBy": "vero@acme.com",
    "contactNumber": "123-456-7980",
    "corporateInfo": {
      "company": "acme"
    },
    "createAt": "1687204041",
    "createdBy": "vero@acme.com",
    "customReferences": [
      {
        "id": "Sample value",
        "typeCode": "Sample value"
      }
    ],
    "customerNumber": "Sample value",
    "customerType": "Sample value",
    "defaultAddress": {
      "addressUUID": "Sample value",
      "city": "North Vancouver",
      "country": "Canada",
      "email": "chandni@acme.come",
      "houseNumber": "34",
      "isDefault": false,
      "phone": "123-456-7890",
      "postalCode": "V7H 2P1",
      "state": "British Columbia",
      "street": "Maple"
    },
    "externalObjectReferences": [
      {
        "externalId": "{EXTERNAL_ID}",
        "externalIdTypeCode": "{EXTERNAL_ID_TYPE_CODE}",
        "externalSystemId": "{EXTERNAL_SYSTEM_ID}"
      }
    ],
    "markets": [
      {
        "active": false,
        "country": "USA",
        "currency": "USD",
        "marketId": "Sample value",
        "priceinfo": {
          "incoterms": "{INCO_TERMS}",
          "incotermsLocation": "{INCO_TERMS_LOCATION}",
          "priceGroup": "{PRICE_GROUP}",
          "priceListType": "{PRICE_LIST_TYPE}"
        },
        "salesArea": {
          "distributionChannel": "{DISTRIBUTION_CHANNEL}",
          "division": "{DIVISION}",
          "salesOrganization": "{SALES_ORGANIZATION}"
        }
      }
    ],
    "personalInfo": {
      "firstName": "Chandni",
      "lastName": "Kaur"
    }
  },
  "_id": "/uri-reference",
  "_repo": {
    "createDate": "2004-10-23T12:00:00-06:00",
    "modifyDate": "2004-10-23T12:00:00-06:00"
  },
  "createdByBatchID": "/uri-reference",
  "modifiedByBatchID": "/uri-reference",
  "personID": "{PERSON_ID}",
  "repositoryCreatedBy": "kevin@acme.com",
  "repositoryLastModifiedBy": "kevin@acme.com"
}
```

+++

## Conectar su cuenta de [!DNL SAP Commerce] {#connect-account}

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *eCommerce*, seleccione **[!UICONTROL SAP Commerce]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![Captura de pantalla de la interfaz de usuario de Experience Platform para el catálogo con tarjeta SAP Commerce](../../../../images/tutorials/create/ecommerce/sap-commerce/catalog-card.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de SAP Commerce]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente {#existing-account}

Para usar una cuenta existente, seleccione la cuenta de [!DNL SAP Commerce] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Captura de pantalla de la IU de Experience Platform para conectar la cuenta de SAP Commerce con una cuenta existente](../../../../images/tutorials/create/ecommerce/sap-commerce/existing.png)

### Nueva cuenta {#new-account}

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Captura de pantalla de la IU de Experience Platform para conectar la cuenta de SAP Commerce con una nueva cuenta](../../../../images/tutorials/create/ecommerce/sap-commerce/new.png)

### Seleccionar datos {#select-data}

Finalmente, debe seleccionar el tipo de objeto que desea introducir en Experience Platform.

| Tipo de objeto | Descripción |
| --- | --- |
| `Customers` | Las entidades que tienen suscripciones. |
| `Contacts` | Los datos de contacto de los clientes. |

>[!BEGINTABS]

>[!TAB Clientes]

Para introducir datos de clientes, selecciona **[!UICONTROL Clientes]** como tipo de objeto y, a continuación, selecciona **[!UICONTROL Siguiente]**.

![Captura de pantalla de la interfaz de usuario de Experience Platform para SAP Commerce que muestra la configuración con la opción Customers seleccionada](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-customers.png)

>[!TAB Contactos]

Para introducir datos de contacto, selecciona **[!UICONTROL Contactos]** como tipo de objeto y, a continuación, selecciona **[!UICONTROL Siguiente]**.

![Captura de pantalla de la IU de Experience Platform para SAP Commerce que muestra la configuración con la opción Contactos seleccionada](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-contacts.png)

>[!ENDTABS]

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL SAP Commerce]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Experience Platform](../../dataflow/ecommerce.md).

## Recursos adicionales {#additional-resources}

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al usar el origen [!DNL SAP Commerce].

### Asignación {#mapping}

Experience Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignador y los campos calculados, consulte la [guía de la interfaz de usuario de la preparación de datos](../../../../../data-prep/ui/mapping.md).

Las configuraciones de asignación para el flujo de datos variarán según el esquema y el tipo de objeto que seleccione para la ingesta.

>[!BEGINTABS]

>[!TAB Clientes]

Para los datos del cliente, [!DNL SAP Commerce] usa los extremos de [clientes](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers) y [relaciones cliente-contactos](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) de la API [!DNL SAP Business Partners] para recuperar los datos

A continuación se muestra un ejemplo de asignación de configuraciones para el flujo de datos [!DNL SAP Commerce] para los datos del cliente:

| Campo de destino | Descripción |
| --- | --- |
| `customerNumber` | El número del cliente. |
| `corporateInfo` | El número del cliente. |
| `customerType` | El tipo de cliente. |
| `createdAt` | Una marca de tiempo que indica cuándo se creó el cliente. |
| `changedAt` | Una marca de tiempo que indica cuándo se actualizó el cliente por última vez. |
| `markets[*].country` | Los mercados de clientes, recuperados como un objeto de matriz. |
| `addresses[*].email` | Correos electrónicos asociados a las múltiples direcciones del cliente, recuperados como objeto de matriz. |
| `addresses[*].city` | Ciudades asociadas con las varias direcciones del cliente, recuperadas como un objeto de matriz. |
| `addresses[*].addressUUID` | ID asociados con las varias direcciones del cliente, recuperados como un objeto de matriz. |
| `externalObjectReferences[*].externalSystemId` | Datos adicionales, recuperados como un objeto de matriz. |
| `externalObjectReferences[*].externalId` | Datos adicionales, recuperados como un objeto de matriz. |
| `customReferences[*].id` | Datos adicionales, recuperados como un objeto de matriz. |
| `customReferences[*].typeCode` | Datos adicionales, recuperados como un objeto de matriz. |

![Paso de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-customers.png)

>[!TAB Contactos]

Para los datos de contacto, [!DNL SAP Commerce] usa el extremo [contacts](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts) de la API [!DNL SAP Business Partners] para recuperar los datos.

A continuación se muestra un ejemplo de asignación de configuraciones para el flujo de datos [!DNL SAP Commerce] para los datos de contacto:

| Campo de destino | Descripción |
| --- | --- |
| `contactNumber` | El número del contacto. |
| `createdAt` | Una marca de tiempo que indica cuándo se creó el contacto. |
| `changedAt` | Una marca de tiempo que indica cuándo se actualizó el contacto por última vez. |
| `personalInfo.lastName` | Apellido del contacto. - ¿Qué? |
| `personalInfo.firstName` | El nombre del contacto. |
| `externalObjectReferences[*].externalSystemId` | Datos adicionales, recuperados como un objeto de matriz. |
| `externalObjectReferences[*].externalId` | Datos adicionales, recuperados como un objeto de matriz. |
| `externalObjectReferences[*].externalIdTypeCode` | Datos adicionales, recuperados como un objeto de matriz. |

![Paso de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-contacts.png)

>[!ENDTABS]
