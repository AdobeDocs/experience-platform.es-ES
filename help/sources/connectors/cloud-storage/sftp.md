---
keywords: Experience Platform;inicio;temas populares;SFTP;sftp
solution: Experience Platform
title: Información general sobre el conector SFTP Source
description: Obtenga información sobre cómo conectar un servidor SFTP a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
source-git-commit: 52c1c8e6bc332bd6ee579cad52a7343007615efd
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Conector SFTP

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Lea este documento para conocer los pasos necesarios que debe llevar a cabo para conectar correctamente su cuenta de [!DNL SFTP] al Experience Platform.

>[!TIP]
>
>Debe deshabilitar la autenticación interactiva de teclado en la configuración del servidor SFTP antes de conectarse. Si deshabilita esta opción, las contraseñas se pueden escribir manualmente, en lugar de hacerlo a través de un servicio o un programa.

## Requisitos previos {#prerequisites}

Lea esta sección para ver los pasos necesarios que debe llevar a cabo para conectar correctamente el origen de [!DNL SFTP] al Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

### Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento en la nube.

* Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
* Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
* Los siguientes caracteres de URL reservadas deben ser de escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
* No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
* No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, si bien son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

### Configure una clave privada OpenSSH codificada en Base64 para [!DNL SFTP]

El origen [!DNL SFTP] admite la autenticación mediante clave privada OpenSSH con codificación [!DNL Base64]. Consulte los pasos siguientes para obtener información sobre cómo generar la clave privada OpenSSH codificada en Base64 y conectar [!DNL SFTP] a Platform.

>[!BEGINTABS]

>[!TAB Windows]

### [!DNL Windows] usuarios

Si usa un equipo [!DNL Windows], abra el menú **Inicio** y, a continuación, seleccione **Configuración**.

![configuración](../../images/tutorials/create/sftp/settings.png)

En el menú **Configuración** que aparece, seleccione **Aplicaciones**.

![aplicaciones](../../images/tutorials/create/sftp/apps.png)

A continuación, seleccione **características opcionales**.

![características opcionales](../../images/tutorials/create/sftp/optional-features.png)

Aparecerá una lista de funciones opcionales. Si **OpenSSH Client** ya está preinstalado en tu equipo, entonces se incluirá en la lista **Características instaladas** en **Características opcionales**.

![open-ssh](../../images/tutorials/create/sftp/open-ssh.png)

Si no está instalado, seleccione **Instalar** y, a continuación, abra **[!DNL Powershell]** y ejecute el siguiente comando para generar su clave privada:

```shell
PS C:\Users\lucy> ssh-keygen -t rsa -m pem
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\lucy/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\lucy/.ssh/id_rsa.
Your public key has been saved in C:\Users\lucy/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:osJ6Lg0TqK8nekNQyZGMoYwfyxNc+Wh0hYBtBylXuGk lucy@LAPTOP-FUJT1JEC
The key's randomart image is:
+---[RSA 3072]----+
|.=.*+B.o.        |
|=.O.O +          |
|+o+= B           |
|+o +E .          |
|.o=o  . S        |
|+... . .         |
| *o .            |
|o.B.             |
|=O..             |
+----[SHA256]-----+
```

A continuación, ejecute el siguiente comando mientras proporciona la ruta de acceso del archivo de la clave privada para codificar la clave privada en [!DNL Base64]:

```shell
C:\Users\lucy> [convert]::ToBase64String((Get-Content -path "C:\Users\lucy\.ssh\id_rsa" -Encoding byte)) > C:\Users\lucy\.ssh\id_rsa_base64
```

El comando anterior guarda la clave privada con codificación [!DNL Base64] en la ruta de acceso de archivo designada. Puede usar esa clave privada para autenticarse en [!DNL SFTP] y conectarse a Platform.

>[!TAB Mac]

### [!DNL Mac] usuarios

Si usa un [!DNL Mac], abra **Terminal** y ejecute el siguiente comando para generar la clave privada (en este caso, la clave privada se guardará en `/Documents/id_rsa`):

```shell
ssh-keygen -t rsa -m pem -f ~/Documents/id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/vrana/Documents/id_rsa.
Your public key has been saved in /Users/vrana/Documents/id_rsa.pub.
The key fingerprint is:
SHA256:s49PCaO4a0Ee8I7OOeSyhQAGc+pSUQnRii9+5S7pp1M vrana@vrana-macOS
The key's randomart image is:
+---[RSA 2048]----+
|o ==..           |
|.+..o            |
|oo.+             |
|=.. +            |
|oo = .  S        |
|+.+ +E . = .     |
|o*..*.. . o      |
|.o*=.+   +       |
|.oo=Oo  ..o      |
+----[SHA256]-----+
```

A continuación, ejecute el siguiente comando para codificar la clave privada en [!DNL Base64]:

```shell
base64 ~/Documents/id_rsa > ~/Documents/id_rsa_base64
 
 
# Print Content of base64 encoded file
cat ~/Documents/id_rsa_base64
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUJGd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFRRUF0cWFYczlXOUF1ZmtWazUwSXpwNXNLTDlOMU9VYklaYXVxbVM0Q0ZaenI1NjNxUGFuN244CmFxZWdvQTlCZnVnWDJsTVpGSFl5elEzbnp6NXdXMkdZa1hkdjFjakd0elVyNyt1NnBUeWRneGxrOGRXZWZsSzBpUlpYWW4KVFRwS0E5c2xXaHhjTXg3R2x5ejdGeDhWSzI3MmdNSzNqY1d1Q0VIU3lLSFR5SFFwekw0MEVKbGZJY1RGR1h1dW1LQjI5SwpEakhwT1grSDdGcG5Gd1pabTA4Uzc2UHJveTVaMndFalcyd1lYcTlyUDFhL0E4ejFoM1ZLdllzcG53c2tCcHFQSkQ1V3haCjczZ3M2OG9sVllIdnhWajNjS3ZsRlFqQlVFNWRNUnB2M0I5QWZ0SWlrYmNJeUNDaXV3UnJmbHk5eVNPQ2VlSEc0Z2tUcGwKL3V4YXNOT0h1d0FBQThqNnF6R1YrcXN4bFFBQUFBZHpjMmd0Y25OaEFBQUJBUUMycHBlejFiMEM1K1JXVG5Rak9ubXdvdgowM1U1UnNobHE2cVpMZ0lWbk92bnJlbzlxZnVmeHFwNkNnRDBGKzZCZmFVeGtVZGpMTkRlZlBQbkJiWVppUmQyL1Z5TWEzCk5TdnY2N3FsUEoyREdXVHgxWjUrVXJTSkZsZGlkTk9rb0QyeVZhSEZ3ekhzYVhMUHNYSHhVcmJ2YUF3cmVOeGE0SVFkTEkKb2RQSWRDbk12alFRbVY4aHhNVVplNjZZb0hiMG9PTWVrNWY0ZnNXbWNYQmxtYlR4THZvK3VqTGxuYkFTTmJiQmhlcjJzLwpWcjhEelBXSGRVcTlpeW1mQ3lRR21vOGtQbGJGbnZlQ3pyeWlWVmdlL0ZXUGR3cStVVkNNRlFUbDB4R20vY0gwQiswaUtSCnR3aklJS0s3Qkd0K1hMM0pJNEo1NGNiaUNST21YKzdGcXcwNGU3QUFBQUF3RUFBUUFBQVFBcGs0WllzMENSRnNRTk9WS0sKYWxjazlCVDdzUlRLRjFNenhrSGVydmpJYk9kL0lvRXpkcHlVa28rbm41RmpGK1hHRnNCUXZnOFdTaUlJTk1oU3BNYWI1agpvWXlka2gvd0ovWElOaDlZaE5QVXlURi9NNkFnMkNYd21KS2RxN1VKWjZyNjloV3V0VVN6U05QbkVYWTZLc29GeVUwTEFvCko0OHJMT1pMZldtMHFhWDBLNUgzNmJPaHFXSWJwMDNoZk94eno5M0MrSDM5MFJkRkp4bzJVZ0FVY3UvdHREb0REVldBdmEKVkVyMWEzak9LenVHbThrK21WeXpPZERjVFY4ckZIT0pwRnRBU3l6Q24yVld1MjV0TWtrcGRPRjNKcVdMZHdOY3loeG1URApXZGVDNWh4V0Fiano0WDZ5WXpHcFcwTmptVkFoWUVVZGNBSVlXWWM3OGEvQkFBQUFnRm8wakl4aGhwZkJ6QjF6b09FMDJBClpjTC9hcUNuYysrdmJ1a2V0aFg5Zzhlb0xQMTQyeUgzdlpLczl3c1RtbVVsZ0prZURaN2hUcklwOGY2eEwzdDRlMXByY1kKb2ZLd0gwckNGOTFyaldPbGZOUmxEempoR1NTTEVMczZoNlNzMEdBQXE2Z0ZQTVF2dTB4TDlQUTlGQ21YZVVKazJpRm1MWgpEWWJGc0NyVUxEQUFBQWdRRGF0a1pMamJaSTBFM0ZuY2dTOVF5Y3lVWmtkZ1dVNjBQcG9ud3BMQXdUdHRpOG1EQXE5cHYwClEvUlk1WE9UeGF3VXNHa0tYMjNtV1BYR0grdUlBSzhrelVVM2dGM1dRWGVkTWw4NHVCVFZCTEtUdStvVVAvZmIvMEE0dE0KSE9BSythbXZPMkZuYzFiSmVwd05USTE2cjZXWk9sZWV2ZklJQVpXcEgxVVpIdkVRQUFBSUVBMWNwcStDNUVXSFJwbnVPZQpiNHE4T0tKTlJhSUxIRUN6U0twWlFpZDFhRmJYWlVKUXpIQU85YzhINVZMcjBNUjFkcW1ORkNja2ZsZzI2Y3BEUEl3TjBYCm5HMFBxcmhKbXp0U3ZQZ3NGdkNPallncXF6U0RYUjkxd1JQTEN5cU8zcGMyM2kzZnp2WkhtMGhIdWdoNVJqV0loUlFZVkwKZUpDWHRqM08vY3p1SWdzQUFBQVJkbkpoYm1GQWRuSmhibUV0YldGalQxTUJBZz09Ci0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

Una vez guardada la clave privada con codificación [!DNL Base64] en la carpeta designada, debe agregar el contenido del archivo de clave pública a una nueva línea en las claves autorizadas del host [!DNL SFTP]. Ejecute el siguiente comando en la línea de comandos:

```shell
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

Para confirmar si la clave pública se agregó correctamente, ejecute lo siguiente en la línea de comandos:

```shell
more ~/.ssh/authorized_keys
```

>[!ENDTABS]

### Recopilar credenciales necesarias {#credentials}

Debe proporcionar valores para las siguientes credenciales a fin de conectar el servidor [!DNL SFTP] al Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Proporcione los valores apropiados para las siguientes credenciales a fin de autenticar el servidor [!DNL SFTP] mediante la autenticación básica.

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociada con el servidor [!DNL SFTP]. |
| `port` | El puerto del servidor [!DNL SFTP] al que se está conectando. Si no se proporciona, el valor predeterminado es `22`. |
| `username` | El nombre de usuario con acceso a su servidor [!DNL SFTP]. |
| `password` | Contraseña del servidor [!DNL SFTP]. |
| `maxConcurrentConnections` | Este parámetro le permite especificar un límite máximo para el número de conexiones simultáneas que Platform creará al conectarse al servidor SFTP. Debe configurar este valor para que sea inferior al límite establecido por SFTP. **Nota**: Cuando esta configuración está habilitada para una cuenta SFTP existente, solo afectará los flujos de datos futuros y no los existentes. |
| `folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. [!DNL SFTP] origen, puede proporcionar la ruta de la carpeta para especificar el acceso del usuario a la subcarpeta que elija. |
| `disableChunking` | Durante la ingesta de datos, el origen [!DNL SFTP] puede recuperar primero la longitud del archivo, dividirlo en varias partes y, a continuación, leerlo en paralelo. Puede habilitar o deshabilitar este valor para especificar si el servidor [!DNL SFTP] puede recuperar las longitudes de archivo o leer datos de un desplazamiento específico. |
| `connectionSpec.id` | (Solo API) La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y fuente. El id. de especificación de conexión para [!DNL SFTP] es: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

>[!TAB Autenticación de clave pública SSH]

Proporcione los valores apropiados para las siguientes credenciales a fin de autenticar su servidor [!DNL SFTP] mediante la autenticación de clave pública SSH.

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociada con el servidor [!DNL SFTP]. |
| `port` | El puerto del servidor [!DNL SFTP] al que se está conectando. Si no se proporciona, el valor predeterminado es `22`. |
| `username` | El nombre de usuario con acceso a su servidor [!DNL SFTP]. |
| `password` | Contraseña del servidor [!DNL SFTP]. |
| `privateKeyContent` | El contenido de clave privada SSH codificado en Base64. El tipo de clave OpenSSH debe clasificarse como RSA o DSA. |
| `passPhrase` | La contraseña o frase de paso para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de paso. Si PrivateKeyContent está protegido con contraseña, este parámetro debe utilizarse con la frase de contraseña de PrivateKeyContent como valor. |
| `maxConcurrentConnections` | Este parámetro le permite especificar un límite máximo para el número de conexiones simultáneas que Platform creará al conectarse al servidor SFTP. Debe configurar este valor para que sea inferior al límite establecido por SFTP. **Nota**: Cuando esta configuración está habilitada para una cuenta SFTP existente, solo afectará los flujos de datos futuros y no los existentes. |
| `folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. [!DNL SFTP] origen, puede proporcionar la ruta de la carpeta para especificar el acceso del usuario a la subcarpeta que elija. |
| `disableChunking` | Durante la ingesta de datos, el origen [!DNL SFTP] puede recuperar primero la longitud del archivo, dividirlo en varias partes y, a continuación, leerlo en paralelo. Puede habilitar o deshabilitar este valor para especificar si el servidor [!DNL SFTP] puede recuperar las longitudes de archivo o leer datos de un desplazamiento específico. |
| `connectionSpec.id` | (Solo API) La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y fuente. El id. de especificación de conexión para [!DNL SFTP] es: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

>[!ENDTABS]

## Conectar SFTP al Experience Platform

La siguiente documentación proporciona información sobre cómo conectar un servidor SFTP al Experience Platform mediante API o la interfaz de usuario de:

### Uso de las API

* [Creación de una conexión base SFTP mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/sftp.md)
* [Explore la estructura de datos y el contenido de una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/explore/cloud-storage.md)
* [Cree un flujo de datos para una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Uso de la IU

* [Creación de una conexión de origen SFTP en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/sftp.md)
* [Cree un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/batch/cloud-storage.md)
