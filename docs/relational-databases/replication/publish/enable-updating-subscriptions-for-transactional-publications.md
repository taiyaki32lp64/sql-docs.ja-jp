---
title: トランザクション パブリケーションの更新可能なサブスクリプションの有効化
description: SQL Server でトランザクション パブリケーションの更新可能なサブスクリプションを有効化する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, enabling
- subscriptions [SQL Server replication], updatable
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8afde3ebd4082df0c1fc0065b2aa058095905ead
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321259"
---
# <a name="enable-updating-subscriptions-for-transactional-publications"></a>トランザクション パブリケーションの更新可能なサブスクリプションの有効化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、トランザクション パブリケーションに対するサブスクリプションの更新を有効にする方法について説明します。  
  
> **注:** [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリケーションの新規作成ウィザードの **[パブリケーションの種類]** ページで、トランザクション パブリケーションの更新サブスクリプションを有効にします。  
  
 更新サブスクリプションを使用するには、サブスクリプションの新規作成ウィザードでオプションも構成する必要があります。  
  
#### <a name="to-enable-updating-subscriptions"></a>更新サブスクリプションを有効にするには  
  
1.  パブリケーションの新規作成ウィザードの **[パブリケーションの種類]** ページで、 **[更新可能なサブスクリプションを含むトランザクション パブリケーション]** を選択します。  
  
2.  **[エージェント セキュリティ]** ページで、スナップショット エージェントおよびログ リーダー エージェントの他に、キュー リーダー エージェントのセキュリティ設定を指定します。 キュー リーダー エージェントが実行されるアカウントに必要な権限の詳細については、「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  

    > **注:** 即時更新サブスクリプションのみを使用する場合でも、キュー リーダー エージェントは構成されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 レプリケーション ストアド プロシージャを使用してプログラムからトランザクション パブリケーションを作成するときに、即時更新サブスクリプションまたはキュー更新サブスクリプションを有効にできます。  
  
#### <a name="to-create-a-publication-that-supports-immediate-updating-subscriptions"></a>即時更新サブスクリプションをサポートするパブリケーションを作成するには  
  
1.  必要に応じて、パブリケーション データベース用のログ リーダー エージェント ジョブを作成します。  
  
    -   パブリケーション データベース用のログ リーダー エージェント ジョブが既に存在する場合、手順 2. に進みます。  
  
    -   パブリッシュされたデータベース用のログ リーダー エージェント ジョブが存在するかどうかわからない場合は、パブリッシャー側のパブリケーション データベースに対して [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) を実行します。 結果セットが空の場合、ログ リーダー エージェント ジョブを作成する必要があります。  
  
    -   パブリッシャーで、[sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) を実行します。 エージェントの実行に使用される [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 資格情報を **\@job_name** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に SQL Server 認証を使用する場合は、 **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン情報を指定する必要もあります。  
  
2.  パラメーター **\@allow_sync_tran** に **true** を指定し、[sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) を実行します。  
  
3.  パブリッシャーで [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 手順 2 で使用したパブリケーション名を **\@publication** に指定し、スナップショット エージェントを実行するときに使用される Windows 資格情報を **\@job_name** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に SQL Server 認証を使用する場合、さらに **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン情報を指定する必要があります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。  
  
4.  パブリケーションにアーティクルを追加します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
5.  サブスクライバーで、このパブリケーションに対する更新サブスクリプションを作成します。   
  
#### <a name="to-create-a-publication-that-supports-queued-updating-subscriptions"></a>キュー更新サブスクリプションをサポートするパブリケーションを作成するには  
  
1.  必要に応じて、パブリケーション データベース用のログ リーダー エージェント ジョブを作成します。  
  
    -   パブリケーション データベース用のログ リーダー エージェント ジョブが既に存在する場合、手順 2. に進みます。  
  
    -   パブリッシュされたデータベース用のログ リーダー エージェント ジョブが存在するかどうかわからない場合は、パブリッシャー側のパブリケーション データベースに対して [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) を実行します。 結果セットが空の場合、ログ リーダー エージェント ジョブを作成する必要があります。  
  
    -   パブリッシャーで、[sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) を実行します。 エージェントの実行に使用される Windows 資格情報を **\@job_name** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に SQL Server 認証を使用する場合、さらに **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン情報を指定する必要があります。  
  
2.  必要に応じて、ディストリビューター用のキュー リーダー エージェント ジョブを作成します。  
  
    -   ディストリビューション データベース用のキュー リーダー エージェント ジョブが既に存在する場合、手順 3. に進みます。  
  
    -   ディストリビューション データベース用のキュー リーダー エージェント ジョブが存在するかどうかわからない場合は、ディストリビューター側のディストリビューション データベースに対して [sp_helpqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md) を実行します。 結果セットが空の場合、キュー リーダー エージェント ジョブを作成する必要があります。  
  
    -   ディストリビューターで、[sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) を実行します。 エージェントの実行に使用される Windows 資格情報を **\@job_name** と **\@password** に指定します。 これらの資格情報は、キュー リーダー エージェントがパブリッシャーとサブスクライバーに接続するときに使用されます。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](../../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
3.  パラメーター **\@allow_queued_tran** に **true** を指定し、 **\@conflict_policy** に **pub wins**、**sub reinit**、または **sub wins** を指定して、[sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) を実行します。  
  
4.  パブリッシャーで [sp_addpublication_snapshot (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 手順 3 で使用したパブリケーション名を **\@publication** に指定し、スナップショット エージェントを実行するときに使用される Windows 資格情報を **\@snapshot_job_name** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に SQL Server 認証を使用する場合、さらに **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン情報を指定する必要があります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。  
  
5.  パブリケーションにアーティクルを追加します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
6.  サブスクライバーで、このパブリケーションに対する更新サブスクリプションを作成します。  
  
#### <a name="to-change-the-conflict-policy-for-a-publication-that-allows-queued-updating-subscriptions"></a>キュー更新サブスクリプションが可能なパブリケーションの競合ポリシーを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_changepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) を実行します。 **\@property** に **conflict_policy** を指定し、**pub wins**、**sub reinit**、**sub wins** のいずれかの競合ポリシー モードを **\@value** に指定します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 この例では、即時更新プル サブスクリプションとキュー更新プル サブスクリプションの両方がサポートされるパブリケーションを作成します。  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../relational-databases/replication/codesnippet/tsql/enable-updating-subscrip_1.sql)]  
  
## <a name="see-also"></a>参照  
 [キュー更新の競合解決オプションの設定 (SQL Server Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [トランザクション レプリケーション](../../../relational-databases/replication/transactional/transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sqlcmd でのスクリプト変数の使用](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
