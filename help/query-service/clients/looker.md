---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar con el buscador
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Conectar con el buscador

Para conectar Looker con el servicio de Consulta de Adobe en la plataforma Adobe Experience, siga los pasos a continuación:

Después de iniciar sesión en el buscador, haga clic en **Administrador**, seguido de **Conexiones**.

![](../images/clients/looker/click-admin-connections.png)

En esta página, haga clic en **Nueva conexión**.

![](../images/clients/looker/click-new-connection.png)

Desde aquí puede completar los detalles de la Configuración de conexión.

![](../images/clients/looker/new-connection.png)

- **Nombre:** Nombre de la conexión.
- **Dialect:** El dialecto utilizado para la base de datos SQL. El servicio de Consulta utiliza **PostgreSQL**.
- **Host y puerto:** El extremo del host y su puerto para el servicio de Consulta.
- **Base de datos:** Base de datos que se utilizará.
- **Nombre de usuario y contraseña:** Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario tendrá la forma de `ORG_ID@AdobeOrg`.

>[!NOTE] Para obtener más información sobre cómo encontrar el host y el puerto, el nombre de la base de datos y las credenciales de inicio de sesión, visite la página de [credenciales en la plataforma](https://platform.adobe.com/query/configuration). Para buscar las credenciales, inicie sesión en Plataforma, haga clic en **Consultas** y, a continuación, haga clic en **Credenciales**.

Después de introducir los detalles de la conexión, haga clic en **Probar esta configuración** para asegurarse de que las credenciales funcionan correctamente. Si lo hacen, a continuación aparecerá un mensaje que indica que puede conectarse. Si la conexión es correcta, haga clic en **Añadir conexión** para crear la conexión.

![](../images/clients/looker/click-test-connection.png)

## Pasos siguientes

Ahora que se ha conectado con el servicio de Consulta, puede utilizar el buscador para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía de consultas [en ejecución](../creating-queries/creating-queries.md).