---
title: ディストリビューターとパブリッシャーのプロパティの表示および変更
description: SQL Server Management Studio (SSMS)、Transact-SQL (T-SQL)、またはレプリケーション管理オブジェクト (RMO) を使用して、ディストリビューターとパブリッシャーのプロパティを変更する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- Distributors [SQL Server replication], modifying
- modifying replication properties, Distributors
- Distributors [SQL Server replication], properties
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 5fcc1f21654fedc935a604fac37c7a3ca591b3d5
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321563"
---
# <a name="view-and-modify-distributor-and-publisher-properties"></a>ディストリビューターとパブリッシャーのプロパティの表示および変更
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、ディストリビューターとパブリッシャーのプロパティを表示および変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **ディストリビューターとパブリッシャーのプロパティを表示または変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] より前のバージョンのパブリッシャーでは、固定サーバー ロール **sysadmin** のユーザーが、 **[サブスクライバー]** ページでサブスクライバーを登録できます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降では、サブスクライバーをレプリケーションに明示的に登録する必要はありません。  
  
###  <a name="Security"></a> セキュリティ  
 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-and-modify-distributor-properties"></a>ディストリビューターのプロパティを表示および変更するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でディストリビューターに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを右クリックし、 **[ディストリビューターのプロパティ]** をクリックします。  
  
3.  **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスで、プロパティを表示および変更します。  
  
    -   ディストリビューション データベースのプロパティを表示および変更するには、ダイアログ ボックスの **[全般]** ページにあるデータベースのプロパティ ボタン ( **[...]** ) をクリックします。  
  
    -   ディストリビューターと関連付けられたパブリッシャーのプロパティを表示および変更するには、ダイアログ ボックスの **[パブリッシャー]** ページでパブリッシャーのプロパティ ボタン ( **[...]** ) をクリックします。  
  
    -   レプリケーション エージェントのプロファイルにアクセスするには、ダイアログ ボックスの **[全般]** ページの **[プロファイルの既定値]** をクリックします。 詳しくは、「 [レプリケーション エージェント プロファイル](../../relational-databases/replication/agents/replication-agent-profiles.md)」をご覧ください。  
  
    -   パブリッシャーで管理用のストアド プロシージャを実行したり、ディストリビューターで情報を更新したりするときに使用するアカウントのパスワードを変更するには、ダイアログ ボックスの **[パブリッシャー]** ページで **[パスワード]** ボックスおよび **[パスワードの確認入力]** ボックスに新しいパスワードを入力します。 詳細については、「[ディストリビューターのセキュリティ保護](../../relational-databases/replication/security/secure-the-distributor.md)」を参照してください。  
  
4.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
#### <a name="to-view-and-modify-publisher-properties"></a>パブリッシャーのプロパティを表示および変更するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを右クリックし、 **[パブリッシャーのプロパティ]** をクリックします。  
  
3.  **[パブリッシャーのプロパティ - < Publisher >]** ダイアログ ボックスで、パブリッシャーのプロパティを表示および変更します。  
  
    -   固定サーバー ロール **sysadmin** のユーザーは、 **[パブリケーション データベース]** のページでデータベースのレプリケーションを有効化できます。 データベースを有効化しても、そのデータベースがパブリッシュされるわけではありません。固定データベース ロール **db_owner** の任意のユーザーが、1 つ以上のパブリケーションをデータベースに作成できるようになります。  
  
4.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 パブリッシャーとディストリビューターのプロパティは、プログラムからレプリケーション ストアド プロシージャを使用して表示できます。  
  
#### <a name="to-view-distributor-and-distribution-database-properties"></a>ディストリビューターとディストリビューション データベースのプロパティを表示するには  
  
1.  [sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md) を実行すると、ディストリビューター、ディストリビューション データベース、作業ディレクトリに関する情報が返されます。  
  
2.  [sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) を実行すると、指定されたディストリビューション データベースのプロパティが返されます。  
  
#### <a name="to-change-distributor-and-distribution-database-properties"></a>ディストリビューターとディストリビューション データベースのプロパティを変更するには  
  
1.  ディストリビューターのプロパティを変更するには、ディストリビューターで [sp_changedistributor_property](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md) を実行します。  
  
2.  ディストリビューション データベースのプロパティを変更するには、ディストリビューターで [sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md) を実行します。  
  
3.  ディストリビューターのパスワードを変更するには、ディストリビューターで [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) を実行します。  
  
    > [!IMPORTANT]  
    >  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報をスクリプト ファイルに含める必要がある場合は、不正なアクセスが行われないようにファイルをセキュリティで保護してください。  
  
4.  ディストリビューターを使用しているパブリッシャーのプロパティを変更するには、ディストリビューターで [sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) を実行します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトによってディストリビューターおよびディストリビューション データベースに関する情報を返します。  
  
 [!code-sql[HowTo#sp_helpdistributor](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_1.sql)]  
  
 [!code-sql[HowTo#sp_helpdistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_2.sql)]  
  
 次の例では、ディストリビューターの保有期間、ディストリビューターへの接続時に使用されるパスワード、およびディストリビューターが各種レプリケーション エージェントの状態を確認する間隔 (ハートビート間隔) を変更します。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報をスクリプト ファイルに含める必要がある場合は、不正なアクセスが行われないようにファイルをセキュリティで保護してください。  
  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_3.sql)]  
  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_4.sql)]  
  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_5.sql)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
  
#### <a name="to-view-and-modify-distributor-properties"></a>ディストリビューターのプロパティを表示および変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> クラスのインスタンスを作成します。 手順 1 の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを渡します。  
  
3.  (省略可) <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> プロパティをチェックして、現在接続されているサーバーがディストリビューターであることを確認します。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> メソッドを呼び出して、サーバーからプロパティを取得します。  
  
5.  (省略可) プロパティを変更するには、 <xref:Microsoft.SqlServer.Replication.ReplicationServer> オブジェクトの設定可能なディストリビューター プロパティに新しい値を設定します。  
  
6.  (省略可) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> オブジェクトの <xref:Microsoft.SqlServer.Replication.ReplicationServer> プロパティが **true**に設定されている場合は、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出して変更内容をサーバーにコミットします。  
  
#### <a name="to-view-and-modify-distribution-database-properties"></a>ディストリビューション データベースのプロパティを表示および変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.DistributionDatabase> クラスのインスタンスを作成します。 name プロパティを指定し、手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを渡します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、サーバーからプロパティを取得します。 このメソッドから **false**が返された場合、指定した名前のデータベースはサーバー上に存在しません。  
  
4.  (省略可) プロパティを変更するには、 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> の設定可能なプロパティに新しい値を設定します。  
  
5.  (省略可) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> オブジェクトの <xref:Microsoft.SqlServer.Replication.DistributionDatabase> プロパティが **true**に設定されている場合は、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出して変更内容をサーバーにコミットします。  
  
#### <a name="to-view-and-modify-publisher-properties"></a>パブリッシャーのプロパティを表示および変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> プロパティを指定し、手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを渡します。  
  
3.  (省略可) プロパティを変更するには、 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> の設定可能なプロパティに新しい値を設定します。  
  
4.  (省略可) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> オブジェクトの <xref:Microsoft.SqlServer.Replication.DistributionPublisher> プロパティが **true**に設定されている場合は、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出して変更内容をサーバーにコミットします。  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>パブリッシャーからディストリビューターへの管理接続に使用されているパスワードを変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに、手順 1. の接続を設定します。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> メソッドを呼び出します。 新しいパスワード値を *password* パラメーターに渡します。  
  
    > [!IMPORTANT]  
    >  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報を保存する必要がある場合は、 [Windows .NET&#xA0;Framework に用意されている](https://go.microsoft.com/fwlink/?LinkId=34733) 暗号化サービス [!INCLUDE[msCoName](../../includes/msconame-md.md)] を使用します。  
  
6.  (省略可) このディストリビューターを使用している各リモート パブリッシャーでパスワードを変更するには、次の手順に従います。  
  
    1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
    2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> クラスのインスタンスを作成します。  
  
    3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに、手順 6a. で作成した接続を設定します。  
  
    4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。  
  
    5.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> メソッドを呼び出します。 手順 5. の新しいパスワード値を *password* パラメーターに渡します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例に、ディストリビューションのプロパティおよびディストリビューション データベースのプロパティを変更する方法を示します。  
  
> [!IMPORTANT]  
>  資格情報をコードに記述するのを避けるため、新しいディストリビューター パスワードは実行時に指定するようにしています。  
  
 [!code-cs[HowTo#rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## <a name="see-also"></a>参照  
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [パブリッシングおよびディストリビューションの無効化](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [[ディストリビューションの構成]](../../relational-databases/replication/configure-distribution.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [ディストリビューターおよびパブリッシャーの情報スクリプト](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [パブリッシャーの情報を表示し、タスクを実行する &#40;レプリケーション モニター&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)  
  
  
