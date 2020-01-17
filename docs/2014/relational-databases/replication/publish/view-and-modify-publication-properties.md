---
title: パブリケーション プロパティの表示および変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- modifying replication properties, articles
- articles [SQL Server replication], modifying
- publications [SQL Server replication], properties
- articles [SQL Server replication], properties
- modifying replication properties, publications
- publications [SQL Server replication], modifying
ms.assetid: 27d72ea4-bcb6-48f2-b4aa-eb1410da7efc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5053cc16734cc18c75e163fec4c06b1768e590cc
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941063"
---
# <a name="view-and-modify-publication-properties"></a>パブリケーション プロパティの表示および変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、パブリケーションのプロパティを表示および変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
-   **パブリケーションのプロパティを表示または変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   パブリケーションの作成後には変更できないプロパティや、パブリケーションへのサブスクリプションがある場合には変更できないプロパティもあります。 変更できないプロパティは、読み取り専用として表示されます。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   パブリケーションの作成後、プロパティの変更によっては新しいスナップショットが必要となります。 パブリケーションにサブスクリプションが含まれている場合、変更によっては、すべてのサブスクリプションを再初期化する必要もあります。 詳細については、「[Change Publication and Article Properties](change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) と「[Add Articles to and Drop Articles from Existing Publications](add-articles-to-and-drop-articles-from-existing-publications.md)」(既存パブリケーションでのアーティクルの追加と削除) をご覧ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] とレプリケーション モニターで使用可能な **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、パブリケーションのプロパティを表示および変更します。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスには、以下のページがあります。  
  
-   **[全般]** ページ。パブリケーションの名前と説明、データベースの名前、パブリケーションの種類、およびサブスクリプションの有効期限の設定が含まれています。  
  
-   **[アーティクル]** ページ。パブリケーションの新規作成ウィザードの **[アーティクル]** ページに相当します。 このページでは、アーティクルの追加や削除、およびアーティクルのプロパティや列のフィルター選択の変更を行うことができます。  
  
-   **[行のフィルター選択]** ページ。パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページに相当します。 このページでは、すべての種類のパブリケーションの静的行フィルターや、マージ パブリケーションのパラメーター化された行フィルターと結合フィルターを追加、編集、および削除できます。  
  
-   **[スナップショット]** ページ。このページでは、スナップショットの形式と場所、スナップショットを圧縮するかどうか、およびスナップショットの適用の前後に実行するスクリプトを指定できます。  
  
-   **[FTP スナップショット]** ページ (スナップショット パブリケーション、トランザクション パブリケーション、および SQL Server 2005 より前のバージョンを実行しているパブリッシャーのマージ パブリケーションの場合)。このページでは、サブスクライバーがスナップショット ファイルをファイル転送プロトコル (FTP) でダウンロードできるかどうかを指定できます。  
  
-   **[FTP スナップショットとインターネット]** ページ (SQL Server 2005 以降を実行しているパブリッシャーからのマージ パブリケーションの場合)。このページでは、サブスクライバーがスナップショット ファイルを FTP でダウンロードできるかどうか、および HTTPS でサブスクリプションを同期できるかどうかを指定できます。  
  
-   **[サブスクリプション オプション]** ページ。このページでは、すべてのサブスクリプションに適用されるさまざまなオプションを設定できます。 利用できるオプションは、パブリケーションの種類によって異なります。  
  
-   **[パブリケーション アクセス リスト]** ページ。このページでは、パブリケーションにアクセスできるログインやグループを指定できます。  
  
-   **[エージェント セキュリティ]** ページ。このページでは、エージェントの実行やレプリケーション トポロジ内のコンピューターへの接続に使用されるアカウントの設定にアクセスできます。この設定を使用するエージェントは、すべてのパブリケーションのスナップショット エージェント、すべてのトランザクション パブリケーションのログ リーダー エージェント、およびキュー更新サブスクリプションを許可するトランザクション パブリケーションのキュー リーダー エージェントです。  
  
-   **[データ パーティション]** ページ (SQL Server 2005 以降を実行しているパブリッシャーからのマージ パブリケーションの場合)。このページでは、パラメーター化されたフィルターを使用するパブリケーションのサブスクライバーが、スナップショットを利用できない場合にスナップショットを要求できるかどうかを指定できます。 また、1 つ以上のパーティションのスナップショットを 1 回生成したり、スケジュールによって定期的に生成したりすることもできます。  
  
#### <a name="to-view-and-modify-publication-properties-in-management-studio"></a>Management Studio でパブリケーションのプロパティを表示および変更するには  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  パブリケーションを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
#### <a name="to-view-and-modify-publication-properties-in-replication-monitor"></a>レプリケーション モニターでパブリケーションのプロパティを表示および変更するには  
  
1.  レプリケーション モニターの左ペインでパブリッシャー グループを展開し、パブリッシャーを展開します。  
  
2.  パブリケーションを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 パブリケーションのプロパティは、レプリケーションのストアド プロシージャを使用して、プログラムから変更および取得できます。 どのストアド プロシージャを使用するかは、パブリケーションの種類によって異なります。  
  
#### <a name="to-view-the-properties-of-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのプロパティを表示するには  
  
1.  [Sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)を実行し、  **\@パブリケーション**パラメーターにパブリケーションの名前を指定します。 このパラメーターを指定しなかった場合、パブリッシャーのすべてのパブリケーションの情報が返されます。  
  
#### <a name="to-change-the-properties-of-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのプロパティを変更するには  
  
1.  [Sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)を実行します。このとき、  **\@プロパティ**パラメーターで変更するパブリケーションプロパティを指定し、  **\@value**パラメーターにこのプロパティの新しい値を指定します。  
  
    > [!NOTE]  
    >  変更時に新しいスナップショットの生成が必要な場合は、  **\@force_invalidate_snapshot**に**1**を指定する必要があります。また、サブスクライバーを再初期化する必要がある場合は、値1を指定する必要があります。  **\@force_reinit_subscription**の場合。 変更時に新しいスナップショットの生成または再初期化が必要となるプロパティの詳細については、「[Change Publication and Article Properties](change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) を参照してください。  
  
#### <a name="to-view-the-properties-of-a-merge-publication"></a>マージ パブリケーションのプロパティを表示するには  
  
1.  [Sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)を実行し、  **\@パブリケーション**パラメーターにパブリケーションの名前を指定します。 このパラメーターを指定しなかった場合、パブリッシャーのすべてのパブリケーションの情報が返されます。  
  
#### <a name="to-change-the-properties-of-a-merge-publication"></a>マージ パブリケーションのプロパティを変更するには  
  
1.  [Sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)を実行します。これは、  **\@property**パラメーターで変更されるパブリケーションプロパティと、  **\@value**パラメーターでのこのプロパティの新しい値を指定します。  
  
    > [!NOTE]  
    >  変更時に新しいスナップショットの生成が必要な場合は、  **\@force_invalidate_snapshot**に**1**を指定する必要があります。また、サブスクライバーを再初期化する必要がある場合は、値1を指定する必要があります。  **force_reinit_subscription\@** の詳細については、変更時に新しいスナップショットまたは再初期化が必要なプロパティの詳細については、「[パブリケーションおよびアーティクルのプロパティの変更](change-publication-and-article-properties.md)」を参照してください。  
  
#### <a name="to-view-the-properties-of-a-snapshot"></a>スナップショットのプロパティを表示するには  
  
1.  [Sp_helppublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql)を実行し、  **\@パブリケーション**パラメーターにパブリケーションの名前を指定します。  
  
#### <a name="to-change-the-properties-of-a-snapshot"></a>スナップショットのプロパティを変更するには  
  
1.  変更対象のスナップショット パラメーターに新しいスナップショット プロパティを少なくとも 1 つ指定して、 [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql)を実行します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 パブリケーションのプロパティを取得するトランザクション レプリケーションの例を、次に示します。  
  
 [!code-sql[HowTo#sp_helppublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranpub.sql#sp_helppublication)]  
  
 パブリケーションのスキーマ レプリケーションを無効化するトランザクション レプリケーションの例を、次に示します。  
  
 [!code-sql[HowTo#sp_changepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranpub.sql#sp_changepublication)]  
  
 パブリケーションのプロパティを取得するマージ レプリケーションの例を、次に示します。  
  
 [!code-sql[HowTo#sp_helpmergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergepub.sql#sp_helpmergepublication)]  
  
 パブリケーションのスキーマ レプリケーションを無効化するマージ レプリケーションの例を、次に示します。  
  
 [!code-sql[HowTo#sp_changemergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergepub.sql#sp_changemergepublication)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 レプリケーション管理オブジェクト (RMO) を使用して、パブリケーションの変更とそのプロパティへのアクセスをプログラムから実行できます。 パブリケーション プロパティの表示と変更に使用する RMO クラスは、パブリケーションの種類によって異なります。  
  
#### <a name="to-view-or-modify-properties-of-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのプロパティを表示または変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成し、パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティと <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定して、手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドが `false` を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  (省略可) プロパティを変更するには、設定可能なプロパティに新しい値を設定します。 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> プロパティに特定の <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 値が設定されているかどうかを判断するには、論理積演算子 (Microsoft Visual C# では `&`、Microsoft Visual Basic では `And`) を使用します。 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> プロパティの <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 値を変更するには、包括的論理和演算子 (Visual C# では `|`、Visual Basic では `Or`) および排他的論理和演算子 (Visual C# では `^`、Visual Basic では `Xor`) を使用します。  
  
5.  (省略可) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> に `true` を指定した場合、<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出してサーバーに変更をコミットします。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> に `false` (既定値) を指定した場合、変更は直ちにサーバーに送られます。  
  
#### <a name="to-view-or-modify-properties-of-a-merge-publication"></a>マージ パブリケーションのプロパティを表示または変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成し、パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティと <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定して、手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドが `false` を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  (省略可) プロパティを変更するには、設定可能なプロパティに新しい値を設定します。 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> プロパティに特定の <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 値が設定されているかどうかを判断するには、論理積演算子 (Visual C# では `&`、Visual Basic では `And`) を使用します。 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> プロパティの <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 値を変更するには、包括的論理和演算子 (Visual C# では `|`、Visual Basic では `Or`) および排他的論理和演算子 (Visual C# では `^`、Visual Basic では `Xor`) を使用します。  
  
5.  (省略可) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> に `true` を指定した場合、<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出してサーバーに変更をコミットします。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> に `false` (既定値) を指定した場合、変更は直ちにサーバーに送られます。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、トランザクション パブリケーションにパブリケーション属性を設定します。 変更は明示的にサーバーに送られるまでキャッシュされます。  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeTranPub_cached](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changetranpub_cached)]  
  
 次の例では、マージ パブリケーションの DDL レプリケーションを無効にします。  
  
 [!code-csharp[HowTo#rmo_ChangeMergePub_ddl](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changemergepub_ddl)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergePub_ddl](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changemergepub_ddl)]  
  
## <a name="see-also"></a>関連項目  
 [データとデータベース オブジェクトのパブリッシュ](publish-data-and-database-objects.md)   
 [パブリケーションとアーティクルのプロパティの変更](change-publication-and-article-properties.md)   
 [パブリケーション データベースでのスキーマの変更](make-schema-changes-on-publication-databases.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [パブリケーションに対してアーティクルを追加または削除する](add-articles-to-and-drop-articles-from-a-publication.md)   
 [レプリケーション モニターを使用して情報を表示し、タスクを実行する](../monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [アーティクルのプロパティの表示および変更](view-and-modify-article-properties.md)  
  
  
