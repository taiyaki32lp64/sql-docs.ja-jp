---
title: '[エージェント セキュリティ] (パブリケーションの新規作成ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.agentsecurity.articles.f1
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: db3e9b71b5e19e4dec55d64f9e0dde75a38947f5
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770776"
---
# <a name="agent-security-new-publication-wizard"></a>[エージェント セキュリティ] \(パブリケーションの新規作成ウィザード)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[エージェント セキュリティ]** ページを使用すると、次のエージェントを実行したり、レプリケーション トポロジ内のコンピューターに接続したりする際のアカウントを指定できます。  
  
-   すべてのパブリケーションに対応する、スナップショット エージェント。  
  
-   すべてのトランザクション パブリケーションに対応する、ログ リーダー エージェント。  
  
-   更新可能なサブスクリプションを許容するトランザクション パブリケーションに対応する、キュー リーダー エージェント。 **[パブリケーションの種類]** ページで **[更新可能なサブスクリプションを含むトランザクション パブリケーション]** を指定した場合、使用する更新可能なサブスクリプションの種類に関係なく、このエージェント向けの [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブが作成されます。 更新可能なサブスクリプションの詳細については、「[トランザクション レプリケーションの更新可能なサブスクリプション](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)」を参照してください。  
  
 エージェントで必要とされる権限と、レプリケーションのセキュリティに関する推奨事項については、「 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md) 」および「 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **スナップショット エージェント**  
 すべてのパブリケーションで表示されます。 **[セキュリティ設定]** をクリックすると、 **[スナップショット エージェントのセキュリティ]** ダイアログ ボックスでセキュリティ設定を指定できます。  
  
 スナップショット エージェントで使用されるアカウントに必要な権限の詳細については、 **[スナップショット エージェントのセキュリティ]** ダイアログ ボックスの **[ヘルプ]** をクリックしてください。  
  
 **ログ リーダー エージェント (Log Reader Agent)**  
 すべてのトランザクション パブリケーションで表示されます。 **[セキュリティ設定]** をクリックすると、 **[ログ リーダー エージェントのセキュリティ]** ダイアログ ボックスでセキュリティ設定を指定できます。  
  
 ログ リーダー エージェントで使用されるアカウントに必要な権限の詳細については、 **[ログ リーダー エージェントのセキュリティ]** ダイアログ ボックスの **[ヘルプ]** をクリックしてください。  
  
> [!NOTE]  
>  トランザクション レプリケーションを使用してパブリッシュされるデータベースには、それぞれ 1 つのログ リーダー エージェントが存在します。 データベースにトランザクション パブリケーションが既に存在している場合、セキュリティ設定は読み取り専用になります。 セキュリティ設定は **[パブリケーションのプロパティ]** ダイアログ ボックスを使用して変更できますが、この変更はデータベース内のすべてのトランザクション パブリケーションに反映されます。  
  
 **キュー リーダー エージェント (Queue Reader Agent)**  
 更新可能なサブスクリプションを許容するトランザクション パブリケーションで表示されます。 **[セキュリティ設定]** をクリックすると、 **[キュー リーダー エージェントのセキュリティ]** ダイアログ ボックスでセキュリティ設定を指定できます。 このウィザードが完了すると、キュー更新サブスクリプションを作成するかどうかには関係なく、キュー リーダー エージェント ジョブが作成されます。 キュー更新サブスクリプションを作成しない場合には、このジョブを無効にできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの **[ジョブ]** フォルダーで、ジョブ ( *[\<Publisher>].\<integer>* という名前になります) を右クリックし、 **[無効化]** をクリックします。  
  
 キュー リーダー エージェントで使用されるアカウントに必要な権限の詳細については、 **[キュー リーダー エージェントのセキュリティ]** ダイアログ ボックスの **[ヘルプ]** をクリックしてください。  
  
> [!NOTE]  
>  ディストリビューション データベース (および、それを使用するすべてのパブリッシャー) には、それぞれに対応するキュー リーダー エージェントが 1 つずつ存在します。 指定されたディストリビューション データベースを使用するパブリッシャーのいずれかに、キュー更新サブスクリプションを許容するトランザクション パブリケーションが既に存在する場合、セキュリティ設定は読み取り専用になります。 **[ディストリビューターのプロパティ]** ダイアログ ボックスで、キュー リーダー エージェントの実行と接続に使用されるアカウントを変更できますが、この変更はディストリビューション データベースを使用するすべてのパブリッシャーのパブリケーションに反映されます。  
  
## <a name="see-also"></a>参照  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [ID およびアクセス制御 (レプリケーション)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
