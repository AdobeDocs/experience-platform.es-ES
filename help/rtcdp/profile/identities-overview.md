---
title: Identidades y espacios de nombres de identidad
seo-title: Servicio de ID de Adobe Experience Platform
description: descripción
seo-description: descripción de seo
translation-type: tm+mt
source-git-commit: 5cba5a1e8139dd85f23250d42a1cd8d2318eb916

---


# Identidades en CDP en tiempo real

Adobe Experience Platform Identity Service le ayuda a obtener una mejor vista de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas. Normalmente, los clientes interactúan con su marca a través de múltiples canales, lo que podría incluir explorar su sitio web en línea, realizar una compra en la tienda, unirse a su programa de fidelidad o llamar a un servicio de asistencia para obtener ayuda, por citar algunos. En estos múltiples sistemas, se crea una identidad para ese cliente, y el servicio de identidad permite unir esas identidades para ver el panorama completo.

Ahora, en lugar de cinco clientes distintos que interactúan con su marca en cinco canales diferentes, puede ver que es el mismo cliente y asegurarse de que reciben una experiencia consistente, personalizada y relevante a través de cada interacción. A medida que se va conociendo más información sobre su cliente (por ejemplo, un navegador anónimo del sitio Web decide registrarse para una cuenta e iniciar sesión), la información se vincula y la imagen de su cliente se vuelve cada vez más clara.

## Espacios de nombres de identidad

Los espacios de nombres de identidad son un componente de Identity Service y sirven como indicadores que proporcionan contexto adicional a las identidades de los clientes. Un ejemplo de un espacio de nombres de ID de uso común sería &quot;Correo electrónico&quot;, donde el uso de la misma dirección de correo electrónico en varios sitios web permite unir varias identidades diferentes, cada una con un ID de cliente único, ya que en realidad pertenece al mismo cliente. La plataforma de experiencia permite utilizar espacios de nombres de ID para buscar perfiles individuales dentro de la interfaz de usuario. Para obtener más información sobre la visualización de perfiles, consulte la descripción general [del visor de](/help/rtcdp/profile/profile-viewer.md)perfiles. Para obtener más información sobre los espacios de nombres de identidad, consulte la descripción general del espacio de nombres de [identidad en Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md).

## Gráficos de identidad

Un gráfico de identidad es un mapa de las relaciones entre diferentes espacios de nombres de identidad, que le proporciona una representación visual de la forma en que el cliente interactúa con la marca a través de distintos canales. Todos los gráficos de identidad del cliente son administrados y actualizados colectivamente por Identity Service en tiempo real, en respuesta a la actividad del cliente.

Identity Service administra un gráfico de identidad visible únicamente por su organización y creado en función de sus datos, denominado gráfico privado. Identity Service aumenta el gráfico privado cuando un registro de datos ingerido contiene más de una identidad, agregando una relación entre las identidades encontradas.

## Pasos siguientes

El servicio de identidad define y mantiene las identidades y las relaciones entre ellas, y lo aprovecha el perfil del cliente en tiempo real para obtener una imagen completa de cada cliente individual y sus interacciones. Para obtener más información, visite la documentación del servicio de [identidad en Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_architectural_overview.md).