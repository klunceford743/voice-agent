---

copyright:
  years: 2018
lastupdated: "2018-11-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# 從_管理_ 儀表板建立語音代理程式
{: #config_instance}

建立 {{site.data.keyword.iva_full}} 服務之後，您可以從_管理_ 儀表板建立個別的語音代理程式。
{: shortdesc}


## 建立語音代理程式
{: #create_instance}

當您建立語音代理程式時，{{site.data.keyword.iva_short}} 會自動搜尋您可使用的任何可用 Watson 服務實例。如果服務無法使用，您可以選擇將其與語音代理程式一起建立，或連接至不同 {{site.data.keyword.Bluemix_short}} 帳戶空間中的服務。您也可以選擇將語音代理程式連接至「服務編排引擎」、Google Speech to Text 或 Google Text to Speech 實例。

1. 移至_管理_ 儀表板上的_語音代理程式_ 標籤，然後按一下**建立語音代理程式**。

1. 在**名稱**中，指定語音代理程式的唯一名稱。例如，`Customer Support - North America`。

1. 在**電話號碼**中，新增來自 SIP 幹線的號碼（包括國碼及區域碼）。例如，若為美國 800 號碼，請將電話號碼指定為 `18883334444`。電話號碼可以有空格及 `+ ( ) -` 字元。

1. 選擇性地說明您的語音代理程式。

1. 如果您想要啟用通話轉接，請輸入**轉接預設目標**的終止 URI。如需如何設定終止 URI 的相關資訊，請參閱[設定通話轉接](call-transfer.html)。請不要在轉接目標使用個人電話號碼。

1. 配置與 Watson 服務實例的連線。您可以配置**位置 1** 及**位置 2** 的連線，以連接至多個 Watson 服務實例。具有與多個服務實例的連線可讓語音代理程式在運作中斷時切換至替代服務實例。請參閱[新增多個 Watson 服務位置](managing_disaster_recovery.html#add_location)。

1. 在 **{{site.data.keyword.conversationshort}}** 下，按一下**位置 1** 或**位置 2** 並啟用您選取的位置，以配置 {{site.data.keyword.conversationshort}} 服務實例的連線。您可以在您或其他人擁有的 {{site.data.keyword.Bluemix_notm}} 帳戶中使用 {{site.data.keyword.conversationshort}} 實例。您也可以透過服務編排引擎，連接至其中任何選項。

   * 如果您在「達拉斯」或「華盛頓特區」地區中建立語音代理程式，但沒有 {{site.data.keyword.conversationshort}} 服務實例，則可以在**服務實例**功能表中建立服務實例。
   * 或者，您也可以藉由變更[**服務類型**](managing_other.html#other_service)，以連接至 {{site.data.keyword.conversationshort}} 對話的其他來源，或與 SOE 進行連接。
   * 如果您要配置多個服務位置，請按一下另一個位置選項，然後選取**啟用位置**以配置與其他 {{site.data.keyword.conversationshort}} 實例的連線。請參閱[新增多個 Watson 服務位置](managing_disaster_recovery.html#add_location)。

1. 在 **{{site.data.keyword.speechtotextshort}}** 下，選取**位置 1** 或**位置 2** 並啟用該位置，以檢閱 {{site.data.keyword.speechtotextshort}} 服務實例的預設配置。您可以使用下列各項自訂配置。
   * 若要將語音代理程式連接至現有的實例，作為您的**服務類型**，請選擇**我的語音轉文字實例**。接著，針對**選取模型類型**，選擇**窄頻**、**寬頻**或**窄頻與寬頻**，然後選取語言**模型**。
   * 如果您在「達拉斯」或「華盛頓特區」地區中建立語音代理程式，但沒有 {{site.data.keyword.speechtotextshort}} 服務實例，則可以從**服務實例**功能表建立服務實例。
   * 針對**服務類型**，可以選擇[不同 {{site.data.keyword.Bluemix_notm}} 工作區中的 {{site.data.keyword.speechtotextshort}} 實例](managing_other.html)，或[協力廠商語音轉文字服務](managing_third_party.html)，例如 Google Cloud Speech-to-Text。
   * 如果您要配置多個服務位置，請按一下另一個位置選項，然後選取**啟用位置**以配置與其他 {{site.data.keyword.speechtotextshort}} 實例的連線。請參閱[新增多個 Watson 服務位置](managing_disaster_recovery.html)。

1. 在 **{{site.data.keyword.texttospeechshort}}** 下，按一下**位置 1** 或**位置 2** 並啟用該位置，以檢閱 {{site.data.keyword.texttospeechshort}} 服務實例的預設配置。您可以使用下列各項自訂配置。
   * 如果您在「達拉斯」或「華盛頓特區」地區中建立語音代理程式，但沒有 {{site.data.keyword.texttospeechshort}} 服務實例，則可以從**服務實例**功能表建立服務實例。
   * 針對**服務類型**，可以選擇[不同 {{site.data.keyword.Bluemix_notm}} 工作區中的 {{site.data.keyword.texttospeechshort}} 實例](managing_other.html)，或[協力廠商文字轉語音服務](managing_third_party.html)，例如 Google Cloud Text-to-Speech。
   * 如果您要配置多個服務位置，請按一下另一個位置選項，然後選取**啟用位置**以配置與其他 {{site.data.keyword.texttospeechshort}} 實例的連線。請參閱[新增多個 Watson 服務位置](managing_disaster_recovery.html)。

1. 您也可以選擇啟用事件轉遞，收集 {{site.data.keyword.cloudantfull}} 中語音代理程式所處理通話的相關資訊。請參閱[啟用語音代理程式的事件轉遞](event-forwarding.html)。如需其他配置選項，請參閱[配置語音代理程式](managing.html#configure_va)。

1. 按一下**建立語音代理程式**，以建立您的語音代理程式及任何新服務。

建立語音代理程式之後，即可藉由與其電話號碼通話來測試語音代理程式。您可以在_用量_ 儀表板上，檢視通話的詳細資料。  