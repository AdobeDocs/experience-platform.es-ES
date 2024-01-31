---
solution: Experience Platform
title: Limitaciones conocidas y solución de problemas con los libros de reproducción
description: Obtenga más información acerca de los problemas conocidos y los problemas comunes con los libros de reproducción y cómo solucionarlos
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: ecce42e2c759bda31bc37d0aae1da2c7b3d141fc
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 2%

---


# Solución de problemas y limitaciones conocidas {#troubleshooting-known-limitations}

Aprenda a solucionar errores al trabajar con libros de reproducción de casos de uso y comprenda las limitaciones conocidas de la versión de disponibilidad general.

## Resolución de problemas {#troubleshooting}

Vea sugerencias para la resolución de problemas con errores comunes al trabajar con libros de reproducción de casos de uso

### Superficies Adobe Journey Optimizer no configuradas

Al crear una instancia de un manual de implementación, es posible que vea el mensaje siguiente.

![Resolución de problemas](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Esto se debe a que los libros de reproducción de Journey Optimizer crean mensajes para canales de correo electrónico, push y SMS. Lea el [introducción](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) guía para configurar las diferentes superficies.

### Estado *error* al crear una nueva instancia

Si ve un mensaje de error cuando intenta crear una instancia, puede deberse a que el administrador no le ha concedido los permisos de usuario necesarios. Un libro de reproducción contiene muchos recursos diferentes y el usuario necesita permisos para crear esos recursos para poder crear la instancia del libro de reproducción correctamente. Consulte la [permissions](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) de esta guía sobre cómo configurar permisos.

## Limitaciones conocidas

Un par de limitaciones conocidas se muestran al crear una instancia de un manual y generar recursos.

* Para los esquemas generados, si se genera un esquema en una instancia de un manual y se edita, otro esquema *no* se generan si habilita otra instancia del manual de implementación. En su lugar, siga utilizando el esquema editado también dentro de la instancia.

* Al usar el [funcionalidad de sensibilización de datos](/help/use-case-playbooks/playbooks/data-awareness.md) para promocionar el esquema de la zona protegida de inspiración a la de desarrollo, podría ver algunos errores similares a los siguientes:

![Errores mostrados en el flujo de trabajo de asignación de esquemas.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Esto se debe a que algunos de los campos generados a partir del esquema no están presentes en el esquema en el entorno limitado de desarrollo al que está copiando. Busca lo que son esos campos. A continuación, vuelva a la zona protegida de desarrollo, donde podrá hacer lo siguiente:

* Cree un nuevo grupo de campos que incluya esos campos o
* Incluya en el esquema un grupo de campos estándar predefinido que incluya los campos que faltan.

Después de incluir esos campos en el esquema en la zona protegida de desarrollo, vuelva al flujo de trabajo para copiar los campos de esquema de la zona protegida inspiracional en la zona protegida de desarrollo. Los errores ya no existen.

Para obtener más información, vea el siguiente vídeo para crear grupos de campos de esquema.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
