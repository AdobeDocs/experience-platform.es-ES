---
keywords: Experience Platform;inicio;temas populares;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Crear una conexión de origen de IBM DB2 en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen de IBM DB2 mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Crear una conexión de origen de IBM DB2 en la interfaz de usuario

>[!NOTE]
>
> El conector IBM DB2 está en versión beta. Consulte la [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen IBM DB2 (en adelante denominado &quot;DB2&quot;) mediante el uso de [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión DB2 válida, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a DB2 mediante el [!DNL Flow Service] API.

| Credencial | Descripción |
| ---------- | ----------- |
| `server` | Nombre del servidor DB2. Puede especificar el número de puerto después del nombre del servidor delimitado por dos puntos. Por ejemplo: server:port. |
| `database` | Nombre de la base de datos DB2. |
| `username` | El nombre de usuario utilizado para conectarse a la base de datos DB2. |
| `password` | La contraseña de la cuenta de usuario que especificó para el nombre de usuario. |

Para obtener más información sobre cómo empezar, consulte [este documento DB2](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Conecte su cuenta de IBM DB2

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de DB2 a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la **[!UICONTROL Fuentes]** espacio de trabajo. La variable **[!UICONTROL Catálogo]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccione **[!UICONTROL IBM DB2]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector DB2.

![catálogo](../../../../images/tutorials/create/ibm-db2/catalog.png)

La variable **[!UICONTROL Conexión a IBM DB2]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de DB2. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta DB2 con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/ibm-db2/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de DB2. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos [!DNL Platform]](../../dataflow/databases.md).
