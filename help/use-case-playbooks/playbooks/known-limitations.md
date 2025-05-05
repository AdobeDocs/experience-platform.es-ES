---
solution: Experience Platform
title: Limitaciones conocidas con los libros de reproducción
description: Obtenga más información acerca de los problemas conocidos y los problemas comunes con los libros de reproducción y cómo solucionarlos
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# Limitaciones conocidas {#known-limitations}

Aprenda a solucionar errores al trabajar con libros de reproducción de casos de uso y comprenda las limitaciones conocidas de la versión de disponibilidad general.

## Limitaciones conocidas

Un par de limitaciones conocidas se muestran al crear una instancia de un manual y generar recursos.

* En el caso de los esquemas generados, si se genera un esquema en una instancia de un libro de reproducción y usted lo edita, entonces no se generará otro esquema ** si habilita otra instancia del libro de reproducción. En su lugar, siga utilizando el esquema editado también dentro de la instancia.

* Al usar la [funcionalidad de reconocimiento de datos](/help/use-case-playbooks/playbooks/data-awareness.md) para promocionar el esquema de la zona protegida inspiracional a la zona protegida de desarrollo, es posible que vea algunos errores similares a los siguientes:

![Errores mostrados en el flujo de trabajo de asignación de esquemas.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Esto se debe a que algunos de los campos generados a partir del esquema no están presentes en el esquema en el entorno limitado de desarrollo al que está copiando. Busca lo que son esos campos. A continuación, vuelva a la zona protegida de desarrollo, donde podrá hacer lo siguiente:

* Cree un nuevo grupo de campos que incluya esos campos o
* Incluya en el esquema un grupo de campos estándar predefinido que incluya los campos que faltan.

Después de incluir esos campos en el esquema en la zona protegida de desarrollo, vuelva al flujo de trabajo para copiar los campos de esquema de la zona protegida inspiracional en la zona protegida de desarrollo. Los errores ya no existen.

Para obtener más información, vea el siguiente vídeo para crear grupos de campos de esquema.

>[!VIDEO](https://video.tv.adobe.com/v/3413601/?learn=on&captions=spa)
