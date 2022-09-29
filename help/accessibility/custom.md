---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;perfil unificado;perfil unificado;unificado;perfil;rtcp;gráficos XDM
title: Soluciones de accesibilidad personalizadas para Experience Platform
topic-legacy: guide
type: Documentation
description: Obtenga más información sobre las soluciones de accesibilidad personalizadas en la interfaz de usuario de Adobe Experience Platform.
exl-id: cb5ad99e-8a95-4c9e-aae6-1d0036ecf052
source-git-commit: 7f4202c9c4a132ed9d74c495f6608357eac8003f
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# Soluciones de accesibilidad personalizadas para Experience Platform

Adobe Experience Platform se mejora continuamente para satisfacer las necesidades de todos los tipos de usuarios y cumplir los estándares mundiales que incluyen personas con discapacidades visuales, auditivas, de movilidad o de otro tipo. Este documento describe soluciones de accesibilidad personalizadas dentro de la interfaz de usuario del Experience Platform.

## Información general sobre la página principal y la interfaz de usuario

La interfaz de usuario del Experience Platform cumple los índices de contraste necesarios para los componentes de texto normal, gráficos y interfaz de usuario. Los colores de la interfaz de usuario también se han elegido para admitir la accesibilidad para todos los usuarios, incluidos los que tienen discapacidades visuales.

En Platform, los elementos de la interfaz de usuario en los que se puede hacer clic o activar con un puntero también se pueden utilizar con un teclado. Esto incluye la navegación izquierda, los reproductores de vídeo, las tablas y mucho más.

El Experience Platform se esfuerza por cumplir los estándares de accesibilidad internacionales, incluyendo las Directrices de accesibilidad al contenido web 2.1 Nivel A y Nivel AA y los estándares web de la Iniciativa de accesibilidad a la web - Aplicaciones de Internet enriquecidas accesibles (WAI-ARIA).

![La página de inicio de la interfaz de usuario de Adobe Experience Platform.](images/homepage.png)

## Navegación izquierda

La navegación izquierda en la interfaz de usuario del Experience Platform es accesible mediante el teclado y proporciona contraste de color en los estados normal, de desplazamiento y de selección que cumplen los estándares de accesibilidad.

Desde la pantalla de inicio, los usuarios pueden desplazarse por la pestaña en el panel de navegación izquierdo. Selección **Mayús + Tab** devuelve al usuario a la pantalla de inicio.

![Navegación izquierda del Experience Platform.](images/left-navigation-select.png)

Con la navegación izquierda enfocada, **Tabulación** lleva a los usuarios a la interacción expandir y contraer. La capacidad de expandir o contraer la navegación izquierda se activa con **Intro (devolución)**.

![La navegación izquierda del Experience Platform se ha contraído.](images/left-navigation-collapse.png)

Con la navegación izquierda enfocada, las teclas de flecha hacia arriba y hacia abajo navegan hasta cada elemento de la navegación y realizan un ciclo continuo (es decir, el enfoque no se aleja hasta que el usuario se aleja de la navegación izquierda). El enfoque se muestra para los elementos de navegación cuando se seleccionan. La selección actual se muestra con un texto resaltado y en negrita. Al seleccionar un elemento de navegación izquierdo, **Intro (devolución)** abre el elemento de la interfaz de usuario seleccionado en el panel derecho; sin embargo, el enfoque permanece en la navegación izquierda hasta que el usuario se desplace.

![El Experience Platform de navegación izquierdo con Fuentes seleccionadas.](images/left-navigation-sources.png)

Algunas funciones de Platform no están habilitadas para todos los usuarios. Estos elementos aparecen en la navegación, pero no se pueden seleccionar. Al navegar con un teclado, estos elementos se omiten durante la navegación por la flecha y no se pueden seleccionar mediante **Intro (devolución)**.

![Las secciones de la navegación izquierda del Experience Platform que no están habilitadas para el usuario no se pueden seleccionar.](images/left-navigation-sections-disabled.png)

## Cuadro de diálogo de vídeo incrustado

Los vídeos se pueden ver en el Experience Platform mediante la navegación mediante el teclado para resaltar y seleccionar un vínculo de vídeo disponible. Esto abre un cuadro de diálogo de vídeo incrustado en la interfaz de usuario de Platform.

![Borde azul que aparece alrededor de un elemento seleccionado para indicar que se ha aplicado el enfoque.](images/profile-overview-tab.png)

## Accesibilidad del teclado del cuadro de diálogo de vídeo

El cuadro de diálogo de vídeo incrustado también se puede navegar mediante el teclado. La siguiente tabla describe la navegación completa por teclado disponible para el cuadro de diálogo de vídeo incrustado.

| Elemento Diálogo | Accesibilidad del teclado | Descripción |
|---|---|---|
| Reproducir y pausar | Tabulación<br/>Barra espaciadora | Uso **Tabulación** para definir el enfoque en el botón de reproducción. **Barra espaciadora** inicia la reproducción de vídeo y detiene la reproducción de vídeo. |
| Depurador | Tabulación<br/>Flecha izquierda<br/>Flecha derecha | Cuando se esté reproduciendo el vídeo, utilice **Tabulación** para enfocar la selección. Con el depurador en enfoque, **teclas de flecha izquierda y derecha** omita la reproducción de vídeo hacia delante y hacia atrás 5 segundos, respectivamente. |
| Silenciar | Tabulación<br/>Barra espaciadora | Uso **Tabulación** para enfocar el elemento de volumen silencioso. Uso **barra espaciadora** para silenciar o anular el silencio de la reproducción de vídeo. |
| Volumen | Tabulación<br/>Flecha izquierda<br/>Flecha derecha | Uso **Tabulación** para centrarse en el elemento de volumen. **Teclas de flecha izquierda y derecha** mueva el volumen hacia arriba y hacia abajo, respectivamente. |
| [!UICONTROL Subtítulos] (&quot;cc&quot;) | Tabulación<br/>Entrar<br/>Flecha arriba<br/>Flecha abajo | **Tabulación** a [!UICONTROL Subtítulos] (&quot;cc&quot;). Uso **Entrar** para abrir el menú y **teclas de flecha arriba y abajo** para seleccionar un idioma para los rótulos. **Entrar** confirma la selección. |
| [!UICONTROL Calidad] | Tabulación<br/>Entrar<br/>Flecha arriba<br/>Flecha abajo | Uso **Tabulación** para enfocar el [!UICONTROL Calidad] elemento. Uso **Entrar** para abrir el menú y el **teclas de flecha arriba y abajo** para seleccionar la calidad de vídeo. **Entrar** confirma la selección. |
| Pantalla completa | Tabulación<br/>Barra espaciadora o Entrar<br/>Escape | Uso **Tabulación** para enfocar el elemento de pantalla completa. Uso **barra espaciadora o Intro** para activar la vista de pantalla completa. **Escape** (&quot;esc&quot;) sale del modo de pantalla completa. |
| Cerrar | Tabulación<br/>Barra espaciadora o Entrar | Uso **Tabulación** para enfocar el botón de cierre. Uso **barra espaciadora o Intro** para salir del cuadro de diálogo de vídeo. |

>[!NOTE]
>
>En cualquier momento durante la reproducción, se puede utilizar la tecla escape (&quot;esc&quot;) para cerrar el cuadro de diálogo de vídeo incrustado.

![El cuadro de diálogo de vídeo incrustado con números que identifican los elementos de navegación mediante el teclado.](images/video-dialog.png)

## Arrastrar y soltar archivos

En el Experience Platform, todas las zonas de arrastrar y soltar para la selección de archivos son accesibles mediante el teclado. Uso **Tabulación** para resaltar **[!UICONTROL Elegir archivos]** y **Entrar o barra espaciadora** para seleccionarlo, se invoca la IU de selección de archivos del sistema operativo.

Una vez cargado un archivo, se puede navegar mediante el teclado para eliminar el archivo seleccionado y cargar uno nuevo. Los usuarios pueden utilizar **Tabulación** para centrarse en el icono de eliminación y **Entrar o barra espaciadora** para seleccionarlo. Una vez eliminado el archivo, **[!UICONTROL Elegir archivos]** está enfocado automáticamente y se puede seleccionar.

Alternativamente, si el archivo que se carga no tiene el formato correcto, se muestra un icono de error junto con un mensaje de error y la variable **[!UICONTROL Elegir archivos]** está enfocado y se puede seleccionar.

![Zona de arrastrar y soltar un archivo con un mensaje de error y el botón de selección de archivos seleccionado.](images/drag-and-drop.png)

Si se utiliza el ratón para seleccionar la zona de arrastrar y soltar, también se invoca la IU de selección de archivos, o si se utiliza el ratón, se puede seleccionar un archivo y arrastrarlo a la zona para comenzar la carga.

![Zona de arrastrar y soltar un archivo enfocada mientras el usuario arrastra un archivo a la zona.](images/drag-and-drop-mouse-over.png)

## Exploración de tabla

Todas las tablas de la interfaz de usuario del Experience Platform son accesibles mediante el teclado. La navegación y la interacción con filas y columnas de tablas es posible mediante una serie de métodos abreviados del teclado:

* Desde el encabezado de tabla, utilice el **flecha abajo** para examinar la tabla. Los encabezados de tabla se pueden seleccionar al navegar mediante **Tabulación**, y puede cambiar el orden de clasificación mediante **barra espaciadora**.
* **Teclas de flecha arriba y abajo** se desplaza hacia arriba o hacia abajo por las filas de la tabla.
* Cuando se selecciona una fila o está enfocada, se utiliza **Entrar** en la fila proporciona detalles en el carril derecho.
* Cuando una fila está seleccionada o en foco, utilice **teclas de flecha** para moverse por cada elemento de la fila.
* Uso **Entrar** para seleccionar un elemento en la fila. Se avisa a los usuarios con lectores de pantalla si es necesario abrir una nueva ventana.
* Si amplía el zoom al 200 % o más, puede ver la variable **inspector de raíl** a medida que el carril derecho se contrae para proporcionar más espacio de visualización para la tabla.

![Icono del inspector de raíl enfocado cuando un usuario aumenta al 200%.](images/rail-inspector.png)

### Accesibilidad del teclado de la tabla

| Accesibilidad del teclado | Descripción |
|---|---|
| HOME (Función + flecha izquierda) | Cuando la fila está centrada, lleva a los usuarios al primer elemento de la fila |
| END (Función + flecha derecha) | Cuando la fila está centrada, lleva a los usuarios al último elemento de la fila |
| Re Pág | Recorre 10 filas hacia arriba en la tabla (por página) |
| Page down | Desplaza 10 filas hacia abajo en la tabla (por página) |
| Control + HOME | Accede a la primera fila de la tabla |
| Control + END | Accede a la primera palabra de la tabla por página |

## IU del Editor de esquemas

La interfaz de usuario del Editor de esquemas es accesible a través de la siguiente funcionalidad:

* El Editor de esquemas admite la navegación mediante el teclado, incluido el uso de **Tabulación** para navegar por los elementos de la interfaz de usuario.
* **Tabulación** introduce el campo de búsqueda y, a continuación, en el árbol de esquema.
* El árbol de esquemas admite el uso de teclas de flecha para navegar por la interfaz de usuario del árbol de esquemas
   * **Flechas arriba y abajo** para recorrer el árbol.
   * **Flechas izquierda y derecha** se puede utilizar para expandir y contraer nodos o para moverse entre acciones en línea en el árbol de esquemas.
* **Intro (devolución)** activa los detalles de nodos individuales en el panel de detalles de la derecha.
* La variable **Página principal** vuelve a la parte superior del árbol.
* La variable **Fin** se desplaza hasta la parte inferior del árbol.
* El árbol de esquema también incluye etiquetas ARIA para lectores de pantalla.

## Interfaz de usuario del Generador de segmentos

Al utilizar la interfaz de usuario del Generador de segmentos para crear, editar e interactuar con segmentos dentro del Experience Platform, las siguientes funciones mejoran la accesibilidad:

* Se puede acceder a la interfaz de usuario del Generador de segmentos mediante la navegación mediante el teclado.
* Los lectores de pantalla deben reconocer las etiquetas de marcado de los encabezados y pueden anunciar el encabezado junto con su nivel.
* Otras tecnologías de asistencia pueden cambiar la visualización de una página mediante el uso de encabezados codificados correctamente para mostrar un esquema o una vista alternativa.

Ahora puede contraer o expandir los carriles izquierdo y derecho del lienzo del generador de segmentos para ganar más espacio en la pantalla. Esta función es especialmente útil, ya que ofrece funciones completas con un zoom del 200%.

![El lienzo del generador de segmentos con las utilidades de publicación de carril izquierdo y derecho resaltadas.](images/left-right-rail-expandables.png)

## Editor del servicio de consultas

Las siguientes funciones de accesibilidad están disponibles en el editor del servicio de consulta:

* El contraste de color en la interfaz de usuario del editor de Query Service cumple con la conformidad de accesibilidad.
* La navegación mediante el teclado es compatible fuera de la interfaz de usuario del editor. La interfaz de usuario del editor es una réplica de código incrustada.

## Ficha Vista del sistema en Fuentes y destinos

Al examinar el **[!UICONTROL Vista del sistema]** en Orígenes y destinos, la siguiente funcionalidad mejora la accesibilidad:

* **Tabulación** establece el enfoque en la primera tarjeta de conexión de origen
   * **Tabulación** para centrarse en el botón dentro de la tarjeta
   * Select **Entrar** para activar el botón de llamada a la acción dentro de la tarjeta
* Selección **Entrar** en la tarjeta de conexión también activa más detalles en el carril derecho
   * Cuando se activa el carril derecho, el enfoque se establece en esa área. **Tabulación** se centra en **Cerrar** para el panel carril derecho. Selección **Tabulación** de nuevo mueve el enfoque a través del panel del carril derecho
   * Si hay más de una tarjeta de conexión de origen, **Tabulación** se desplaza a través de las conexiones
   * Uso **teclas de flecha (arriba, abajo, izquierda y derecha)** para desplazarse por la lista de fuentes
   * Select **Tabulación** para definir el enfoque en el panel del carril derecho
