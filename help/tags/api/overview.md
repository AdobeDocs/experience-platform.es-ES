---
title: Guía de la API de Reactor
description: La API de Reactor permite a los desarrolladores administrar mediante programación todos los recursos para etiquetas en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 95%

---

# Guía de la API de [!DNL Reactor]

La API de Reactor proporciona varios extremos que le permiten administrar mediante programación todos los recursos para etiquetas en Adobe Experience Platform.

Estos extremos se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para conocer información importante sobre cómo autenticarse en la API.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [Referencia de la API de Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/).

## Compañías

Una compañía representa la organización de un usuario de etiquetas, normalmente un negocio. Estas compañías coinciden 1:1 con los ID de organización de IMS. Los usuarios de API solo tendrán visibilidad de las empresas a las que tienen acceso.

Consulte la [guía de extremo de compañías](./endpoints/companies.md) para obtener información sobre cómo ver las empresas disponibles en la API.

## Propiedades

Una propiedad es un contenedor que contiene la mayoría de los otros recursos disponibles en la API de Reactor. Los únicos recursos que no pertenecen a una propiedad son eventos de auditoría, compañías, paquetes de extensión y perfiles. Una propiedad pertenece a exactamente una compañía y una compañía puede tener muchas propiedades.

Consulte la [guía de extremo de propiedades](./endpoints/properties.md) para obtener información sobre cómo administrar propiedades en la API.

## Elementos de datos

Un elemento de datos funciona como una variable que apunta a un fragmento importante de datos dentro de la aplicación. Los elementos de datos se utilizan en las reglas y configuraciones de extensión. Cuando la regla se activa durante la ejecución en un explorador o una aplicación, el valor del elemento de datos se resuelve y se utiliza dentro de la regla.

Consulte la [guía de extremo de elementos de datos](./endpoints/data-elements.md) para obtener información sobre cómo administrar los elementos de datos en la API.

## Reglas

Las reglas controlan el comportamiento de los recursos contenidos en una biblioteca implementada. Una regla es un grupo de uno o más componentes de regla y existe para unirlos de una manera lógica.

Consulte la [guía de extremo de reglas](./endpoints/rules.md) para obtener información sobre cómo administrar reglas en la API.

## Regla componentes

Los componentes de regla son elementos individuales que constituyen una regla. Los componentes de regla tienen tres tipos básicos:

* **Eventos**: Lo que activa una regla
* **Condiciones**: Lo que comprueba la regla para determinar una acción
* **Acciones**: Lo que ejecuta la regla en función de si se cumple la condición

Consulte la [guía de extremo de reglas](./endpoints/rules.md) para obtener información sobre cómo administrar reglas en la API.

## Paquetes de extensiones

Un paquete de extensión representa una agrupación de funcionalidades individuales que se pueden poner a disposición de un usuario de etiquetas. Normalmente, estas funcionalidades se presentan en forma de componentes de regla y elementos de datos, pero también pueden incluir módulos principales y módulos compartidos. Las funcionalidades proporcionadas por un paquete de extensión se instalan como una extensión cuando se incluyen en una biblioteca.

Consulte la [guía de extremo de paquetes de extensiones](./endpoints/extension-packages.md) para obtener información sobre cómo administrar paquetes de extensiones en la API.

## Extensiones

Una extensión representa la instancia instalada de un paquete de extensión. Una extensión hace que las funciones definidas por un paquete de extensión estén disponibles para una propiedad. Estas funciones se aprovechan al crear elementos de datos y componentes de reglas.

Consulte la [guía de extremo de extensiones](./endpoints/extensions.md) para obtener información sobre cómo administrar las extensiones en la API.

## Bibliotecas

Una biblioteca es una colección de recursos (extensiones, reglas y elementos de datos) que representan el comportamiento deseado de una propiedad. Las bibliotecas se compilan en compilaciones y estas se asignan a diferentes entornos a medida que descienden en el flujo de publicación de las pruebas a la producción.

Consulte la [guía de extremo de bibliotecas](./endpoints/libraries.md) para obtener información sobre cómo administrar bibliotecas en la API.

## Versiones

Una biblioteca de etiquetas se compila en una compilación para que se asigne a un entorno y realizar pruebas e implementaciones. El contenido de una compilación varía en función de los recursos incluidos en la biblioteca, la configuración del entorno al que se asigna la compilación y la plataforma de la propiedad a la que pertenece la compilación.

Consulte la [guía de extremo de compilaciones](./endpoints/builds.md) para aprender a administrar compilaciones en la API.

## Entornos

Un entorno indica el host específico en el que se puede implementar una compilación y si la compilación debe implementarse como un conjunto de archivos o comprimirse en un formato de archivo. En la API de Reactor, los entornos son independientes de los propios hosts, que son administrados por el extremo `/hosts`.

Consulte la [guía de extremo de compilaciones](./endpoints/builds.md) para aprender a administrar compilaciones en la API.

## Hosts

Un host representa un destino alojado en el que se puede entregar una compilación de biblioteca y, finalmente, implementarse. Los hosts pueden ser servidores Akamai o SFTP.

Consulte la [guía de extremo de hosts](./endpoints/hosts.md) para obtener información sobre cómo administrar los hosts en la API.

## Configuraciones de aplicaciones

Las configuraciones de aplicación permiten almacenar y recuperar las credenciales para usarlas más adelante. Consulte la [guía de extremo de las configuraciones de aplicación](./endpoints/app-configurations.md) para obtener información sobre cómo administrar las configuraciones de aplicación en la API.

## Eventos de auditoría

Un evento de auditoría es un registro de un cambio específico a otro recurso de etiquetas, generado en el momento en que se realiza el cambio. Estos son eventos del sistema a los que se puede suscribir mediante el uso de una función de llamada de retorno.

Consulte la [guía de extremo de eventos de auditoría](./endpoints/audit-events.md) para obtener información sobre cómo administrar eventos de auditoría en la API.

## Llamadas

Una llamada de retorno es un mensaje que Platform envía a un host de URL cada vez que se genera un nuevo evento de auditoría. Consulte la [guía de extremo de llamadas de retorno](./endpoints/callbacks.md) para obtener información sobre cómo administrar las llamadas de retorno en la API.

## Notas

Las notas son anotaciones textuales que se pueden añadir a determinados recursos de etiquetas, como elementos de datos, extensiones, bibliotecas, propiedades, reglas y componentes de reglas. Consulte la [guía de extremo de notas](./endpoints/notes.md) para obtener información sobre cómo administrar las notas en la API.

## Perfil

Un perfil contiene toda la información acerca del usuario que ha iniciado sesión, incluidas todas las organizaciones de Adobe a las que pertenece, los perfiles de producto a los que pertenece dentro de cada organización y los derechos que tiene de cada perfil de producto.

Consulte la [guía de extremo de perfil](./endpoints/profile.md) para obtener información sobre cómo ver esta información en la API.

## Buscar

El extremo `/search` proporciona una forma de encontrar recursos que coincidan con un criterio deseado, expresado como consulta. Todas las consultas están enfocadas a su compañía y propiedades accesibles actuales. Consulte la [guía de extremo de búsqueda](./endpoints/search.md) para conocer cómo utilizar esta funcionalidad.

## Secretos

Un secreto contiene credenciales que permiten al reenvío de eventos autenticarse en otro sistema para un intercambio de datos seguro. Consulte la [guía de secretos](./guides/secrets.md) para obtener información general sobre cómo funcionan los secretos en el reenvío de eventos, y la [guía de extremo de secretos](./endpoints/secrets.md) para obtener información sobre cómo administrarlos en la API de Reactor.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de Registro de esquemas, lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos.
