---
title: sys.dm_db_index_physical_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_physical_stats
- sys.dm_db_index_physical_stats_TSQL
- sys.dm_db_index_physical_stats
- dm_db_index_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_physical_stats dynamic management function
- fragmentation [SQL Server]
ms.assetid: d294dd8e-82d5-4628-aa2d-e57702230613
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d7fe788192aac7f7bd3e4723b615391c5d8c6e86
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811522"
---
# <a name="sysdm_db_index_physical_stats-transact-sql"></a>sys.dm_db_index_physical_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定されたテーブルまたはビューのデータとインデックスのサイズと断片化に関する情報を返します。 インデックスの場合、各パーティションの B ツリーのレベルごとに 1 行のデータが返されます。 ヒープの場合、各パーティションの IN_ROW_DATA アロケーション ユニットごとに 1 行のデータが返されます。 ラージオブジェクト (LOB) データの場合、各パーティションの LOB_DATA アロケーションユニットに対して1行が返されます。 テーブルに行オーバーフロー データが存在する場合、各パーティションの ROW_OVERFLOW_DATA アロケーション ユニットごとに 1 行のデータが返されます。 XVelocity メモリ最適化列ストアインデックスに関する情報は返されません。  
  
> [!IMPORTANT]
> [読み取り可能なセカンダリレプリカ](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)Always On をホストしているサーバーインスタンスで、このクエリを実行すると、再実行のブロックの問題が発生する可能性があります。 これは、この動的管理ビューが、指定したユーザー テーブルまたはビューで IS ロックを獲得することが原因です。IS ロックは、そのユーザー テーブルまたはビューの X ロックに関して REDO スレッドの要求をブロックする可能性があります。  
  
 **sys.dm_db_index_physical_stats**は、メモリ最適化インデックスに関する情報を返しません。 メモリ最適化インデックスの使用方法については、[sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md) を参照してください。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.dm_db_index_physical_stats (   
    { database_id | NULL | 0 | DEFAULT }  
  , { object_id | NULL | 0 | DEFAULT }  
  , { index_id | NULL | 0 | -1 | DEFAULT }  
  , { partition_number | NULL | 0 | DEFAULT }  
  , { mode | NULL | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>引数  
 *database_id* | NULL | 0 | DEFAULT  
 データベースの ID を示します。 *database_id*は**smallint**です。 有効な入力値は、データベースの ID 番号、NULL、0、または DEFAULT です。 既定値は 0 です。 このコンテキストでは、NULL、0、および DEFAULT は同じ値になります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのすべてのデータベースに関する情報を返すには NULL を指定します。 *Database_id*に null を指定する場合は、 *object_id*、 *index_id*、および*partition_number*にも null を指定する必要があります。  
  
 組み込み関数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)を指定できます。 データベース名を指定しないで DB_ID を使用する場合、現在のデータベースの互換性レベルが 90 以上である必要があります。  
  
 *object_id* | NULL | 0 | DEFAULT  
 インデックスがあるテーブルまたはビューのオブジェクト ID を示します。 *object_ID* は **int**です。  
  
 有効な入力値は、テーブルおよびビューの ID 番号、NULL、0、または DEFAULT です。 既定値は 0 です。 このコンテキストでは、NULL、0、および DEFAULT は同じ値になります。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]以降、有効な入力には、service broker のキュー名またはキューの内部テーブル名も含まれます。 既定のパラメーター (つまり、すべてのオブジェクト、すべてのインデックスなど) が適用されると、すべてのキューの断片化情報が結果セットに含まれます。  
  
 NULL を指定すると、指定されたデータベース内にあるすべてのテーブルとビューに関する情報が返されます。 *Object_id*に null を指定する場合は、 *index_id*と*partition_number*にも null を指定する必要があります。  
  
 *index_id* | 0 | NULL | -1 | DEFAULT  
 インデックスの ID です。 *index_id*は**int**です。有効な入力値は、インデックスの ID 番号です。 *object_id*がヒープ、NULL、-1、または DEFAULT の場合は0です。 既定値は-1 です。 このコンテキストでは、NULL、-1、および DEFAULT は同じ値です。  
  
 NULL を指定すると、ベーステーブルまたはビューのすべてのインデックスに関する情報が返されます。 *Index_id*に null を指定する場合は、 *PARTITION_NUMBER*にも null を指定する必要があります。  
  
 *partition_number* | NULL | 0 | DEFAULT  
 オブジェクトのパーティション番号です。 *partition_number*は**int**です。有効な入力値は、インデックスまたはヒープの*partion_number* 、NULL、0、または DEFAULT です。 既定値は 0 です。 このコンテキストでは、NULL、0、および DEFAULT は同じ値になります。  
  
 NULL を指定すると、所有するオブジェクトのすべてのパーティションに関する情報が返されます。  
  
 *partition_number*は1から始まるです。 非パーティションインデックスまたはヒープの*partition_number*が1に設定されています。  
  
 *mode* | NULL | DEFAULT  
 モードの名前を指定します。 *モード*統計を取得するために使用するスキャンレベルを指定します。 *モード*は**sysname**です。 有効な入力値は DEFAULT、NULL、LIMITED、SAMPLED、DETAILED です。 既定値 (NULL) は制限されています。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|テーブルまたはビューのデータベース ID。|  
|object_id|**int**|インデックスがあるテーブルまたはビューのオブジェクト ID。|  
|index_id|**int**|インデックスのインデックス ID。<br /><br /> 0 = ヒープ。|  
|partition_number|**int**|所有しているオブジェクト内の1から始まるパーティション番号。テーブル、ビュー、またはインデックスです。<br /><br /> 1 = パーティション分割されていないインデックスまたはヒープ。|  
|index_type_desc|**nvarchar(60)**|インデックスの種類の説明。<br /><br /> HEAP<br /><br /> クラスター化インデックス<br /><br /> NONCLUSTERED INDEX<br /><br /> プライマリ XML インデックス<br /><br /> EXTENDED INDEX<br /><br /> XML INDEX<br /><br /> 列ストアマッピングインデックス (内部)<br /><br /> 列ストア DELETEBUFFER インデックス (内部)<br /><br /> 列ストア DELETEBITMAP インデックス (内部)|  
|hobt_id|**bigint**|インデックスまたはパーティションのヒープまたは B-tree ID。<br /><br /> これは、ユーザー定義のインデックスの hobt_id を返すだけでなく、内部列ストアインデックスの hobt_id も返します。|  
|alloc_unit_type_desc|**nvarchar(60)**|アロケーション ユニットの種類の説明。<br /><br /> IN_ROW_DATA<br /><br /> LOB_DATA<br /><br /> ROW_OVERFLOW_DATA<br /><br /> LOB_DATA アロケーションユニットには、 **text**、 **ntext**、 **image**、 **varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、および**xml**型の列に格納されているデータが含まれています。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。<br /><br /> ROW_OVERFLOW_DATA アロケーションユニットには、行外に移動された**varchar (n)** 、 **nvarchar (n)** 、 **varbinary (n)** 、および**sql_variant**型の列に格納されているデータが含まれています。|  
|index_depth|**tinyint**|インデックス レベルの数です。<br /><br /> 1 = ヒープ、LOB_DATA アロケーションユニット、または ROW_OVERFLOW_DATA アロケーションユニット。|  
|index_level|**tinyint**|インデックスの現在のレベル。<br /><br /> インデックスのリーフレベル、ヒープ、LOB_DATA または ROW_OVERFLOW_DATA アロケーションユニットの場合は0。<br /><br /> 非リーフインデックスレベルの場合は0より大きい。 *index_level*は、インデックスのルートレベルで最大になります。<br /><br /> インデックスの非リーフレベルは、 *mode* = DETAILED の場合にのみ処理されます。|  
|avg_fragmentation_in_percent|**float**|インデックスの論理的な断片化、または IN_ROW_DATA アロケーション ユニットでのヒープのエクステントの断片化。<br /><br /> 値はパーセンテージとして測定され、複数のファイルを考慮に入れます。 論理的な断片化とエクステントの断片化の定義については、「解説」を参照してください。<br /><br /> LOB_DATA と ROW_OVERFLOW_DATA アロケーションユニットの場合は0です。<br /><br /> *Mode* = サンプリングされた場合のヒープの場合は NULL です。|  
|fragment_count|**bigint**|IN_ROW_DATA アロケーションユニットのリーフレベルのフラグメントの数。 フラグメントの詳細については、「解説」を参照してください。<br /><br /> インデックスの非リーフ レベル、および LOB_DATA または ROW_OVERFLOW_DATA アロケーション ユニットでは NULL になります。<br /><br /> *Mode* = サンプリングされた場合のヒープの場合は NULL です。|  
|avg_fragment_size_in_pages|**float**|IN_ROW_DATA アロケーション ユニットのリーフ レベルにおける、フラグメントあたりのページの平均数。<br /><br /> インデックスの非リーフ レベル、および LOB_DATA または ROW_OVERFLOW_DATA アロケーション ユニットでは NULL になります。<br /><br /> *Mode* = サンプリングされた場合のヒープの場合は NULL です。|  
|page_count|**bigint**|インデックスまたはデータページの合計数。<br /><br /> インデックスの場合、IN_ROW_DATA アロケーションユニットにおける b-tree の現在のレベルにおけるインデックスページの合計数。<br /><br /> ヒープの場合は、IN_ROW_DATA アロケーションユニット内のデータページの合計数。<br /><br /> LOB_DATA または ROW_OVERFLOW_DATA アロケーションユニットの場合、アロケーションユニット内のページの合計数。|  
|avg_page_space_used_in_percent|**float**|すべてのページで使用可能なデータストレージ領域の平均割合。<br /><br /> インデックスの場合、平均は、IN_ROW_DATA アロケーションユニットの b-tree の現在のレベルに適用されます。<br /><br /> ヒープでは、IN_ROW_DATA アロケーション ユニットに含まれるすべてのデータ ページの平均になります。<br /><br /> LOB_DATA または ROW_OVERFLOW のデータアロケーションユニットの場合、アロケーションユニット内のすべてのページの平均です。<br /><br /> *Mode* = が制限されている場合は NULL です。|  
|record_count|**bigint**|レコードの合計数。<br /><br /> インデックスの場合、レコードの合計数は、IN_ROW_DATA アロケーションユニットの b ツリーの現在のレベルに適用されます。<br /><br /> ヒープの場合は、IN_ROW_DATA アロケーションユニット内のレコードの合計数。<br /><br /> **注:** ヒープの場合、この関数から返されるレコードの数が、ヒープに対して SELECT COUNT (\*) を実行することによって返される行数と一致しない可能性があります。 これは、1 行に複数のレコードが含まれる場合があるためです。 たとえば、更新の状況によっては、更新操作の結果として転送元レコードと転送先レコードが 1 つのヒープ行に含まれることがあります。 また、大きな LOB 行のほとんどは、LOB_DATA ストレージ内で複数のレコードに分割されます。<br /><br /> LOB_DATA または ROW_OVERFLOW_DATA アロケーション ユニットでは、アロケーション ユニット全体でのレコードの合計数になります。<br /><br /> *Mode* = が制限されている場合は NULL です。|  
|ghost_record_count|**bigint**|アロケーション ユニットで、非実体クリーンアップ タスクによる削除の準備ができているゴースト レコードの数。<br /><br /> IN_ROW_DATA アロケーションユニット内のインデックスの非リーフレベルの場合は0です。<br /><br /> *Mode* = が制限されている場合は NULL です。|  
|version_ghost_record_count|**bigint**|アロケーションユニット内の未処理のスナップショット分離トランザクションによって保持されているゴーストレコードの数。<br /><br /> IN_ROW_DATA アロケーションユニット内のインデックスの非リーフレベルの場合は0です。<br /><br /> *Mode* = が制限されている場合は NULL です。|  
|min_record_size_in_bytes|**int**|最小レコードサイズ (バイト単位)。<br /><br /> インデックスの場合、最小レコードサイズは、IN_ROW_DATA アロケーションユニットの b ツリーの現在のレベルに適用されます。<br /><br /> ヒープでは、IN_ROW_DATA アロケーション ユニットに含まれる最小レコード サイズになります。<br /><br /> LOB_DATA または ROW_OVERFLOW_DATA アロケーション ユニットでは、アロケーション ユニット全体での最小レコード サイズになります。<br /><br /> *Mode* = が制限されている場合は NULL です。|  
|max_record_size_in_bytes|**int**|最大レコードサイズ (バイト単位)。<br /><br /> インデックスでは、IN_ROW_DATA アロケーション ユニットに含まれる B ツリーの現在のレベルでの最大レコード サイズになります。<br /><br /> ヒープの場合は、IN_ROW_DATA アロケーションユニットの最大レコードサイズ。<br /><br /> LOB_DATA または ROW_OVERFLOW_DATA アロケーションユニットでは、アロケーションユニット全体の最大レコードサイズになります。<br /><br /> *Mode* = が制限されている場合は NULL です。|  
|avg_record_size_in_bytes|**float**|平均レコード サイズ (バイト単位)。<br /><br /> インデックスでは、IN_ROW_DATA アロケーション ユニットに含まれる B ツリーの現在のレベルでの平均レコード サイズになります。<br /><br /> ヒープの場合は、IN_ROW_DATA アロケーションユニットの平均レコードサイズ。<br /><br /> LOB_DATA または ROW_OVERFLOW_DATA アロケーションユニットでは、アロケーションユニット全体の平均レコードサイズになります。<br /><br /> *Mode* = が制限されている場合は NULL です。|  
|forwarded_record_count|**bigint**|別のデータの場所への転送ポインターを持つ、ヒープ内の転送されたレコード数 (この状態は、更新中に、新しい行を格納できる十分なスペースが元の場所にない場合に発生します)。<br /><br /> ヒープの IN_ROW_DATA アロケーション ユニット以外のアロケーション ユニットでは NULL になります。<br /><br /> *Mode*が制限されている場合のヒープの場合は NULL です。|  
|compressed_page_count|**bigint**|圧縮されたページの数。<br /><br /> ヒープの場合、新しく割り当てられたページはページ圧縮されません。 ヒープは、2 つの特殊な条件、つまりデータを一括インポートする場合、またはヒープを再構築する場合に、ページ圧縮されます。 ページ割り当ての原因となる一般的な DML 操作は、ページ圧縮されません。 compressed_page_count の値が目標のしきい値を超えた場合は、ヒープを再構築してください。<br /><br /> クラスター化インデックスを含むテーブルの場合、compressed_page_count の値はページ圧縮の効果を示します。|  
|hobt_id|BIGINT|**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [現在のバージョンまで](https://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 列ストアインデックスの場合にのみ、これはパーティションの内部列ストアデータを追跡する行セットの ID です。 行セットは、データヒープまたはバイナリツリーとして格納されます。 親列ストアインデックスと同じインデックス ID を持っています。 詳細については、「 [internal_partitions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)」を参照してください。<br /><br /> NULL の場合|  
|column_store_delete_buffer_state|TINYINT|**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [現在のバージョンまで](https://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = OPEN<br /><br /> 2 = ドレイン中<br /><br /> 3 = フラッシュ<br /><br /> 4 = インベントリからの削除<br /><br /> 5 = 準備完了|  
|column_store_delete_buff_state_desc||**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [現在のバージョンまで](https://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 無効-親インデックスが列ストアインデックスではありません。<br /><br /> OPEN-deleters とスキャナーはこれを使用します。<br /><br /> ドレイン中-deleters はドレインされますが、スキャナーでは引き続き使用されます。<br /><br /> フラッシュ-バッファーが閉じられ、バッファー内の行が削除ビットマップに書き込まれています。<br /><br /> 削除-閉じた削除バッファーの行が delete ビットマップに書き込まれましたが、スキャナーがまだ使用しているため、バッファーが切り捨てられていません。 開いているバッファーが十分であるため、新しいスキャナーでは、インベントリから削除するバッファーを使用する必要はありません。<br /><br /> READY-この削除バッファーは使用する準備ができています。|  
  
## <a name="remarks"></a>コメント  
 sys.dm_db_index_physical_stats 動的管理関数は、DBCC SHOWCONTIG ステートメントの代わりに使用できます。  
  
## <a name="scanning-modes"></a>スキャン モード  
 関数が実行されるモードによって、関数で使用する統計データを取得するためのスキャンのレベルが決まります。 *モード*は、制限、サンプリング、または詳細として指定されます。 関数は、テーブルまたはインデックスの指定されたパーティションを構成するアロケーションユニットのページチェーンを走査します。 実行されているモードに関係なく、インテント共有 (IS) テーブルロックのみが必要になります。 (_c)  
  
 LIMITED モードは最も高速なモードで、スキャンするページ数は最小です。 インデックスでは、B ツリーの親レベルのページ (リーフ レベルより上のページ) だけがスキャンされます。 ヒープでは、関連付けられた PFS ページおよび IAM ページが調べられます。LIMITED モードではヒープのデータ ページがスキャンされます。  
  
 LIMITED モードでは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]は B ツリーの非リーフ ページとヒープの IAM および PFS ページのみをスキャンするので、compressed_page_count は NULL です。 サンプリングモードを使用して compressed_page_count の推定値を取得し、詳細モードを使用して compressed_page_count の実際の値を取得します。 サンプリングモードでは、インデックスまたはヒープ内のすべてのページの 1% のサンプルに基づいて統計が返されます。 SAMPLED モードの結果は近似と見なす必要があります。 インデックスまたはヒープのページが1万未満の場合は、サンプリングされるのではなく詳細モードが使用されます。  
  
 DETAILED モードではすべてのページがスキャンされ、すべての統計が返されます。  
  
 各モードでは、より多くの作業が実行されるため、モードは徐々に [詳細] になります。 テーブルまたはインデックスの断片化レベルのサイズをすばやく計測するには、LIMITED モードを使用します。 これは最速であり、インデックスの IN_ROW_DATA アロケーションユニットに含まれる各非リーフレベルの行を返しません。  
  
## <a name="using-system-functions-to-specify-parameter-values"></a>システム関数によるパラメーター値の指定  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]関数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)および[object_id](../../t-sql/functions/object-id-transact-sql.md)を使用して、 *database_id*パラメーターと*object_id*パラメーターの値を指定できます。 ただし、これらの関数に無効な値を渡すと、意図しない結果が生じる可能性があります。 たとえば、データベース名またはオブジェクト名が存在しないか、スペルが間違っているために見つからない場合、両方の関数は NULL を返します。 sys.dm_db_index_physical_stats 関数では、NULL 値はすべてのデータベースまたはすべてのオブジェクトを指定するワイルドカード値として解釈されます。  
  
 また、OBJECT_ID 関数は、 *database_id*で指定されたデータベースではなく、現在のデータベースのコンテキストで評価される前に処理され、その結果、現在のデータベースのコンテキストで評価されます。 この動作により、OBJECT_ID 関数で NULL 値が返される場合があります。または、オブジェクト名が現在のデータベースのコンテキストと指定したデータベースの両方に存在する場合は、エラー メッセージが返されることがあります。 次の例は、こうした意図しない結果を示すものです。  
  
```  
USE master;  
GO  
-- In this example, OBJECT_ID is evaluated in the context of the master database.   
-- Because Person.Address does not exist in master, the function returns NULL.  
-- When NULL is specified as an object_id, all objects in the database are returned.  
-- The same results are returned when an object that is not valid is specified.  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'AdventureWorks'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- This example demonstrates the results of specifying a valid object name  
-- that exists in both the current database context and  
-- in the database specified in the database_id parameter of the   
-- sys.dm_db_index_physical_stats function.  
-- An error is returned because the ID value returned by OBJECT_ID does not  
-- match the ID value of the object in the specified database.  
CREATE DATABASE Test;  
GO  
USE Test;  
GO  
CREATE SCHEMA Person;  
GO  
CREATE Table Person.Address(c1 int);  
GO  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'Test'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- Clean up temporary database.  
DROP DATABASE Test;  
GO  
```  
  
### <a name="best-practice"></a>推奨事項  
 DB_ID または OBJECT_ID を使用する場合は、必ず有効な ID が返されるようにしてください。 たとえば、OBJECT_ID を使用する場合は、のような`OBJECT_ID(N'AdventureWorks2012.Person.Address')`3 部構成の名前を指定するか、関数によって返された値をテストしてから、それらを使用してください。 次の例 A と B は、データベース Id とオブジェクト Id を安全に指定する方法を示しています。  
  
## <a name="detecting-fragmentation"></a>断片化の検出  
 断片化は、テーブルとテーブルに定義されたインデックスに対して、INSERT、UPDATE、DELETE ステートメントによるデータ変更が行われる過程で発生します。 これらの変更は、テーブルとインデックスの行間で均等に分散されるとは限りません。そのため、各ページのゆとりは時間の経過と共に変化することがあります。 このような断片化があるときに、クエリでテーブルのインデックスの一部または全部をスキャンしようとすると、余分なページの読み取りが必要になり、 データの並列スキャンの妨げになります。  
  
 インデックスまたはヒープの断片化レベルは、avg_fragmentation_in_percent 列で確認できます。 ヒープの場合、値はヒープのエクステントの断片化を表します。 インデックスの場合、この値はインデックスの論理的な断片化を表します。 DBCC SHOWCONTIG とは異なり、どちらの場合の断片化計算アルゴリズムでも複数のファイルにまたがるストレージが考慮されるため、正確です。  
  
 **論理的な断片化**  
  
 これは、インデックスのリーフページでの順序のないページの割合です。 順序が不正なページとは、インデックスに割り当てられている次の物理的なページと、現在のリーフ ページの*次ページ* ポインターが示すページが異なるページのことです。  
  
 **エクステントの断片化**  
  
 これは、ヒープのリーフページでの順序が不足しているエクステントの割合です。 順序が無効なエクステントとは、ヒープの現在のページを含むエクステントの物理的な位置が、前のページを含むエクステントの直後でない状態のエクステントを指します。  
  
 最大のパフォーマンスを得るには、avg_fragmentation_in_percent の値をできるだけ 0 に近くする必要があります。 ただし、0 ~ 10% の値は許容される可能性があります。 再構築、再構成、再作成など、断片化を解消するためのさまざまな手段を使用することによって、この値を下げることができます。 インデックスの断片化の程度を分析する方法の詳細については、「[インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。  
  
## <a name="reducing-fragmentation-in-an-index"></a>インデックスの断片化の解消  
 断片化がクエリのパフォーマンスに影響するような方法でインデックスがフラグメント化されている場合、断片化を減らすには次の3つの選択肢があります。  
  
-   クラスター化インデックスを削除し、再作成する。  
  
     クラスター化インデックスを再作成すると、データが再分配され、データ ページにデータが満たされます。 ページのゆとりのレベルは、CREATE INDEX の FILLFACTOR オプションを使用して構成できます。 この方法の欠点は、削除と再作成のサイクル中にインデックスがオフラインになり、操作がアトミックであることです。 インデックスの作成が中断されると、インデックスは再作成されません。 詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」を参照してください。  
  
-   DBCC INDEXDEFRAG の代わりとして ALTER INDEX 再構成を使用して、インデックスのリーフレベルページを論理的な順序で並べ替えます。 これはオンライン操作なので、ステートメントの実行中にインデックスを使用できます。 操作を中断しても、それまでに完了した作業は失われません。 この方法の欠点は、インデックスの再構築操作としてデータを再編成するのは適切ではなく、統計を更新しないことです。  
  
-   DBCC DBREINDEX の代わりとして ALTER INDEX REBUILD を使用して、インデックスをオンラインまたはオフラインで再構築します。 詳細については、「[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)」を参照してください。  
  
 断片化だけでは、インデックスを再構成または再構築するための十分な理由ではありません。 断片化の主な効果は、インデックススキャン中にページの先行読み取りスループットが低下することです。 これは、応答時間の遅れの原因となります。 断片化したテーブルまたはインデックスでのクエリのワークロードにスキャンが関係していない場合、ワークロードは主に単一参照のため、断片化を解消しても効果はありません。
  
> [!NOTE]  
>  圧縮操作中にインデックスが部分的または完全に移動した場合、DBCC SHRINKFILE または DBCC SHRINKDATABASE を実行すると、断片化が発生する可能性があります。 このため、圧縮操作を実行する必要がある場合は、断片化が解除される前に実行する必要があります。  
  
## <a name="reducing-fragmentation-in-a-heap"></a>ヒープの断片化の解消  
 ヒープのエクステントの断片化を軽減するには、テーブルにクラスター化インデックスを作成してから、インデックスを削除します。 これによって、クラスター化インデックスの作成中にデータが再分配されます。 この操作では、データベースの空き領域の分布を考慮に入れて、可能な限り最適化も行われます。 その後、ヒープを再作成するためにクラスター化インデックスが削除されると、データは移動されず、最適な位置に維持されます。 これらの操作を実行する方法については、「 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) 」および「 [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)」を参照してください。  
  
> [!CAUTION]  
>  テーブルのクラスター化インデックスを作成および削除すると、そのテーブルのすべての非クラスター化インデックスが2回再構築されます。  
  
## <a name="compacting-large-object-data"></a>ラージ オブジェクト データの圧縮  
 既定では、ALTER INDEX 再構成ステートメントは、ラージオブジェクト (LOB) データを含むページを圧縮します。 LOB ページは空のときに割り当て解除されないので、LOB データの多くが削除された場合や LOB 列が削除された場合は、このデータを圧縮するとディスク領域の使用が向上します。  
  
 指定されたクラスター化インデックスを再構成すると、クラスター化インデックスに含まれるすべての LOB 列が圧縮されます。 非クラスター化インデックスを再構成すると、そのインデックス内で非キー列 (付加列) となっているすべての LOB 列が圧縮されます。 ステートメントで ALL を指定した場合は、指定したテーブルまたはビューに関連付けられているすべてのインデックスが再構成されます。 さらに、クラスター化インデックス、基になるテーブル、または付加列を含む非クラスター化インデックスに関連付けられているすべての LOB 列が圧縮されます。  
  
## <a name="evaluating-disk-space-use"></a>ディスク領域の使用量の評価  
 avg_page_space_used_in_percent 列には、ページのゆとりが示されます。 ディスク領域の使用を最適にするには、ランダムな挿入があまり行われないインデックスの場合はこの値を 100% に近づけます。 ただし、ランダムな挿入が多数あり、ページが非常に多いインデックスの場合、ページ分割の数が増加します。 断片化が大きくなります。 したがって、ページ分割を減らすために、値は 100% 未満にする必要があります。 FILLFACTOR オプションを指定してインデックスを再構築すると、ページのゆとりをインデックスのクエリ パターンに合わせて変更できます。 FILL FACTOR の詳細については、「[インデックスの Fill factor の指定](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)」を参照してください。 また、ALTER INDEX REORGANIZE は最後に指定された FILLFACTOR までページが埋まるよう、インデックスを圧縮します。 これにより、avg_space_used_in_percent の値は増加します。 ALTER INDEX REORGANIZE はページのゆとりを調整できないことに注意してください。 代わりに、インデックスの再構築を実行する必要があります。  
  
## <a name="evaluating-index-fragments"></a>インデックスのフラグメントの評価  
 フラグメントは、1つのアロケーションユニットについて、同じファイル内の物理的に連続するリーフページで構成されます。 1 つのインデックスには少なくとも 1 つのフラグメントが含まれます。 インデックスが持つことのできるフラグメントの最大数は、インデックスのリーフ レベルのページ数と同じです。 フラグメントが大きいほど、同じ数のページの読み取りに必要なディスクの I/O が少なくなります。 したがって、avg_fragment_size_in_pages 値が大きいほど、範囲スキャンのパフォーマンスは向上します。 avg_fragment_size_in_pages と avg_fragmentation_in_percent の値は、互いに反比例します。 そのため、インデックスの再構築または再構成を行うと、断片化の量が減り、フラグメントのサイズが大きくなります。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 では、クラスター化列ストアインデックスのデータは返されません。  
  
## <a name="permissions"></a>アクセス許可  
 次の権限が必要です。  
  
-   データベース内の指定されたオブジェクトに対する CONTROL 権限。  
  
-   オブジェクトのワイルドカード @*object_id*= NULL を使用して、指定したデータベース内のすべてのオブジェクトに関する情報を返す VIEW DATABASE STATE 権限。  
  
-   データベースのワイルドカード @*database_id* = NULL を使用して、すべてのデータベースに関する情報を返す VIEW SERVER STATE 権限。  
  
 VIEW DATABASE STATE 権限を許可すると、特定のオブジェクトに対して CONTROL 権限が拒否されていたとしても、データベース内のすべてのオブジェクトを取得することができます。  
  
 VIEW DATABASE STATE 権限を拒否すると、特定のオブジェクトに対する CONTROL 権限が許可されていたとしても、そのデータベース内のどのオブジェクトも取得できません。 また、データベースのワイルドカード @*database_id*= NULL が指定されている場合、データベースは省略されます。  
  
 詳細については、「[動的管理ビューと関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-information-about-a-specified-table"></a>A. 指定されたテーブルに関する情報を返す  
 次の例では、`Person.Address` テーブルのすべてのインデックスとパーティションについて、サイズと断片化の統計を返します。 最適なパフォーマンスを得るため`'LIMITED'` 、および返される統計を制限するために、スキャンモードがに設定されています。 このクエリを実行するには、少なくとも `Person.Address` テーブルに対する CONTROL 権限が必要です。  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
  
IF @db_id IS NULL  
BEGIN;  
    PRINT N'Invalid database';  
END;  
ELSE IF @object_id IS NULL  
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'LIMITED');  
END;  
GO  
  
```  
  
### <a name="b-returning-information-about-a-heap"></a>B. ヒープに関する情報を返す  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースのヒープ `dbo.DatabaseLog` に関するすべての統計を返します。 テーブルには LOB データが含まれているため、ヒープ`LOB_DATA`のデータページを格納して`IN_ROW_ALLOCATION_UNIT`いるに対して返される行に加えて、アロケーションユニットの行が返されます。 このクエリを実行するには、少なくとも `dbo.DatabaseLog` テーブルに対する CONTROL 権限が必要です。  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.DatabaseLog');  
IF @object_id IS NULL   
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, 0, NULL , 'DETAILED');  
END;  
GO  
  
```  
  
### <a name="c-returning-information-for-all-databases"></a>C. すべてのデータベースに関する情報を返す  
 次の例では、すべてのパラメーターに対してワイルドカード[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `NULL`を指定することによって、のインスタンス内のすべてのテーブルとインデックスに関するすべての統計を返します。 このクエリを実行するには、VIEW SERVER STATE 権限が必要です。  
  
```  
SELECT * FROM sys.dm_db_index_physical_stats (NULL, NULL, NULL, NULL, NULL);  
GO  
  
```  
  
### <a name="d-using-sysdm_db_index_physical_stats-in-a-script-to-rebuild-or-reorganize-indexes"></a>D. インデックスの再構築または再構成のためのスクリプトでの使用 (_d)  
 次の例では、平均断片化が 10% を超えるデータベース内のすべてのパーティションを自動的に再編成または再構築します。 このクエリを実行するには、VIEW DATABASE STATE 権限が必要です。 この例では、データベース名を指定せずに `DB_ID` を 1 番目のパラメーターとして指定しています。 現在のデータベースの互換性レベルが80以下の場合は、エラーが生成されます。 このエラーを解決するには、`DB_ID()` を有効なデータベース名で置き換えます。 データベース互換性レベルの詳細については、「 [ALTER DATABASE &#40;Transact-SQL&#41; 互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。  
  
```  
-- Ensure a USE <databasename> statement has been executed first.  
SET NOCOUNT ON;  
DECLARE @objectid int;  
DECLARE @indexid int;  
DECLARE @partitioncount bigint;  
DECLARE @schemaname nvarchar(130);   
DECLARE @objectname nvarchar(130);   
DECLARE @indexname nvarchar(130);   
DECLARE @partitionnum bigint;  
DECLARE @partitions bigint;  
DECLARE @frag float;  
DECLARE @command nvarchar(4000);   
-- Conditionally select tables and indexes from the sys.dm_db_index_physical_stats function   
-- and convert object and index IDs to names.  
SELECT  
    object_id AS objectid,  
    index_id AS indexid,  
    partition_number AS partitionnum,  
    avg_fragmentation_in_percent AS frag  
INTO #work_to_do  
FROM sys.dm_db_index_physical_stats (DB_ID(), NULL, NULL , NULL, 'LIMITED')  
WHERE avg_fragmentation_in_percent > 10.0 AND index_id > 0;  
  
-- Declare the cursor for the list of partitions to be processed.  
DECLARE partitions CURSOR FOR SELECT * FROM #work_to_do;  
  
-- Open the cursor.  
OPEN partitions;  
  
-- Loop through the partitions.  
WHILE (1=1)  
    BEGIN;  
        FETCH NEXT  
           FROM partitions  
           INTO @objectid, @indexid, @partitionnum, @frag;  
        IF @@FETCH_STATUS < 0 BREAK;  
        SELECT @objectname = QUOTENAME(o.name), @schemaname = QUOTENAME(s.name)  
        FROM sys.objects AS o  
        JOIN sys.schemas as s ON s.schema_id = o.schema_id  
        WHERE o.object_id = @objectid;  
        SELECT @indexname = QUOTENAME(name)  
        FROM sys.indexes  
        WHERE  object_id = @objectid AND index_id = @indexid;  
        SELECT @partitioncount = count (*)  
        FROM sys.partitions  
        WHERE object_id = @objectid AND index_id = @indexid;  
  
-- 30 is an arbitrary decision point at which to switch between reorganizing and rebuilding.  
        IF @frag < 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REORGANIZE';  
        IF @frag >= 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REBUILD';  
        IF @partitioncount > 1  
            SET @command = @command + N' PARTITION=' + CAST(@partitionnum AS nvarchar(10));  
        EXEC (@command);  
        PRINT N'Executed: ' + @command;  
    END;  
  
-- Close and deallocate the cursor.  
CLOSE partitions;  
DEALLOCATE partitions;  
  
-- Drop the temporary table.  
DROP TABLE #work_to_do;  
GO  
  
```  
  
### <a name="e-using-sysdm_db_index_physical_stats-to-show-the-number-of-page-compressed-pages"></a>E. sys.dm_db_index_physical_stats を使用して、ページ圧縮されたページの数を表示する  
 次の例では、行とページが圧縮されているページとの合計ページ数を表示および比較する方法を示します。 この情報を使用して、インデックスまたはテーブルに対して圧縮が提供する特典を判断できます。  
  
```  
SELECT o.name,  
    ips.partition_number,  
    ips.index_type_desc,  
    ips.record_count, ips.avg_record_size_in_bytes,  
    ips.min_record_size_in_bytes,  
    ips.max_record_size_in_bytes,  
    ips.page_count, ips.compressed_page_count  
FROM sys.dm_db_index_physical_stats ( DB_ID(), NULL, NULL, NULL, 'DETAILED') ips  
JOIN sys.objects o on o.object_id = ips.object_id  
ORDER BY record_count DESC;  
```  
  
### <a name="f-using-sysdm_db_index_physical_stats-in-sampled-mode"></a>F. SAMPLED モードで sys.dm_db_index_physical_stats を使用する  
 次の例は、サンプリングモードで、詳細モードの結果とは異なる概数を返す方法を示しています。  
  
```  
CREATE TABLE t3 (col1 int PRIMARY KEY, col2 varchar(500)) WITH(DATA_COMPRESSION = PAGE);  
GO  
BEGIN TRAN  
DECLARE @idx int = 0;  
WHILE @idx < 1000000  
BEGIN  
    INSERT INTO t3 (col1, col2)   
    VALUES (@idx,   
    REPLICATE ('a', 100) + CAST (@idx as varchar(10)) + REPLICATE ('a', 380))  
    SET @idx = @idx + 1  
END  
COMMIT;  
GO  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'SAMPLED');  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'DETAILED');  
```  
  
### <a name="g-querying-service-broker-queues-for-index-fragmentation"></a>G. インデックスの断片化のために service broker キューを照会しています  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
 次の例では、サーバーブローカーキューの断片化をクエリする方法を示します。  
  
```  
--Using queue internal table name   
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('sys.queue_messages_549576996'), default, default, default)   
  
--Using queue name directly  
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('ExpenseQueue'), default, default, default)  
  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [インデックス関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [SQL server の統計&#40;情報 (_d): transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [システムの&#40;transact-sql (_d) (_d)&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [システムビュー &#40;Transact-sql&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  

