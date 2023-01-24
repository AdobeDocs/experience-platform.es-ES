---
title: Crear una conexión de origen de cuentas y contactos de SugarCRM en la interfaz de usuario
description: Aprenda a crear una conexión de origen de cuentas y contactos de SugarCRM mediante la interfaz de usuario de Adobe Experience Platform.
source-git-commit: d4b5c3b897371eea591925d071afc120a3f246d7
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# (Beta) Cree un [!DNL SugarCRM Accounts & Contacts] conexión de origen en la interfaz de usuario

>[!NOTE]
>
>La variable [!DNL SugarCRM Accounts & Contacts] el origen está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Este tutorial proporciona los pasos para crear un [!DNL SugarCRM Accounts & Contacts] conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL SugarCRM] cuenta, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar las credenciales necesarias

Para conectarse [!DNL SugarCRM Accounts & Contacts] en Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `Host` | El extremo de la API de SugarCRM al que se conecta el origen. | `developer.salesfusion.com` |
| `Username` | El nombre de usuario de su cuenta de desarrollador de SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | La contraseña de su cuenta de desarrollador de SugarCRM. | `123456789` |

### Crear un esquema de Platform

Antes de crear una [!DNL SugarCRM] conexión de origen, también debe asegurarse de crear primero un esquema de Platform para utilizarlo con el origen. Consulte el tutorial en [creación de un esquema de Platform](../../../../../xdm/schema/composition.md) para ver los pasos completos sobre cómo crear un esquema.

La variable [!DNL SugarCRM Accounts & Contacts] admite varias API. Esto significa que debe crear un esquema independiente, en función del tipo de objeto que aproveche. Consulte los ejemplos siguientes para esquemas de cuentas y contactos:

>[!BEGINTABS]

>[!TAB Cuentas]

![Captura de pantalla de la interfaz de usuario de Platform que muestra un esquema de ejemplo para cuentas](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB Contactos]

![Captura de pantalla de la interfaz de usuario de Platform que muestra un esquema de ejemplo para Contactos](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## Conecte su [!DNL SugarCRM Accounts & Contacts] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el *CRM* categoría, seleccione **[!UICONTROL Cuentas y contactos de SugarCRM]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![Captura de pantalla de la interfaz de usuario de Platform para el catálogo con la tarjeta Cuentas y contactos de SugarCRM](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

La variable **[!UICONTROL Conectar la cuenta de cuentas y contactos de SugarCRM]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL SugarCRM Accounts & Contacts] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Captura de pantalla de la interfaz de usuario de Platform para la cuenta de contactos y cuentas de Connect SugarCRM con una cuenta existente](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![Captura de pantalla de la interfaz de usuario de Platform para la cuenta de contactos y cuentas de Connect SugarCRM con una cuenta nueva](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### Selección de datos

Finalmente, debe seleccionar el tipo de objeto que desea introducir en Platform.

| Tipo de objeto | Descripción |
| --- | --- |
| `Accounts` | Las empresas con las que su organización tiene una relación. |
| `Contacts` | Personas individuales con las que su organización tiene una relación establecida. |

>[!BEGINTABS]

>[!TAB Cuentas]

![Captura de pantalla de la interfaz de usuario de Platform para cuentas y contactos de SugarCRM que muestra la configuración con la opción Cuenta seleccionada](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB Contactos]

![Captura de pantalla de la interfaz de usuario de Platform para cuentas y contactos de SugarCRM que muestran la configuración con la opción Contactos seleccionada](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL SugarCRM Accounts & Contacts] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).

## Recursos adicionales

Las secciones a continuación proporcionan recursos adicionales a los que puede hacer referencia al utilizar la variable [!DNL SugarCRM] fuente.

### Límites de protección  {#guardrails}

La variable [!DNL SugarCRM] Las tasas de aceleración de la API son de 90 llamadas por minuto o 2000 llamadas al día, lo que suceda primero. Sin embargo, esta restricción se ha eludido añadiendo un parámetro en la especificación de conexión que retrasará el tiempo de solicitud para que el límite de velocidad nunca se alcance.

### Validación {#validation}

Para validar que ha configurado correctamente el origen y [!DNL SugarCRM Accounts & Contacts] se están incorporando los datos, siga los pasos a continuación:

* En la interfaz de usuario de Platform, seleccione **[!UICONTROL Ver flujos de datos]** al lado del [!DNL SugarCRM Accounts & Contacts] en el catálogo de fuentes. A continuación, seleccione **[!UICONTROL Vista previa del conjunto de datos]** para verificar los datos introducidos.

* Según el tipo de objeto con el que esté trabajando, puede verificar los datos agregados con los recuentos visibles en la variable [!DNL SugarMarket] Cuentas o páginas de contactos a continuación:

>[!BEGINTABS]

>[!TAB Cuentas]

![Captura de pantalla de la página Cuentas de SugarMarket que muestra la lista de cuentas](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB Contactos]

![Captura de pantalla de la página de contactos de SugarMarket que muestra la lista de contactos](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>La variable [!DNL SugarMarket] las páginas no incluyen los recuentos de objetos eliminados. Sin embargo, los datos recuperados a través de esta fuente también incluirán el recuento eliminado, que se marcarán con un indicador eliminado.