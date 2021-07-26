---
keywords: Experience Platform;inicio;temas populares;Amazon Redshift;amazon redshift;Redshift;redshift
solution: Experience Platform
title: Crear una conexión de origen de Amazon Redshift en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen Amazon Redshift utilizando la interfaz de usuario de Adobe Experience Platform.
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: 600b216932a7d19440534c4b190fb2f3766c8785
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Amazon Redshift] en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Amazon Redshift] (en adelante denominado &quot;[!DNL Redshift]&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Redshift] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta [!DNL Redshift] en [!DNL Platform], debe proporcionar los siguientes valores:

| **Credencial** | **Descripción** |
| -------------- | --------------- |
| `server` | El servidor asociado a su cuenta [!DNL Redshift]. |
| `username` | El nombre de usuario asociado a su cuenta [!DNL Redshift]. |
| `password` | La contraseña asociada a su cuenta [!DNL Redshift]. |
| `database` | La base de datos [!DNL Redshift] a la que está accediendo. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Conecte su cuenta [!DNL Redshift]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Redshift] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Orígenes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Orígenes]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]**, seleccione **[!UICONTROL Amazon Redshift]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector [!DNL Redshift].

![](../../../../images/tutorials/create/redshift/catalog.png)

Aparece la página **[!UICONTROL Connect to Amazon Redshift]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL Redshift]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![](../../../../images/tutorials/create/redshift/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Redshift] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/redshift/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Redshift]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
