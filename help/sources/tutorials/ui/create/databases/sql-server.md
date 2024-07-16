---
title: Crear una conexión de Microsoft SQL Server Source en la IU
description: Obtenga información sobre cómo crear una conexión de origen de Microsoft SQL Server mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Microsoft SQL Server] en la interfaz de usuario

Lea este tutorial para aprender a conectar su cuenta de [!DNL Microsoft SQL Server] a Adobe Experience Platform mediante la interfaz de usuario.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL SQL Server] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para conectarse a [!DNL SQL Server] en [!DNL Platform], debe proporcionar la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| Cadena de conexión | La cadena de conexión asociada a su cuenta de [!DNL Microsoft SQL Server]. El patrón de la cadena de conexión depende de si está utilizando un nombre de servidor o de instancia para el origen de datos:<ul><li>Cadena de conexión con nombre de servidor: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Cadena de conexión con nombre de instancia:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

Para obtener más información sobre cómo empezar, consulte [este [!DNL SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Conectar su cuenta de [!DNL SQL Server]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *Bases de datos*, seleccione **[!DNL Microsoft SQL Server]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con el origen de Microsoft SQL Server seleccionado.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con Microsoft SQL Server]**. En esta página, puede usar credenciales nuevas o existentes.

>[!BEGINTABS]

>[!TAB Crear una nueva cuenta]

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y proporciona un nombre, una descripción opcional y tus credenciales.

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta con los detalles de conexión de origen especificados y resaltados.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Usar una cuenta existente]

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta que desee usar del catálogo de cuentas existente.

Seleccione **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente que muestra una lista de las cuentas existentes.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL SQL Server]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
