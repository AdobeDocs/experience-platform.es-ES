---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;perfil unificado;perfil unificado;perfil unificado;perfil unificado;rtcp;gráficos XDM
title: Funciones generales de accesibilidad en Experience Platform
type: Documentation
description: Obtenga más información acerca de las funciones de accesibilidad generales que admite Adobe Experience Platform, como la navegación mediante el teclado, las paletas de color y el contraste, y la compatibilidad con tecnología de asistencia.
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Funciones de accesibilidad en Experience Platform

Adobe Experience Platform se compromete a proporcionar funciones accesibles e inclusivas a todas las personas, incluidos los usuarios que trabajan con dispositivos de asistencia, como software de reconocimiento de voz y lectores de pantalla. Este documento describe las funciones generales de accesibilidad que admite Experience Platform, incluida la navegación mediante el teclado, la estructura semántica, el contraste suficiente entre elementos en primer plano y elementos en segundo plano y la compatibilidad con tecnologías de asistencia.

## Tecnologías de asistencia

Los usuarios con discapacidad suelen depender del hardware y el software, conocidos como tecnologías de asistencia, para acceder al contenido digital y utilizar productos de software. Adobe Experience Platform admite varios tipos de tecnologías de asistencia (AT), como lectores de pantalla, zoom y software de reconocimiento de voz, mediante las siguientes prácticas recomendadas de accesibilidad, como el uso de código semántico, equivalentes de texto, etiquetas y ARIA donde sea necesario. Los elementos interactivos dentro de la interfaz de usuario (IU) de Experience Platform utilizan etiquetas, nombres accesibles y funciones correspondientes que identifican su propósito y su estado actual. Esto garantiza que las tecnologías de asistencia, como los lectores de pantalla, puedan leer las etiquetas y otra información a los usuarios para que puedan interactuar fácilmente con los controles de la aplicación.

## Accesibilidad del teclado

Experience Platform se esfuerza por admitir la accesibilidad total del teclado.

Los siguientes elementos de navegación facilitan la accesibilidad:
* El tabulador permite desplazarse entre elementos de la interfaz de usuario, secciones y grupos de menús.
* Las teclas de flecha se mueven dentro de los grupos de menús para definir el enfoque en elementos activos individuales.
* Mayús + Tab se mueve hacia atrás en el orden de tabulación.
* Las teclas Retorno (Intro) y Barra espaciadora activan los elementos seleccionados.
* La tecla Esc actúa como un botón de cancelación para cerrar un cuadro de diálogo cuando está presente.
* Experience Platform muestra un borde azul alrededor de un elemento seleccionado para mostrar una indicación clara de qué elemento de la interfaz de usuario está seleccionado actualmente.

![Aparece un borde azul alrededor de un elemento seleccionado para indicar que se ha aplicado el enfoque.](images/profile-overview-tab.png)

## Paletas de color y contraste

Experience Platform se esfuerza por lograr la conformidad con [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/), incluidos los requisitos para el contraste de color. La interfaz de usuario de Experience Platform proporciona suficiente contraste en la aplicación para garantizar una experiencia de visualización accesible para los usuarios con deficiencias bajas de visión o color.

![La paleta de colores y el contraste están presentes en la página principal de la interfaz de usuario de Experience Platform.](images/homepage.png)

## Validación de campo requerida

Al agregar datos, crear esquemas o definir segmentos, los campos obligatorios se indican tanto visualmente, con un asterisco junto a la etiqueta de texto de un campo, como mediante programación. Estos campos almacenan en déclencheur la validación cuando se introducen datos no válidos en los campos y al guardarlos. Si un campo requerido no supera la validación, se delinea en rojo con un icono de error y también aparece una descripción por escrito del problema que debe solucionarse.

![Un primer plano de un campo obligatorio que no ha superado la validación. El campo aparece en rojo y hay un icono de error.](images/field-validation.png)
