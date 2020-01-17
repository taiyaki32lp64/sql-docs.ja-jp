---
title: パーティション テーブルとパーティション インデックスのレプリケート | Microsoft Docs
ms.custom: ''
ms.date: 09/10/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- partitioned indexes [SQL Server], replicating
- partitioned tables [SQL Server], replicating
- replication [SQL Server], partitioned tables
- publishing [SQL Server replication], partitioned tables
- transactional replication, partitioned tables
ms.assetid: c9fa81b1-6c81-4c11-927b-fab16301a8f5
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: b12d35d27fd4c90603cce6d798d8011ad1e65b81
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710830"
---
# <a name="replicate-partitioned-tables-and-indexes"></a>パーティション テーブルとパーティション インデックスのレプリケート
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  大きなテーブルやインデックスをパーティション分割すると、データのサブセットに対するアクセスや管理を迅速かつ効率的に行うと同時に、データ コレクションの整合性を維持することができるので、大きなテーブルやインデックスを管理しやすくなります。 詳細については、「 [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)」を参照してください。 レプリケーションでは、パーティション テーブルとパーティション インデックスを扱う方法を指定するプロパティ セットによって、パーティション分割をサポートします。  
  
## <a name="article-properties-for-transactional-and-merge-replication"></a>トランザクション レプリケーションおよびマージ レプリケーションのアーティクルのプロパティ  
 次の表に、データのパーティション分割に使用されるオブジェクトを示します。  
  
|Object|作成に使用するステートメント|  
|------------|----------------------|  
|パーティション テーブルまたはパーティション インデックス|CREATE TABLE または CREATE INDEX|  
|パーティション関数|CREATE PARTITION FUNCTION|  
|パーティション構成|CREATE PARTITION SCHEME|  
  
 パーティション分割に関連するプロパティの最初のセットは、パーティション分割するオブジェクトをサブスクライバーにコピーするかどうかを指定するアーティクルのスキーマ オプションです。 これらのスキーマ オプションは次の方法で設定できます。  
  
-   パブリケーションの新規作成ウィザードの **[アーティクルのプロパティ]** ページ、または [パブリケーションのプロパティ] ダイアログ ボックス。 上記の表に示したオブジェクトをコピーするには、 **[テーブル分割構成のコピー]** プロパティと **[インデックス分割構成のコピー]** プロパティに、値 **true**を指定します。 **[アーティクルのプロパティ]** ページへのアクセス方法については、「[View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
-   次のいずれかのストアド プロシージャの *schema_option* パラメーターの使用。  
  
    -   トランザクション レプリケーションの[sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) または [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) fまたは transactional replication  
  
    -   マージ レプリケーションの[sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) または [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) fまたは merge replication  
  
     上記の表に示したオブジェクトをコピーするには、適切なスキーマ オプション値を指定します。 スキーマ オプションを指定する方法については、「 [Specify Schema Options](../../../relational-databases/replication/publish/specify-schema-options.md)」を参照してください。  
  
 レプリケーションでは、初期同期中にオブジェクトがサブスクライバーにコピーされます。 パーティション構成で PRIMARY 以外のファイル グループを使用する場合、そのファイル グループは初期同期の前にサブスクライバーに存在している必要があります。  
  
 サブスクライバーが初期化された後、データ変更がサブスクライバーに反映され、適切なパーティションに適用されます。 ただし、パーティション構成に対する変更はサポートされていません。 トランザクション レプリケーションとマージ レプリケーションでは、次のコマンドのレプリケーションはサポートされていません。ALTER PARTITION FUNCTION、ALTER PARTITION SCHEME、または ALTER INDEX の REBUILD WITH PARTITION ステートメント。 これらに関連付けられた変更は、サブスクライバーに自動的にレプリケートされません。 ユーザーがサブスクライバー側で同様の変更を手動で行う必要があります。  
  
## <a name="replication-support-for-partition-switching"></a>レプリケーションによるパーティション切り替えのサポート  
 テーブル分割の主な利点の 1 つは、パーティション間でデータのサブセットをすばやく効率的に移動できることです。 データは SWITCH PARTITION コマンドを使用して移動します。 既定では、テーブルのレプリケーションが有効な場合、SWITCH PARTITION 操作は次の理由でブロックされます。  
  
-   パブリッシャーに存在するテーブルを移動元または移動先としてデータを移動する場合に、そのデータがサブスクライバーに存在しないと、パブリッシャーとサブスクライバーの間で不整合が発生します。 この問題は、一般に、ステージング テーブルにかかわるデータの移動で発生します。  
  
-   サブスクライバーにパブリッシャーとは異なるパーティション テーブルの定義がある場合、ディストリビューション エージェントが変更をサブスクライバーに適用しようとすると失敗します。  
  
 このような問題が発生する可能性はありますが、トランザクション レプリケーションでパーティション切り替えを有効にすることができます。 パーティション切り替えを有効にする前に、パーティション切り替えに関連するすべてのテーブルがパブリッシャーとサブスクライバーに存在し、テーブル定義およびパーティション定義が同じであることを確認してください。  
  
 パブリッシャーとサブスクライバーでパーティションにまったく同じパーティション構成が使用されている場合は、パブリッシャーへのパーティション切り替えステートメントのレプリケートのみを行う *allow_partition_switch* と共に、 *replication_partition_switch* を有効にすることができます。 DDL をレプリケートしないで、 *allow_partition_switch* を有効にすることもできます。 これは、過去の月をパーティションからロール アウトする一方、バックアップの目的で、レプリケートしたパーティションをサブスクライバーにもう 1 年保持する場合に便利です。  
  
 SQL Server 2008 R2 から現在のバージョンまででパーティション切り替えを有効にすると、近い将来、分割操作とマージ操作が必要になる可能性があります。 レプリケートされたテーブルでの分割またはマージ操作を実行する前に、該当するパーティションに保留中のレプリケートされたコマンドがないことを確認します。 分割操作とマージ操作中にパーティションで DML 操作が実行されないようにする必要もあります。 ログ リーダーが処理していないトランザクションがある場合や、分割操作またはマージ操作中に、レプリケートされたテーブルのパーティションで DML 操作が実行される場合 (同じパーティションに関連する場合)、ログ リーダー エージェントで処理エラーが発生する可能性があります。 このエラーを修正するには、サブスクリプションの再初期化が必要になる場合があります。  
  
> [!WARNING]  
>  ピア ツー ピア パブリケーションでは、非表示の列が競合の検出および解決のために使用されるため、パーティション切り替えを有効にしないでください。  
  
### <a name="enabling-partition-switching"></a>パーティション切り替えの有効化  
 トランザクション パブリケーションの次のプロパティを使用すると、レプリケーション環境でのパーティション切り替えの動作を制御できます。  
  
-   `@allow_partition_switch` を `true` に設定すると、パブリケーション データベースに対して SWITCH PARTITION を実行できます。  
  
-   `@replicate_partition_switch` では、SWITCH PARTITION DDL ステートメントをサブスクライバーにレプリケートするかどうかを決定します。 このオプションは、`@allow_partition_switch` が `true` に設定されている場合にのみ有効です。  
  
 これらのプロパティは、パブリケーションの作成時に [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) を使用するか、パブリケーションの作成後に [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) を使用することによって設定できます。 既に述べたとおり、マージ レプリケーションではパーティション切り替えがサポートされません。 マージ レプリケーションが有効になっているテーブルで SWITCH PARTITION を実行するには、パブリケーションからテーブルを削除します。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
