---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;conectar;conectar con el servicio de consultas;aqua data studio;Aqua Data Studio;Buscador;mirador;Postico;postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Conectar clientes al servicio de consultas
description: En este documento se explica cómo conectarse al servicio de consultas desde diversas aplicaciones cliente de escritorio y cómo comprobar esas conexiones.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 5e5a196074e844826579102fa6b36102c6481096
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Conectar clientes al servicio de consultas

En esta sección se explica cómo conectarse al servicio de consultas desde diversas aplicaciones cliente de escritorio y cómo comprobar esas conexiones. El servicio de consultas utiliza el protocolo PostgreSQL, por lo que las instrucciones de esta sección explican cómo utilizar las herramientas y los controladores de PostgreSQL para conectarse y escribir consultas.

>[!IMPORTANT]
>
>Los certificados TLS/SSL en entornos de producción para la API interactiva de Postgres del servicio de consulta se actualizaron el miércoles, 24 de enero de 2024.<br>Aunque se trata de un requisito anual, en esta ocasión el certificado raíz de la cadena también ha cambiado porque el proveedor de certificados TLS/SSL de Adobe ha actualizado su jerarquía de certificados. Esto puede afectar a ciertos clientes de Postgres si a su lista de autoridades certificadoras les falta el certificado raíz. Por ejemplo, un cliente CLI de PSQL puede necesitar que se agreguen los certificados raíz a un archivo explícito `~/postgresql/root.crt`; de lo contrario, esto puede generar un error, como `psql: error: SSL error: certificate verify failed`. Consulte la [documentación oficial de PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) para obtener más información sobre este problema.<br>El certificado raíz que desea agregar se puede descargar desde [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Se proporcionan instrucciones para los siguientes clientes:

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)

>[!IMPORTANT]
>
>Como usuario de Power BI y Tableau, puede conectar Customer Journey Analytics a sus herramientas de BI con las credenciales proporcionadas en la pestaña Credenciales del servicio de consulta. Consulte la documentación de credenciales para obtener instrucciones sobre cómo [conectar las herramientas de BI a Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).
