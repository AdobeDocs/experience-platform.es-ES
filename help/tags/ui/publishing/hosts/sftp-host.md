---
title: Alojamientos de SFTP
description: Aprenda a configurar etiquetas en Adobe Experience Platform para enviar compilaciones de biblioteca a un servidor SFTP autoalojado y protegido.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 44%

---

# Alojamientos de SFTP

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Si no quiere que Adobe administre sus bibliotecas alojadas, la otra opción que tiene es que Adobe Experience Platform envíe compilaciones a un servidor SFTP protegido que usted aloje.

Platform se conecta al sitio SFTP mediante una clave cifrada. Debe seguir algunos pasos para configurar esto correctamente:

1. Debe tener un par de clave pública o privada instalado en el servidor SFTP. Puede generar estas claves en el servidor o generarlas en otro lugar e instalarlas en el servidor. Consulte la documentación de GitHub sobre [cómo generar claves SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) para obtener más información.
1. La clave privada se utiliza para cifrar la clave GPG pública. Debe proporcionar la clave privada durante el proceso de creación del host SFTP. Consulte la sección [Cifrar valores](https://developer.adobelaunch.com/api/guides/encrypting_values/) en la documentación de la API de Reactor para obtener instrucciones sobre el cifrado de claves GPG públicas. Utilice la clave GPG del entorno de producción a menos que sepa que necesita una específica. Por último, puede cifrar la clave privada desde cualquier equipo, y no es necesario instalar GPG en el servidor para completar este paso.
1. Es posible que deba aprobar las direcciones IP utilizadas con el cortafuegos de su empresa para permitir que Platform acceda al servidor SFTP y se conecte a él. Estas direcciones IP son:
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>La estructura de las compilaciones de etiquetas ha cambiado con el paso del tiempo. Utilizan vínculos simbólicos (enlaces simbólicos) internamente para mantener la compatibilidad con versiones anteriores, de modo que los códigos incrustados anteriores seguirán funcionando con la estructura de versión más reciente. El servidor SFTP debe admitir el uso de enlaces simbólicos para que sirva como destino válido para las compilaciones de etiquetas.

Para obtener información más detallada, consulte el siguiente artículo Medio sobre [cómo configurar los servidores SFTP para enviar una compilación](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Creación de un host SFTP

1. Abra la pestaña [!UICONTROL Hosts].
1. Cree el nuevo host.
1. Asigne un nombre al host.
1. Seleccione **[!UICONTROL SFTP]** como tipo de host.
1. Introduzca el host, la ruta, el puerto, el nombre de usuario y la clave privada cifrada.

   El puerto debe ser uno de los siguientes:

   * 21
   * 22
   * 80
   * 200-299
   * 443
   * 2000-2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >Como práctica recomendada de seguridad, Adobe limita la cantidad de puertos que se pueden utilizar para el tráfico saliente. Los puertos seleccionados suelen permitirse a través de servidores de seguridad corporativos, además de incluir algunos rangos de flexibilidad.

1. Seleccione **[!UICONTROL Guardar]**.

Al seleccionar **[!UICONTROL Guardar]**, se comprueba la conexión y la capacidad de enviar los archivos al servidor SFTP. Platform crea una carpeta, escribe un archivo dentro de esa carpeta, comprueba si el archivo está allí y limpia después. Si la cuenta de usuario del servidor SFTP (la que se adjunta al certificado seguro que ha proporcionado a Platform) no tiene los permisos necesarios para realizar esta acción, el host pasa a estar en estado &quot;failed&quot;.
