---
keywords: Experience Platform;inicio;temas populares;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Creación de una conexión de origen de IBM DB2 en la IU
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de IBM DB2 mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Crear una conexión de origen de IBM DB2 en la interfaz de usuario

>[!NOTE]
>
> El conector IBM DB2 está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen de IBM DB2 (en adelante, &quot;DB2&quot;) utilizando [!DNL Platform] interfaz de usuario.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión DB2 válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a DB2 utilizando [!DNL Flow Service] API.

| Credencial | Descripción |
| ---------- | ----------- |
| `server` | Nombre del servidor DB2. Puede especificar el número de puerto después del nombre del servidor delimitado por dos puntos. Por ejemplo: server:port. |
| `database` | Nombre de la base de datos DB2. |
| `username` | Nombre de usuario utilizado para conectarse a la base de datos DB2. |
| `password` | Contraseña de la cuenta de usuario especificada para el nombre de usuario. |

Para obtener más información sobre cómo empezar, consulte [este documento DB2](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Conectar su cuenta de IBM DB2

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta DB2 a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL IBM DB2]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector DB2.

![catalogar](../../../../images/tutorials/create/ibm-db2/catalog.png)

El **[!UICONTROL Conectar con IBM DB2]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de DB2. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/ibm-db2/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta DB2 con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/ibm-db2/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de DB2. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
