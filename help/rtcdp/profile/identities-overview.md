---
keywords: identidades rtcdp;identidades rtcdp;identidades cdp en tiempo real
title: Identidades en Real-time Customer Data Platform
description: El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas.
feature: Get Started, Identities
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# Resumen de identidades

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas. Normalmente, los clientes interactúan con su marca en varios canales, como navegar por su sitio web en línea, realizar una compra en la tienda, unirse al programa de fidelidad o llamar a un servicio de asistencia para obtener asistencia, por nombrar algunos. En estos sistemas múltiples, existe una identidad creada para ese cliente, y [!DNL Identity Service] hace posible reunir esas identidades para ver la imagen completa.

Ahora, en lugar de cinco clientes independientes que interactúan con su marca en cinco canales diferentes, puede ver que se trata del mismo cliente y puede asegurarse de que reciban una experiencia coherente, personalizada y relevante mediante cada interacción. A medida que se conoce más información sobre su cliente (por ejemplo, un navegador anónimo de su sitio web decide registrarse para una cuenta e iniciar sesión), esa información se vincula y la imagen de su cliente se vuelve cada vez más clara.

## Áreas de nombres de identidad

Las áreas de nombres de identidad son un componente de [!DNL Identity Service] y sirven como indicadores que proporcionan contexto adicional a las identidades de los clientes. Un ejemplo de área de nombres de ID que se utiliza con frecuencia sería &quot;Correo electrónico&quot;, donde el uso de la misma dirección de correo electrónico en varios sitios web le permite unir varias identidades diferentes, cada una con un ID de cliente único, como si realmente pertenecieran al mismo cliente. [!DNL Experience Platform] le permite utilizar áreas de nombres de ID para buscar perfiles individuales dentro de la interfaz de usuario. Para obtener más información sobre la visualización de perfiles, consulte la [descripción general del examen de perfiles](profile-browse.md). Para obtener más información sobre áreas de nombres de identidad, consulte la [descripción general del área de nombres de identidad](../../identity-service/features/namespaces.md).

## Gráficos de identidad

Un gráfico de identidad es un mapa de relaciones entre identidades diferentes, que le proporciona una representación visual de cómo su cliente interactúa con su marca en diferentes canales. El servicio de identidad administra y actualiza colectivamente todos los gráficos de identidad de los clientes en respuesta a la actividad de los clientes.

[!DNL Identity Service] administra un gráfico de identidades visible solamente para su organización y creado a partir de sus datos. [!DNL Identity Service] aumenta el gráfico cuando un registro de datos ingerido contiene más de una identidad, lo que agrega una relación entre las identidades encontradas.

## Pasos siguientes

[!DNL Identity Service] define y mantiene las identidades y las relaciones entre ellas, y [!DNL Real-Time Customer Profile] las aprovecha para generar una imagen completa de cada cliente individual y sus interacciones. Para obtener más información, visite la [documentación del servicio de identidad](../../identity-service/home.md).
