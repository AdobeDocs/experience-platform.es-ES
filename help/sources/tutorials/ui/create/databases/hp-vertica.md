---
keywords: Experience Platform;inicio;temas populares;HP Vertica
solution: Experience Platform
title: Crear una conexión de origen HP Vertica en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen HP Vertica utilizando la interfaz de usuario de Adobe Experience Platform.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Crear una conexión de origen HP [!DNL Vertica] en la interfaz de usuario

>[!NOTE]
>
> El conector HP [!DNL Vertica] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona pasos para crear un conector de origen HP [!DNL Vertica] utilizando la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión HP [!DNL Vertica] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a HP [!DNL Vertica] mediante la API [!DNL Flow Service].

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a la instancia de HP [!DNL Vertica]. El patrón de cadena de conexión para HP [!DNL Vertica] es `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obtener más información sobre cómo empezar, consulte [este documento HP [!DNL Vertica] ](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## Conecte su cuenta de HP [!DNL Vertica]

Una vez que haya reunido sus credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de HP [!DNL Vertica] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Databases]**, seleccione **[!UICONTROL HP Vertica]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector HP [!DNL Vertica].

![catálogo](../../../../images/tutorials/create/hp-vertica/catalog.png)

Aparece la página **[!UICONTROL Connect to HP Vertica]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de HP [!DNL Vertica]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de HP [!DNL Vertica] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/hp-vertica/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de HP [!DNL Vertica]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
