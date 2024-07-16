---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;Db Visualizer;DbVisualizer;db visualizer;conectarse al servicio de consultas;
solution: Experience Platform
title: Conectar DbVisualizer al servicio de consultas
description: Este documento explica los pasos para conectar DbVisualizer con el servicio de consultas de Adobe Experience Platform.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# Conectar [!DNL DbVisualizer] a [!DNL Query Service] {#connect-dbvisualizer}

Este documento describe los pasos para conectar la herramienta de base de datos [!DNL DbVisualizer] con Adobe Experience Platform [!DNL Query Service].

## Introducción

Esta guía requiere que ya tenga acceso a la aplicación de escritorio [!DNL DbVisualizer] y que esté familiarizado con la forma de navegar por su interfaz. Para descargar la aplicación de escritorio [!DNL DbVisualizer] o para obtener más información, consulte la [documentación oficial [!DNL DbVisualizer] 3}.](https://www.dbvis.com/download/)

Para adquirir las credenciales necesarias para conectar [!DNL  DbVisualizer] al Experience Platform, debe tener acceso al área de trabajo Consultas en la interfaz de usuario de Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso al área de trabajo Consultas.

## Crear una conexión de base de datos {#connect-database}

Una vez que haya instalado la aplicación de escritorio en el equipo local, siga las instrucciones oficiales de BDVisualizer para [crear una nueva conexión de base de datos](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Una vez que haya seleccionado **[!DNL PostgreSQL]** de la lista [!DNL Connections], aparecerá una ficha [!DNL Object View] para la nueva conexión [!DNL PostgreSQL].

### Establecer las propiedades del controlador para la conexión {#properties}

En la ficha [!DNL PostgreSQL] vista de objeto, seleccione la ficha **[!DNL Properties]**, seguida de **[!DNL Driver Properties]** en la barra lateral de navegación. Encontrará más información sobre [propiedades del controlador](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) en la documentación oficial.

A continuación, introduzca las propiedades del controlador descritas en la tabla siguiente.

>[!IMPORTANT]
>
>Para conectar DBVisualizer con Adobe Experience Platform, debe habilitar el uso de SSL. Consulte la [documentación sobre los modos SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad de SSL para conexiones de terceros al servicio Adobe Experience Platform Query y cómo conectarse mediante el modo SSL `verify-full`.

| Propiedad | Descripción |
| ------ | ------ |
| `PGHOST` | Nombre de host del servidor [!DNL PostgreSQL]. Este valor es su credencial de Experience Platform **[!UICONTROL Host]**. |
| `ssl` | Defina el valor SSL `1` para habilitar el uso de SSL. |
| `sslmode` | Controla el nivel de protección SSL. Se recomienda utilizar el modo SSL `require` al conectar clientes de terceros a Adobe Experience Platform. El modo `require` garantiza que se requiere cifrado en todas las comunicaciones y que se confía en la red para conectarse al servidor correcto. No se requiere la validación del certificado SSL del servidor. |
| `user` | El nombre de usuario conectado a la base de datos es su ID de organización. Es una cadena alfanumérica que termina en `@Adobe.Org`. Este valor es su credencial de Experience Platform **[!UICONTROL nombre de usuario]**. |

Utilice la barra de búsqueda para buscar cada propiedad y, a continuación, seleccione la celda correspondiente para el valor del parámetro. La celda se resaltará en azul. Escriba su credencial de plataforma en el campo de valor y seleccione **[!DNL Apply]** para agregar la propiedad del controlador.

>[!NOTE]
>
>Para agregar un segundo perfil `user`, seleccione `user` en la columna de parámetros y, a continuación, seleccione el icono azul + (más) para agregar credenciales a cada usuario. Seleccione **[!DNL Apply]** para agregar la propiedad del controlador.

La columna [!DNL Edited] muestra una marca de verificación para indicar que el valor del parámetro se ha actualizado.

### Credenciales del servicio de consulta de entrada {#query-service-credentials}

Para encontrar las credenciales necesarias para conectar BBVisualizer con Query Service, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** en el panel de navegación izquierdo, seguido de **[!UICONTROL Credenciales]**. Para obtener más información sobre cómo encontrar las credenciales de **host**, **puerto**, **base de datos**, **nombre de usuario** y **contraseña**, lea la [guía de credenciales](../ui/credentials.md).

![Se resaltaron la página Credenciales del área de trabajo Consultas de Experience Platform con las credenciales y las credenciales que caducan.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación para obtener [instrucciones completas sobre cómo generar y utilizar credenciales que no caducan](../ui/credentials.md#non-expiring-credentials). Es necesario completar este proceso si desea conectar BDVisualizer como una configuración única. Los valores `credential` y `technicalAccountId` adquiridos comprenden el valor del parámetro DBVisualizer `password`.

## Autenticación {#authentication}

Para requerir un identificador de usuario y una autenticación basada en contraseña cada vez que se establece una conexión, vaya a la pestaña [!DNL Properties] y seleccione **[!DNL Authentication]** en la barra lateral de navegación bajo [!DNL PostgreSQL].

En el panel Autenticación de conexión, marque las casillas de verificación **[!DNL Require Userid]** y **[!DNL Require Password]** y luego seleccione **[!DNL Apply]**. Encontrará más información sobre [configurar opciones de autenticación](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) en la documentación oficial.

## Conectar con Platform

Puede establecer una conexión con credenciales que caducan o no caducan. Para establecer una conexión, seleccione la ficha **[!DNL Connection]** en la ficha de vista de objetos [!DNL PostgreSQL] e introduzca sus credenciales de Experience Platform para la siguiente configuración. Las instrucciones complementarias para [configurar una conexión manual](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) están disponibles en el sitio web oficial de DBVisualizer.

>[!NOTE]
>
>Todas las credenciales requeridas por BDVisualizer en la tabla siguiente son las mismas para las credenciales que caducan y no caducan a menos que se indique en la descripción del parámetro.

| Parámetro de conexión | Descripción |
|---|---|
| **[!UICONTROL Nombre]** | Cree un nombre para la conexión. Se recomienda proporcionar un nombre descriptivo para reconocer la conexión. |
| **[!UICONTROL Servidor de base de datos]** | Esta es su credencial de Experience Platform **[!UICONTROL Host]**. |
| **[!UICONTROL Puerto de base de datos]** | El puerto de [!DNL Query Service]. Debe usar el puerto **80** o **5432** para conectarse con [!DNL Query Service]. |
| **[!UICONTROL Database]** | Use su valor de credencial de Experience Platform **[!UICONTROL Database]**: `prod:all`. |
| **[!UICONTROL Id. de usuario de base de datos]** | Este es su ID de organización de Platform Use su valor de credencial de Experience Platform **[!UICONTROL Username]**. El id. tendrá el formato `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Contraseña de base de datos]** | Esta cadena alfanumérica es su credencial de Experience Platform **[!UICONTROL Password]**. Si desea utilizar credenciales que no caduquen, este valor son los argumentos concatenados de `technicalAccountID` y `credential` descargados en el archivo JSON de configuración. El valor de contraseña adopta la forma: {technicalAccountId}:{credential}. El archivo JSON de configuración para credenciales que no caducan es una descarga única durante su inicialización de la que la Adobe no conserva una copia. |

Una vez que haya escrito todas las credenciales relevantes, seleccione **[!DNL Connect]**.

El cuadro de diálogo [!DNL Connect] aparece en la primera ocasión de la sesión. Escriba su Id. de usuario y contraseña y seleccione **[!DNL Connect]**. Aparece un mensaje en el registro para confirmar que la conexión se ha realizado correctamente.

## Pasos siguientes

Ahora que ha conectado [!DNL DbVisualizer] con [!DNL Query Service], puede usar [!DNL DbVisualizer] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía sobre la ejecución de consultas](../best-practices/writing-queries.md).
