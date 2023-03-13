---
title: Compatibilidad con CDN Premium para etiquetas
description: Obtenga información acerca de la función Premium de CDN para etiquetas y cómo se puede utilizar para entregar contenido en varias regiones geográficas.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Compatibilidad con CDN Premium para etiquetas (Beta)

>[!IMPORTANT]
>
>La función Premium de CDN para etiquetas está actualmente en versión beta y es posible que su organización aún no tenga acceso a ella. Esta documentación está sujeta a cambios.

Cuando utiliza un [host administrado por Adobe](./hosts/managed-by-adobe-host.md) para ofrecer sus recursos de etiquetas de Adobe Experience Platform en su sitio web, estos se distribuyen entre varias redes de entrega de contenido (CDN) de todo el mundo para ofrecer la velocidad de descarga más rápida. Sin embargo, hay ciertas regiones que requieren que todos los recursos del sitio web se dupliquen y alojen en un servidor dentro de esa región.

Para tener en cuenta esto, las etiquetas de Experience Platform proporcionan una función de CDN Premium que le permite enviar contenido a estas regiones especiales.

La compatibilidad con CDN Premium es una función de pago y su organización debe adquirirla para habilitarla y utilizarla. Esta guía explica cómo configurar y utilizar esta función en la IU de Experience Platform o en la IU de recopilación de datos después de comprarla.

## Habilite CDN Premium para su organización

La CDN Premium está habilitada en el nivel de compañía. Una vez que su organización haya adquirido la función Premium de CDN, un administrador de Adobes la habilitará en la interfaz de usuario de para su empresa.

## Reconstruir e instalar bibliotecas de etiquetas con códigos incrustados actualizados

Una vez habilitada la CDN Premium, no significa que los recursos de etiquetas se dupliquen inmediatamente y estén listos para usarlos dentro de las nuevas regiones. Solo significa que ahora puede elegir cuándo adherirse a esta funcionalidad.

>[!IMPORTANT]
>
>Las bibliotecas creadas antes de habilitar CDN Premium seguirán funcionando tal cual exactamente como lo hacen hoy. Esto también se aplica a las bibliotecas no administradas por el Adobe, ya que [entornos archivados](./environments.md#archive) solo utilizan direcciones URL relativas para sus rutas de recursos. Tenga en cuenta que, después de habilitar CDN Premium, cualquier biblioteca que cree que no esté administrada por Adobe se comportará como si la función CDN Premium no estuviera habilitada.

Una vez que haya habilitado Premium CDN y haya reconstruido las bibliotecas que desee utilizar desde las nuevas regiones de alojamiento, puede recuperar los nuevos códigos incrustados de región de alojamiento para añadirlos a sus sitios web.

>[!NOTE]
>
>El código incrustado de biblioteca de que se enumera en la variable [!UICONTROL Standard] La región de alojamiento seguirá funcionando tal cual, así como cualquier código incrustado de Principio de página o Final de página que ya esté en los sitios web.

Visite la **[!UICONTROL Entornos]** o vea las instrucciones de instalación del entorno desde la pantalla de edición de la biblioteca para buscar los nuevos códigos incrustados. Cada nueva región de alojamiento admitida aparece después de [!UICONTROL Standard] región de alojamiento (se utiliza para áreas en el mundo que son compatibles sin CDN Premium). La captura de pantalla siguiente muestra un código incrustado para la región de China, que utiliza `.cn` como su dominio de nivel superior (TLD).

![Código incrustado para la región de China](../../images/ui/publishing/premium-cdn/embed-codes.png)

Elija el código incrustado adecuado para la página web y péguelo dentro de `<head>` de su documento. Para obtener más información sobre el uso de códigos incrustados para instalar bibliotecas de etiquetas, consulte la [Guía de IU de entornos](./environments.md#installation).

## Pasos siguientes

En esta guía se explica cómo habilitar e instalar la función Premium de CDN para la implementación de etiquetas. Para obtener más información sobre la instalación y prueba de bibliotecas de etiquetas en las propiedades web y móviles, consulte la [resumen de publicación](./overview.md).
