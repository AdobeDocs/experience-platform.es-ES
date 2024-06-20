---
solution: Experience Platform
title: Limitaciones conocidas y solución de problemas con los libros de reproducción
description: Obtenga más información acerca de los problemas conocidos y los problemas comunes con los libros de reproducción y cómo solucionarlos
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Resolución de problemas {#troubleshooting}

Vea sugerencias para la resolución de problemas con errores comunes al trabajar con libros de reproducción de casos de uso

## Superficies Adobe Journey Optimizer no configuradas {#surfaces-not-configured}

Al crear una instancia de un manual de implementación, es posible que vea el mensaje siguiente.

![Resolución de problemas](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Esto se debe a que los libros de reproducción de Journey Optimizer crean mensajes para canales de correo electrónico, push y SMS. Lea el [introducción](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) guía para configurar las diferentes superficies.

## Estado *error* al crear una nueva instancia {#status-failed}

Si ve un mensaje de error cuando intenta crear una instancia, puede deberse a que el administrador no le ha concedido los permisos de usuario necesarios. Un libro de reproducción contiene muchos recursos diferentes y el usuario necesita permisos para crear esos recursos para poder crear la instancia del libro de reproducción correctamente. Consulte la [permissions](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) de esta guía sobre cómo configurar permisos.

## Error de importación {#import-failure}

Los clientes trabajan en diferentes entornos de prueba y, ocasionalmente, al importar una instancia de su entorno al entorno limitado de Adobe, puede fallar. Para ver el estado de estas importaciones, seleccione Zona protegida en el panel de navegación izquierdo y, a continuación, seleccione Trabajos. Aquí puede ver todos los detalles de los archivos importados. Seleccione un archivo con un estado fallido y, a continuación, seleccione Ver detalles del trabajo. Aparecerá un modal. Seleccione Ver archivo JSON, desplácese hacia abajo y copie el mensaje de error que aparece en &quot;mensajes&quot;. Es muy posible que aparezcan varios mensajes de error, por lo que asegúrese de copiarlos todos. Envíe estos mensajes a su equipo de Adobe mientras intenta registrar un ticket de error. Esto acelera el proceso de resolución y proporciona a su equipo más contexto sobre lo que está ocurriendo.
