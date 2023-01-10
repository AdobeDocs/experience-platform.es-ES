---
keywords: Experience Platform;resolución de problemas;Data Science Workspace;temas populares
solution: Experience Platform
title: Guía de solución de problemas de Data Science Workspace
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] guía de solución de problemas

Este documento proporciona respuestas a las preguntas frecuentes acerca de Adobe Experience Platform [!DNL Data Science Workspace]. Para preguntas y solución de problemas con [!DNL Platform] API en general, consulte la [Guía de solución de problemas de la API de Adobe Experience Platform](../landing/troubleshooting.md).

## Estado de consulta de JupyterLab Notebook atascado en el estado de ejecución

Un bloc de notas de JupyterLab puede indicar que una celda está en estado de ejecución, indefinidamente, en algunas condiciones de memoria. Por ejemplo, al consultar un conjunto de datos grande o realizar varias consultas subsiguientes, el bloc de notas de JupyterLab puede quedarse sin memoria disponible para almacenar el objeto dataframe resultante. Hay algunos indicadores que se pueden ver en esta situación. Primero, el núcleo entra en estado inactivo aunque la celda se muestre como ejecutándose indicada por el [`*`] junto a la celda. Además, la barra inferior indica la cantidad de RAM utilizada/disponible.

![RAM disponible](./images/jupyterlab/user-guide/allocate-ram.png)

Durante la lectura de los datos, la memoria puede crecer hasta alcanzar la cantidad máxima de memoria asignada. La memoria se libera tan pronto como se alcanza la memoria máxima y se reinicia el núcleo. Esto significa que la memoria usada en este escenario puede mostrarse como muy baja debido al reinicio del núcleo, mientras que justo antes del reinicio, la memoria hubiera estado muy cerca de la RAM máxima asignada.

Para resolver este problema, seleccione el icono de engranaje en la parte superior derecha de JupyterLab y deslice el control deslizante a la derecha seguido de la selección **[!UICONTROL Actualizar configuraciones]** para asignar más RAM. Además, si está ejecutando múltiples consultas y su valor de RAM está cerca de la cantidad máxima asignada, a menos que necesite los resultados de consultas anteriores, reinicie el núcleo para restablecer la cantidad disponible de RAM. Esto garantiza que tenga la cantidad máxima de RAM disponible para la consulta actual.

![asignar más ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

En el caso de que asigne la cantidad máxima de memoria (RAM) y siga teniendo este problema, puede modificar la consulta para que funcione en un tamaño de conjunto de datos más pequeño reduciendo las columnas o el rango de datos. Para utilizar toda la cantidad de datos, se recomienda utilizar un bloc de notas Spark.

## [!DNL JupyterLab] el entorno no se carga en [!DNL Google Chrome]

>[!IMPORTANT]
>
>Este problema se ha resuelto, pero aún podría estar presente en el explorador Google Chrome 80.x. Asegúrese de que el explorador Chrome esté actualizado.

Con la variable [!DNL Google Chrome] versión 80.x del explorador, todas las cookies de terceros están bloqueadas de forma predeterminada. Esta política puede evitar [!DNL JupyterLab] desde la carga en Adobe Experience Platform.

Para solucionar este problema, siga estos pasos:

En [!DNL Chrome] , vaya a la parte superior derecha y seleccione **Configuración** (también puede copiar y pegar &quot;chrome://settings/&quot; en la barra de direcciones). A continuación, desplácese hasta la parte inferior de la página y haga clic en el botón **Avanzadas** lista desplegable.

![avanzado de chrome](./images/faq/chrome-advanced.png)

La variable **Privacidad y seguridad** aparece. A continuación, haga clic en **Configuración del sitio** seguido de **Cookies y datos del sitio**.

![avanzado de chrome](./images/faq/privacy-security.png)

![avanzado de chrome](./images/faq/cookies.png)

Por último, cambie &quot;Bloquear cookies de terceros&quot; a &quot;Desactivado&quot;.

![avanzado de chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>También puede deshabilitar las cookies de terceros y agregar [*.]ds.adobe.net a la lista de permitidos .

Vaya a &quot;chrome://flags/&quot; en la barra de direcciones. Busque y deshabilite el indicador llamado *&quot;SameSite con cookies predeterminadas&quot;* utilizando el menú desplegable de la derecha.

![deshabilitar indicador samesite](./images/faq/samesite-flag.png)

Después del paso 2, se le pedirá que vuelva a iniciar el explorador. Después de reiniciar, [!DNL Jupyterlab] debe ser accesible.

## ¿Por qué no puedo acceder a [!DNL JupyterLab] en Safari?

Safari deshabilita las cookies de terceros de forma predeterminada en Safari &lt; 12. Porque [!DNL Jupyter] la instancia de máquina virtual reside en un dominio diferente al de su fotograma principal; actualmente, Adobe Experience Platform requiere que se habiliten las cookies de terceros. Habilite las cookies de terceros o cambie a un explorador diferente como [!DNL Google Chrome].

Para Safari 12, debe cambiar el agente de usuario a &quot;[!DNL Chrome]&#39; o &#39;[!DNL Firefox]&#39;. Para cambiar el agente de usuario, abra el *Safari* y seleccione **Preferencias**. Aparecerá la ventana de preferencias.

![Preferencias de Safari](./images/faq/preferences.png)

En la ventana de preferencias de Safari, seleccione **Avanzadas**. A continuación, compruebe el *Mostrar menú Desarrollo en la barra de menús* en la ventana Puede cerrar la ventana de preferencias una vez completado este paso.

![Safari avanzado](./images/faq/advanced.png)

A continuación, en la barra de navegación superior, seleccione la opción **Desarrollo** para abrir el Navegador. Desde dentro de la variable **Desarrollo** lista desplegable, pase el ratón sobre **Agente de usuario**. Puede seleccionar el **[!DNL Chrome]** o **[!DNL Firefox]** Cadena del agente de usuario que desee usar.

![Menú Desarrollo](./images/faq/user-agent.png)

## ¿Por qué veo un mensaje &quot;403 prohibido&quot; al intentar cargar o eliminar un archivo en [!DNL JupyterLab]?

Si el explorador está habilitado con software de bloqueo de anuncios como [!DNL Ghostery] o [!DNL AdBlock] Además, el dominio &quot;\*.adobe.net&quot; debe estar permitido en cada anuncio que bloquee el software para [!DNL JupyterLab] para funcionar normalmente. Esto se debe a que [!DNL JupyterLab] las máquinas virtuales se ejecutan en un dominio diferente al [!DNL Experience Platform] dominio.

## ¿Por qué algunas partes de mi [!DNL Jupyter Notebook] ¿se ven revueltos o no se representan como código?

Esto puede suceder si la celda en cuestión se cambia accidentalmente de &quot;Código&quot; a &quot;Marcado&quot;. Mientras se centra una celda de código, presione la combinación de teclas **ESC+M** cambia el tipo de celda a Markdown. El tipo de celda se puede cambiar mediante el indicador desplegable situado en la parte superior del bloc de notas para las celdas seleccionadas. Para cambiar un tipo de celda a código, comience por seleccionar la celda que desee cambiar. A continuación, haga clic en el menú desplegable que indica el tipo actual de la celda y seleccione &quot;Código&quot;.

![](./images/faq/code_type.png)

## ¿Cómo instalo las [!DNL Python] bibliotecas?

La variable [!DNL Python] viene preinstalado con muchas bibliotecas populares de aprendizaje automático. Sin embargo, puede instalar bibliotecas personalizadas adicionales ejecutando el siguiente comando en una celda de código:

```shell
!pip install {LIBRARY_NAME}
```

Para obtener una lista completa de preinstalados [!DNL Python] bibliotecas, consulte la [sección del apéndice de la Guía del usuario de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## ¿Puedo instalar bibliotecas PySpark personalizadas?

Desafortunadamente, no puede instalar bibliotecas adicionales para el núcleo PySpark. Sin embargo, puede ponerse en contacto con el representante de servicio al cliente de Adobe para que le instalen bibliotecas PySpark personalizadas.

Para obtener una lista de las bibliotecas PySpark preinstaladas, consulte la [sección del apéndice de la Guía del usuario de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## ¿Es posible configurar [!DNL Spark] recursos de clúster para [!DNL JupyterLab] [!DNL Spark] o kernel PySpark?

Puede configurar los recursos añadiendo el siguiente bloque a la primera celda del bloc de notas:

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Para obtener más información, consulte [!DNL Spark] la configuración de los recursos del clúster, incluida la lista completa de propiedades configurables, consulte la [Guía del usuario de JupyterLab](./jupyterlab/overview.md#kernels).

## ¿Por qué recibo un error al intentar ejecutar ciertas tareas para conjuntos de datos más grandes?

Si recibe un error por un motivo como `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Esto suele significar que el controlador o un ejecutor se está quedando sin memoria. Ver los portátiles de JupyterLab [acceso a datos](./jupyterlab/access-notebook-data.md) documentación para obtener más información sobre los límites de datos y cómo ejecutar tareas en conjuntos de datos grandes. Normalmente, este error se puede resolver cambiando la variable `mode` from `interactive` a `batch`.

Además, mientras escribe grandes conjuntos de datos de Spark/PySpark, almacena en caché sus datos (`df.cache()`) antes de ejecutar el código de escritura puede mejorar en gran medida el rendimiento.

<!-- remove this paragraph at a later date once the sdk is updated -->

Si tiene problemas al leer datos y aplica transformaciones a los datos, intente almacenar los datos en caché antes de las transformaciones. El almacenamiento en caché de los datos evita que se lean varias veces en la red. Comience por leer los datos. A continuación, caché (`df.cache()`) los datos. Finalmente, realice las transformaciones.

## ¿Por qué mis portátiles Spark/PySpark tardan tanto en leer y escribir datos?

Si realiza transformaciones en los datos, como el uso de `fit()`, es posible que las transformaciones se estén ejecutando varias veces. Para aumentar el rendimiento, almacene en caché los datos mediante `df.cache()` antes de realizar la `fit()`. Esto garantiza que las transformaciones solo se ejecuten una sola vez y evita que se lean varias veces en la red.

**Pedido recomendado:** Comience por leer los datos. A continuación, realice transformaciones seguidas de almacenamiento en caché (`df.cache()`) los datos. Finalmente, realice una `fit()`.

## ¿Por qué mis portátiles Spark/PySpark no funcionan?

Si está recibiendo cualquiera de los siguientes errores:

- Trabajo anulado debido a un error en la etapa ... Solo puede comprimir RDD con el mismo número de elementos en cada partición.
- Cliente RPC remoto desasociado y otros errores de memoria.
- Rendimiento deficiente al leer y escribir conjuntos de datos.

Compruebe que está almacenando en caché los datos (`df.cache()`) antes de escribir los datos. Al ejecutar código en blocs de notas, mediante `df.cache()` antes de una acción como `fit()` puede mejorar en gran medida el rendimiento de los portátiles. Uso `df.cache()` antes de escribir un conjunto de datos, garantiza que las transformaciones solo se ejecuten una sola vez en lugar de varias veces.

## [!DNL Docker Hub] restricciones de límite en Data Science Workspace

A partir del 20 de noviembre de 2020, entraron en vigor los límites de velocidad para el uso anónimo y autenticado gratuito de Docker Hub. Anónima y libre [!DNL Docker Hub] los usuarios de se limitan a 100 solicitudes de extracción de imágenes de contenedor cada seis horas. Si se ve afectado por estos cambios, recibirá este mensaje de error: `ERROR: toomanyrequests: Too Many Requests.` o `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Actualmente, este límite solo afectará a su organización si está intentando crear 100 Notebook para fórmulas en un lapso de seis horas o si está utilizando portátiles basados en Spark en Data Science Workspace que a menudo están aumentando y reduciendo. Sin embargo, es poco probable, ya que el clúster en el que se ejecutan permanece activo durante dos horas antes de apagarse. Esto reduce el número de llamadas necesarias cuando el clúster está activo. Si recibe cualquiera de los errores anteriores, tendrá que esperar hasta que su [!DNL Docker] se restablece el límite.

Para obtener más información, consulte [!DNL Docker Hub] límites de tasa, visite [Documentación de DockerHub](https://www.docker.com/increase-rate-limits). Se está trabajando en una solución para esto, y se espera que así sea en una versión posterior.
