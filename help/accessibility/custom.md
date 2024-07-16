---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;perfil unificado;perfil unificado;perfil unificado;perfil unificado;rtcp;gráficos XDM
title: Soluciones de accesibilidad personalizadas para Experience Platform
type: Documentation
description: Obtenga más información acerca de las soluciones de accesibilidad personalizadas en la interfaz de usuario de Adobe Experience Platform.
exl-id: cb5ad99e-8a95-4c9e-aae6-1d0036ecf052
source-git-commit: 2cf28acb5b0ddb4965b2d5120333659e0ac460bf
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 0%

---

# Soluciones de accesibilidad personalizadas para Experience Platform

Adobe Experience Platform se mejora continuamente para satisfacer las necesidades de todo tipo de usuarios y se adhiere a los estándares mundiales que incluyen personas con deficiencias visuales, auditivas, de movilidad u otras. Este documento describe las soluciones de accesibilidad personalizadas en la interfaz de usuario de Experience Platform.

## Página principal e IU general

La interfaz de usuario del Experience Platform cumple las relaciones de contraste requeridas para los componentes normales de texto, gráficos e interfaz de usuario. Los colores de la interfaz de usuario también se han elegido para admitir la accesibilidad para todos los usuarios, incluidos los que tienen discapacidades visuales.

En Platform, los elementos de la interfaz de usuario en los que se puede hacer clic o procesar con un puntero también se pueden activar mediante un teclado. Esto incluye la navegación izquierda, reproductores de vídeo, tablas y más.

Experience Platform se esfuerza por cumplir con los estándares de accesibilidad internacionales, incluidas las Directrices de accesibilidad al contenido web 2.1 de nivel A y nivel AA y las normas web de la Iniciativa de accesibilidad web - Aplicaciones de Internet enriquecidas accesibles (WAI-ARIA).

![Página principal de la interfaz de usuario de Adobe Experience Platform.](images/homepage.png)

## Navegación izquierda

La navegación izquierda dentro de la interfaz de usuario del Experience Platform es accesible mediante el teclado y proporciona un contraste de color en los estados normal, de desplazamiento y de selección que cumplen los estándares de accesibilidad.

Desde la pantalla de inicio, los usuarios pueden pulsar el tabulador en el panel de navegación izquierdo. Si selecciona **Mayús + Tab**, el usuario volverá a la pantalla Inicio.

![El Experience Platform dejó la navegación.](images/left-navigation-select.png)

Con la navegación izquierda enfocada, **Tab** lleva a los usuarios a la interacción de expandir y contraer. La capacidad para expandir o contraer la navegación izquierda está activada con **Intro (retorno)**.

![La navegación izquierda del Experience Platform se ha contraído.](images/left-navigation-collapse.png)

Con la navegación izquierda enfocada, las teclas de flecha arriba y abajo navegan a cada elemento de la navegación y cierran continuamente (en otras palabras, el enfoque no se aleja hasta que el usuario aleja la navegación izquierda). Cuando se selecciona, se muestra el enfoque de los elementos de navegación. La selección actual se muestra con un resaltado y texto en negrita. Al seleccionar un elemento de navegación izquierdo, **Intro (volver)** abre el elemento de interfaz de usuario seleccionado en el panel derecho; sin embargo, el enfoque permanece en la navegación izquierda hasta que el usuario sale de la pestaña.

![El Experience Platform dejó seleccionada la navegación con orígenes.](images/left-navigation-sources.png)

Algunas funciones de Platform no están habilitadas para todos los usuarios. Estos elementos aparecen en la navegación, pero no se pueden seleccionar. Al navegar con un teclado, estos elementos se omiten durante la navegación con flecha y no se pueden seleccionar con **Intro (retorno)**.

![No se pueden seleccionar las secciones de navegación de la izquierda del Experience Platform que no estén habilitadas para el usuario.](images/left-navigation-sections-disabled.png)

## Cuadro de diálogo de vídeo incorporado

Los vídeos se pueden ver en Experience Platform mediante la navegación con el teclado para resaltar y seleccionar un vínculo de vídeo disponible. Esto abre un cuadro de diálogo de vídeo incrustado en la interfaz de usuario de Platform.

![Aparece un borde azul alrededor de un elemento seleccionado para indicar que se ha aplicado el enfoque.](images/profile-overview-tab.png)

## Accesibilidad del teclado del cuadro de diálogo de vídeo

El cuadro de diálogo de vídeo incrustado también se puede navegar con el teclado. La siguiente tabla describe la navegación completa del teclado disponible para el cuadro de diálogo de vídeo incrustado.

| Elemento Dialog | Accesibilidad del teclado | Descripción |
|---|---|---|
| Reproducir y pausar | Tabulación<br/>Barra espaciadora | Usa **Tab** para definir el enfoque en el botón de reproducción. **Barra espaciadora** comienza la reproducción del vídeo y pausa la reproducción. |
| Depurador | Tab<br/>Flecha izquierda<br/>Flecha derecha | Cuando se esté reproduciendo el vídeo, usa **Tab** para enfocar el depurador. Con el depurador enfocado, **teclas de flecha izquierda y derecha** omiten la reproducción del vídeo 5 segundos antes y después, respectivamente. |
| Silenciar | Tabulación<br/>Barra espaciadora | Use **Tab** para enfocar el elemento de volumen silencioso. Use la **barra espaciadora** para silenciar o reactivar la reproducción de vídeo. |
| Volumen | Tab<br/>Flecha izquierda<br/>Flecha derecha | Use **Tab** para centrarse en el elemento de volumen. **Las teclas de flecha izquierda y derecha** mueven el volumen hacia arriba y hacia abajo, respectivamente. |
| [!UICONTROL Subtítulos opcionales] (&quot;cc&quot;) | Ficha<br/>Introducir<br/>flecha arriba<br/>flecha abajo | **Tab** a [!UICONTROL subtítulos] (&quot;cc&quot;). Use **Intro** para abrir el menú y **teclas de flecha arriba y abajo** para seleccionar un idioma para los subtítulos. **Escriba** confirma su selección. |
| [!UICONTROL Calidad] | Ficha<br/>Introducir<br/>flecha arriba<br/>flecha abajo | Use **Tab** para enfocar el elemento [!UICONTROL Quality]. Use **Intro** para abrir el menú y las **teclas de flecha arriba y abajo** para seleccionar la calidad del vídeo. **Escriba** confirma su selección. |
| Pantalla completa | Tab<br/>Barra espaciadora o Enter<br/>Escape | Use **Tab** para enfocar el elemento de pantalla completa. Use la barra espaciadora **o Intro** para activar la vista a pantalla completa. **Escape** (&quot;esc&quot;) sale del modo de pantalla completa. |
| Cerrar | Tab<br/>Barra espaciadora o Entrar | Use **Tab** para enfocar el botón de cierre. Use la barra espaciadora **o la tecla Intro** para salir del cuadro de diálogo de vídeo. |

>[!NOTE]
>
>En cualquier momento durante la reproducción, la tecla escape (&quot;esc&quot;) se puede utilizar para cerrar el cuadro de diálogo de vídeo incrustado.

![Cuadro de diálogo de vídeo incrustado con números que identifican los elementos de navegación del teclado.](images/video-dialog.png)

## Arrastrar y soltar archivos

En Experience Platform, todas las zonas de arrastrar y soltar de selección de archivos son accesibles mediante el teclado. Si usa **Tab** para resaltar **[!UICONTROL Elegir archivos]** y usa **Enter o la barra espaciadora** para seleccionarlo, se invoca la interfaz de usuario de selección de archivos del sistema operativo.

Una vez cargado un archivo, se puede navegar por el teclado con un icono de eliminación para eliminar el archivo seleccionado y cargar uno nuevo. Los usuarios pueden usar **Tab** para centrarse en el icono de eliminación y **Entrar o la barra espaciadora** para seleccionarlo. Una vez eliminado el archivo, **[!UICONTROL Elegir archivos]** se enfoca automáticamente y se puede seleccionar.

Alternativamente, si el archivo que se carga no tiene el formato correcto, se muestra un icono de error junto con un mensaje de error y el botón **[!UICONTROL Elegir archivos]** está enfocado y se puede seleccionar.

![Zona de arrastrar y soltar archivos con un mensaje de error y el botón Elegir archivos enfocado.](images/drag-and-drop.png)

El uso de un ratón para seleccionar la zona de arrastrar y soltar también invoca la interfaz de usuario de selección de archivos, o un usuario del ratón puede seleccionar un archivo y arrastrarlo a la zona para comenzar a cargar.

![Zona de arrastrar y soltar archivos enfocada cuando un usuario del mouse arrastra un archivo a la zona.](images/drag-and-drop-mouse-over.png)

## Exploración de tabla

Todas las tablas de la interfaz de usuario del Experience Platform son accesibles mediante el teclado. Es posible explorar e interactuar con filas y columnas de la tabla mediante una serie de métodos abreviados de teclado:

* Desde el encabezado de la tabla, utilice la **flecha abajo** para examinar la tabla. Los encabezados de tabla se pueden seleccionar al navegar por **Tab**, y puede cambiar el orden de clasificación con **barra espaciadora**.
* **Teclas de flecha arriba y abajo** se mueve arriba y abajo por las filas de la tabla.
* Cuando se selecciona una fila o está enfocada, al usar **Enter** en la fila, se proporcionan detalles en el carril derecho.
* Cuando una fila está seleccionada o enfocada, use **teclas de dirección** para desplazarse por cada elemento de la fila.
* Use **Intro** para seleccionar un elemento en la fila. Los usuarios con lectores de pantalla reciben una alerta si se debe abrir una nueva ventana.
* Si amplía la imagen al 200% o más, verá el icono **inspector de raíles** cuando el carril derecho se contraiga para proporcionar más espacio de visualización para la tabla.

![Icono del inspector de carril enfocado cuando un usuario amplía a 200%.](images/rail-inspector.png)

### Explorar accesibilidad del teclado de tabla

| Accesibilidad del teclado | Descripción |
|---|---|
| INICIO (función + flecha izquierda) | Cuando la fila está centrada, lleva a los usuarios al primer elemento de la fila |
| END (función + flecha derecha) | Cuando la fila está centrada, lleva a los usuarios al último elemento de la fila |
| Re Pág | Sube 10 filas en la tabla (por página) |
| Página anterior | Recorre 10 filas hacia abajo en la tabla (por página) |
| Control + INICIO | Va a la primera fila de la tabla |
| Control + FIN | Va a la primera palabra de la tabla por página |

## IU del Editor de esquemas

La siguiente funcionalidad permite acceder a la interfaz de usuario del Editor de esquemas:

* El Editor de esquemas admite la navegación mediante el teclado, incluido el uso de **Tab** para navegar por los elementos de la interfaz de usuario.
* **Tab** entra en el campo de búsqueda y luego en el árbol de esquemas.
* El árbol de esquemas admite el uso de teclas de flecha para desplazarse por la interfaz de usuario del árbol de esquemas
   * **Se pueden usar flechas arriba y abajo** para atravesar el árbol.
   * **Las flechas izquierda y derecha** se pueden usar para expandir y contraer nodos o para moverse entre acciones en línea en el árbol de esquemas.
* **Intro (Retorno)** activa los detalles individuales del nodo en el panel de detalles de la derecha.
* La clave **Home** vuelve a la parte superior del árbol.
* La tecla **End** se desplaza al final del árbol.
* El árbol de esquema también incluye etiquetas ARIA para lectores de pantalla.

## IU del Generador de segmentos

Al utilizar la interfaz de usuario del Generador de segmentos para crear, editar e interactuar con segmentos dentro de Experience Platform, las siguientes funciones mejoran la accesibilidad:

* Se puede acceder a la IU del Generador de segmentos mediante la navegación mediante el teclado.
* Los lectores de pantalla deben reconocer las etiquetas de marcado de los encabezados y pueden anunciarlos junto con su nivel.
* Otras tecnologías de asistencia pueden cambiar la visualización visual de una página, utilizando encabezados codificados correctamente para mostrar una vista esquemática o alternativa.

Ahora puede contraer o expandir los carriles izquierdo y derecho del lienzo del generador de segmentos para obtener más espacio en la pantalla. Esta función es especialmente útil, ya que ofrece una funcionalidad completa con un zoom del 200%.

![El lienzo del generador de segmentos con los widgets de revelación de carril izquierdo y derecho resaltados.](images/left-right-rail-expandables.png)

## Editor del servicio de consultas

Las siguientes funciones de accesibilidad están disponibles en el editor del servicio de consultas:

* El contraste de color en la interfaz de usuario del editor del servicio de consultas cumple los requisitos de accesibilidad.
* La navegación mediante el teclado es compatible fuera de la interfaz de usuario del editor. La interfaz de usuario del editor es un reflejo de código incrustado.

>[!NOTE]
>
>El editor de consultas no administra la clave **Tab** de forma predeterminada. Para invocar la funcionalidad **Tab** mientras estás en el editor, debes presionar la tecla **Escape** y luego presionar **Tab** directamente después. Pulse **Tab** de nuevo para desplazar el enfoque más allá del editor.

## Pestaña Vista de sistema en Orígenes y destinos

Al examinar **[!UICONTROL Vista de sistema]** en orígenes y destinos, la siguiente funcionalidad mejora la accesibilidad:

* **Tab** establece el enfoque en la primera tarjeta de conexión de origen
   * **Tabulador** de nuevo para enfocarse en el botón dentro de la tarjeta
   * Seleccione **Enter** para activar el botón de llamada a la acción dentro de la tarjeta
* Seleccionar **Enter** en la tarjeta de conexión también activa más detalles en el carril derecho
   * Cuando se activa el carril derecho, el enfoque se establece en esa área. **Tab** se centra en **Cerrar** para el panel del carril derecho. Si vuelve a seleccionar **Tab**, el enfoque se mueve a través del panel del carril derecho
   * Si hay más de una tarjeta de conexión de origen, **Tab** se mueve a través de las conexiones
   * Utilice **teclas de dirección (arriba, abajo, izquierda y derecha)** para desplazarse por la lista de orígenes
   * Seleccione **Tab** para establecer el enfoque en el panel del carril derecho
