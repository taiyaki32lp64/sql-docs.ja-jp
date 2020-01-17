---
title: アーティクルのプロパティの表示および変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changearticle
- sp_helparticle
- viewing replication properties
- sp_changemergearticle
- sp_helpmergearticle
- modifying replication properties, articles
- articles [SQL Server replication], modifying
- articles [SQL Server replication], properties
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 325bedac3968cb59c70863d54c7e0ef429cedd75
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941073"
---
# <a name="view-and-modify-article-properties"></a>アーティクルのプロパティの表示および変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、アーティクルのプロパティを表示および変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
-   **アーティクルのプロパティを表示および変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   パブリケーションの作成後には変更できないプロパティや、パブリケーションへのサブスクリプションがある場合には変更できないプロパティもあります。 変更できないプロパティは、読み取り専用として表示されます。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   パブリケーションの作成後、プロパティの変更によっては新しいスナップショットが必要となります。 パブリケーションにサブスクリプションが含まれている場合、変更によっては、すべてのサブスクリプションを再初期化する必要もあります。 詳細については、「[Change Publication and Article Properties](change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) と「[Add Articles to and Drop Articles from Existing Publications](add-articles-to-and-drop-articles-from-existing-publications.md)」(既存パブリケーションでのアーティクルの追加と削除) をご覧ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] とレプリケーション モニターにある **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、アーティクルのプロパティを表示および変更します。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
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
  
#### <a name="to-view-and-modify-article-properties"></a>アーティクルのプロパティを表示および変更するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで、アーティクルを選択し、 **[アーティクルのプロパティ]** をクリックします。  
  
2.  プロパティの変更を適用するアーティクルを選択します。  
  
    -   **[反転表示された \<ObjectType> アーティクルのプロパティを設定]** をクリックし、 **[アーティクルのプロパティ - \<ObjectName>]** ダイアログ ボックスを表示します。このダイアログ ボックスで行われたプロパティの変更は、 **[アーティクル]** ページのオブジェクト ペインで反転表示されたオブジェクトだけに適用されます。  
  
    -   **[すべての\<ObjectType> アーティクルのプロパティを設定]** をクリックし、 **[すべての \<ObjectType> アーティクルのプロパティ]** ダイアログ ボックスを表示します。このダイアログ ボックスで行われたプロパティの変更は、パブリケーションが選択されていないオブジェクトも含めた、 **[アーティクル]** ページのオブジェクト ペインにあるこの種類のすべてのオブジェクトに適用されます。  
  
        > [!NOTE]  
        >  **[すべての \<ObjectType&gt; アーティクルのプロパティ]** ダイアログ ボックスで行われたプロパティの変更は、 **[アーティクルのプロパティ - \<ObjectName&gt;]** ダイアログ ボックスで以前行われたすべての変更をオーバーライドします。 たとえば、あるオブジェクトの種類のすべてのアーティクルに対して複数の既定を設定し、かつそれぞれのオブジェクトに対してプロパティを設定する場合には、最初にすべてのアーティクルに対する既定を設定します。 次に、それぞれのオブジェクトに対してプロパティを設定します。  
  
3.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
4.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 アーティクルのプロパティは、レプリケーションのストアド プロシージャを使用して、プログラムから変更および取得できます。 使用するストアド プロシージャは、アーティクルが属するパブリケーションの種類によって異なります。  
  
#### <a name="to-view-the-properties-of-an-article-belonging-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに属するアーティクルのプロパティを表示するには  
  
1.  [Sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)を実行します。  **\@パブリケーション**パラメーターにパブリケーションの名前を指定し、  **\@article**パラメーターにアーティクルの名前を指定します。 **\@アーティクル**を指定しない場合は、パブリケーションのすべてのアーティクルに関する情報が返されます。  
  
2.  テーブル アーティクルについて [sp_helparticlecolumns](/sql/relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql) を実行し、ベース テーブルで使用できるすべての列を一覧表示します。  
  
#### <a name="to-modify-the-properties-of-an-article-belonging-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに属するアーティクルのプロパティを変更するには  
  
1.  [Sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)を実行します。このとき、  **\@プロパティ**パラメーターで変更するアーティクルのプロパティと、  **\@value**パラメーターのこのプロパティの新しい値を指定します。  
  
    > [!NOTE]  
    >  変更で新しいスナップショットを生成する必要がある場合は、  **\@force_invalidate_snapshot**に値**1**を指定する必要があります。また、サブスクライバーを再初期化する必要がある場合は、値**1**を指定する必要もあります。 **\@force_reinit_subscription**の場合。 変更時に新しいスナップショットの生成または再初期化が必要となるプロパティの詳細については、「[Change Publication and Article Properties](change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) を参照してください。  
  
#### <a name="to-view-the-properties-of-an-article-belonging-to-a-merge-publication"></a>マージ パブリケーションに属するアーティクルのプロパティを表示するには  
  
1.  [Sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)を実行します。  **\@パブリケーション**パラメーターにパブリケーションの名前を指定し、  **\@article**パラメーターにアーティクルの名前を指定します。 これらのパラメーターを指定しない場合、パブリケーションまたはパブリッシャーのすべてのアーティクルに関する情報が返されます。  
  
2.  テーブル アーティクルに対して [sp_helpmergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql) を実行し、ベース テーブルで使用できるすべての列を一覧表示します。  
  
#### <a name="to-modify-the-properties-of-an-article-belonging-to-a-merge-publication"></a>マージ パブリケーションに属するアーティクルのプロパティを変更するには  
  
1.  [Sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)を実行します。このとき、  **\@プロパティ**パラメーターで変更するアーティクルのプロパティと、  **\@value**パラメーターのこのプロパティの新しい値を指定します。  
  
    > [!NOTE]  
    >  変更で新しいスナップショットを生成する必要がある場合は、  **\@force_invalidate_snapshot**に値**1**を指定する必要があります。また、サブスクライバーを再初期化する必要がある場合は、値**1**を指定する必要もあります。 **\@force_reinit_subscription**の場合。 変更時に新しいスナップショットの生成または再初期化が必要となるプロパティの詳細については、「[Change Publication and Article Properties](change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) を参照してください。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 パブリッシュされたアーティクルのプロパティを取得するトランザクション レプリケーションの例を、次に示します。  
  
 [!code-sql[HowTo#sp_helptranarticle](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranart.sql#sp_helptranarticle)]  
  
 パブリッシュされたアーティクルのスキーマ オプションを変更するトランザクション レプリケーションの例を、次に示します。  
  
 [!code-sql[HowTo#sp_changetranarticle](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranart.sql#sp_changetranarticle)]  
  
 パブリッシュされたアーティクルのプロパティを取得するマージ レプリケーションの例を、次に示します。  
  
 [!code-sql[HowTo#sp_helpmergearticle](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergeart.sql#sp_helpmergearticle)]  
  
 パブリッシュされたアーティクルの競合検出の設定を変更するマージ レプリケーションの例を、次に示します。  
  
 [!code-sql[HowTo#sp_changemergearticle](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergeart.sql#sp_changemergearticle)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 アーティクルのプロパティは、レプリケーション管理オブジェクト (RMO) を使用してプログラムから変更できます。 アーティクルのプロパティを表示または変更する際に使用する RMO のクラスは、アーティクルが属しているパブリケーションの種類によって異なります。  
  
#### <a name="to-view-or-modify-properties-of-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに属しているアーティクルのプロパティを表示または変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransArticle> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> の各プロパティを設定します。  
  
4.  手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから `false` が返された場合、手順 3. で指定したアーティクルのプロパティが正しく定義されていないか、アーティクルが存在していません。  
  
6.  (省略可) プロパティを変更するには、 <xref:Microsoft.SqlServer.Replication.TransArticle> の設定可能なプロパティに新しい値を設定します。  
  
7.  (省略可) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> に `true` を指定した場合、<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出してサーバーに変更をコミットします。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> に `false` (既定値) を指定した場合、変更は直ちにサーバーに送られます。  
  
#### <a name="to-view-or-modify-properties-of-an-article-that-belongs-to-a-merge-publication"></a>マージ パブリケーションに属しているアーティクルのプロパティを表示または変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> の各プロパティを設定します。  
  
4.  手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから `false` が返された場合、手順 3. で指定したアーティクルのプロパティが正しく定義されていないか、アーティクルが存在していません。  
  
6.  (省略可) プロパティを変更するには、 <xref:Microsoft.SqlServer.Replication.MergeArticle> の設定可能なプロパティに新しい値を設定します。  
  
7.  (省略可) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> に `true` を指定した場合、<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出してサーバーに変更をコミットします。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> に `false` (既定値) を指定した場合、変更は直ちにサーバーに送られます。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、マージ アーティクルに変更を加え、アーティクル用のビジネス ロジック ハンドラーを指定しています。  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## <a name="see-also"></a>関連項目  
 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../implement-a-business-logic-handler-for-a-merge-article.md)   
 [データとデータベース オブジェクトのパブリッシュ](publish-data-and-database-objects.md)   
 [パブリケーションとアーティクルのプロパティの変更](change-publication-and-article-properties.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [マージ レプリケーションの競合検出および解決の詳細](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
