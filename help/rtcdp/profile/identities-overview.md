---
title: Identidades y Áreas de nombres de identidad
seo-title: Servicio de ID de Adobe Experience Platform
description: description
seo-description: descripción de seo
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Identidades en CDP en tiempo real

Adobe Experience Platform Identity Service le ayuda a obtener una mejor vista de sus clientes y su comportamiento al unir identidades entre dispositivos y sistemas. Normalmente, los clientes interactúan con la marca en varios canales, como explorar el sitio web en línea, realizar una compra en la tienda, unirse a su programa de fidelidad o llamar a un servicio de asistencia para obtener ayuda, por citar algunos. En estos múltiples sistemas, se crea una identidad para ese cliente, y el servicio de identidad permite unir esas identidades para ver el panorama completo.

Ahora, en lugar de cinco clientes distintos que interactúan con su marca en cinco canales diferentes, puede ver que es el mismo cliente y puede asegurarse de que reciben una experiencia coherente, personalizada y relevante a través de cada interacción. A medida que se va conociendo más información sobre su cliente (por ejemplo, un navegador anónimo del sitio Web decide registrarse para una cuenta e iniciar sesión), la información se vincula y la imagen de su cliente se vuelve cada vez más clara.

## Áreas de nombres de identidad

Las Áreas de nombres de identidad son un componente del servicio de identidad y sirven de indicadores que proporcionan un contexto adicional a las identidades de los clientes. Un ejemplo de una Área de nombres de ID de uso común sería &quot;Correo electrónico&quot;, donde el uso de la misma dirección de correo electrónico en varios sitios web permite unir varias identidades diferentes, cada una con un ID de cliente único, ya que en realidad pertenece al mismo cliente. La plataforma de experiencia permite utilizar Áreas de nombres de ID para buscar perfiles individuales en la interfaz de usuario. Para obtener más información sobre la visualización de perfiles, consulte la descripción general [del visor de](/help/rtcdp/profile/profile-viewer.md)perfil. Para obtener más información sobre las Áreas de nombres de identidad, consulte la descripción general [de la Área de nombres de](../../identity-service/namespaces.md)identidad.

## Gráficos de identidad

Un gráfico de identidad es un mapa de las relaciones entre diferentes Áreas de nombres de identidad, que le proporciona una representación visual de la forma en que el cliente interactúa con la marca en diferentes canales. Todos los gráficos de identidad del cliente son administrados y actualizados colectivamente por Identity Service en tiempo real, en respuesta a la actividad del cliente.

Identity Service administra un gráfico de identidad visible únicamente por su organización y creado en función de sus datos, denominado gráfico privado. Identity Service aumenta el gráfico privado cuando un registro de datos ingerido contiene más de una identidad, agregando una relación entre las identidades encontradas.

## Pasos siguientes

El servicio de identidad define y mantiene las identidades y las relaciones entre ellas, y las aprovecha el Perfil del cliente en tiempo real para obtener una imagen completa de cada cliente individual y sus interacciones. Para obtener más información, visite la documentación [del servicio de](../../identity-service/home.md)identidad.