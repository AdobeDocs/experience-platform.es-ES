---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;conectar;conectar con servicio de consultas;aqua data studio;Aqua Data Studio;Buscador;mirador;póstico;póstico;póstico;Power BI;poder;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Conectar clientes al servicio de consultas
description: En este documento se explica cómo conectarse al servicio de consultas desde diversas aplicaciones cliente de escritorio y cómo comprobar esas conexiones.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 778c65c6310ed4a627be0fd3ae076784cfc8495b
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Conectar clientes a [!DNL Query Service]

En esta sección se explica cómo conectarse a [!DNL Query Service] desde una variedad de aplicaciones cliente de escritorio y cómo comprobar esas conexiones. [!DNL Query Service] utiliza el [!DNL PostgreSQL] , por lo que las instrucciones de esta sección explican cómo utilizar [!DNL PostgreSQL] herramientas y controladores para conectarse y escribir consultas.

>[!IMPORTANT]
>
>Los certificados TLS/SSL en entornos de producción para la API interactiva de Postgres del servicio de consulta se actualizaron el miércoles, 24 de enero de 2024.<br>Aunque se trata de un requisito anual, en esta ocasión el certificado raíz de la cadena también ha cambiado, ya que el proveedor de certificados TLS/SSL de Adobe ha actualizado su jerarquía de certificados. Esto puede afectar a ciertos clientes de Postgres si a su lista de autoridades de certificación les falta el certificado raíz. Por ejemplo, un cliente CLI de PSQL puede necesitar que se agreguen los certificados raíz a un archivo explícito `~/postgresql/root.crt`, de lo contrario, esto puede provocar un error. Por ejemplo, `psql: error: SSL error: certificate verify failed`. Consulte la [Documentación oficial de PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) para obtener más información sobre este problema.<br>El certificado raíz que se va a agregar se puede descargar desde [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Se proporcionan instrucciones para los siguientes clientes:

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)
