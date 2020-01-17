---
title: IHsyscolumns (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: a432685809676f997049940ea5aa1ce43dc38a60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029629"
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHsyscolumns**ビューから、SQL Server 以外のパブリッシャーのパブリッシュされたアーティクルの列情報を公開します。 このビューは、distributiondatabase に格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|列またはプロシージャ パラメーターの名前です。|  
|**id**|**int**|この列が所属するテーブルのオブジェクト ID、またはこのパラメーターが使用されているストアド プロシージャの ID です。|  
|**xtype**|**tinyint**|物理記憶型[sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)します。|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|拡張ユーザー定義データ型の ID。|  
|**length**|**bigint**|最大物理記憶長[sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)します。|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|列またはパラメーターの id。|  
|**xoffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|この列の既定の ID。|  
|**domain**|**int**|ルールまたはこの列の CHECK 制約の ID。|  
|**number**|**int**|プロシージャがグループ化すると、サブプロシージャ番号 (**0**以外のエントリの)。|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**int**|この列が表示される行へのオフセット。|  
|**collationid**|**int**|列の照合順序の ID。 ベースの列の文字以外の場合は NULL です。|  
|**language**|**int**|列の言語識別子です。|  
|**status**|**int**|列またはパラメーターのプロパティを説明するために使用するビットマップ。<br /><br /> **0x08** = 列は null 値を許容します。<br /><br /> **0x10** = ANSI による埋め込みがとき**varchar**または**varbinary**列が追加されました。 末尾の空白が保持されます**varchar**後続のゼロが保持される**varbinary**列。<br /><br /> **0x40** = パラメーターは出力パラメーターです。<br /><br /> **0x80** = 列は id 列です。|  
|**type**|**int**|物理記憶型[sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)します。|  
|**usertype**|**tinyint**|ユーザー定義データ型の ID [sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)します。|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|この列の有効桁数のレベル。|  
|**scale**|**int**|この列の小数点以下桁数です。|  
|**iscomputed**|**int**|列が計算列かどうかを示すフラグ。<br /><br /> **0** = 計算します。<br /><br /> **1** = 計算します。|  
|**isoutparam**|**int**|プロシージャのパラメーターが出力パラメーターであるかどうかを示します。<br /><br /> **1** = true。<br /><br /> **0** = false。|  
|**isnullable**|**int**|列が NULL 値を許容するかどうかを示します。<br /><br /> **1** = true。<br /><br /> **0** = false。|  
|**collation**|**int**|列の照合順序の名前。 ベースの列の文字以外の場合は NULL です。|  
|**tdscollation**|**int**|表形式のデータ ストリーム (TDS) で返された場合の列の照合順序の名前です。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
