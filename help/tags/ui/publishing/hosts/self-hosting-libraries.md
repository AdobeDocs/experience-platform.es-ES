---
title: Bibliotecas de alojamiento propio
description: Aprenda a implementar el alojamiento propio para las compilaciones de su biblioteca de etiquetas en Adobe Experience Platform.
exl-id: 8c3bf202-de7a-46e0-801f-0cede24865fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 90%

---

# Bibliotecas de alojamiento propio

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Las etiquetas en Adobe Experience Platform permiten la producción de un conjunto de archivos llamados [compilación](../builds.md). Este conjunto de archivos controla el comportamiento de la aplicación en tiempo de ejecución.

Las compilaciones deben alojarse en alguna parte para que los dispositivos cliente puedan recuperarlas en el tiempo de ejecución según lo necesiten.

Experience Platform puede administrar el alojamiento de estos archivos por usted o puede hacerlo usted mismo.

## Administrado por Adobe {#managed-by-adobe}

Adobe no se ocupa del alojamiento web. Si decide que Adobe administre el alojamiento, las compilaciones se entregan a una red de distribución de contenido (CDN) de terceros con la que tenemos un contrato.

Actualmente, el proveedor principal de CDN es Akamai. Los archivos alojados en Akamai tienen un dominio de `assets.adobedtm.com`.

### ¿Por qué utilizar el alojamiento administrado?

La razón principal para utilizar el alojamiento administrado es la comodidad. Es más fácil crear el host necesario, ya que de esa forma no tiene que preocuparse por el mantenimiento.

## Alojamiento propio

Si no desea que Adobe administre los archivos alojados, debe alojarlos por su cuenta. Para alojar los archivos, debe obtener las compilaciones completadas de Experience Platform y asegurarse de que los archivos pasan por el ciclo de lanzamiento de la empresa hasta los servidores administrados de la empresa.

### ¿Por qué utilizar el alojamiento propio?

Existen varias razones para elegir alojar sus propios archivos de compilación.

* Algunos exploradores bloquean el dominio assets.adobedtm.com basándose en la configuración de privacidad configurada por el usuario final
* El alojamiento propio reduce la cantidad necesaria de búsquedas de DNS
* Necesita establecer ciertos encabezados específicos por motivos de seguridad
* Los requisitos de control de caché difieren de la configuración predeterminada de Adobe
* Desea controlar mejor la ubicación de los nodos periféricos
* Su organización tiene requisitos legales y de seguridad que le impiden utilizar la opción administrada por Adobe

### Como utilizar el alojamiento propio

Puede utilizar dos métodos para adquirir compilaciones completadas para poder utilizar el alojamiento propio.

* Descargar
* Envío directo

#### Descargar

Las compilaciones se pueden enviar como un archivo .zip empaquetado (cifrado opcional). Luego puede descomprimir el paquete e insertar el contenido en el ciclo de lanzamiento para introducirlo en sus propios servidores.

Use un host [administrado por Adobe](self-hosting-libraries.md) y seleccione la opción [Archive](../environments.md). El entorno proporciona un enlace de descarga. Siempre que se cree una compilación, puede recuperarla desde el enlace de descarga del entorno.

#### Envío directo

Las compilaciones también se pueden enviar directamente a un servidor SFTP que haya creado. Es responsabilidad suya archivar estas compilaciones en su ciclo de lanzamiento y ponerlas en marcha.

Para realizar un envío directo, debe crear un [host SFTP](sftp-host.md) y asignar dicho host a su entorno. Cada vez que crea una biblioteca en ese entorno, los archivos se envían al servidor SFTP.
