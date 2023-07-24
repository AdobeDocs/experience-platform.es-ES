---
title: Crear una conexión de origen de SAP Commerce en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de SAP Commerce mediante la interfaz de usuario de Adobe Experience Platform.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 99edb8b2bcd4225235038e966a367d91375c961a
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 2%

---

# Crear un [!DNL SAP Commerce] conexión de origen en la interfaz de usuario

>[!NOTE]
>
>El [!DNL SAP Commerce] el origen está en versión beta. Consulte la [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

El siguiente tutorial le guiará para crear una [!DNL SAP Commerce] conexión de origen para traer [[!DNL SAP] Facturación de suscripción](https://www.sap.com/products/financial-management/subscription-billing.html) contactos y datos de clientes mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL SAP Commerce] cuenta de, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/ecommerce.md).

### Recopilar credenciales necesarias {#gather-credentials}

Para poder conectarse [!DNL SAP Commerce] para acceder a Experience Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| ID del cliente | El valor de `clientId` desde la clave de servicio. |
| Secreto de cliente | El valor de `clientSecret` desde la clave de servicio. |
| Extremo de token | El valor de `url` desde la clave de servicio, será similar a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Región | Su ubicación del centro de datos. La región está presente en el `url` y tiene un valor similar al siguiente `eu10` o `us10`. Por ejemplo, si la variable `url` es `https://eu10.revenue.cloud.sap/api` usted necesitará `eu10`. |

Para obtener más información, consulte la [[!DNL SAP Commerce] documentación](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

### Creación de un esquema de Platform {#create-platform-schema}

Antes de crear un [!DNL SAP Commerce] conexión de origen, también debe asegurarse de crear primero un esquema de Experience Platform para utilizarlo con el origen. Consulte el tutorial sobre [creación de un esquema de Platform](../../../../../xdm/schema/composition.md) para obtener información detallada sobre cómo crear un esquema.

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

## Conecte su [!DNL SAP Commerce] account {#connect-account}

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el *eCommerce* categoría, seleccionar **[!UICONTROL SAP Commerce]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![Captura de pantalla de la IU de Platform para el catálogo con la tarjeta SAP Commerce](../../../../images/tutorials/create/ecommerce/sap-commerce/catalog-card.png)

El **[!UICONTROL Conectar cuenta de SAP Commerce]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente {#existing-account}

Para utilizar una cuenta existente, seleccione la [!DNL SAP Commerce] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![Captura de pantalla de la IU de Platform para conectar la cuenta de SAP Commerce con una cuenta existente](../../../../images/tutorials/create/ecommerce/sap-commerce/existing.png)

### Nueva cuenta {#new-account}

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![Captura de pantalla de la IU de Platform para conectar la cuenta de SAP Commerce con una nueva cuenta](../../../../images/tutorials/create/ecommerce/sap-commerce/new.png)

### Seleccionar datos {#select-data}

Finalmente, debe seleccionar el tipo de objeto que desea introducir en Platform.

| Tipo de objeto | Descripción |
| --- | --- |
| `Customers` | Las entidades que tienen suscripciones. |
| `Contacts` | Los datos de contacto de los clientes. |

>[!BEGINTABS]

>[!TAB Clientes]

Para introducir datos de clientes, seleccione **[!UICONTROL Clientes]** como tipo de objeto y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Captura de pantalla de la IU de Platform para SAP Commerce que muestra la configuración con la opción Clientes seleccionada](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-customers.png)

>[!TAB Contactos]

Para introducir datos de contacto, seleccione **[!UICONTROL Contactos]** como tipo de objeto y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Captura de pantalla de la IU de Platform para SAP Commerce que muestra la configuración con la opción Contactos seleccionada](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-contacts.png)

>[!ENDTABS]

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha establecido una conexión con su [!DNL SAP Commerce] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Platform](../../dataflow/ecommerce.md).

## Recursos adicionales {#additional-resources}

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al utilizar el [!DNL SAP Commerce] origen.

### Asignación {#mapping}

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

Las configuraciones de asignación para el flujo de datos variarán según el esquema y el tipo de objeto que seleccione para la ingesta.

>[!BEGINTABS]

>[!TAB Clientes]

Para datos de clientes, [!DNL SAP Commerce] utiliza el [clientes](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers) y el [relaciones cliente-contactos](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) puntos finales del [!DNL SAP Business Partners] API para recuperar los datos

A continuación se muestra un ejemplo de asignación de configuraciones para [!DNL SAP Commerce] flujo de datos para los datos de clientes:

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

Para datos de contacto, [!DNL SAP Commerce] utiliza el [contactos](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts) punto final del [!DNL SAP Business Partners] API para recuperar los datos.

A continuación se muestra un ejemplo de asignación de configuraciones para [!DNL SAP Commerce] flujo de datos para datos de contacto:

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

