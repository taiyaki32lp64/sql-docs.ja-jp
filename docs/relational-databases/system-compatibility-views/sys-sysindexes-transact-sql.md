---
title: sys.sysindexes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysindexes
- sysindexes_TSQL
- sys.sysindexes
- sys.sysindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysindexes system table
- sys.sysindexes compatibility view
ms.assetid: f483d89c-35c4-4a08-8f8b-737fd80d13f5
author: rothja
ms.author: jroth
ms.openlocfilehash: 560b5ab5d85c7f2a69fb5062a6eacc6e5c85ee1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053438"
---
# <a name="syssysindexes-transact-sql"></a>sys.sysindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  現在のデータベース内のインデックスとテーブルごとに 1 行のデータを格納します。 このビューでは、XML インデックスはサポートされていません。 パーティション テーブルとインデックスは完全にサポートされていません。 このビューで使用して、 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)カタログ ビューを代わりにします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|インデックスが属するテーブルの ID。|  
|**status**|**int**|システム状態情報。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**first**|**binary(6)**|最初のページまたはルート ページへのポインター。<br /><br /> 使用されていない場合に**indid** = 0。<br /><br /> NULL = インデックスがパーティション分割すると**indid** > 1。<br /><br /> NULL = テーブルはパーティション分割すると**indid**が 0 または 1。|  
|**indid**|**smallint**|インデックスの ID。<br /><br /> 0 = ヒープ<br /><br /> 1 = クラスター化インデックス<br /><br /> > 1 = 非クラスター化インデックス|  
|**root**|**binary(6)**|**Indid** > = 1、**ルート**ルート ページへのポインターです。<br /><br /> 使用されていない場合に**indid** = 0。<br /><br /> NULL = インデックスがパーティション分割すると**indid** > 1。<br /><br /> NULL = テーブルはパーティション分割すると**indid**が 0 または 1。|  
|**minlen**|**smallint**|行の最小サイズ。|  
|**keycnt**|**smallint**|キーの数。|  
|**groupid**|**smallint**|オブジェクトが作成されたファイル グループ ID。<br /><br /> NULL = インデックスがパーティション分割すると**indid** > 1。<br /><br /> NULL = テーブルはパーティション分割すると**indid**が 0 または 1。|  
|**dpages**|**int**|**Indid** = 0 または**indid** = 1、 **dpages**は使用するデータ ページの数です。<br /><br /> **Indid** > 1、 **dpages**は使用されているインデックス ページの数です。<br /><br /> 0 = インデックスがパーティション分割すると**indid** > 1。<br /><br /> 0 = テーブルはパーティション分割すると**indid**が 0 または 1。<br /><br /> 行オーバーフローが発生した場合は、正確な結果を生成しません。|  
|**reserved**|**int**|**Indid** = 0 または**indid** = 1、**予約**は割り当てられているすべてのインデックスおよびテーブル データ ページの数です。<br /><br /> **Indid** > 1、**予約**はインデックスに割り当てられたページの数です。<br /><br /> 0 = インデックスがパーティション分割すると**indid** > 1。<br /><br /> 0 = テーブルはパーティション分割すると**indid**が 0 または 1。<br /><br /> 行オーバーフローが発生した場合は、正確な結果を生成しません。|  
|**used**|**int**|**Indid** = 0 または**indid** = 1、**使用**のすべてのインデックスとテーブル データに使用される合計ページ数です。<br /><br /> **Indid** > 1、**使用**はインデックスで使用されるページの数です。<br /><br /> 0 = インデックスがパーティション分割すると**indid** > 1。<br /><br /> 0 = テーブルはパーティション分割すると**indid**が 0 または 1。<br /><br /> 行オーバーフローが発生した場合は、正確な結果を生成しません。|  
|**rowcnt**|**bigint**|基づくデータ レベルの行数**indid** = 0 と**indid** = 1。<br /><br /> 0 = インデックスがパーティション分割すると**indid** > 1。<br /><br /> 0 = テーブルはパーティション分割すると**indid**が 0 または 1。|  
|**rowmodctr**|**int**|テーブルの統計情報が前回更新されてから挿入、削除、更新された行の総数。<br /><br /> 0 = インデックスがパーティション分割すると**indid** > 1。<br /><br /> 0 = テーブルはパーティション分割すると**indid**が 0 または 1。<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降では、 **rowmodctr**以前のバージョンと完全に互換性がありません。 詳細については、「解説」を参照してください。|  
|**reserved3**|**int**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved4**|**int**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xmaxlen**|**smallint**|行の最大サイズ|  
|**maxirow**|**smallint**|非リーフ インデックス行の最大サイズ。<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降では、 **maxirow**以前のバージョンと完全に互換性がありません。|  
|**OrigFillFactor**|**tinyint**|元の fill factor 値が、インデックスが作成されたときに使用します。 この値は保持されません。ただし、その役に立ちます使用された fill factor 値を覚えていないし、インデックスを再作成する必要がある場合。|  
|**StatVersion**|**tinyint**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved2**|**int**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**FirstIAM**|**binary(6)**|NULL = インデックスがパーティション分割します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**impid**|**smallint**|インデックス実装フラグ。<br /><br /> 0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**lockflags**|**smallint**|インデックスのロックの粒度を制限するために使用します。 たとえば、ロック コストを最小限にするには、基本的に読み取り専用の参照テーブルで、テーブル レベルのロックだけを行うように設定します。|  
|**pgmodctr**|**int**|0 を返します。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**keys**|**varbinary(816)**|インデックス キーを構成する列の列 ID の一覧。<br /><br /> NULL を返します。<br /><br /> インデックス キー列を表示する使用[sys.sysindexkeys](../../relational-databases/system-compatibility-views/sys-sysindexkeys-transact-sql.md)します。|  
|**name**|**sysname**|インデックスまたは統計の名前。 ときに、NULL を返します**indid** = 0。 NULL ヒープ名を検索するアプリケーションを変更します。|  
|**statblob**|**image**|統計バイナリ ラージ オブジェクト (BLOB)。<br /><br /> NULL を返します。|  
|**maxlen**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**rows**|**int**|基づくデータ レベルの行数**indid** = 0 と**indid** = 1、値は繰り返されます**indid** > 1。|  
  
## <a name="remarks"></a>コメント  
 予約済みとして定義された列を使用しない必要があります。  
  
 列**dpages**、**予約**、および**使用**場合は、テーブルまたはインデックスが ROW_OVERFLOW アロケーション ユニット内のデータが含まれています。 正確な結果は返されません。 また、各インデックスのページ数は個別に追跡され、ベース テーブル用に集計されることはありません。 ページ数を表示する、 [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)または[sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)カタログ ビュー、または[sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)動的管理ビュー。  
  
 SQL Server 2000 以前では、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって行レベルの変更カウンターが管理されていました。 現在、こうしたカウンターは列レベルで管理されます。 そのため、 **rowmodctr**列が計算され、結果は、以前のバージョンでは、結果に似ていますが、正確ではありません。  
  
 値を使用する場合**rowmodctr**に統計を更新するタイミングを決定するには、次の解決策を検討してください。  
  
-   何もしない。 新しい**rowmodctr**値頻繁にする際に役立つため、動作は以前のバージョンの結果に統計を更新するタイミングを決定します。  
  
-   AUTO_UPDATE_STATISTICS を使用します。 詳細については、「[統計](../../relational-databases/statistics/statistics.md)します。  
  
-   統計を更新するのにタイミングを決定するのにには、制限時間を使用します。 たとえば、1 時間ごと、毎日または毎週に。  
  
-   統計を更新するのにタイミングを決定するのにには、アプリケーション レベルの情報を使用します。 たとえば、毎回の最大値、 **identity**列は、10,000 以上に変更またはたびに、一括挿入操作を実行します。  
  
## <a name="see-also"></a>関連項目  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
