---
title: データとデータベース オブジェクトのパブリッシュ | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- user-defined types [SQL Server replication]
- articles [SQL Server replication], dropping
- objects [SQL Server replication]
- publications [SQL Server replication], creating
- merge replication [SQL Server replication], publications
- schema-only articles [SQL Server replication]
- publishing [SQL Server replication], database objects
- articles [SQL Server replication], defining
- publishing [SQL Server replication], functions
- replication [SQL Server], publications
- publishing [SQL Server replication], views
- tables [SQL Server replication]
- schemas [SQL Server replication]
- publishing [SQL Server replication], data
- schemas [SQL Server replication], publishing
- articles [SQL Server replication], stored procedures and
- publishing [SQL Server replication], tables
- alias data types [SQL Server replication]
- publications [SQL Server replication], deleting
- snapshot replication [SQL Server], publications
- articles [SQL Server replication], modifying
- transactional replication, publications
- publishing [SQL Server replication], stored procedures
- publishing [SQL Server replication]
- views [SQL Server replication]
- stored procedures [SQL Server replication], publishing
- publications [SQL Server replication], schema options
- articles [SQL Server replication], adding
- publications [SQL Server replication], modifying
- user-defined functions [SQL Server replication]
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70e31ec60f8f47dfbc0a4761357c99a42623c6eb
ms.sourcegitcommit: ea6603e20c723553c89827a6b8731a9e7b560b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2019
ms.locfileid: "74479317"
---
# <a name="publish-data-and-database-objects"></a>データとデータベース オブジェクトのパブリッシュ
  パブリケーションの作成時には、パブリッシュするテーブルやその他のデータベース オブジェクトを選択します。 レプリケーションを使用すると、以下のデータベース オブジェクトをパブリッシュできます。  
  
|データベース オブジェクト|スナップショット レプリケーションおよびトランザクション レプリケーション|マージ レプリケーション|  
|---------------------|--------------------------------------------------------|-----------------------|  
|テーブル|X|X|  
|パーティション テーブル|X|X|  
|ストアド プロシージャ - 定義 ([!INCLUDE[tsql](../../../includes/tsql-md.md)] および CLR)|X|X|  
|ストアド プロシージャ - 実行 ([!INCLUDE[tsql](../../../includes/tsql-md.md)] および CLR)|X|×|  
|ビュー|X|X|  
|インデックス付きビュー|X|X|  
|テーブルとしてのインデックス付きビュー|X|×|  
|ユーザー定義型 (CLR)|X|X|  
|ユーザー定義関数 ([!INCLUDE[tsql](../../../includes/tsql-md.md)] および CLR)|X|X|  
|別名データ型|X|X|  
|フル テキスト インデックス|X|X|  
|スキーマ オブジェクト (制約、インデックス、ユーザー DML トリガー、拡張プロパティ、および照合順序)|X|X|  
  
## <a name="creating-publications"></a>パブリケーションの作成  
 パブリケーションを作成するには、次の情報を指定します。  
  
-   ディストリビューター。  
  
-   スナップショット ファイルの場所。  
  
-   パブリケーション データベース。  
  
-   作成するパブリケーションの種類 (スナップショット、トランザクション、更新可能なサブスクリプションを含むトランザクション、またはマージ)。  
  
-   パブリケーションに含めるデータとデータベース オブジェクト (アーティクル)。  
  
-   すべての種類のパブリケーションの静的行フィルターと列フィルター、およびマージ パブリケーションのパラメーター化された行フィルターと結合フィルター。  
  
-   スナップショット エージェントのスケジュール。  
  
-   エージェントの実行に使用するアカウント。対象となるエージェントは、スナップショット エージェント (すべてのパブリケーション用)、ログ リーダー エージェント (すべてのトランザクション パブリケーション用)、およびキュー リーダー エージェント (サブスクリプションの更新が許可されているトランザクション パブリケーション用) です。  
  
-   パブリケーションの名前と説明。  
  
 パブリケーションの操作方法の詳細については、次のトピックを参照してください。  
  
-   [パブリケーションを作成する](create-a-publication.md)  
  
-   [アーティクルの定義](define-an-article.md)  
  
-   [パブリケーションのプロパティの表示および変更](view-and-modify-publication-properties.md)  
  
-   [アーティクルのプロパティの表示および変更](view-and-modify-article-properties.md)  
  
-   [パブリケーションを削除する](delete-a-publication.md)  
  
-   [アーティクルの削除](delete-an-article.md)  
  
> [!NOTE]  
>  アーティクルまたはパブリケーションを削除しても、オブジェクトはサブスクライバーから削除されません。  
  
## <a name="publishing-tables"></a>テーブルのパブリッシュ  
 パブリッシュされるオブジェクトで最も一般的なのはテーブルです。 以下のリンクは、テーブルのパブリッシュに関連する分野についての情報を提供します。  
  
-   [パブリッシュされたデータのフィルター処理](filter-published-data.md)  
  
-   [トランザクションレプリケーションのアーティクルオプション](../transactional/article-options-for-transactional-replication.md)  
  
-   [マージレプリケーションのアーティクルオプション](../merge/article-options-for-merge-replication.md)  
  
-   [Id 列のレプリケート](replicate-identity-columns.md)  
  
 レプリケーションでテーブルをパブリッシュする場合、宣言された参照整合性 (主キー制約、参照に関する制約、一意制約)、インデックス、ユーザー DML トリガー (DDL トリガーはレプリケートできません)、拡張プロパティ、照合順序などの、サブスクライバーにコピーするスキーマ オブジェクトを指定できます。 拡張プロパティは、パブリッシャーとサブスクライバー間で初期同期を実行するときにのみレプリケートされます。 初期同期の完了後に拡張プロパティを追加または変更した場合、その変更はレプリケートされません。  
  
 スキーマ オプションを指定する場合は、「[スキーマ オプションの指定](specify-schema-options.md)」または「<xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>」を参照してください。  
  
### <a name="partitioned-tables-and-indexes"></a>パーティション テーブルとパーティション インデックス  
 レプリケーションでは、パーティション テーブルとパーティション インデックスのパブリッシュがサポートされます。 サポート レベルは、使用するレプリケーションの種類、パブリケーションに指定するオプション、およびパーティション テーブルに関連付けられたアーティクルによって異なります。 詳細については、「[パーティション テーブルとパーティション インデックスのレプリケート](replicate-partitioned-tables-and-indexes.md)」を参照してください。  
  
## <a name="publishing-stored-procedures"></a>ストアド プロシージャのパブリッシュ  
 すべての種類のレプリケーションで、ストアド プロシージャの定義をレプリケートできます。各サブスクライバーに CREATE PROCEDURE がコピーされます。 共通言語ランタイム (CLR) ストアド プロシージャの場合は、関連するアセンブリもコピーされます。 プロシージャの変更はサブスクライバーにレプリケートされますが、関連するアセンブリの変更はレプリケートされません。  
  
 トランザクション レプリケーションでは、ストアド プロシージャの定義の他に、ストアド プロシージャの実行もレプリケートできます。 これは、大量のデータに影響を与えるメンテナンス用ストアド プロシージャの結果をレプリケートする場合に便利です。 詳細については、「[トランザクション レプリケーションにおけるパブリッシング ストアド プロシージャの実行](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)」をご覧ください。  
  
## <a name="publishing-views"></a>ビューのパブリッシュ  
 すべての種類のレプリケーションで、ビューをレプリケートできます。 ビュー (インデックス付きビューの場合は付属するインデックスも含む) はサブスクライバーにコピーできますが、ベース テーブルもレプリケートする必要があります。  
  
 トランザクション レプリケーションでは、インデックス付きビューをビューではなくテーブルとしてレプリケートできます。この場合、ベース テーブルをレプリケートする必要はありません。 これを行うには、 [sp_addarticle &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)の* \@type*パラメーターに "indexed view logbased" オプションのいずれかを指定します。 
  **sp_addarticle** の使用方法の詳細については、「[アーティクルの定義](define-an-article.md)」を参照してください。  
  
## <a name="publishing-user-defined-functions"></a>ユーザー定義関数のパブリッシュ  
 CLR 関数および [!INCLUDE[tsql](../../../includes/tsql-md.md)] 関数の CREATE FUNCTION ステートメントが各サブスクライバーにコピーされます。 CLR 関数の場合は、関連するアセンブリもコピーされます。 関数の変更はサブスクライバーにレプリケートされますが、関連するアセンブリの変更はレプリケートされません。  
  
## <a name="publishing-user-defined-types-and-alias-data-types"></a>ユーザー定義型および別名データ型のパブリッシュ  
 ユーザー定義型または別名データ型を使用する列は、他の列と同様にサブスクライバーにレプリケートされます。 レプリケートされた各データ型の CREATE TYPE ステートメントがテーブルの作成前にサブスクライバーで実行されます。 ユーザー定義型の場合は、関連するアセンブリも各サブスクライバーにコピーされます。 ユーザー定義型および別名データ型の変更はサブスクライバーにレプリケートされません。  
  
 データベースで型が定義されている場合でも、パブリケーションの作成時に列で参照されていなければ、その型はサブスクライバーにコピーされません。 この型を使用する列を後でデータベースに作成してレプリケートする場合、最初にこの型 (ユーザー定義型の場合は関連するアセンブリも含む) を手動で各サブスクライバーにコピーする必要があります。  
  
## <a name="publishing-full-text-indexes"></a>フルテキスト インデックスのパブリッシュ  
 CREATE FULLTEXT INDEX ステートメントが各サブスクライバーにコピーされ、フルテキスト インデックスがサブスクライバーに作成されます。 ALTER FULLTEXT INDEX を使用して行われたフルテキスト インデックスの変更はレプリケートされません。  
  
## <a name="making-schema-changes-to-published-objects"></a>パブリッシュされたオブジェクトに対するスキーマの変更  
 レプリケーションは、パブリッシュされたオブジェクトに対するさまざまなスキーマ変更をサポートしています。 パブリッシュされた適切なオブジェクトに対して、以下に示すスキーマ変更を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パブリッシャーで実行した場合、既定ではすべての [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サブスクライバーにその変更が反映されます。  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 詳細については、「[パブリケーション データベースでのスキーマの変更](make-schema-changes-on-publication-databases.md)」を参照してください。  
  
## <a name="considerations-for-publishing"></a>パブリッシングに関する注意点  
 データベース オブジェクトをパブリッシュするときは、以下の点に注意してください。  
  
-   パブリケーションおよび初期スナップショットの作成中でもユーザーはデータベースにアクセスできますが、パブリッシャーの利用状況が低い時間帯にパブリケーションを作成することをお勧めします。  
  
-   データベースにパブリケーションを作成した後で、そのデータベースの名前を変更することはできません。 データベース名を変更するには、まずデータベースからレプリケーションを削除する必要があります。  
  
-   1 つまたは複数の他のデータベース オブジェクトに依存するデータベース オブジェクトをパブリッシュする場合、参照されているオブジェクトをすべてパブリッシュする必要があります。 たとえば、テーブルに依存しているビューをパブリッシュする場合は、そのテーブルもパブリッシュする必要があります。  
  
    > [!NOTE]  
    >  マージパブリケーションにアーティクルを追加し、その新しいアーティクルに既存のアーティクルが依存している場合は、 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)と[sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)の** \@processing_order**パラメーターを使用して、両方のアーティクルの処理順序を指定する必要があります。 たとえば、テーブルをパブリッシュし、テーブルが参照している関数はパブリッシュしない場合を考えます。 この関数をパブリッシュしないと、サブスクライバー側でテーブルを作成できないとします。 この場合は、この関数をパブリケーションに追加するときに、**sp_addmergearticle** の **\@processing_order** パラメーターに値 **1** を指定し、**sp_changemergearticle** の **\@processing_order** パラメーターに値 **2** を指定します。パラメーター **\@article** にはテーブル名を指定します。 この処理順序により、サブスクライバー側で関数に依存するテーブルを作成する前に、関数の作成が求められるようになります。 各アーティクルに使用する値は、関数の値がテーブルの値より小さければ、別の値でもかまいません。  
  
-   パブリケーション名には、% * [ ] | : " ? を使用できません。 \/ \< >。  
  
### <a name="limitations-on-publishing-objects"></a>オブジェクトのパブリッシュに関する制限事項  
  
-   パブリッシュできるアーティクルおよび列の最大数は、パブリケーションの種類によって異なります。 詳細については、「[SQL Server の最大容量仕様](../../../sql-server/maximum-capacity-specifications-for-sql-server.md)」の「レプリケーション オブジェクト」のセクションを参照してください。  
  
-   WITH ENCRYPTION として定義されているストアド プロシージャ、ビュー、トリガー、およびユーザー定義関数は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーションの一部としてパブリッシュすることはできません。  
  
-   XML スキーマ コレクションはレプリケートできますが、初期スナップショットの後で変更をレプリケートすることはできません。  
  
-   トランザクション レプリケーションでは、パブリッシュされたテーブルは主キーを持たなければなりません。 テーブルがトランザクション レプリケーション パブリケーション内にある場合、主キー列に関連付けられているインデックスを無効にすることはできません。 これらのインデックスはレプリケーションで必要です。 インデックスを無効にするには、まずパブリケーションからテーブルを削除する必要があります。  
  
-   
  [sp_bindefault &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindefault-transact-sql) で作成されたバインドされたデフォルトはレプリケートできません (バインドされたデフォルトは非推奨のため、ALTER TABLE または CREATE TABLE の DEFAULT オプションで作成されたデフォルトを使用してください)。  
  
-   ディストリビューション エージェントが配信を行う順序が原因で、インデックス付きビューに `NOEXPAND` ヒントを含む関数を、参照テーブルやインデックス付きビューと同じパブリケーション内でパブリッシュすることはできません。 この問題を回避するために、最初のパブリケーション内にテーブルとインデックス付きビューを配置し、インデックス付きビューに `NOEXPAND` ヒントを含む関数を、最初のパブリケーションが完了した後にパブリッシュする 2 番目のパブリケーションに追加します。 または、これらの関数のスクリプトを作成し、の`sp_addpublication` * \@post_snapshot_script*パラメーターを使用してスクリプトを配信します。  
  
### <a name="schemas-and-object-ownership"></a>スキーマおよびオブジェクトの所有権  
 既定では、パブリケーションの新規作成ウィザードは、スキーマとオブジェクトの所有権に関して、以下のように動作します。  
  
-   互換性レベル 90 以上のマージ パブリケーションと、スナップショット パブリケーション、およびトランザクション パブリケーションのアーティクルの場合、既定では、サブスクライバーでのオブジェクト所有者は、パブリッシャーでの対応するオブジェクトの所有者と同じになります。 オブジェクトを所有するスキーマがサブスクライバーに存在しない場合は、スキーマが自動的に作成されます。  
  
-   互換性レベルが 90 未満のマージ パブリケーションのアーティクルの場合。既定では、所有者名は空白のままなり、サブスクライバーにオブジェクトを作成する際に **dbo** と指定されます。  
  
-   Oracle パブリケーションのアーティクルの場合。既定では、所有者名が **dbo**と指定されます。  
  
-   キャラクター モードのスナップショット ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のバージョンのサブスクライバーや [!INCLUDE[ssEW](../../../includes/ssew-md.md)] サブスクライバーで使用されます) を使用するパブリケーションのアーティクルの場合。既定では、所有者は空白のままになります。 既定の所有者は、サブスクライバーに接続しているディストリビューション エージェントまたはマージ エージェントで使用されるアカウントに関連付けられている所有者になります。  
  
 オブジェクトの所有者は、**[アーティクルのプロパティ - \<***Article***>]** ダイアログ ボックスと、ストアド プロシージャの **sp_addarticle**、**sp_addmergearticle**、**sp_changearticle**、**sp_changemergearticle** で変更できます。 詳細については、「[View and Modify Publication Properties](view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更)、「[Define an Article](define-an-article.md)」 (アーティクルの定義)、および「[View and Modify Article Properties](view-and-modify-article-properties.md)」 (アーティクルのプロパティの表示および変更) を参照してください。  
  
### <a name="publishing-data-to-subscribers-running-previous-versions-of-sql-server"></a>以前のバージョンの SQL Server を実行するサブスクライバーへのデータのパブリッシュ  
  
-   以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を実行するサブスクライバーにパブリッシュする場合、レプリケーション固有の機能および製品の全般的な機能は共に、該当するバージョンの機能に制限されます。  
  
-   マージ パブリケーションでは互換性レベルが利用されます。この互換性レベルによってパブリケーションで使用する機能が決定され、また以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を実行するサブスクライバーをサポートできるようになります。  
  
### <a name="publishing-tables-in-more-than-one-publication"></a>複数のパブリケーションでのテーブルのパブリッシュ  
 レプリケーションでは、以下に示す制限付きで、アーティクルを複数のパブリケーションでパブリッシュできます (データの再パブリッシュを含む)。  
  
-   アーティクルがトランザクションパブリケーションとマージパブリケーションでパブリッシュされている場合は、マージアーティクルに対して* \@published_in_tran_pub*プロパティが TRUE に設定されていることを確認してください。 プロパティの設定の詳細については、「[View and Modify Publication Properties](view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更)、「[View and Modify Article Properties](view-and-modify-article-properties.md)」 (アーティクルのプロパティの表示および変更) を参照してください。  
  
     アーティクルがトランザクションサブスクリプションの一部であり、マージパブリケーションに含まれている場合は、 * \@published_in_tran_pub*プロパティも設定する必要があります。 これに該当する場合、特に指定がなければ、トランザクション レプリケーションでは、サブスクライバー側のテーブルが読み取り専用として扱われるものと想定しているので、注意が必要です。マージ レプリケーションがトランザクション サブスクリプションに含まれるテーブルに対してデータ変更を行うと、データの非収束が発生する可能性があります。 この可能性を回避するため、マージ パブリケーションではこのようなテーブルをダウンロードのみとして指定することをお勧めします。 これはマージ サブスクライバーがテーブルにデータの変更をアップロードすることを防ぎます。 詳細については、「[ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンスの最適化](../merge/optimize-merge-replication-performance-with-download-only-articles.md)」を参照してください。  
  
-   マージ パブリケーションおよびキュー更新サブスクリプションを使用するトランザクション パブリケーションのどちらも、アーティクルをパブリッシュすることはできません。  
  
-   更新サブスクリプションをサポートするトランザクション パブリケーションのアーティクルを再パブリッシュすることはできません。  
  
-   キュー更新サブスクリプションをサポートする複数のトランザクション パブリケーションでアーティクルをパブリッシュする場合には、すべてのパブリケーションで、次に示すプロパティの値を同一にする必要があります。  
  
    |プロパティ|sp_addarticle のパラメーター|  
    |--------------|---------------------------------|  
    |ID 範囲の管理|auto_identity_range (非推奨) と identityrangemangementoption ** \@** ** \@**|  
    |パブリッシャーの ID 範囲|**\@pub_identity_range**|  
    |ID 範囲|**\@identity_range**|  
    |ID 範囲のしきい値|**\@進入**|  
  
     これらのパラメーターの詳細については、「[sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)」を参照してください。  
  
-   複数のマージ パブリケーションでアーティクルをパブリッシュする場合には、すべてのパブリケーションにわたって、以下に示すプロパティの値を同一にする必要があります。  
  
    |プロパティ|sp_addmergearticle のパラメーター|  
    |--------------|--------------------------------------|  
    |列追跡|**\@column_tracking**|  
    |スキーマ オプション|**\@schema_option**|  
    |列のフィルター選択|**\@vertical_partition**|  
    |サブスクライバーのアップロード オプション|**\@subscriber_upload_options**|  
    |条件付き削除の追跡|**\@delete_tracking**|  
    |エラー補正|**\@compensate_for_errors**|  
    |ID 範囲の管理|auto_identity_range (非推奨) と identityrangemangementoption ** \@** ** \@**|  
    |パブリッシャーの ID 範囲|**\@pub_identity_range**|  
    |ID 範囲|**\@identity_range**|  
    |ID 範囲のしきい値|**\@進入**|  
    |パーティション オプション|**\@partition_options**|  
    |BLOB 列のストリーミング|**\@stream_blob_columns**|  
    |フィルターの種類|filter_type ( **sp_addmergefilter**内のパラメーター) ** \@**|  
  
     これらのパラメーターの詳細については、「[sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)」と「[sp_addmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql)」を参照してください。  
  
-   トランザクション レプリケーションおよびフィルター選択されていないマージ レプリケーションでは、複数のパブリケーションでのテーブルのパブリッシュを行ってから、サブスクリプション データベースの単一テーブル内でサブスクライブすることがサポートされています (一般にロール アップ シナリオと呼ばれています)。 ロール アップは、複数の場所からのデータを中央のサブスクライバーの単一テーブルに集計することを目的として使用されるのが一般的です。 フィルター選択されたマージ パブリケーションでは、中央のサブスクライバーを使用するシナリオはサポートされません。 マージ レプリケーションでは通常、パラメーター化された行フィルターを使用した単一のパブリケーションを介してロール アップが実装されます。 詳細については、「 [パラメーター化された行フィルター](../merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [既存のパブリケーションに対してアーティクルを追加または削除する](add-articles-to-and-drop-articles-from-existing-publications.md)   
 [ディストリビューションの構成](../configure-distribution.md)   
 [サブスクリプションを初期化する](../initialize-a-subscription.md)   
 [レプリケーションのスクリプト作成](../scripting-replication.md)   
 [パブリッシャーのセキュリティ保護](../security/secure-the-publisher.md)   
 [パブリケーションをサブスクライブする](../subscribe-to-publications.md)  
  
  
