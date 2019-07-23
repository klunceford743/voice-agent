---

copyright:
  years: 2019
lastupdated: "2019-06-24"
subcollection: "voice-agent"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Création d'un agent vocal
{: #config_instance}

Après avoir créé votre service {{site.data.keyword.iva_full}}, vous pouvez créer des agents vocaux individuels à partir du tableau de bord _Gestion_.
{: shortdesc}

Lorsque vous créez un agent vocal, {{site.data.keyword.iva_short}} recherche automatiquement les instances de service Watson disponibles que vous pouvez utiliser. Si aucune instance de service n'est disponible, vous pouvez en créer une en même temps que l'agent vocal ou vous connecter aux services d'un autre compte {{site.data.keyword.Bluemix_short}}. Vous pouvez également choisir de connecter votre agent vocal à un moteur d'orchestration de service, ou bien à une instance Google Speech to Text ou Google Text to Speech.

1. Accédez à l'onglet _Agents vocaux_ sur le tableau de bord _Gestion_, puis cliquez sur **Créer un agent vocal**.

1. Pour **Type d'agent**, sélectionnez _Voix_.

1. Dans la zone **Nom**, spécifiez un nom unique pour votre agent vocal. Par exemple, `Customer Support - North America`. Le nom peut comporter jusqu'à 64 caractères.

1. Dans la zone **Numéro de téléphone**, ajoutez le numéro depuis votre liaison SIP, en incluant le code pays et l'indicatif régional. Par exemple, pour un numéro 800 aux Etats-Unis, spécifiez le numéro de téléphone sous la forme suivante : `18883334444`. Le numéro de téléphone peut comporter jusqu'à 30 caractères, y compris des espaces et les caractères + ( ) -. 

1. Par défaut, ce numéro de téléphone sera défini comme étant le **Numéro principal** du service. Il s'agit simplement du premier numéro qui s'affiche lorsque vous avez une liste et sert uniquement à des fins d'affichage. Pour modifier votre numéro principal, voir [Définition d'un numéro principal](/docs/services/voice-agent?topic=voice-agent-multi_num#primary_num).

1. Vous pouvez éventuellement décrire votre agent vocal en 256 caractères maximum.

1. Vous pouvez ajouter plusieurs numéros à un même agent vocal en cliquant sur **Gérer**, en regard de **Numéro de téléphone**. Voir [Configuring Multiple Phone Numbers in a Voice Agent Instance](/docs/services/voice-agent?topic=voice-agent-multi_num) pour en savoir plus sur la manière de configurer et d'associer plusieurs numéros de téléphone. Vous pouvez également modifier les numéros et ajouter des descriptions pour des numéros individuels à partir de la boîte de dialogue **Gestion**.
    
1. Pour éditer les numéro, vous pouvez également cliquer sur la zone grisée **Numéro de téléphone** ou cliquer sur **Gérer**. Pour plus d'informations, voir [Modification d'un numéro et/ou Description de plusieurs numéros](/docs/services/voice-agent?topic=voice-agent-multi_num#edit_num).
    
1. Pour activer le transfert d'appel, entrez l'URI de terminaison de votre **Cible de transfert par défaut**. Voir [Configuration du transfert d'appel](/docs/services/voice-agent?topic=voice-agent-call-transfer) pour obtenir des informations sur la manière dont vous pouvez configurer un URI de terminaison. N'utilisez pas un numéro de téléphone personnel pour votre cible de transfert. L'URI de terminaison **Cible de transfert par défaut** peut comporter jusqu'à 256 caractères.
    
1. Configurez les connexions à vos instances de service Watson. Vous pouvez établir des connexions à plusieurs instances de service Watson en configurant des connexions pour **Emplacement 1** et pour **Emplacement 2**. Lorsque des connexions sont établies avec plusieurs instances de service, votre agent vocal peut passer à une autre instance de service si une indisponibilité se produit. Voir [Ajout de plusieurs emplacements de service Watson](/docs/services/voice-agent?topic=voice-agent-disaster-recovery#add_location).
    
1. Sous **Conversation**, configurez la connexion à votre instance de service {{site.data.keyword.conversationshort}} en cliquant sur **Emplacement 1** ou **Emplacement 2** et en activant l'emplacement que vous avez sélectionné. Vous pouvez utiliser des instances de service {{site.data.keyword.conversationshort}} dans vos comptes {{site.data.keyword.Bluemix_notm}} ou ceux de quelqu'un d'autre. Vous pouvez également vous connecter à l'une de ces options via un moteur d'orchestration de service.
    
   * Si vous créez un agent vocal dans la région de Dallas ou de Washington DC et n'avez pas d'instance de service {{site.data.keyword.conversationshort}}, vous pouvez en créer une dans le menu **Instance de service**.
   * Vous pouvez également vous connecter à d'autres sources d'un dialogue {{site.data.keyword.conversationshort}} ou à un moteur d'orchestration de service en changeant le [**Type de service**](/docs/services/voice-agent?topic=voice-agent-other_service#other_service).
   * Si vous souhaitez configurer plusieurs emplacements de service, cliquez sur l'option **Autre emplacement** et sélectionnez **Activer l'emplacement** pour configurer la connexion à votre autre instance {{site.data.keyword.conversationshort}}. Pour plus d'informations, voir [Ajout de plusieurs emplacements de service Watson](/docs/services/voice-agent?topic=voice-agent-disaster-recovery#add_location).
    
1. Sous **{{site.data.keyword.speechtotextshort}}**, passez en revue la configuration par défaut de votre instance de service {{site.data.keyword.speechtotextshort}} en sélectionnant **Emplacement 1** ou **Emplacement 2** et en activant cet emplacement. Vous pouvez personnaliser votre configuration comme suit.
   * Pour connecter votre agent vocal à une instance existante en tant que votre **Type de service**, choisissez **Mon instance de service Speech to Text**. Ensuite, sous **Sélectionner un type de modèle**, sélectionnez **Bande étroite**, **Bande large** ou **Bande étroite et bande large**, puis sélectionnez le **Modèle** de langue.
   * Si vous créez un agent vocal dans la région de Dallas ou de Washington DC et n'avez pas d'instance de service {{site.data.keyword.speechtotextshort}}, vous pouvez en créer une à partir du menu **Instance de service**.
   * Sous **Type de service**, sélectionnez [une instance {{site.data.keyword.speechtotextshort}} d'un espace de travail {{site.data.keyword.Bluemix_notm}} différent](/docs/services/voice-agent?topic=voice-agent-other_service) ou un [service parole-texte tiers](/docs/services/voice-agent?topic=voice-agent-third-party#third-party), tel que Google Cloud Speech-to-Text.
   * Si vous souhaitez configurer plusieurs emplacements de service, cliquez sur l'option Autre emplacement et sélectionnez **Activer l'emplacement** afin de configurer la connexion à votre autre instance {{site.data.keyword.speechtotextshort}}. Pour plus d'informations, voir [Ajout de plusieurs emplacements de service Watson](/docs/services/voice-agent?topic=voice-agent-disaster-recovery).
    
1. Sous **{{site.data.keyword.texttospeechshort}}**, passez en revue la configuration par défaut de votre instance de service {{site.data.keyword.texttospeechshort}} en cliquant sur **Emplacement 1** ou **Emplacement 2** et en ajoutant cet emplacement. Vous pouvez personnaliser votre configuration comme suit.
   * Si vous créez un agent vocal dans la région de Dallas ou de Washington DC et n'avez pas d'instance de service {{site.data.keyword.texttospeechshort}}, vous pouvez en créer une à partir du menu **Instance de service**.
   * Sous **Type de service**, sélectionnez une [instance {{site.data.keyword.texttospeechshort}} d'un espace de travail {{site.data.keyword.Bluemix_notm}} différent](/docs/services/voice-agent?topic=voice-agent-other_service) ou un [service texte-parole tiers](/docs/services/voice-agent?topic=voice-agent-third-party), tel que Google Cloud Text-to-Speech.
   * Si vous souhaitez configurer plusieurs emplacements de service, cliquez sur l'option Autre emplacement et sélectionnez **Activer l'emplacement** afin de configurer la connexion à votre autre instance {{site.data.keyword.texttospeechshort}}. Voir [Ajout de plusieurs emplacements de service Watson](/docs/services/voice-agent?topic=voice-agent-disaster-recovery).
      
1. Vous pouvez également choisir d'activer la transmission d'événements afin de collecter des informations sur les appels qui sont gérés par vos agents vocaux dans une instance {{site.data.keyword.cloudantfull}}. Voir [Activation de la transmission d'événements pour les agents vocaux](/docs/services/voice-agent?topic=voice-agent-event_forwarding). Pour connaître d'autres options de configuration, voir [Configuration d'un agent vocal](/docs/services/voice-agent?topic=voice-agent-managing#configure_va).

1. Cliquez sur **Créer un agent vocal** pour créer votre agent vocal et de nouveaux services.

Une fois l'agent vocal créé, testez-le en appelant le numéro de téléphone qui lui est associé. Vous pouvez afficher les détails de votre interaction sur le tableau de bord _Utilisation_. Pour plus d'informations, voir [Affichage de l'utilisation et des journaux](/docs/services/voice-agent?topic=voice-agent-logging).   