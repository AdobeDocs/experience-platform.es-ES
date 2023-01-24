---
title: Crear una conexión de origen de eventos de SugarCRM en la interfaz de usuario
description: Aprenda a crear una conexión de origen de eventos de SugarCRM mediante la interfaz de usuario de Adobe Experience Platform.
source-git-commit: 17d8a6517686ee2459955f766d75980b41851320
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# (Beta) Cree un [!DNL SugarCRM Events] conexión de origen en la interfaz de usuario

>[!NOTE]
>
>La variable [!DNL SugarCRM Events] el origen está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Este tutorial proporciona los pasos para crear un [!DNL SugarCRM Events] conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL SugarCRM] cuenta, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar las credenciales necesarias

Para conectarse [!DNL SugarCRM Events] en Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `Host` | El extremo de la API de SugarCRM al que se conecta el origen. | `developer.salesfusion.com` |
| `Username` | El nombre de usuario de su cuenta de desarrollador de SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | La contraseña de su cuenta de desarrollador de SugarCRM. | `123456789` |

### Crear un esquema de Platform para [!DNL SugarCRM]

Antes de crear una [!DNL SugarCRM] conexión de origen, también debe asegurarse de crear primero un esquema de Platform para utilizarlo con el origen. Consulte el tutorial en [creación de un esquema de Platform](../../../../../xdm/schema/composition.md) para ver los pasos completos sobre cómo crear un esquema.

![Captura de pantalla de la interfaz de usuario de Platform que muestra un esquema de ejemplo para SugarCRM Events](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Al asignar el esquema, asegúrese de que también asigna la variable obligatoria `event_id` y `timestamp` campos requeridos por Platform.

## Conecte su [!DNL SugarCRM Events] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el *CRM* categoría, seleccione **[!UICONTROL Eventos de SugarCRM]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![Captura de pantalla de la interfaz de usuario de Platform para el catálogo con la tarjeta SugarCRM Events](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

La variable **[!UICONTROL Conectar cuenta de eventos de SugarCRM]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL SugarCRM Events] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Captura de pantalla de la interfaz de usuario de Platform para la cuenta de eventos de Connect SugarCRM con una cuenta existente](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![Captura de pantalla de la interfaz de usuario de Platform para la cuenta de eventos de Connect SugarCRM con una cuenta nueva](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL SugarCRM Events] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).

## Recursos adicionales

Las secciones a continuación proporcionan recursos adicionales a los que puede hacer referencia al utilizar la variable [!DNL SugarCRM] fuente.

### Límites de protección  {#guardrails}

La variable [!DNL SugarCRM] Las tasas de aceleración de la API son de 90 llamadas por minuto o 2000 llamadas al día, lo que suceda primero. Sin embargo, esta restricción se ha eludido añadiendo un parámetro en la especificación de conexión que retrasará el tiempo de solicitud para que el límite de velocidad nunca se alcance.

### Validación {#validation}

Para validar que ha configurado correctamente el origen y [!DNL SugarCRM Events] se están incorporando los datos, siga los pasos a continuación:

* En la interfaz de usuario de Platform, seleccione **[!UICONTROL Ver flujos de datos]** al lado del [!DNL SugarCRM Events] en el catálogo de fuentes. A continuación, seleccione **[!UICONTROL Vista previa del conjunto de datos]** para verificar los datos introducidos.

* Según el tipo de objeto con el que esté trabajando, puede verificar los datos agregados con los recuentos visibles en la variable [!DNL SugarMarket] Página Eventos a continuación:

![Captura de pantalla de la página Cuentas de SugarMarket que muestra la lista de cuentas](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>La variable [!DNL SugarMarket] las páginas no incluyen los recuentos de objetos eliminados. Sin embargo, los datos recuperados a través de esta fuente también incluirán el recuento eliminado, que se marcarán con un indicador eliminado.