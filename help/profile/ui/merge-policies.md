---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guía del usuario de directivas de combinación
topic: guide
translation-type: tm+mt
source-git-commit: 83c7ff45af7266904121b7ff6edcb0f9b0559fee

---


# Guía del usuario de directivas de combinación

Adobe Experience Platform le permite reunir datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que utiliza la Plataforma para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada.

Mediante las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar políticas existentes y establecer una directiva de combinación predeterminada para su organización. Esta guía proporciona instrucciones paso a paso para trabajar con políticas de combinación mediante la interfaz de usuario de Adobe Experience Platform.

Si prefiere trabajar con políticas de combinación mediante la API de Perfil del cliente en tiempo real, siga las instrucciones descritas en el tutorial [de API de políticas de](../api/merge-policies.md)combinación.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los diversos servicios de la plataforma de experiencia relacionados con las políticas de combinación. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

* [Perfil](../home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Servicio](../../identity-service/home.md)de identidad: Permite el Perfil del cliente en tiempo real al enlazar identidades de orígenes de datos dispares que se están ingeriendo en la plataforma.
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

## Directivas de combinación de Vistas

En la interfaz de usuario de la plataforma de experiencia, puede empezar a trabajar con políticas de combinación y ver una lista de las directivas de combinación existentes de su organización haciendo clic en el **Perfil** en el carril izquierdo y, a continuación, seleccionando la ficha **Combinar directivas** .

![página de aterrizaje de políticas de combinación](../images/merge-policies/landing.png)

Los detalles de cada directiva de combinación disponible para su organización están visibles en la página de aterrizaje, incluidos el nombre *de la* directiva, la directiva *de combinación* predeterminada y el *Esquema*.

Para seleccionar qué detalles están visibles o para agregar columnas adicionales a la pantalla, seleccione el icono del selector de columnas de la derecha y haga clic en el nombre de una columna para agregarla o quitarla de la vista.

![](../images/merge-policies/adjust-view.png)

## Crear una directiva de combinación

Para crear una nueva directiva de combinación, haga clic en **Crear directiva** de combinación cerca de la parte superior derecha de la ficha **Combinar directivas** .

![página de aterrizaje de políticas de combinación](../images/merge-policies/create-new.png)

Aparece la pantalla **Crear directiva** de combinación, que le permite proporcionar información importante para la nueva directiva de combinación.

![](../images/merge-policies/create.png)

* **Nombre**: El nombre de la directiva de combinación debe ser descriptivo pero conciso.
* **Esquema**: esquema asociado a la directiva de combinación. Esto especifica el esquema XDM para el que se crea esta directiva de combinación. Las organizaciones pueden crear varias directivas de combinación por esquema.
* **Coincidencia** de ID: Este campo define cómo determinar las identidades relacionadas de un cliente. Existen dos valores posibles:
   * **Ninguno**: No realice ninguna vinculación de identidad.
   * **Gráfico** privado: Realice la vinculación de identidad en función del gráfico de identidad privado.
* **Combinación** de atributos: Un fragmento de perfil es la información de perfil para una sola identidad de la lista de identidades que existe para un cliente individual. Cuando el tipo de gráfico de identidad utilizado da como resultado más de una identidad, existe la posibilidad de que se produzcan conflictos entre los valores de propiedad de perfil y se debe especificar la prioridad. El uso de la combinación *de* atributos permite especificar los valores de perfil de conjuntos de datos que se deben priorizar si se produce un conflicto de combinación. Existen dos valores posibles:
   * **Marca de hora pedida**: En caso de conflicto, dé prioridad al perfil que se actualizó más recientemente.
   * **Prioridad** del conjunto de datos: Asigne prioridad a los fragmentos de perfil en función del conjunto de datos del que provienen. Al seleccionar esta opción, debe seleccionar los conjuntos de datos relacionados y su orden de prioridad. Consulte los detalles sobre la prioridad [del](#dataset-precedence) conjunto de datos a continuación para obtener más información.
* **Directiva** de combinación predeterminada: Botón de alternancia que permite seleccionar si esta directiva de combinación será o no la predeterminada para su organización. Si el selector está activado y se guarda la nueva directiva, la directiva predeterminada anterior se actualiza automáticamente para que ya no sea la predeterminada.

### Prioridad de conjunto de datos {#dataset-precedence}

Al seleccionar un valor de combinación *de* atributos, puede seleccionar la prioridad ** de conjunto de datos, que le permite dar prioridad a los fragmentos de perfil según el conjunto de datos del que provienen.

Un caso de uso de ejemplo sería si su organización tuviera información presente en un conjunto de datos que sea preferible o de confianza sobre los datos de otro conjunto de datos.

Al seleccionar la prioridad ** del conjunto de datos, se abre un panel independiente que requiere que seleccione entre los conjuntos de datos ** disponibles (o utilice la casilla de verificación para seleccionar todos) los conjuntos de datos que se incluirán. A continuación, puede arrastrar y soltar esos conjuntos de datos en el panel Conjuntos de datos ** seleccionados y arrastrarlos al orden de prioridad correcto. Al conjunto de datos superior se le dará la prioridad más alta, luego al segundo más alto, y así sucesivamente.

![](../images/merge-policies/dataset-precedence.png)

Una vez que haya terminado de crear la directiva de combinación, haga clic en **Guardar** para volver a la ficha *Combinar directivas* , donde la nueva directiva de combinación aparece ahora en la lista de políticas.

## Editar una directiva de combinación

Puede modificar una directiva de combinación existente a través de la ficha *Combinar directivas* haciendo clic en el nombre *de* directiva de la directiva de combinación que desee editar.

![página de aterrizaje de políticas de combinación](../images/merge-policies/select-edit.png)

Cuando aparece la pantalla *Editar directiva* de combinación, puede realizar cambios en los tipos de combinación ** Nombre *,* Esquema *,* ID *y* ** Atributo, así como seleccionar si esta directiva será o no la directiva de combinación predeterminada de su organización.

>[!Note]
>No se puede editar la ID de la directiva de combinación, que se muestra en la parte superior de la pantalla de edición. Se trata de un ID de sólo lectura, generado por el sistema, que no se puede cambiar.

![](../images/merge-policies/edit-screen.png)

Una vez que haya realizado los cambios necesarios, haga clic en **Guardar** para volver a la ficha *Combinar directivas* , donde la información actualizada de la directiva de combinación ya está visible.

![](../images/merge-policies/edited.png)


## Pasos siguientes

Ahora que ha creado y configurado directivas de combinación para su organización de IMS, puede utilizarlas para crear segmentos de audiencia a partir de los datos de perfil. Consulte la descripción general [de la](../../segmentation/home.md) segmentación para obtener más información sobre cómo crear y trabajar con segmentos mediante la plataforma de experiencia.