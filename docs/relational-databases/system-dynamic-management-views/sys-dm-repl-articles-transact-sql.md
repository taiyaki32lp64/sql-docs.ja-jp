---
title: sys.dm_repl_articles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_articles_TSQL
- dm_repl_articles
- dm_repl_articles_TSQL
- sys.dm_repl_articles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_articles dynamic management function
ms.assetid: 794d514e-bacd-432e-a8ec-3a063a97a37b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 07dc611371cbff373fb60036c8c16da6656a8de1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088591"
---
# <a name="sysdmreplarticles-transact-sql"></a>sys.dm_repl_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  レプリケーション トポロジ内のアーティクルとしてパブリッシュされたデータベース オブジェクトに関する情報を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artcache_db_address**|**varbinary(8)**|パブリケーション データベースのキャッシュされたデータベース構造のメモリ内アドレス。|  
|**artcache_table_address**|**varbinary(8)**|パブリッシュされたテーブル アーティクルのキャッシュされたテーブルの構造体のメモリ内アドレス。|  
|**artcache_schema_address**|**varbinary(8)**|パブリッシュされたテーブル アーティクルに関する、キャッシュされたアーティクル スキーマ構造のメモリ内アドレス。|  
|**artcache_article_address**|**varbinary(8)**|パブリッシュされたテーブル アーティクルに関する、キャッシュされたアーティクル構造のメモリ内アドレス。|  
|**artid**|**bigint**|このテーブル内の各エントリを一意に識別します。|  
|**artfilter**|**bigint**|アーティクルを行方向へフィルター選択する場合に使用されるストアド プロシージャの ID。|  
|**artobjid**|**bigint**|パブリッシュされたオブジェクトの ID。|  
|**artpubid**|**bigint**|アーティクルが属しているパブリケーションの ID。|  
|**artstatus**|**tinyint**|ビットマスクのアーティクル オプションおよび状態で、これらの値の 1 つ以上のビットごとの論理和演算を指定できます。<br /><br /> **1** = アーティクルはアクティブです。<br /><br /> **8** = INSERT ステートメントに列名を含みます。<br /><br /> **16** = ステートメントをパラメーター化を使用します。<br /><br /> **24** = INSERT ステートメントに列名は、どちらも、パラメーター化されたステートメントを使用しています。<br /><br /> たとえば、パラメーター化されたステートメントを使用するアクティブなアーティクルの場合、この列の値は 17 になります。 値 0 は、アーティクルが非アクティブであり、追加のプロパティが定義されていないことを表します。|  
|**arttype**|**tinyint**|アーティクルの種類。<br /><br /> **1**ログベースのアーティクルを = です。<br /><br /> **3** = 手動フィルター付きログベースのアーティクルです。<br /><br /> **5** = 手動ビュー付きログベースのアーティクルです。<br /><br /> **7** = 手動フィルターおよび手動ビュー付きログベースのアーティクルです。<br /><br /> **8**ストアド プロシージャの実行を = です。<br /><br /> **24**シリアル化可能なストアド プロシージャの実行を = です。<br /><br /> **32** = ストアド プロシージャ (スキーマのみ)。<br /><br /> **64** = ビュー (スキーマのみ)。<br /><br /> **128** = 関数 (スキーマのみ)。|  
|**wszArtdesttable**|**nvarchar(514)**|転送先にパブリッシュされたオブジェクトの名前。|  
|**wszArtdesttableowner**|**nvarchar(514)**|パブリッシュ先での、パブリッシュされたオブジェクトの所有者。|  
|**wszArtinscmd**|**nvarchar(510)**|挿入に使用されるコマンドまたはストアド プロシージャ。|  
|**cmdTypeIns**|**int**|Insert ストアド プロシージャの呼び出し構文と、これらの値のいずれかを指定できます。<br /><br /> **1**呼び出しを =<br /><br /> **2** = SQL<br /><br /> **3** = なし<br /><br /> **7** = UNKNOWN|  
|**wszArtdelcmd**|**nvarchar(510)**|削除に使用されるコマンドまたはストアド プロシージャ。|  
|**cmdTypeDel**|**int**|Delete ストアド プロシージャの呼び出し構文と、これらの値のいずれかを指定できます。<br /><br /> **0** XCALL を =<br /><br /> **1**呼び出しを =<br /><br /> **2** = SQL<br /><br /> **3** = なし<br /><br /> **7** = UNKNOWN|  
|**wszArtupdcmd**|**nvarchar(510)**|更新に使用されるコマンドまたはストアド プロシージャ。|  
|**cmdTypeUpd**|**int**|更新プログラムの呼び出し構文は、ストアド プロシージャ、およびこれらの値のいずれかを指定できます。<br /><br /> **0** XCALL を =<br /><br /> **1**呼び出しを =<br /><br /> **2** = SQL<br /><br /> **3** = なし<br /><br /> **4** MCALL を =<br /><br /> **5** VCALL を =<br /><br /> **6** SCALL を =<br /><br /> **7** = UNKNOWN|  
|**wszArtpartialupdcmd**|**nvarchar(510)**|コマンドまたはストアド プロシージャの部分的な更新のために使用します。|  
|**cmdTypePartialUpd**|**int**|部分更新ストアド プロシージャの呼び出し構文。次のいずれかになります。<br /><br /> **2** = SQL|  
|**numcol**|**int**|垂直方向にフィルター選択されたアーティクルのパーティション内の列の数。|  
|**artcmdtype**|**tinyint**|現在レプリケートされているコマンドの種類。次のいずれかになります。<br /><br /> **1** = 挿入<br /><br /> **2** = DELETE<br /><br /> **3** = UPDATE<br /><br /> **4** = UPDATETEXT<br /><br /> **5** = なし<br /><br /> **6** = 内部使用のみ<br /><br /> **7** = 内部使用のみ<br /><br /> **8** = 部分的な更新|  
|**artgeninscmd**|**nvarchar(510)**|アーティクルに含まれる列に基づく INSERT コマンド テンプレート。|  
|**artgendelcmd**|**nvarchar(510)**|DELETE コマンド テンプレートは、プライマリ キーまたは呼び出し構文に応じて、アーティクルに含まれる列を含めることができますが使用されます。|  
|**artgenupdcmd**|**nvarchar(510)**|UPDATE コマンド テンプレートは、主キーを含めることができます、更新された列、または呼び出し構文によって完全な列リストが使用されます。|  
|**artpartialupdcmd**|**nvarchar(510)**|部分 UPDATE コマンド テンプレート。主キーと更新された列が含まれます。|  
|**artupdtxtcmd**|**nvarchar(510)**|UPDATETEXT コマンド テンプレートを含む主キー列を更新します。|  
|**artgenins2cmd**|**nvarchar(510)**|INSERT コマンド テンプレートが同時実行スナップショット処理中に、アーティクルを調整するときに使用します。|  
|**artgendel2cmd**|**nvarchar(510)**|同時実行スナップショット処理中に、アーティクルを調整するときに使用するコマンド テンプレートを削除します。|  
|**fInReconcile**|**tinyint**|同時実行スナップショット処理中にアーティクルが現在調整されているかどうかを示します。|  
|**fPubAllowUpdate**|**tinyint**|パブリケーションがサブスクリプションの更新を許可するかどうかを示します。|  
|**intPublicationOptions**|**bigint**|ビットごとのオプションの値が、追加のパブリッシング オプションを指定するビットマップ。<br /><br /> **0x1** - ピア ツー ピア レプリケーションに対して有効です。<br /><br /> **0x2** -ローカル変更のみをパブリッシュします。<br /><br /> **0x4**の SQL Server 以外のサブスクライバーに対応します。|  
  
## <a name="permissions"></a>アクセス許可  
 呼び出すパブリケーション データベースに対する VIEW DATABASE STATE 権限が必要**dm_repl_articles**します。  
  
## <a name="remarks"></a>コメント  
 情報は、レプリケーション アーティクル キャッシュに現在読み込まれているレプリケートされたデータベース オブジェクトに対してのみ返されます。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [レプリケーション関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

