---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Programación de agentes de voz mediante la API
{: #api}

Puede controlar el comportamiento del agente de voz definiendo etiquetas de acción y variables de estado desde el servicio {{site.data.keyword.conversationfull}}. Las etiquetas de acción inician acciones que el agente de voz realiza durante una sesión de conversación y las variables de estado definen características del agente de voz que se mantienen durante la conversación a no ser que se modifiquen.
{: shortdesc}

Puesto que {{site.data.keyword.iva_full}} se basa en IBM Voice Gateway, la API funciona del mismo modo. Si está familiarizado con Voice Gateway, puede utilizar las mismas acciones y variables de estado en los diálogos de {{site.data.keyword.conversationshort}} con {{site.data.keyword.iva_short}}. Consulte [Etiquetas de acción y variables de estado en la API de Voice Gateway](https://www.ibm.com/support/knowledgecenter/SS4U29/api.html).
{: tip}

## Edición de JSON en la respuesta del diálogo
{: #json-editor}

Las acciones y los estados se definen en una respuesta de nodo de diálogo en formato JSON. Para editar el código JSON, abra el editor JSON.

1. En el panel de control de {{site.data.keyword.Bluemix_short}}, seleccione la instancia de servicio de {{site.data.keyword.conversationshort}}.
1. Inicie la herramienta {{site.data.keyword.conversationshort}}.
1. Pulse el espacio de trabajo que contiene el diálogo que desea editar.
1. Vaya al separador **Diálogo** y seleccione el nodo donde desea establecer una acción o estado.
1. En la respuesta, pulse el icono ![Respuesta avanzada](../conversation/images/kabob.png) y seleccione **Abrir editor JSON**.

En el editor JSON, puede definir acciones en la propiedad `output` y estados en la propiedad `context`, tal como se describe en las secciones siguientes.

## Inicio de acciones
{: #defining-actions}

Para iniciar acciones en el agente de voz durante una llamada, puede definir etiquetas de acción en un nodo de diálogo de {{site.data.keyword.conversationshort}} en formato JSON en la propiedad `output`. Puede definir una acción única en la etiqueta `vgwAction` o una secuencia de acciones en la etiqueta `vgwActionSequence`. Cada acción consta de una propiedad `command`, seguida por una propiedad opcional `parameter` para definir atributos para los mandatos que los necesitan.

### Acciones únicas
{: #single-actions}

Para realizar una acción única, defina la acción en la etiqueta `vgwAction` con cualquier atributo de parámetro necesario. En el bloque `text` en la propiedad `output`, puede incluir de forma opcional una expresión que el agente de voz reproduce una vez que se realiza la acción.

La acción única siguiente en la etiqueta `vgwAction` indica al agente de voz que cuelgue la llamada cuando se activa la respuesta del nodo. Puesto que el mandato `vgwActHangup` no tiene parámetros, no se define ninguno.
```json
{
  "output": {
    "vgwAction": {
      "command": "vgwActHangup"
    }
  }
}
```
{: codeblock}

La acción siguiente indica al agente de voz que recopile la entrada de señalización de multifrecuencia de tono dual (DTMF) y que reproduzca el texto definido para el interlocutor.

```json
{
  "output": {
    "vgwAction": {
      "command": "vgwActCollectDtmf",
      "parameters": {
        "dtmfTermKey": "#"
      }
    },
    "text": {
      "values": [
        "Enter your phone number."
      ]
    }
  }
}
```
{: codeblock}

### Secuencias de acciones
{: #action-sequences}

Para realizar una o varias acciones en un solo turno de la conversación, puede definir una secuencia de acciones en la etiqueta `vgwActionSequence` como una lista JSON. Las acciones se realizan en el orden en el que las define.

A diferencia de las acciones únicas, para que el agente de voz reproduzca una expresión al utilizar la etiqueta `vgwActionSequence`, la lista de acciones debe contener la acción `vgwActPlayText`. Al contrario que en la etiqueta `vgwAction`, las expresiones del campo `output.text` no se reproduce automáticamente.
{: tip}

En el ejemplo siguiente, más complejo, las acciones definidas en la etiqueta `vgwActionSequence` indican al agente de voz que inhabilite el procesamiento de habla a texto y recopile la entrada DTMF mientras reproduce una expresión.

```json
{
  "output": {
    "vgwActionSequence": [
      {
        "command": "vgwActPauseSTT"
      },
      {
        "command": "vgwActCollectDtmf",
        "parameters": {
          "dtmfTermKey": "#"
        }
      },
      {
        "command": "vgwActPlayText",
        "parameters": {
          "text": [
            "Enter your social security number."
          ]
        }
      }
    ]
  }
}

```
{: codeblock}


### Atributos y mandatos de acción
{: #actions-and-attributes}

La tabla siguiente muestra una lista de las acciones que puede especificar en el diálogo de {{site.data.keyword.conversationshort}} y los atributos que puede definir para cada acción.

| Mandato de acción | Descripción | Atributos |
| ----- | ----- | ----- |
| `vgwActPlayText`| Reproduce una expresión que el servicio {{site.data.keyword.texttospeechshort}} convierte en habla. | <ul><li>`text`: Una lista de expresiones que reproducir. Opcional. <p>Por ejemplo:<br/><code>"text": [<br/>&nbsp;&nbsp;&nbsp;"Hello. How can I help you today?"<br/>&nbsp;&nbsp;&nbsp;]</code><p> De forma predeterminada, la acción reproduce una lista de expresiones que están configuradas en el campo `output.text`. </li><li>`errAudioURL`: Un URL a un archivo de audio que se reproduce si el agente de voz no se puede poner en contacto con el servicio {{site.data.keyword.texttospeechshort}} para completar la acción. El archivo de audio debe estar en formato WAV.</li></ul>|
| `vgwActPlayUrl` | Reproduce un archivo de audio una vez reproducido el texto incluido, como al reproducir música en espera (MOH) o expresiones puntuales comunes. Si no se incluye ningún texto, el audio se reproduce inmediatamente. El archivo debe ser de canal único (mono), estar codificado en PCM y tener una tasa de muestreo de 8.000 Hz con 16 bits por muestra. | <ul><li>`url`: El URL que reproducir. Obligatorio.</li><li> `playURLInLoop`: Opcionalmente establecido en `Yes` o `No` para indicar si reproducir el URL en bucle. El valor predeterminado es `No`.</li></ul> |
| `vgwActHangup` | Cuelga la llamada. | No tiene atributos. |
| `vgwActSetSTTConfig` | Aplica un conjunto de parámetros para que el agente de voz los transfiera al servicio Watson {{site.data.keyword.speechtotextshort}}. El servicio {{site.data.keyword.conversationshort}} define dinámicamente los parámetros en función de la llamada. | Los atributos se transfieren de forma transparente como propiedades JSON al servicio {{site.data.keyword.speechtotextshort}}. |
| `vgwActSetTTSConfig` | Aplica un conjunto de parámetros para que el agente de voz los transfiera al servicio Watson {{site.data.keyword.texttospeechshort}}. El servicio {{site.data.keyword.conversationshort}} define dinámicamente los parámetros en función de la llamada. |  Los atributos se transfieren de forma transparente como propiedades JSON al servicio {{site.data.keyword.texttospeechshort}}.  |
| `vgwActSetConversationConfig` | Aplica un conjunto de parámetros para que el agente de voz defina un espacio de trabajo de {{site.data.keyword.conversationshort}}. El servicio {{site.data.keyword.conversationshort}} define dinámicamente los parámetros en función de la llamada. | <ul><li>`url`: La credencial de `url` para la API del servicio {{site.data.keyword.conversationshort}}.</li><li>`workspaceID`: ID del espacio de trabajo de {{site.data.keyword.conversationshort}}</li><li>`username`: La credencial de `username` para el servicio {{site.data.keyword.conversationshort}}.</li><li>`password`: La credencial de `password` para el servicio {{site.data.keyword.conversationshort}}.</li></ul> |
| `vgwActCollectDtmf` | Indica al agente de voz que recopile la entrada de señalización de multifrecuencia de tono dual (DTMF). | Se debe definir uno de los atributos siguientes. <ul><li> `dtmfTermKey`: La clave de terminación DTMF, que indica el final de la entrada DTMF. Por ejemplo, "`#`". </li><li> `dtmfCount`: El número de dígitos DTMF que se deben recopilar.</li></ul> Cuando se cumple alguna de estas condiciones, el agente de voz detiene la recopilación de entrada DTMF. |
| `vgwActPauseDTMF` | Inhabilita la entrada DTMF. Se ignoran las entradas DTMF hasta que se vuelvan a habilitar con la acción `vgwActUnPauseDTMF`. | No tiene atributos. |
| `vgwActUnPauseDTMF` | Habilita la entrada DTMF que se ha inhabilitado con la acción `vgwActPauseDTMF`. | No tiene atributos. |
| `vgwActExcludeFromTTSCache` | Indica al agente de voz que no almacene en caché la respuesta del servicio {{site.data.keyword.texttospeechshort}}. Por ejemplo, se deben excluir las respuestas que contengan datos confidenciales de PHI, PII y PCI DSS, o información dinámica, como nombres o fechas de nacimiento. <br/>Esta etiqueta de acción se debe definir en el nodo de diálogo de {{site.data.keyword.conversationshort}} para cada expresión que no desee almacenar en caché. | No tiene atributos. |
| `vgwActPauseSTT` | Detiene el procesamiento de habla a texto hasta que se vuelve a habilitar con la acción `vgwActUnPauseSTT`. Si se habilita la grabación y se detiene el proceso de habla a texto, el audio de la llamada no se captura. | No tiene atributos. |
| `vgwActUnPauseSTT` | Reanuda el procesamiento de habla a texto que ha detenido anteriormente la acción `vgwActPauseSTT`. | No tiene atributos. |
| `vgwActEnableSpeechBargeIn` | Habilita la interferencia mediante el habla, de forma que los interlocutores pueden interrumpir la reproducción del agente de voz al hablar. | No tiene atributos. |
| `vgwActDisableSpeechBargeIn` | Inhabilita la interferencia mediante el habla, de forma que la reproducción del agente de voz no se interrumpe cuando habla el interlocutor. | No tiene atributos. |
| `vgwActEnableDTMFBargeIn`| Habilita la interferencia mediante DTMF, de forma que los interlocutores pueden interrumpir la reproducción del agente de voz pulsando una tecla. | No tiene atributos. |
| `vgwActDisableDTMFBargeIn` | Inhabilita la interferencia mediante DTMF, de forma que la reproducción del agente de voz no se interrumpe cuando el interlocutor pulsa alguna tecla. | No tiene atributos. |
| `vgwActForceNoInputTurn` | Fuerza un nuevo turno en la conversación sin esperar a la entrada del interlocutor. | No tiene atributos. |
{: caption="Tabla 1. Acciones que puede iniciar desde el servicio {{site.data.keyword.conversationshort}}" caption-side="top"}

## Definición de estados
{: #setting-states}

Para indicar un cambio de estado que se mantiene entre turnos de conversación, el agente de voz intercambia variables de estado con el servicio {{site.data.keyword.conversationfull}} configurado. Estas variables de estado están definidas en un nodo de diálogo de {{site.data.keyword.conversationshort}} como [variables de contexto](https://console.bluemix.net/docs/services/conversation/dialog-build.html#context) en formato JSON.

Por ejemplo, puede definir la variable de estado siguiente para establecer el mensaje que se transmite al interlocutor si la conexión con el servicio {{site.data.keyword.conversationshort}} falla.

```json
{
  "context": {
    "vgwConversationFailedMessage": "Sorry, we're unable to connect you to our help line. Please try again later."
  }
}
```
{: codeblock}

El agente de voz presupone que el servicio {{site.data.keyword.conversationshort}} no tiene estado y que todo el estado se mantiene en el agente de voz entre intercambios con el servicio {{site.data.keyword.conversationshort}}. Para cada turno de conversación de una llamada, el estado se transfiere al servicio {{site.data.keyword.conversationshort}} y se recibe de nuevo desde el servicio en la sección `context` de los mensajes REST.

### Variables de estado definidas en el diálogo de {{site.data.keyword.conversationshort}}
{: #state-variables-conv}

Puede definir las variables de estado siguientes dentro del diálogo de {{site.data.keyword.conversationshort}} para modificar el comportamiento del agente de voz.

| Nombre de variable de estado | Valor esperado | Descripción |
| -------------- | ------ | ----------- |
| `vgwByeCustomHeader` | Definido por el usuario | Define una cabecera personalizada en un mensaje saliente SIP BYE. El valor de cabecera personalizada se define mediante las variables de estado `vgwByeCustomHeaderVal`.  |
| `vgwByeCustomHeaderVal` | Definido por el usuario | Define el valor de una cabecera personalizada en un mensaje saliente SIP BYE. La cabecera personalizada se define mediante las variables de estado `vgwByeCustomHeader`. |
| `vgwPostResponseTimeoutCount` | Tiempo en milisegundos | La cantidad de tiempo que se debe esperar una nueva expresión una vez que se reproduce la respuesta al interlocutor. Si se supera este valor, {{site.data.keyword.conversationshort}} recibe una actualización de texto con la palabra "vgwPostResponseTimeout" para indicar que se producido un tiempo de espera excedido.|
| `vgwConversationFailedMessage` | Serie de texto | Mensaje transmitido al interlocutor si falla el servicio {{site.data.keyword.conversationshort}}. Configure el diálogo de {{site.data.keyword.conversationshort}} para definir esta variable en el primer turno. |
| `vgwSessionInactivityTimeout` | Tiempo en minutos <br/><br/>Valor predeterminado: `2` | El intervalo de tiempo de espera de inactividad. El valor de intervalo de tiempo de espera especifica en minutos cuánto tiempo permite el agente de voz que esté inactiva una sesión. Cuando caduca el tiempo de espera, el agente de voz finaliza la sesión. |
| `vgwErrAudioURL` | Definido por el usuario | Un URL a un archivo de audio que se reproduce si no se puede contactar con el servicio {{site.data.keyword.texttospeechshort}} cuando el agente de voz intenta reproducir una respuesta. El archivo de audio debe estar en formato WAV. |
{: caption="Tabla 2. Variables establecidas por el servicio {{site.data.keyword.conversationshort}}" caption-side="top"}

### Variables de estado definidas por el agente de voz
{: #state-variables-iva}

| Nombre de variable de estado | Valor esperado | Descripción |
| -------------- | ----- | ----------- |
| `vgwSessionID`   | Definido por el usuario <br/><br/> Valor predeterminado: `Call-ID` | Una cabecera de ID de sesión personalizada que se obtiene de la solicitud SIP INVITE. El valor representa el ID de sesión global que se utiliza en todos los registros de auditoría del agente de voz relacionados con la sesión. |
| `vgwSIPCallID` | `Call-ID` de SIP | El ID de llamada SIP asociado con la llamada. |
| `vgwSIPRequestURI` | `Request-URI` de SIP | El URI de solicitud de SIP que ha iniciado la llamada. |
| `vgwSIPToURI` | URI SIP `To` | El URI SIP `To` asociado con la llamada. |
| `vgwSIPFromURI` | URI SIP `From` | El URI SIP `From` asociado con la llamada. |
| `vgwBargeInOccurred` | `Yes`/`No` | Indica si ha habido interferencia o no. |
| `vgwHangUp` | `Yes`/`No` | Indica si la conversación ha finalizado. |
| `vgwHangupReason` | Serie | Cuando se cuelga una llamada por parte del interlocutor o debido a un error, esta variable se envía al servicio {{site.data.keyword.conversationshort}} para indicar por qué se ha desconectado la llamada. El texto de la solicitud de mensaje que se envía al servicio {{site.data.keyword.conversationshort}} también incluye "vgwHangUp". |
| `vgwConversationResponseTimeout` | Tiempo en segundos<br/><br/>Valor predeterminado: `5`  | El tiempo en segundos que el agente de voz espera una respuesta del servicio {{site.data.keyword.conversationshort}}. Si se supera el tiempo, el agente de voz intentará ponerse en contacto con el servicio {{site.data.keyword.conversationshort}}. Si aun así no consigue ponerse en contacto con el servicio, la llamada falla. |
| `vgwSTTResponse` | Objeto JSON | La respuesta final del servicio {{site.data.keyword.speechtotextshort}} en formato JSON, incluida la transcripción y la puntuación de confianza para la hipótesis preferida y cualquier alternativa. <p>Por ejemplo, el siguiente formato coincide exactamente con el formato que se recibe del servicio {{site.data.keyword.speechtotextshort}}:</p><p><code>{<br/>&nbsp;&nbsp;"result_index": 0,<br/>&nbsp;&nbsp;"warnings": [<br/>&nbsp;&nbsp;&nbsp;&nbsp;"Unknown arguments: continuous."<br/>&nbsp;&nbsp;],<br/>&nbsp;&nbsp;"results": [<br/>&nbsp;&nbsp;&nbsp;&nbsp;{<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"final": true,<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"alternatives": [<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"transcript": "Hello world",<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"confidence": 0.758<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"transcript": "Hello wooled",<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"confidence": 0.358<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]<br/>&nbsp;&nbsp;&nbsp;&nbsp;}<br/>&nbsp;&nbsp;]<br/>}.</code></p> |
| `vgwIsDTMF` | `Yes`/`No` | Indica si la entrada al servicio {{site.data.keyword.conversationshort}} es DTMF (señalización de multifrecuencia de tono dual). |
{: caption="Tabla 3. Variables establecido por el agente de voz" caption-side="top"}