---
title: Crear una conexión de origen de Microsoft SQL Server en la IU
description: Obtenga información sobre cómo crear una conexión de origen de Microsoft SQL Server mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Crear un [!DNL Microsoft SQL Server] conexión de origen en la interfaz de usuario

Lea este tutorial para aprender a conectar su [!DNL Microsoft SQL Server] a Adobe Experience Platform mediante la interfaz de usuario de.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL SQL Server] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para conectarse a [!DNL SQL Server] el [!DNL Platform], debe proporcionar la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| Cadena de conexión | La cadena de conexión asociada a su [!DNL Microsoft SQL Server] cuenta. El patrón de la cadena de conexión depende de si está utilizando un nombre de servidor o de instancia para el origen de datos:<ul><li>Cadena de conexión con nombre de servidor: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Cadena de conexión con nombre de instancia:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Conecte su [!DNL SQL Server] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el *Bases de datos* categoría, seleccionar **[!DNL Microsoft SQL Server]**, y luego seleccione **[!UICONTROL Configuración de]**.

>[!TIP]
>
>Las fuentes del catálogo de fuentes muestran el **[!UICONTROL Configuración de]** cuando una fuente determinada aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Añadir datos]**.

![El catálogo de orígenes con el origen de Microsoft SQL Server seleccionado.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

El **[!UICONTROL Conectar con Microsoft SQL Server]** página. En esta página, puede usar credenciales nuevas o existentes.

>[!BEGINTABS]

>[!TAB Crear una nueva cuenta]

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y proporcione un nombre, una descripción opcional y sus credenciales.

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta con los detalles de la conexión de origen introducidos y resaltados.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Usar una cuenta existente]

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y, a continuación, seleccione la cuenta que desee utilizar en el catálogo de cuentas existente.

Seleccione **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente que muestra una lista de las cuentas existentes.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL SQL Server] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
