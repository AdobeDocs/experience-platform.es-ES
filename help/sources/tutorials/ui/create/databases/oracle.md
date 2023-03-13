---
keywords: Experience Platform;inicio;temas populares;Oracle DB;oracle db
solution: Experience Platform
title: Creación de una conexión de origen de base de datos de Oracle en la IU
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de base de datos de Oracle mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Crear un [!DNL Oracle DB] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Oracle DB] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Oracle DB] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para acceder a su [!DNL Oracle DB] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Cadena de conexión utilizada para conectarse a [!DNL Oracle DB]. El [!DNL Oracle DB] el patrón de cadena de conexión es: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | El identificador único necesario para crear una conexión. Identificador de especificación de conexión para [!DNL Oracle DB] es `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

Para obtener más información sobre cómo empezar, consulte [este documento de Oracle](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199).

## Conecte su [!DNL Oracle DB] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Oracle DB] cuenta a la que conectarse [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL ORACLE DB]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL Oracle DB] conector.

![catalogar](../../../../images/tutorials/create/oracle/catalog.png)

El **[!UICONTROL Conectar con Oracle DB]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Oracle DB] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/oracle/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Oracle DB] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/oracle/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Oracle DB] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
