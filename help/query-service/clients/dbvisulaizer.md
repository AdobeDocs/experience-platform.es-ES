---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;Db Visualizer;DbVisualizer;db visualizer;conectarse al servicio de consultas;
solution: Experience Platform
title: Conectar DbVisualizer al servicio de consultas
description: Este documento explica los pasos para conectar DbVisualizer con el servicio de consultas de Adobe Experience Platform.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# Connect [!DNL DbVisualizer] hasta [!DNL Query Service] {#connect-dbvisualizer}

Este documento describe los pasos para conectar el [!DNL DbVisualizer] herramienta de base de datos con Adobe Experience Platform [!DNL Query Service].

## Primeros pasos

Esta guía requiere que ya tenga acceso a [!DNL DbVisualizer] y están familiarizados con cómo navegar por su interfaz. Para descargar [!DNL DbVisualizer] para obtener más información, consulte la [funcionario [!DNL DbVisualizer] documentación](https://www.dbvis.com/download/).

Para adquirir las credenciales necesarias para la conexión [!DNL  DbVisualizer] Para acceder al Experience Platform, debe tener acceso al espacio de trabajo Consultas en la interfaz de usuario de Platform. Póngase en contacto con el administrador de su organización si actualmente no tiene acceso al área de trabajo Consultas.

## Crear una conexión de base de datos {#connect-database}

Una vez instalada la aplicación de escritorio en el equipo local, siga las instrucciones oficiales de BDVisualizer para [crear una nueva conexión de base de datos](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Una vez que haya seleccionado **[!DNL PostgreSQL]** desde el [!DNL Connections] lista, una [!DNL Object View] para el nuevo [!DNL PostgreSQL] aparece la conexión.

### Establecer las propiedades del controlador para la conexión {#properties}

Desde el [!DNL PostgreSQL] pestaña vista de objetos, seleccione **[!DNL Properties]** , seguido de la pestaña **[!DNL Driver Properties]** desde la barra lateral de navegación. Más información sobre [propiedades del controlador](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) se puede encontrar en la documentación oficial.

A continuación, introduzca las propiedades del controlador descritas en la tabla siguiente.

>[!IMPORTANT]
>
>Para conectar DBVisualizer con Adobe Experience Platform, debe habilitar el uso de SSL. Consulte la [Documentación de modos SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad de SSL para conexiones de terceros con Adobe Experience Platform Query Service y cómo conectarse mediante `verify-full` Modo SSL.

| Propiedad | Descripción |
| ------ | ------ |
| `PGHOST` | El nombre de host del [!DNL PostgreSQL] servidor. Este valor es su Experience Platform **[!UICONTROL Host] credencial**. |
| `ssl` | Definición del valor SSL `1` para habilitar el uso de SSL. |
| `sslmode` | Controla el nivel de protección SSL. Se recomienda utilizar el `require` Modo SSL al conectar clientes de terceros a Adobe Experience Platform. El `require` El modo garantiza que se requiere cifrado en todas las comunicaciones y que la red es de confianza para conectarse al servidor correcto. No se requiere la validación del certificado SSL del servidor. |
| `user` | El nombre de usuario conectado a la base de datos es su ID de organización. Es una cadena alfanumérica que termina en `@Adobe.Org`. Este valor es su Experience Platform **[!UICONTROL Nombre de usuario] credencial**. |

Utilice la barra de búsqueda para buscar cada propiedad y, a continuación, seleccione la celda correspondiente para el valor del parámetro. La celda se resaltará en azul. Introduzca sus credenciales de plataforma en el campo value y seleccione **[!DNL Apply]** para agregar la propiedad driver.

>[!NOTE]
>
>Para agregar un segundo `user` perfil, seleccione `user` en la columna parameter, seleccione el icono azul + (más) para añadir credenciales a cada usuario. Seleccionar **[!DNL Apply]** para agregar la propiedad driver.

El [!DNL Edited] La columna muestra una marca de verificación para indicar que el valor del parámetro se ha actualizado.

### Credenciales del servicio de consulta de entrada {#query-service-credentials}

Para encontrar las credenciales necesarias para conectar BBVisualizer con el servicio de consultas, inicie sesión en la interfaz de usuario de Platform y seleccione **[!UICONTROL Consultas]** desde el panel de navegación izquierdo, seguido de **[!UICONTROL Credenciales]**. Para obtener más información sobre cómo encontrar su **host**, **puerto**, **database**, **nombre de usuario**, y **contraseña** credenciales, lea la [guía de credenciales](../ui/credentials.md).

![La página Credenciales del espacio de trabajo Consultas del Experience Platform con las credenciales y las credenciales caducadas resaltadas.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] también ofrece credenciales que no caducan para permitir una configuración única con clientes de terceros. Consulte la documentación de [instrucciones completas sobre cómo generar y utilizar credenciales que no caducan](../ui/credentials.md#non-expiring-credentials). Es necesario completar este proceso si desea conectar BDVisualizer como una configuración única. El `credential` y `technicalAccountId` Los valores adquiridos comprenden el valor del visualizador DBV `password` parámetro.

## Autenticación {#authentication}

Para requerir un ID de usuario y una autenticación basada en contraseña cada vez que se establece una conexión, vaya al [!DNL Properties] y seleccione **[!DNL Authentication]** desde la barra lateral de navegación debajo de [!DNL PostgreSQL].

En el panel Autenticación de conexión, compruebe ambas opciones: **[!DNL Require Userid]** y **[!DNL Require Password]** marque las casillas y seleccione **[!DNL Apply]**. Más información sobre [configurar opciones de autenticación](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) se puede encontrar en la documentación oficial.

## Conectar con Platform

Puede establecer una conexión con credenciales que caducan o no caducan. Para establecer una conexión, seleccione la **[!DNL Connection]** de la pestaña [!DNL PostgreSQL] Ficha Vista de objetos e introduzca sus credenciales de Experience Platform para la siguiente configuración. Instrucciones complementarias para [configuración de una conexión manual](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) están disponibles en el sitio web oficial de DBVisualizer.

>[!NOTE]
>
>Todas las credenciales requeridas por BDVisualizer en la tabla siguiente son las mismas para las credenciales que caducan y no caducan a menos que se indique en la descripción del parámetro.

| Parámetro de conexión | Descripción |
|---|---|
| **[!UICONTROL Nombre]** | Cree un nombre para la conexión. Se recomienda proporcionar un nombre descriptivo para reconocer la conexión. |
| **[!UICONTROL Servidor de base de datos]** | Este es su Experience Platform **[!UICONTROL Host]** credencial. |
| **[!UICONTROL Puerto de base de datos]** | El puerto para [!DNL Query Service]. Debe utilizar el puerto **80** o **5432** para conectar con [!DNL Query Service]. |
| **[!UICONTROL Base de datos]** | Use su Experience Platform **[!UICONTROL Base de datos]** valor de credencial: `prod:all`. |
| **[!UICONTROL Userid de base de datos]** | Este es su ID de organización de Platform Use su Experience Platform **[!UICONTROL Nombre de usuario]** valor de credencial. El ID tendrá el formato de `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Contraseña de base de datos]** | Esta cadena alfanumérica es su Experience Platform **[!UICONTROL Contraseña]** credencial. Si desea utilizar credenciales que no caduquen, este valor son los argumentos concatenados del `technicalAccountID` y el `credential` descargado en el archivo JSON de configuración. El valor de la contraseña adopta la forma siguiente: {technicalAccountId}:{credential}. El archivo JSON de configuración para credenciales que no caducan es una descarga única durante su inicialización de la que la Adobe no conserva una copia. |

Después de introducir todas las credenciales relevantes, seleccione **[!DNL Connect]**.

El [!DNL Connect] el diálogo aparece en la primera ocasión del período de sesiones. Introduzca su ID de usuario y contraseña y seleccione **[!DNL Connect]**. Aparece un mensaje en el registro para confirmar que la conexión se ha realizado correctamente.

## Pasos siguientes

Ahora que se ha conectado [!DNL DbVisualizer] con [!DNL Query Service], puede utilizar [!DNL DbVisualizer] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la [guía de ejecución de consultas](../best-practices/writing-queries.md).
