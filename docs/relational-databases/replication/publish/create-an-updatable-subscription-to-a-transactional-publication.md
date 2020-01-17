---
title: 更新可能なサブスクリプションの作成 (トランザクション)
description: SQL Server トランザクション パブリケーションの更新可能なサブスクリプションを作成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- updatable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5d1a8b0c8f674dd39ece67cb79db0110cfd55994
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321250"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションの更新可能なサブスクリプションの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
> [!NOTE]  
>  この機能は、 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 2012 から 2016 のバージョンでサポートされています。  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

トランザクション レプリケーションは、即時更新サブスクリプションまたはキュー更新サブスクリプションを使用して、サブスクライバーでの変更がパブリッシャーに反映されるようにします。 レプリケーション ストアド プロシージャを使用して、更新サブスクリプションをプログラムで作成できます。 
 
**サブスクリプションの新規作成ウィザード**の **[更新可能なサブスクリプション]** ページで、更新可能なサブスクリプションを構成します。 このページは、更新可能なサブスクリプションに対してトランザクション パブリケーションを有効にした場合にのみ使用できます。 更新可能なサブスクリプションを有効にする方法については、「[トランザクション パブリケーションの更新サブスクリプションを有効にする方法](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)」を参照してください。   
  
## <a name="configure-an-updatable-subscription-from-the-publisher"></a>パブリッシャーから更新可能なサブスクリプションを構成する  

1. Microsoft SQL Server Management Studio でパブリッシャーに接続し、サーバー ノードを展開します。
2. **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。
3. 更新サブスクリプションを有効にしたトランザクション パブリケーションを右クリックし、 **[新しいサブスクリプション]** をクリックします。
4. ウィザード内のページに従って、ディストリビューション エージェントが実行される場所など、サブスクリプションに対するオプションを指定します。
5. **サブスクリプションの新規作成ウィザード**の **[更新可能なサブスクリプション]** ページで、 **[レプリケート]** が選択されていることを確認します。
6. **[パブリッシャーでのコミット]** ボックスの一覧からオプションを選択します。

    * 即時更新サブスクリプションを使用するには、 **[変更を同時にコミットする]** を選択します。 このオプションを選択し、パブリケーションがキュー更新サブスクリプションを許可する場合 (パブリケーションの新規作成ウィザードを使用して作成されたパブリケーションの既定値)、サブスクリプション プロパティ **update_mode** は **failover** に設定されます。 このモードでは、必要に応じて、後からキュー更新に切り替えることができます。

    * キュー更新サブスクリプションを使用するには、 **[変更をキューに登録し、可能な場合はコミット]** を選択します。 このオプションを選択し、パブリケーションが即時更新サブスクリプションを許可していて (パブリケーションの新規作成ウィザードを使用して作成されたパブリケーションの既定値)、サブスクライバーが SQL Server 2005 以降を実行している場合、サブスクリプション プロパティ **update_mode** は queued failover に設定されます。 このモードでは、必要に応じて、後から即時更新に切り替えることができます。

    更新モードの切り替えの詳細については、「[Switch Between Update Modes for an Updatable Transactional Subscription](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)」(更新可能なトランザクション サブスクリプションの更新モードを切り替える) を参照してください。

7. 即時更新を使用するサブスクリプション、または **update_mode** を **queued failover** に設定したサブスクリプションに対して **[更新可能なサブスクリプション用のログイン]** ページが表示されます。 **[更新可能なサブスクリプション用のログイン]** ページで、即時更新サブスクリプション用にパブリッシャーへの接続を作成するリンク サーバーを指定します。 接続はサブスクライバーで起動されるトリガーによって使用され、サブスクライバーに変更を反映します。 以下のオプションの 1 つを選択します。

    * **[SQL Server 認証を使用して接続するリンク サーバーを作成する]** 。 サブスクライバーとパブリッシャーの間でリモート サーバーまたはリンク サーバーを定義していない場合は、このオプションを選択します。 レプリケーションによってリンク サーバーが作成されます。 指定するアカウントは、パブリッシャーに既に存在している必要があります。

    * **[定義済みのリンク サーバーまたはリモート サーバーを使用する]** [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)、[sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)、SQL Server Management Studio、または他の方法を使用してサブスクライバ―とパブリッシャーの間にリモート サーバーまたはリンクされたサーバーを定義した場合は、このオプションを選択します。

    リンクされたサーバー アカウントに必要な権限に関する詳細については、「[ここにサブスクリプションを入力](../../../relational-databases/replication/security/secure-the-subscriber.md)」の「**Queued Updating Subscriptions**」(キューに入れられた更新サブスクリプション) を参照してください。

8. ウィザードを完了します。

## <a name="configure-an-updatable-subscription-from-the-subscriber"></a>サブスクライバーから更新可能なサブスクリプションを構成する


1. SQL Server Management Studio でサブスクライバ―に接続し、サーバー ノードを展開します。
2. **[レプリケーション]** フォルダーを展開します。
3. **[ローカル サブスクリプション]** フォルダーを右クリックし、 **[新しいサブスクリプション]** をクリックします。
4. **サブスクリプションの新規作成ウィザード**の **[パブリケーション]** ページで、 **[パブリッシャー]** ボックスの一覧から **[<SQL Server パブリッシャーの検索>]** を選択します。
5. **[サーバーへの接続]** ダイアログ ボックスでパブリッシャーに接続します。
6. **[パブリケーション]** ページで、更新サブスクリプションを有効にしたトランザクション パブリケーションを選択します。
7. ウィザード内のページに従って、ディストリビューション エージェントが実行される場所など、サブスクリプションに対するオプションを指定します。
8. サブスクリプションの新規作成ウィザードの **[更新可能なサブスクリプション]** ページで、 **[レプリケート]** が選択されていることを確認します。
9. **[パブリッシャーでのコミット]** ボックスの一覧からオプションを選択します。

    * 即時更新サブスクリプションを使用するには、 **[変更を同時にコミットする]** を選択します。 このオプションを選択し、パブリケーションがキュー更新サブスクリプションを許可する場合 (パブリケーションの新規作成ウィザードを使用して作成されたパブリケーションの既定値)、サブスクリプション プロパティ **update_mode** は **failover** に設定されます。 このモードでは、必要に応じて、後からキュー更新に切り替えることができます。

    * キュー更新サブスクリプションを使用するには、 **[変更をキューに登録し、可能な場合はコミット]** を選択します。 このオプションを選択し、パブリケーションが即時更新サブスクリプションを許可していて (パブリケーションの新規作成ウィザードを使用して作成されたパブリケーションの既定値)、サブスクライバーが SQL Server 2005 以降を実行している場合、サブスクリプション プロパティ **update_mode** は queued **failover** に設定されます。 このモードでは、必要に応じて、後から即時更新に切り替えることができます。

    更新モードの切り替えの詳細については、「[Switch Between Update Modes for an Updatable Transactional Subscription](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)」(更新可能なトランザクション サブスクリプションの更新モードを切り替える) を参照してください。

10. 即時更新を使用するサブスクリプション、または **update_mode** を queued **failover** に設定したサブスクリプションに対して **[更新可能なサブスクリプション用のログイン]** ページが表示されます。 **[更新可能なサブスクリプション用のログイン]** ページで、即時更新サブスクリプション用にパブリッシャーへの接続を作成するリンク サーバーを指定します。 接続はサブスクライバーで起動されるトリガーによって使用され、サブスクライバーに変更を反映します。 以下のオプションの 1 つを選択します。

    * **[SQL Server 認証を使用して接続するリンク サーバーを作成する]** 。 サブスクライバーとパブリッシャーの間でリモート サーバーまたはリンク サーバーを定義していない場合は、このオプションを選択します。 レプリケーションによってリンク サーバーが作成されます。 指定するアカウントは、パブリッシャーに既に存在している必要があります。

    * **[定義済みのリンク サーバーまたはリモート サーバーを使用する]** [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)、[sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)、SQL Server Management Studio、または他の方法を使用してサブスクライバ―とパブリッシャーの間にリモート サーバーまたはリンクされたサーバーを定義した場合は、このオプションを選択します。

    リンクされたサーバー アカウントに必要な権限に関する詳細については、「[ここにサブスクリプションを入力](../../../relational-databases/replication/security/secure-the-subscriber.md)」の「**Queued Updating Subscriptions**」(キューに入れられた更新サブスクリプション) を参照してください。

11. ウィザードを完了します。

## <a name="create-an-immediate-updating-pull-subscription"></a>即時更新プル サブスクリプションを作成する ##

1. パブリッシャーで、 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)を実行することにより、パブリケーションが即時更新サブスクリプションをサポートしていることを確認します。 

    * 結果セットの `allow_sync_tran` の値が `1`である場合、パブリケーションは即時更新サブスクリプションをサポートします。
    * 結果セットの `allow_sync_tran` の値が `0`である場合は、即時更新サブスクリプションを有効にしてパブリケーションを再作成する必要があります。

2. パブリッシャーで、 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)を実行することにより、パブリケーションがプル サブスクリプションをサポートしていることを確認します。 

    * 結果セットの `allow_pull` の値が `1`である場合、パブリケーションはプル サブスクリプションをサポートします。
    * `allow_pull` の値が `0`である場合、 [には](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)、 `allow_pull` には `@property` を指定して `true` sp_changepublication `@value`を実行します。 

3. サブスクライバーで、 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)を実行します。 `@publisher` と `@publication`を指定し、 `@update_mode`に次のいずれかの値を指定します。

    * `sync tran` - サブスクリプションの即時更新を有効にします。
    * `failover` キュー更新をフェールオーバー オプションとするサブスクリプションの即時更新を有効にします。
    > [!NOTE]  
>  `failover` では、パブリケーションでもキュー更新サブスクリプションが有効になっていることが必要です。 
 
4. サブスクライバーで、 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)を実行します。 次の指定を行います。

    * `@publisher`、 `@publisher_db`、および `@publication` パラメーター。 
    * `@job_login` および `@job_password`に、サブスクライバーでディストリビューション エージェントを実行するときに使用する Microsoft Windows 資格情報。 

    > [!NOTE]  
    > Windows 統合認証を使用して作成された接続では、常に、 `@job_login` および `@job_password`で指定された Windows 資格情報が使用されます。 ディストリビューション エージェントは、常に Windows 統合認証を使用してサブスクライバーへのローカル接続を作成します。 既定では、エージェントは Windows 統合認証を使用してディストリビューターに接続します。 
 
    * (省略可能) ディストリビューターに接続するときに SQL Server 認証を使用する必要がある場合、 `0` には `@distributor_security_mode` 、 `@distributor_login` と `@distributor_password`には Microsoft SQL Server ログイン情報の値。 
    * このサブスクリプションでのディストリビューション エージェント ジョブのスケジュール。 

5. サブスクライバー側のサブスクリプション データベースに対して、 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)を実行します。 `@publisher`、 `@publication`、 `@publisher_db`のパブリケーション データベース名、および `@security_mode`の次のいずれかの値を指定します。 

    * `0` - パブリッシャーで更新を作成する場合に SQL Server 認証を使用します。 このオプションの場合、パブリッシャーで、 `@login` および `@password`に有効なログインを指定する必要があります。
    * `1` - パブリッシャーへの接続時にサブスクライバーで変更するユーザーのセキュリティ コンテキストを使用します。 このセキュリティ モードに関連する制限の詳細については、 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) のトピックを参照してください。
    * `2` - [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)を使って作成された、既存のユーザー定義リンク サーバー ログインを使用します。

6. パブリッシャーで、 [、](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 、 `@publication`、 `@subscriber`のプル値、 `@destination_db`の手順 3 で指定したものと同じ値を指定し、 `@subscription_type`sp_addsubscription `@update_mode`を実行します。 これにより、パブリッシャーでプル サブスクリプションが登録されます。 


## <a name="create-an-immediate-updating-push-subscription"></a>即時更新プッシュ サブスクリプションを作成する ##

1. パブリッシャーで、 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)を実行することにより、パブリケーションが即時更新サブスクリプションをサポートしていることを確認します。 

    * 結果セットの `allow_sync_tran` の値が `1`である場合、パブリケーションは即時更新サブスクリプションをサポートします。
    * 結果セットの `allow_sync_tran` の値が `0`である場合は、即時更新サブスクリプションを有効にしてパブリケーションを再作成する必要があります。

2. パブリッシャーで、 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)を実行することにより、パブリケーションがプッシュ サブスクリプションをサポートしていることを確認します。 

    * 結果セットの `allow_push` の値が `1`である場合、パブリケーションはプッシュ サブスクリプションをサポートします。
    * `allow_push` の値が `0`である場合、 [には](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)、 `allow_push` には `@property` を指定して `true` sp_changepublication `@value`を実行します。 

3. パブリッシャーで、 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)を実行します。 `@publication`、 `@subscriber`、 `@destination_db`を指定し、 `@update_mode`に次のいずれかの値を指定します。

    * `sync tran` - 即時更新のサポートを有効にします。
    * `failover` - キュー更新をフェールオーバー オプションとする即時更新のサポートを有効にします。

    > [!NOTE]  
    >  `failover` では、パブリケーションでもキュー更新サブスクリプションが有効になっていることが必要です。 
 
4. パブリッシャーで、 [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)を実行します。 次のパラメーターを指定します。

    * `@subscriber`、 `@subscriber_db`、および `@publication`。 

    * `@job_login` および `@job_password`のディストリビューターでディストリビューション エージェントを実行する際に使用する Windows 資格情報。 

    > [!NOTE]  
>  Windows 統合認証を使用して作成された接続では、常に、 `@job_login` および `@job_password`で指定された Windows 資格情報が使用されます。 ディストリビューション エージェントは、常に Windows 統合認証を使用してディストリビューターにローカル接続します。 既定では、エージェントは Windows 統合認証を使用してサブスクライバーに接続します。 

    * (省略可能) サブスクライバーに接続するときに SQL Server 認証を使用する必要がある場合、 `0` には `@subscriber_security_mode` 、 `@subscriber_login` と `@subscriber_password`には SQL Server ログイン情報の値。 
    * このサブスクリプションでのディストリビューション エージェント ジョブのスケジュール。

5. サブスクライバー側のサブスクリプション データベースに対して、 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)を実行します。 `@publisher`、 `@publication`、 `@publisher_db`のパブリケーション データベース名、および `@security_mode`の次のいずれかの値を指定します。 

     * `0` - パブリッシャーで更新を作成する場合に SQL Server 認証を使用します。 このオプションの場合、パブリッシャーで、 `@login` および `@password`に有効なログインを指定する必要があります。
     * `1` - パブリッシャーへの接続時にサブスクライバーで変更するユーザーのセキュリティ コンテキストを使用します。 このセキュリティ モードに関連する制限の詳細については、 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) のトピックを参照してください。
     * `2` - [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)を使って作成された、既存のユーザー定義リンク サーバー ログインを使用します。


## <a name="create-a-queued-updating-pull-subscription"></a>キュー更新プル サブスクリプションを作成する

1. パブリッシャーで、 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)を実行することにより、パブリケーションがキュー更新サブスクリプションをサポートしていることを確認します。 

    * 結果セットの `allow_queued_tran` の値が `1`である場合、パブリケーションは即時更新サブスクリプションをサポートします。
    * 結果セットの `allow_queued_tran` の値が `0`である場合は、キュー更新サブスクリプションを有効にしてパブリケーションを再作成する必要があります。

2. パブリッシャーで、 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)を実行することにより、パブリケーションがプル サブスクリプションをサポートしていることを確認します。 

    * 結果セットの `allow_pull` の値が `1`である場合、パブリケーションはプル サブスクリプションをサポートします。
    * `allow_pull` の値が `0`である場合、 [には](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)、 `allow_pull` には `@property` を指定して `true` sp_changepublication `@value`を実行します。 

3. サブスクライバーで、 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)を実行します。 `@publisher` と `@publication`を指定し、 `@update_mode`に次のいずれかの値を指定します。

    * `queued tran` - サブスクリプションのキュー更新を有効にします。
    * `queued failover` - 即時更新をフェールオーバー オプションとするキュー更新のサポートを有効にします。

    > [!NOTE]  
>  `queued failover` では、パブリケーションでも即時更新サブスクリプションが有効になっていることが必要です。 即時更新へのフェールオーバーを行うために、 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) を使って、サブスクライバーでの変更をパブリッシャーにレプリケートするときに使用する資格情報を定義する必要があります。
 
4. サブスクライバーで、 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)を実行します。 次のパラメーターを指定します。

    * @publisher、 `@publisher_db`、および `@publication`。 
    * `@job_login` および `@job_password`に、サブスクライバーでディストリビューション エージェントを実行するときに使用する Windows 資格情報。 

    > [!NOTE]  
    > Windows 統合認証を使用して作成された接続では、常に、 `@job_login` および `@job_password`で指定された Windows 資格情報が使用されます。 ディストリビューション エージェントは、常に Windows 統合認証を使用してサブスクライバーへのローカル接続を作成します。 既定では、エージェントは Windows 統合認証を使用してディストリビューターに接続します。 
 
    * (省略可能) ディストリビューターに接続するときに SQL Server 認証を使用する必要がある場合、 `0` には `@distributor_security_mode` 、 `@distributor_login` と `@distributor_password`には SQL Server ログイン情報の値。 
    * このサブスクリプションでのディストリビューション エージェント ジョブのスケジュール。

5. パブリッシャーで、 [、](../../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md) 、 `@publication`、 `@subscriber`のプル値、 `@destination_db`の手順 3 で指定したものと同じ値を指定して `@subscription_type`sp_addsubscriber `@update_mode`を実行し、パブリッシャーにサブスクライバーを登録します。 これにより、パブリッシャーでプル サブスクリプションが登録されます。 


## <a name="create-a-queued-updating-push-subscription"></a>キュー更新プッシュ サブスクリプションを作成する 

1. パブリッシャーで、 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)を実行することにより、パブリケーションがキュー更新サブスクリプションをサポートしていることを確認します。 

    * 結果セットの allow_queued_tran の値が 1 である場合、パブリケーションは即時更新サブスクリプションをサポートします。
    * 結果セットの allow_queued_tran の値が 0 である場合は、キュー更新サブスクリプションを有効にしてパブリケーションを再作成する必要があります。 詳細については、トランザクション パブリケーションの更新可能なサブスクリプションを有効化する方法 (レプリケーション Transact-SQL プログラミング) に関する記事を参照してください。

2. パブリッシャーで、 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)を実行することにより、パブリケーションがプッシュ サブスクリプションをサポートしていることを確認します。 

    * 結果セットの `allow_push` の値が `1`である場合、パブリケーションはプッシュ サブスクリプションをサポートします。
    * `allow_push` の値が `0`である場合、 [には allow_push、](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)には `@property` を指定して `true` sp_changepublication `@value`を実行します。 

3. パブリッシャーで、 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)を実行します。 `@publication`、 `@subscriber`、 `@destination_db`を指定し、 `@update_mode`に次のいずれかの値を指定します。

    * `queued tran` - サブスクリプションのキュー更新を有効にします。
    * `queued failover` - 即時更新をフェールオーバー オプションとするキュー更新のサポートを有効にします。

    > [!NOTE]  
    > queued failover オプションでは、パブリケーションでも即時更新サブスクリプションが有効になっていることが必要です。 即時更新へのフェールオーバーを行うために、 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) を使って、サブスクライバーでの変更をパブリッシャーにレプリケートするときに使用する資格情報を定義する必要があります。

4. パブリッシャーで、 [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)を実行します。 次のパラメーターを指定します。

    * `@subscriber`、 `@subscriber_db`、および `@publication`。 
    * `@job_login` および `@job_password`のディストリビューターでディストリビューション エージェントを実行する際に使用する Windows 資格情報。 

    > [!NOTE]  
    > Windows 統合認証を使用して作成された接続では、常に、 `@job_login` および `@job_password`で指定された Windows 資格情報が使用されます。 ディストリビューション エージェントは、常に Windows 統合認証を使用してディストリビューターにローカル接続します。 既定では、エージェントは Windows 統合認証を使用してサブスクライバーに接続します。 
 
    * (省略可能) サブスクライバーに接続するときに SQL Server 認証を使用する必要がある場合、 `0` には `@subscriber_security_mode` 、 `@subscriber_login` と `@subscriber_password`には SQL Server ログイン情報の値。 
    * このサブスクリプションでのディストリビューション エージェント ジョブのスケジュール。

## <a name="set-queued-updating-conflict-resolution-options"></a>キュー更新の競合解決オプションを設定する 
**[パブリケーション プロパティ - \<Publication>]** ダイアログ ボックスの **[サブスクリプション オプション]** ページで、キュー更新サブスクリプションをサポートするパブリケーションの競合解決オプションを設定します。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。  
  
  
1.  **[パブリケーション プロパティ - \<Publication>]** ダイアログ ボックスの **[サブスクリプション オプション]** ページで、 **[競合の解決方法]** オプションに対して、次のいずれかの値を選択します。  
  
    -   **[パブリッシャーの変更を保持します]**    
    -   **[サブスクライバーの変更を保持します]**    
    -   **[サブスクリプションを再初期化します]**  


## <a name="example"></a>例

この例では、即時更新サブスクリプションをサポートするパブリケーションに対する即時更新プル サブスクリプションを作成します。 ログインとパスワードの値は、実行時に sqlcmd スクリプト変数を使用して入力されます。

> [!NOTE]  
>  このスクリプトでは sqlcmd スクリプト変数を使用します。 `$(MyVariable)`という形式です。 コマンド ラインと SQL Server Management Studio でスクリプト変数を使用する方法については、「 **レプリケーション システム ストアド プロシージャの概念** 」トピックの「 [レプリケーション スクリプトの実行](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)」セクションを参照してください。

```sql
-- Execute this batch at the Subscriber.
DECLARE @publication AS sysname;
DECLARE @publicationDB AS sysname;
DECLARE @publisher AS sysname;
DECLARE @login AS sysname;
DECLARE @password AS nvarchar(512);
SET @publication = N'AdvWorksProductTran';
SET @publicationDB = N'AdventureWorks2008R2';
SET @publisher = $(PubServer);
SET @login = $(Login);
SET @password = $(Password);

-- At the subscription database, create a pull subscription to a transactional 
-- publication using immediate updating with queued updating as a failover.
EXEC sp_addpullsubscription 
    @publisher = @publisher, 
    @publication = @publication, 
    @publisher_db = @publicationDB, 
    @update_mode = N'failover', 
    @subscription_type = N'pull';

-- Add an agent job to synchronize the pull subscription, 
-- which uses Windows Authentication when connecting to the Distributor.
EXEC sp_addpullsubscription_agent 
    @publisher = @publisher, 
    @publisher_db = @publicationDB, 
    @publication = @publication,
    @job_login = @login,
    @job_password = @password; 

-- Add a Windows Authentication-based linked server that enables the 
-- Subscriber-side triggers to make updates at the Publisher. 
EXEC sp_link_publication 
    @publisher = @publisher, 
    @publication = @publication,
    @publisher_db = @publicationDB, 
    @security_mode = 0,
    @login = @login,
    @password = @password;
GO

USE AdventureWorks2008R2;
GO

-- Execute this batch at the Publisher.
DECLARE @publication AS sysname;
DECLARE @subscriptionDB AS sysname;
DECLARE @subscriber AS sysname;
SET @publication = N'AdvWorksProductTran'; 
SET @subscriptionDB = N'AdventureWorks2008R2Replica'; 
SET @subscriber = $(SubServer);

-- At the Publisher, register the subscription, using the defaults.
USE [AdventureWorks2008R2]
EXEC sp_addsubscription 
    @publication = @publication, 
    @subscriber = @subscriber, 
    @destination_db = @subscriptionDB, 
    @subscription_type = N'pull', 
    @update_mode = N'failover';
GO
``` 


## <a name="see-also"></a>参照

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
[Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
[sqlcmd でのスクリプト変数の使用](../../../ssms/scripting/sqlcmd-use-with-scripting-variables.md)   


