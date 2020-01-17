---
title: sys.dm_repl_schemas (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_repl_schemas_TSQL
- dm_repl_schemas
- sys.dm_repl_schemas_TSQL
- sys.dm_repl_schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_schemas dynamic management function
ms.assetid: 6f5fefff-8492-4360-bd5b-a97287367914
author: stevestein
ms.author: sstein
ms.openlocfilehash: 152a8b7f4c933874d8190b95404cbbeb91bb098f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088581"
---
# <a name="sysdmreplschemas-transact-sql"></a>sys.dm_repl_schemas (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  レプリケーションでパブリッシュされたテーブル列に関する情報を返します。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artcache_schema_address**|**varbinary(8)**|パブリッシュされたテーブル アーティクルに関する、キャッシュされたスキーマ構造のメモリ内アドレス。|  
|**tabid**|**bigint**|レプリケートされたテーブルの ID。|  
|**indexid**|**smallint**|パブリッシュされたテーブルのクラスター化インデックスの ID。|  
|**idSch**|**bigint**|テーブル スキーマの ID。|  
|**tabschema**|**nvarchar(510)**|テーブル スキーマの名前です。|  
|**ccTabschema**|**smallint**|テーブル スキーマの文字長。|  
|**tabname**|**nvarchar(510)**|パブリッシュされたテーブルの名前。|  
|**ccTabname**|**smallint**|パブリッシュされたテーブル名の文字長。|  
|**rowsetid_delete**|**bigint**|削除された行の ID。|  
|**rowsetid_insert**|**bigint**|挿入された行の ID。|  
|**num_pk_cols**|**int**|主キー列の数。|  
|**pcitee**|**binary(8000)**|計算列を評価するために使用するクエリ式構造へのポインター。|  
|**re_numtextcols**|**int**|レプリケートされたテーブル内のバイナリ ラージ オブジェクト列の数。|  
|**re_schema_lsn_begin**|**binary(8000)**|スキーマ バージョンのログ記録に関する最初のログ シーケンス番号 (LSN)。|  
|**re_schema_lsn_end**|**binary(8000)**|スキーマのバージョン ログの LSN を終了します。|  
|**re_numcols**|**int**|パブリッシュされた列の数。|  
|**re_colid**|**int**|パブリッシャーの列識別子。|  
|**re_awcName**|**nvarchar(510)**|パブリッシュされた列の名前です。|  
|**re_ccName**|**smallint**|列名の文字数。|  
|**re_pk**|**tinyint**|パブリッシュされた列が主キーの一部がかどうか。|  
|**re_unique**|**tinyint**|かどうかパブリッシュされた列には、一意のインデックスの一部です。|  
|**re_maxlen**|**smallint**|パブリッシュされた列の最大長。|  
|**re_prec**|**tinyint**|パブリッシュされた列の有効桁数です。|  
|**re_scale**|**tinyint**|パブリッシュされた列の小数点以下桁数。|  
|**re_collatid**|**bigint**|パブリッシュされた列の照合順序 ID。|  
|**re_xvtype**|**smallint**|パブリッシュされた列の型。|  
|**re_offset**|**smallint**|パブリッシュされた列をオフセットします。|  
|**re_bitpos**|**tinyint**|バイト ベクターでパブリッシュされた列のビット位置。|  
|**re_fNullable**|**tinyint**|パブリッシュされた列が NULL 値をサポートしているかどうかを指定します。|  
|**re_fAnsiTrim**|**tinyint**|パブリッシュされた列で ANSI 切り捨てが使用されるかどうかを指定します。|  
|**re_computed**|**smallint**|パブリッシュされた列が計算列であるかどうかを指定します。|  
|**se_rowsetid**|**bigint**|行セットの ID。|  
|**se_schema_lsn_begin**|**binary(8000)**|スキーマ バージョンのログ記録に関する最初の LSN。|  
|**se_schema_lsn_end**|**binary(8000)**|スキーマのバージョン ログの LSN を終了します。|  
|**se_numcols**|**int**|列の数。|  
|**se_colid**|**int**|サブスクライバーでの列の ID。|  
|**se_maxlen**|**smallint**|列の最大長。|  
|**se_prec**|**tinyint**|列の有効桁数。|  
|**se_scale**|**tinyint**|列の小数点以下桁数。|  
|**se_collatid**|**bigint**|列の照合順序 ID。|  
|**se_xvtype**|**smallint**|列の型。|  
|**se_offset**|**smallint**|列のオフセット。|  
|**se_bitpos**|**tinyint**|バイトのベクトル内の列のビット位置。|  
|**se_fNullable**|**tinyint**|列が NULL 値をサポートしているかどうかを指定します。|  
|**se_fAnsiTrim**|**tinyint**|列で ANSI 切り捨てが使用されるかどうかを指定します。|  
|**se_computed**|**smallint**|指定するかどうか、列、計算列。|  
|**se_nullBitInLeafRows**|**int**|列の値が NULL であるかどうかを指定します。|  
  
## <a name="permissions"></a>アクセス許可  
 呼び出すパブリケーション データベースに対する VIEW DATABASE STATE 権限が必要**dm_repl_schemas**します。  
  
## <a name="remarks"></a>コメント  
 情報は、レプリケーション アーティクル キャッシュに現在読み込まれているレプリケートされたデータベース オブジェクトに対してのみ返されます。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [レプリケーション関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

