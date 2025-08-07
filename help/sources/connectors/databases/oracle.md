---
title: Información general sobre el conector Oracle DB Source
description: Obtenga información sobre cómo conectar Oracle a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# [!DNL Oracle DB]

[!DNL Oracle DB] es un poderoso sistema de administración de bases de datos relacionales desarrollado por [!DNL Oracle Corporation]. Puede usar [!DNL Oracle DB] para almacenar, administrar y recuperar grandes volúmenes de datos estructurados de forma eficaz y segura.

Utilice el origen [!DNL Oracle DB] en el catálogo de orígenes de Adobe Experience Platform para conectar la base de datos e introducir datos en Experience Platform.

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para completar la configuración de requisitos previos antes de conectar su cuenta de [!DNL Oracle DB] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Debe agregar direcciones IP específicas de la región a la lista de permitidos antes de conectar las fuentes a Experience Platform en Azure o Amazon Web Service (AWS). Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform en Azure y AWS](../../ip-address-allow-list.md).

### Autenticar en Experience Platform en Azure {#azure}

Proporcione una cadena de conexión para autenticar y conectar su cuenta de [!DNL Oracle DB] a Experience Platform en Azure.

| Credencial | Descripción |
| --- | --- |
| Cadena de conexión | Una cadena de conexión es una cadena de texto que utilizan las aplicaciones para conectarse a una base de datos. El patrón de cadena de conexión [!DNL Oracle DB] es: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| ID de especificación de conexión | El ID de especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El id. de especificación de conexión para [!DNL Oracle] es `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

### Autenticar en Experience Platform en Amazon Web Service {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Proporcione valores para las siguientes credenciales a fin de autenticar y conectar su cuenta de [!DNL Oracle DB] a Experience Platform en AWS.

| Credencial | Descripción |
| --- | --- |
| Servidor | Dirección IP o nombre de host del servidor [!DNL Oracle DB]. |
| Puerto | Número de puerto del servidor de la base de datos. El número de puerto predeterminado es `1521`. |
| Nombre de usuario | Cuenta de usuario [!DNL Oracle DB] utilizada para autenticar y obtener acceso a la base de datos. |
| Contraseña | La clave secreta asociada a su nombre de usuario, utilizada para la autenticación. |
| Base de datos | Instancia de base de datos [!DNL Oracle] específica a la que desea conectarse. |
| Esquema | Contenedor de objetos de base de datos, como tablas, vistas o procedimientos. |
| Modo SSL | Un valor booleano que controla si SSL se aplica o no. Esta configuración depende de la compatibilidad con el servidor y el valor predeterminado es `false`. |
| ID de especificación de conexión | El ID de especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El id. de especificación de conexión para [!DNL Oracle] es `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |


## Conectar [!DNL Oracle] a [!DNL Experience Platform] mediante API

- [Conexión de Oracle DB mediante la API de Flow Service](../../tutorials/api/create/databases/oracle.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Oracle] a [!DNL Experience Platform] mediante la interfaz de usuario

- [Conecte Oracle DB mediante el espacio de trabajo de la IU de Experience Platform.](../../tutorials/ui/create/databases/oracle.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
