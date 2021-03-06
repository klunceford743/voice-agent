---

copyright:
  years: 2019
lastupdated: "2019-10-31"

keywords: SMS agent, SMS provider

subcollection: "voice-agent"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Creating an SMS agent
{: #sms_config_instance}

After you create your {{site.data.keyword.iva_full}} service, you can create individual SMS agents from the _Manage_ dashboard.
{: shortdesc}

1. Go to the _Agents_ tab on the _Manage_ dashboard, and click **Create an Agent**.

1. For **Agent Type**, select _SMS_.

1. For **Name**, specify a unique name for your agent. For example, `Customer Support - North America`. The name can include up to 64 characters.

1. For Phone number, add the number from your SIP trunk, including the country and area codes. For example, for a United States 800 number, specify the phone number as 18883334444. The phone number can have a maximum of 30 characters, including spaces and + ( ) - characters. SMS supports only one number per users.

1. Under **SMS Provider**, enter the user name, password, and API URL for your SMS provider. For example, if you are using _Twilio_, the user name is your **Account SID**, the password is your **Auth Token** and your SMS provider is `https://api.twilio.com`

1. Under **Conversation**, configure the connection to your {{site.data.keyword.conversationshort}} service instance. You can use {{site.data.keyword.conversationshort}} service instances in {{site.data.keyword.Bluemix_notm}} accounts that you or someone else owns. You can also connect to any of these options through a service orchestration engine (SOE).

   * If you are creating an SMS agent in either the Dallas or Washington DC region and do not have a {{site.data.keyword.conversationshort}} service instance, you can create one in the **Service instance** menu.
   * Alternatively, you can connect to other sources of a {{site.data.keyword.conversationshort}} dialog or to connect with a SOE by changing the [**Service type**](/docs/voice-agent?topic=voice-agent-other_service#other_service).
   * If you want to configure multiple service locations, click the other location option and select **Enable location** to configure the connection to your other {{site.data.keyword.conversationshort}} instance. For more information, see [Adding multiple Watson service locations](/docs/voice-agent?topic=voice-agent-disaster-recovery#add_location).

1. Check the **Initiate conversation from inbound messages** box if you want to allow users to begin an SMS session with your SMS agent.

1. Check the **Notify on session timeout** box to have your SMS agent send an SMS message to the user. The message alerts them that the agent has not received a response in some time and will now time out. 

    - See [Advanced Options](/docs/voice-agent?topic=voice-agent-sms_config_instance#sms_advanced) for more information on the **Advanced Options** available for your SMS agent, such as setting a custom time for the session to time out.
    - Check the box only if you want to be notified when a session times out.

1. You can also choose to enable event forwarding to collect information about calls that are handled by your agents in a {{site.data.keyword.cloudantfull}}. For more information, see [Enabling event forwarding for agents](/docs/voice-agent?topic=voice-agent-event_forwarding). For more configuration options, see [Configuring an agent](/docs/voice-agent?topic=voice-agent-managing#configure_va).

1.  Click **Create an agent** to create your SMS agent and any new services.

1. Follow [the instructions](/docs/voice-agent?topic=voice-agent-connect-sms) to connect to an SMS provider.

After you create the SMS agent, test your SMS agent by texting its phone number. You can view details about your interaction on the _Usage_ dashboard. See [Viewing Usage and Logs](/docs/voice-agent?topic=voice-agent-logging).

To enable SMS messaging between customers and an agent during a voice call, the SMS number must match the voice number.
{: tip}

Before you create an SMS agent or add SMS functions to your agent, you **must** have the proper credentials set up and generate an API key to program to your SMS number. For more information, see [Generating API Key and Setting Credentials](/docs/voice-agent?topic=voice-agent-connect-sms#sms_access).

You **must** also configure your SIP trunk for SMS functions. See your provider's instructions, for example, Twilio. If you do not have a Twilio phone number, see [Creating a Twilio SIP trunk](/docs/voice-agent?topic=voice-agent-connect#twilio-setup).

After you have a Twilio number, configure it for SMS functions. For more information, see [Configuring Twilio for SMS](/docs/voice-agent?topic=voice-agent-connect-sms#twilio-setup).

If you have trouble creating credentials, contact your service instance administrator to grant you *Manager* or *Writer* access.
{: tip}

## Advanced Options for SMS Agents
{: #sms_advanced}

Click **Show Advanced** after the **Phone Number** field.

1. Set an optional **Conversation read timeout** value. This value is the time in seconds that the SMS Gateway waits for a response from Watson Assistant. If the time is exceeded, SMS Gateway reattempts to contact Watson Assistant. If the service still cannot be reached, the SMS/MMS message fails. Set to 30 seconds by default.

1. Set an optional **Session Timeout**. This value is the time in seconds after which the session expires if SMS Gateway does not receive a response from the user.

1. Set a **Conversation failure reply message**. This is the default response message that is sent if Watson Assistant cannot be reached. By default, it is set to `We're sorry, but we can't respond to your message.`.

### Configuring the SMS Agent for Terminating the Session
{: #sms_terminate}

The {{site.data.keyword.iva_full}} SMS agent terminates a session based on the value for the session timeout, which is configurable and set to 3600 seconds by default.

You can also add a node to your {{site.data.keyword.conversationshort}} service to respond to an end session command from the user. 

1. In your {{site.data.keyword.Bluemix_notm}} dashboard, select the {{site.data.keyword.conversationshort}} instance that your voice agent uses.

1. Create a **Terminate SMS intent** from the dashboard. Alternatively, you can modify an existing intent that you already use for the voice agent, such as _End the call_.

1. Add a **Terminate SMS node** from the dashboard.

1. In the _If assistant recognizes:_ section, add the **Terminate SMS intent** attribute that you previously created.

1. Add the response to the node. Copy and paste the following code snippet to replace the code in the field.

    ```json
        {
            "output": {
                 "text": {
                    "values": [
                        "Thank you for using the service. Goodbye!"
                    ],
                    "selection_policy”: “sequential"
                },
                "smsAction": {
                    "command": "terminateSession"
                }
            }
        }
    ```
    {: codeblock}

After you create the agent, test your agent by calling or texting its phone number based on its type. You can view details about your interaction on the _Usage_ dashboard. See [Viewing Usage and Logs](/docs/voice-agent?topic=voice-agent-logging).
