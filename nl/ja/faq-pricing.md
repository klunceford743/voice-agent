---

copyright:
  years: 2019
lastupdated: "2019-06-17"
subcollection: "voice-agent"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 価格設定に関する FAQ
{: #faq-pricing}

## {{site.data.keyword.iva_short}} 標準サービスを使用する場合の料金はいくらですか。
{: #faq-pricing-zero}
{: faq}

 詳しくは、[料金設定ページ](https://cloud.ibm.com/catalog/services/voice-agent-with-watson){: external}を参照してください。

## 「分あたりの料金」とはどういう意味ですか。
{: #faq-pricing-one}
{: faq}

料金は、お客様がサービスに送信した音声の長さ (分単位) に基づいています。料金は、サービスで音声を処理するのにかかった時間には基づいていません。


## API の呼び出しごとに、分単位の近似値を算出しますか。
{: #faq-pricing-two}
{: faq}

'{{site.data.keyword.IBM_notm}} では、サービスで受信した API 呼び出しごとに音声の長さを丸めて分単位の近似値を算出することはありません。代わりに、{{site.data.keyword.IBM_notm}} では各月の総使用時間を集計し、月末に端数を丸めて分単位の近似値を算出します。それぞれの呼び出しの所要時間は秒単位に切り上げられます。例えば最初の呼び出しの長さが 3.1 秒、2 番目の呼び出しの長さが 25.9 秒であるとします。{{site.data.keyword.IBM_notm}} では、最初の呼び出しを 4 秒、2 番目の呼び出しを 26 秒として計算します。その後、音声の合計時間が 1 分と算出されます。


## 同時接続は何に適用され、どんな方法で計算されますか。
{: #faq-pricing-three}
{: faq}

同時接続はボイス・コール (音声呼び出し) にのみ適用されます。SMS は適用外です。同時接続は、サービス・インスタンスで同時に定義された電話番号に接続される数として計算されます。実際の日次の最大同時接続数が課金対象となり、月額課金に基づいて配分されます。

## 最大同時接続数はどのように定義され、どのように変更されますか。

{: #faq-pricing-four}
{: faq}

最大同時接続数とは、任意の時点で許可される接続の最大数であり、課金対象となる最大接続数です。[ダッシュボード](https://cloud.ibm.com/docs/services/voice-agent?topic=voice-agent-edit_concurrency)で最大同時接続数を定義したり変更したりできます。標準プランでは、可能な最大同時接続数は 50 ですが、さらに必要な場合はサポート・チケットをオープンすることができます。

## インバウンドおよびアウトバウンド SMS/MMS メッセージはどのように課金されますか。

{: #faq-pricing-five}
{: faq}

インバウンド・メッセージは、ユーザーに応答が送られるまでは課金されません。Voice Gateway を通してユーザーにアウトバウンド・メッセージが送られたとき、またはインバウンド・メッセージへの応答として、セッションが作成されます。該当する場合、応答されたインバウンド・メッセージとアウトバウンド・メッセージの両方が課金されます。
アウトバウンド・メッセージとインバウンド・メッセージのどちらも、セッション・タイムアウトの時点まで課金されます。セッション・タイムアウトの後は、会話コンテキストが破棄されます。デフォルトのセッション・タイムアウトは 3600 秒ですが、ユーザーはダッシュボードでセッション・タイムアウト期間を設定できます。