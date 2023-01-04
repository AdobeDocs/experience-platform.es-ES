---
keywords: identidades rtcdp;identidades rtcdp;identidades cdp en tiempo real
title: Identidades en Real-time Customer Data Platform
description: El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de sus clientes y su comportamiento al unir identidades entre dispositivos y sistemas.
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Información general sobre identidades

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor visión de sus clientes y su comportamiento al unir identidades entre dispositivos y sistemas. Normalmente, los clientes interactúan con la marca a través de varios canales. Esto podría incluir examinar el sitio web en línea, realizar una compra en la tienda, unirse al programa de fidelidad o llamar a un servicio de asistencia técnica, por nombrar algunos. En estos sistemas múltiples, existe una identidad creada para ese cliente y [!DNL Identity Service] permite unir esas identidades para ver el panorama completo.

Ahora, en lugar de que cinco clientes separados interactúen con su marca en cinco canales diferentes, puede ver que este es el mismo cliente y puede asegurarse de que reciban una experiencia coherente, personalizada y relevante a través de cada interacción. A medida que se conoce más información sobre el cliente (por ejemplo, un navegador anónimo del sitio web decide registrarse para una cuenta e iniciar sesión), esa información se vincula y la imagen del cliente se hace cada vez más clara.

## Espacios de nombres de identidad

Las áreas de nombres de identidad son un componente de [!DNL Identity Service] y sirven como indicadores que proporcionan un contexto adicional a las identidades de los clientes. Un ejemplo de área de nombres de ID utilizada comúnmente sería &quot;Correo electrónico&quot;, donde el uso de la misma dirección de correo electrónico en varios sitios web permite unir varias identidades diferentes, cada una con un ID de cliente único, como perteneciente al mismo cliente. [!DNL Experience Platform] permite utilizar áreas de nombres de ID para buscar perfiles individuales dentro de la interfaz de usuario. Para obtener más información sobre la visualización de perfiles, consulte la [información general sobre la exploración de perfiles](profile-browse.md). Para obtener más información sobre las áreas de nombres de identidad, consulte la [información general del área de nombres de identidad](../../identity-service/namespaces.md).

## Gráficos de identidad

Un gráfico de identidad es un mapa de relaciones entre diferentes áreas de nombres de identidad, que proporciona una representación visual de cómo el cliente interactúa con la marca a través de diferentes canales. Todos los gráficos de identidad de clientes se administran y actualizan de forma colectiva por [!DNL Identity Service] casi en tiempo real, en respuesta a la actividad del cliente.

[!DNL Identity Service] administra un gráfico de identidad visible solo por su organización y creado en función de sus datos, denominado gráfico privado. [!DNL Identity Service] aumenta el gráfico privado cuando un registro de datos ingerido contiene más de una identidad, añadiendo una relación entre las identidades encontradas.

## Pasos siguientes

Las identidades y las relaciones entre ellas se definen y mantienen por [!DNL Identity Service] y aprovechado por [!DNL Real-Time Customer Profile] para crear una imagen completa de cada cliente individual y sus interacciones. Para obtener más información, visite [Documentación del servicio de identidad](../../identity-service/home.md).
