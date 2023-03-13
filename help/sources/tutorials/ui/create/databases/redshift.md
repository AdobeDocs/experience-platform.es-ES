---
keywords: Experience Platform;inicio;temas populares;Amazon Redshift;amazon redshift;Redshift;redshift
solution: Experience Platform
title: Creación de una conexión de origen de Amazon Redshift en la IU
type: Tutorial
description: Aprenda a crear una conexión de origen de Amazon Redshift mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Crear un [!DNL Amazon Redshift] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Amazon Redshift] (en lo sucesivo, &quot;[!DNL Redshift]&quot;) utilizando el conector de origen [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Redshift] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para acceder a su [!DNL Redshift] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| **Credencial** | **Descripción** |
| -------------- | --------------- |
| `server` | El servidor asociado con su [!DNL Redshift] cuenta. |
| `username` | El nombre de usuario asociado con su [!DNL Redshift] cuenta. |
| `password` | La contraseña asociada a su [!DNL Redshift] cuenta. |
| `database` | El [!DNL Redshift] base de datos a la que accede. |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Conecte su [!DNL Redshift] account

>[!NOTE]
>
>El estándar de codificación predeterminado para [!DNL Redshift] es Unicode. Esto no se puede cambiar.

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Redshift] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL Amazon Redshift]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL Redshift] conector.

![](../../../../images/tutorials/create/redshift/catalog.png)

El **[!UICONTROL Conectar con Amazon Redshift]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Redshift] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/redshift/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Redshift] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/redshift/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Redshift] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
