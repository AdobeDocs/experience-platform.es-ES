---
title: Información general sobre la publicación
description: Obtenga información acerca del proceso de publicación de cambios en las bibliotecas de códigos de administración de etiquetas en Adobe Experience Platform.
exl-id: 32eaad87-d7dc-4812-b546-a136511512fe
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 96%

---

# Información general sobre la publicación

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Adobe Experience Platform permite encapsular los cambios realizados en el código de gestión de etiquetas en las bibliotecas individuales. Dado que ahora diferentes equipos pueden desarrollar varias bibliotecas en paralelo, estas deben seguir un proceso deliberado y autorizado para combinar los cambios antes de insertarse en el entorno de producción.

En un nivel básico, cada biblioteca se somete al siguiente proceso de publicación:

1. Cree una nueva biblioteca (o edite una existente) en un entorno de desarrollo.
1. Compruebe la funcionalidad de la biblioteca en un entorno de ensayo cuando sea necesario.
1. Implemente la biblioteca en el entorno de producción.

Piense en una situación en la que crea un nuevo evento de cierre de compra, crea un elemento de datos de ingresos relacionado con ese evento y realiza un cambio en la configuración de la extensión de Adobe Analytics para que se admita el nuevo evento y el elemento de datos. Puede incluir todos estos cambios en una nueva biblioteca y utilizar el proceso de publicación para probarlos, aprobarlos y publicarlos como una sola unidad.

Encontrará amplia información general sobre el flujo de trabajo de publicación de bibliotecas, incluidos detalles sobre cómo heredan las bibliotecas los recursos de las compilaciones de flujo ascendente en función de su estado de publicación, en la [guía del flujo de publicación](./publishing-flow.md).

Además del flujo de publicación, existen varios componentes y relaciones que conviene comprender para desarrollar y publicar sus bibliotecas de forma eficaz. La tabla siguiente describe cada uno de estos conceptos clave y proporciona vínculos a la documentación para que tenga más información de cada uno:

| Componente | Descripción |
| --- | --- |
| Bibliotecas | Una biblioteca es un conjunto de instrucciones que indican cómo interactúan las extensiones, los elementos de datos y las reglas entre sí y con el sitio web. Cuando se compila una biblioteca para implementarla en un entorno, esa biblioteca se convierte en una compilación.<br><br>Consulte la descripción general sobre [bibliotecas](./libraries.md) para saber cómo crear, administrar y activar bibliotecas en la IU. |
| Versiones | Una compilación es una biblioteca compilada. Cuando se implementa en un entorno, una compilación proporciona el conjunto real de archivos que contienen el código que se entrega al explorador de cada usuario cuando este realiza la vista del sitio.<br><br>Consulte la información general sobre [compilaciones](./builds.md) para saber más sobre el contenido y el formato de las compilaciones. |
| Entornos | Un entorno de etiqueta es un conjunto de instrucciones de implementación que indica a Platform en qué formato desea compilar y a dónde desea enviar dicha compilación.<br><br>Consulte la información general sobre [entornos](./environments.md) para conocer los distintos tipos de entornos, cómo instalar y configurar entornos existentes, y cómo crear nuevos entornos. |
| Hosts | Un host representa los detalles de conexión de un entorno para enviar una compilación al sitio web. Puede optar por que Adobe administre el alojamiento de su compilación o puede proporcionar información para sus propios servidores host.<br><br>Consulte la información general sobre [hosts](./hosts/hosts-overview.md) para conocer todas las opciones de alojamiento. |
| Código del lado del cliente | El código del lado del cliente es el conjunto de secuencias de comandos que se coloca en el código fuente del sitio o de la aplicación y que indica a cada dispositivo cliente dónde recuperar la compilación. El código se adjunta a un entorno y puede cambiarse al realizar cambios en la configuración del entorno.<br><br>Consulte la sección sobre [incrustar código](./environments.md#embed-code) en la descripción general de entornos para obtener más información. |

## Pasos siguientes

Este documento proporciona una visión general de los diversos componentes relacionados con la publicación de bibliotecas de etiquetas en Adobe Experience Platform. Consulte la documentación relacionada con esta guía para obtener más información sobre el proceso de publicación en detalle.
