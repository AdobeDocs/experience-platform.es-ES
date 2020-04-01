---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar con Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Conectar con Aqua Data Studio

Este documento recorre los pasos para conectar Aqua Data Studio con el servicio de Consulta de la plataforma Adobe Experience.

Después de instalar Aqua Data Studio, primero debe registrar el servidor. En el menú principal, haga clic en **Servidor** y, a continuación, en **Registrar servidor**.

![](../images/clients/aqua-data-studio/register-server.png)

Aparece el cuadro de diálogo *Registrar servidor* . En la ficha *General* , seleccione **PostgreSQL** en la lista del lado izquierdo. En el cuadro de diálogo que aparece, proporcione los siguientes detalles para la configuración del servidor.

- **Nombre**: Nombre de la conexión.
- **Nombre de inicio de sesión y contraseña**: Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario adopta la forma de `ORG_ID@AdobeOrg`.
- **Host y puerto**: El extremo del host y su puerto para el servicio de Consulta.
- **Base de datos:** Base de datos que se utilizará.

>[!NOTE] Para obtener más información sobre cómo encontrar las credenciales de inicio de sesión, el host, el puerto y el nombre de la base de datos, visite la página de [credenciales en la plataforma](https://platform.adobe.com/query/configuration). Para buscar las credenciales, inicie sesión en Plataforma, haga clic en **Consultas** y, a continuación, haga clic en **Credenciales**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Select the **Driver** tab. En *Parámetros*, establezca el valor como `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Después de introducir los detalles de la conexión, haga clic en **Probar conexión** para asegurarse de que las credenciales funcionan correctamente. Si la conexión es correcta, haga clic en **Guardar** para registrar el servidor. La conexión aparece en el *Panel* tras registrarse correctamente, lo que confirma que ahora puede conectarse al servidor y realizar la vista de los objetos de esquema.

## Pasos siguientes

Ahora que se ha conectado al servicio de Consulta, puede utilizar el analizador *de* Consultas de Aqua Data Studio para ejecutar y editar sentencias SQL. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía de consultas [en ejecución](../creating-queries/creating-queries.md).