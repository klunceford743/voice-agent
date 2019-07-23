---

copyright:

  years: 2019

lastupdated: "2019-06-06"
subcollection: "voice-agent"

keywords: Voice Agent IAM, Voice Agent user access, get started with IAM, IAM tutorial, IAM quick start, user access, SMS IAM, SMS user access

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}

# IAM とユーザー・アクセスの構成
{: #iam}

このチュートリアルの目的は、IBM Cloud ID Identity and Access Management (IAM) を素早く稼働状態にできるようにすることです。その際、ご使用のアカウントにユーザーを招待し、{{site.data.keyword.iva_short}} インスタンス用にそれらのユーザーに Cloud IAM アクセス権限を割り当てます。
{:shortdesc}

## 始めに
{: #iam-before-you-begin}

IAM を初めて使用する場合は、次の資料を確認して、アクセス管理システムの特徴、概念、コンポーネントを詳しく理解してください。

* [IBM Cloud Identity and Access Management](/docs/iam?topic=iam-iamoverview) には、IBM における IAM の概要、利用できる機能、使用可能な CLI と API 資料へのリンクが示されています。
* [IAM の概念](/docs/iam?topic=iam-iamconcepts)では、始めにさまざまなコンポーネントを理解するのに役立つ、IAM の大まかな概念について概説します。
* [IAM アクセス](/docs/iam?topic=iam-userroles)は、アクセス・ポリシーを使用してアクセス管理がどのように機能するかについての詳細なレビューを提供します。

このガイドでは、ユーザーを追加してユーザーにアクセス権限を割り当てる一般的なシナリオを示します。ユーザー・アクセス権限と役割については、他にも多数のオプションや構成があります。詳細については、上記のリンクを参照してください。 

## ステップ 1. ユーザーを招待し、初期アクセス権限を割り当てる
{: #step1}

ユーザーを 1 人以上招待し、招待時にユーザーの初期アクセス・ポリシーを設定することができます。1 回の招待で複数のユーザーを招待する場合、各ユーザーに同じアクセス権限が割り当てられます。 **「ユーザーの招待」**ページの**「アクセス権限」**セクションには、自分が割り当てることができるユーザー役割のみが表示されます。

アカウント所有者は、**「サービス」**セクションで、招待されるユーザーの Cloud IAM 役割を割り当てることができます。アカウント所有者は、次の項目にアクセスする権限を与えることができます。
* リソース・グループ内のすべてのリソース
* リソース・グループ内の特定のサービスに関するすべてのリソース 
* アカウント内のすべての ID およびアクセス対応サービス
* アカウント内の 1 つのリソース
* アカウント管理サービスへのアクセス権限

アカウント内でユーザーの Cloud IAM 役割を割り当てるには、次の手順に従います。

1. **「管理」** &gt; **「アクセス (IAM)」**に移動して、**「ユーザー」**を選択します。
2. **「ユーザーの招待」**をクリックします。
3. 招待するユーザーの E メール・アドレスを指定します。
4. **「アクセス権限」**セクションで、**「サービス」**オプションを展開します。
5. **リソース**、**リソース・グループ** 内のリソース、または**アカウント管理サービス**へのアクセス権限の割り当てを選択します。
6. 選択内容に応じて、プロンプトに従って適切なアクセス権限を指定します。_「リソース・グループ」_オプションを選択した場合は、リソース・グループへのアクセスの役割を 1 つ選択することで、リソース・グループへのアクセス権限を表示、編集、管理できる権限をユーザーに提供することもできます。
7. **「サービス」**入力ボックスで、ドロップダウン・メニューから*「{{site.data.keyword.iva_short}}」*を選択するかボックスに直接入力して、Enter を押します。 
8. 適切な**「地域」**と**「サービス・インスタンス」**を選択します。
9. **「役割の選択」**セクションで、*「管理者」*、*「ライター」*、*「リーダー」*の中から選択します。{{site.data.keyword.iva_short}} *サービス・インスタンス*が SMS を使用している場合、付与するその他の役割に加えて、*「ライター」*または*「管理者」*のいずれかの役割を選択する**必要があります**。
    - **役割**の詳細については、[サービスのアクセス役割](/docs/iam?topic=iam-userroles#service_access_roles)を参照してください。
10. 許可がある場合は、招待時に Cloud Foundry アクセス権限またはインフラストラクチャー・アクセス権限を割り当てることもできます。
11. **「ユーザーの招待」**をクリックします。

詳しくは、[ユーザーの招待とアクセス権限の割り当て](/docs/iam?topic=iam-iamuserinv#iamuserinv)を参照してください。

## ステップ 2. アクセス・グループの作成
{: #step2}

アカウント内のユーザーにアクセス権限を割り当てるプロセスを簡素化するために、アクセス・グループを作成できます。 アクセス・グループは、ユーザーおよびサービス ID を編成し、グループ全体に対して単一のポリシーを定義することでアクセス権限を簡単に割り当てられるようにする方法です。

### グループのセットアップ
{: #group_setup}

アクセス・グループを作成するには、次の手順に従います。

1. メニュー・バーから、**「管理」** &gt; **「アクセス (IAM)」**をクリックして、**「アクセス・グループ」**を選択します。
2. **「作成」**をクリックします。
3. グループの名前を入力します。説明を追加するかどうかはオプションです。
4. **「作成」**をクリックします。

次に、ユーザーまたはサービス ID を追加することでグループをセットアップします。

1. 新規作成されたアクセス・グループのページが表示されます。また、メニュー・バーの**「アクセス・グループ」**ページの_「グループ」_リストにも、このグループが表示されます。
2. **「ユーザーの追加」**をクリックします。
3. 追加するユーザーをリストから選択して、**「グループに追加 (Add to group)」**をクリックします。
4. サービス ID をグループに追加するには、**「サービス ID」**をクリックします。
5. 追加する ID をリストから選択して、**「グループに追加 (Add to group)」**をクリックします。

### グループへのアクセス権限の割り当て
{: #group_access}

グループの作成後に、単一のポリシーまたは複数のポリシーを使用して、グループ内のすべてのエンティティーにアクセス権限を割り当てることができます。

1. メニュー・バーから、**「管理」** &gt; **「アクセス (IAM)」**をクリックして、**「アクセス・グループ」**を選択します。
2. アクセス権限の割り当て先となるグループを選択します。
3. **「アクセス・ポリシー」**タブで、**「アクセス権限の割り当て」**をクリックしてアクセス・ポリシーをセットアップします。必要に応じて操作を繰り返して、さらにアクセス権限を割り当てます。

ユーザーをアクセス・グループに編成すると、ユーザーのグループを単一ポリシーに割り当てることができ、管理すべきポリシーの合計数が減ります。
{: tip}


## ステップ 3. 既存ユーザーのアクセス権限の管理
{: #user_access_manage}

以下のセクションでは、アカウントに既にセットアップしたユーザーとグループのアクセス権限を管理および編集する方法について詳しく示します。

### 新規アクセス権限の割り当て
{: #new_access}

新規アクセス・ポリシーを割り当てるには、以下の手順を実行します。

1. メニュー・バーから、**「管理」** &gt; **「アクセス (IAM)」**をクリックして、**「ユーザー」**を選択します。
2. アクセス権限の割り当て先となるユーザーの名前を選択します。
3. **「アクセス・ポリシー」**をクリックします。
4. **「アクセス権限の割り当て (Assign access)」**をクリックします。
5. 次のようにして、アクセス権限をどのように割り当てるのかを選択します。
    * グループ内のすべてのリソースへのアクセス権限、またはグループ内の特定のサービスに指定されたリソースへのアクセス権限を割り当てるには、**「リソース・グループ内のアクセス権限の割り当て (Assign access within a resource group)」**を選択します。また、リソース・グループに対するユーザー役割をユーザーに割り当てることで、リソース・グループへのアクセス権限を表示、編集、または管理できる権限を与えることもできます。リソース・グループではなく、指定した特定のリソースへのアクセス権限のみをユーザーに付与するには、**「アクセス権限なし」**を選択します。
    * アカウント全体のすべての ID およびアクセス対応リソースへのアクセス権限を割り当てるか、アカウント全体の特定サービスのすべてのリソースへのアクセス権限を割り当てるか、単一インスタンスへのアクセス権限を割り当てるか、または、特定のサービス・インスタンス内の単一リソースへのアクセス権限を割り当てる場合は、**「リソースへのアクセス権限の割り当て (Assign access to resources)」**を選択します。
    * **「アカウント管理サービスへのアクセス権限の割り当て (Assign access to Account management services)」**を選択して、すべてのアカウント管理サービス、または 1 つだけのアカウント管理サービスへのアクセス権限を割り当てます。
5. アクセス有効範囲を定義する役割の組み合わせを選択します。 アクセス権限について詳しくは、[Cloud IAM 役割](/docs/iam?topic=iam-userroles#iamusermanrol)を参照してください。
6. **「割り当て」**をクリックします。


### 既存のアクセス権限の編集
{: #editing_access}

ユーザーに割り当てられた役割を編集することによって、既存のアクセス権限を更新することができます。

1. メニュー・バーから、**「管理」** &gt; **「アクセス (IAM)」**をクリックして、**「ユーザー」**を選択します。
2. アクセス権限の編集対象となるユーザーの名前を選択します。
3. **「アクセス・ポリシー」**をクリックします。
4. 編集するポリシーの行で**「アクション」** ![「アクションのリスト」アイコン](../icons/action-menu-icon.svg) メニューから**「編集」**をクリックします。
4. 割り当てられた役割を更新してポリシーを編集します。
5. **「保存」**をクリックします。

削除したいポリシーの**「アクション」** ![「アクションのリスト」アイコン](../icons/action-menu-icon.svg) メニューから**「削除」**オプションをクリックすることによって、ユーザーからアクセス権限を削除できます。

## ステップ 4. SMS エージェントまたはボイス + SMS エージェントへのアクセス権限を割り当てます (オプション)。
{: #sms_access}

アクセス権限の割り当て対象となるエージェントが **SMS** エージェントまたは**ボイス + SMS** エージェントである場合は、*新規資格情報*を作成します。

### 新規資格情報の作成
{: #new_cred}

ご使用のアカウントで既にアクティブになっている役割に関してのみ、資格情報を作成できます。SMS エージェントとボイス + SMS エージェントの場合、*ライター*または*マネージャー (管理者)* の役割が割り当てられている必要があります。[「ユーザーを招待し、初期アクセス権限を割り当てる」のステップ 9](/docs/services/voice-agent?topic=voice-agent-iam#step1) を参照してください。

1. {{site.data.keyword.iva_short}} インスタンスの*ダッシュボード*で、**「新規資格情報 (+)」**をクリックします。 
2. 新規作成のダイアログ・ボックスが開いたら、**名前**を入力し、**「役割」**ドロップダウン・メニューで*「ライター」*または*「管理者」*を選択します。 
    - **注:** SMS 関連の機能を使用するには、*「ライター」*または*「管理者」*のいずれかの役割を選択する**_必要があります_**。 
3. **「追加」**ボタンをクリックします。

## トラブルシューティング
{: #troubleshoot}

 *新規資格情報*を作成しようとしたとき、**「サービス資格情報」**ページに次のようなエラー・メッセージが表示されることがあります。
> 「ライター」の役割を割り当てるのに必要なアクセス権がありません (You do not have the required permission to assign role‘ Writer’)。アカウント所有者に連絡して、アクセス権限を更新してください。

その場合、手順に従って、SMS 関連の機能に**必須**の*「ライター」*または*「管理者」*アクセス権限を自分自身に割り当てる必要があります。[「アクセス権限の割り当て」のステップ 9](/docs/services/voice-agent?topic=voice-agent-iam#step1) を参照した後で、[新規資格情報の作成](/docs/services/voice-agent?topic=voice-agent-iam#new_cred)に進んでください。

## 次のステップ
{: #next}

[Cloud IAM の機能](/docs/iam?topic=iam-iamoverview#features)にあるリストを確認すると、Cloud IAM の機能をさらに学習できます。