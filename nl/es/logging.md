---

copyright:
  years: 2018
lastupdated: "2018-06-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Visualización de registros de uso y llamadas
{: #logging}

Puede ver el historial de uso y los registros de llamadas de los agentes de voz desde el panel de control de {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Acerca del registro

El registro se habilita automáticamente para {{site.data.keyword.iva_full}}. Puede ver los registros de llamadas del agente de voz en el panel de control _Uso_.

En el panel de control _Uso_ se muestran estadísticas rápidas sobre el uso del servicio durante el mes actual y los recursos que quedan disponibles en el plan. Esta información incluye el número máximo de conexiones simultáneas que se han producido durante el mes actual y el número máximo de conexiones simultáneas disponibles en el plan. También puede ver el número de minutos gratuitos incluidos en el plan y el número de minutos que se han utilizado. En la sección _Registros de llamadas_ se incluye un seguimiento de las _Estadísticas rápidas_.

En la sección _Registros de llamadas_, puede filtrar los registros de llamadas por fecha y nombre de agente de voz para reducir el número de llamadas visualizadas y aislar registros de llamadas específicos.

Para obtener más información sobre la creación y la edición de agentes de voz, consulte [Gestión de agentes de voz](managing.html).

##  Visualización de registros de llamadas

1. Desde el panel de control de {{site.data.keyword.iva_short}}, vaya al panel de control _Uso_ para ver las _Estadísticas rápidas_ y los _Registros de llamadas_. Cada fila de la tabla _Registros de llamadas_ corresponde a una llamada.

      Para cada llamada, puede ver el nombre y el número de teléfono del agente de voz, las horas de inicio y detención y la duración de la llamada. También puede ver un símbolo de aviso junto al nombre del agente de voz, que indica que la llamada ha fallado.

1.  Puede filtrar la lista de llamadas para ver las llamadas de una fecha específica o de un nombre de agente de voz.

1. Para acceder a los registros de errores de llamada de una llamada individual, pulse el icono **Registros** en la columna **Registros de error** de dicha llamada.

1. Puede examinar la lista detallada de registros de mensajes en la nueva vista mediante los métodos siguientes:
  * Buscar los registros de error
  * Filtrar los mensajes en función del tipo de registro, **Error** o **Aviso**
  * Descargar el conjunto de datos
  * Ordenar los registros de error por fecha y hora ascendente o descendente

1. Para ver cualquier mensaje de registro de error en detalle, pulse la flecha al principio de la fila que le interesa para ampliar la vista. Puede ver información más detallada sobre los mensajes de registro en [Mensajes de sistema de Voice Gateway](https://www.ibm.com/support/knowledgecenter/SS4U29/messages.html){:new_window}.

1. Pulse la flecha atrás al principio de la página para volver al panel de control _Uso_.

## Enlaces relacionados
Lea más información detallada sobre el registro en [Resolución de problemas](https://www.ibm.com/support/knowledgecenter/SS4U29/troubleshooting.html){:new_window} en la documentación de IBM Voice Gateway.