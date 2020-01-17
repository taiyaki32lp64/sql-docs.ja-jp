---
title: sysarticles (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticles
- sysarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticles system table
ms.assetid: 9d9d5d51-6d8f-4e42-84a9-82e58eb0301e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0e43c3350b546a13a95392b9e916a1d98ddddc7d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130489"
---
# <a name="sysarticles-transact-sql"></a>sysarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ローカル データベースで定義された各アーティクルに対して行が含まれています。 このテーブルは、パブリッシュされたデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|アーティクルの一意な ID 番号を示す ID 列です。|  
|**creation_script**|**nvarchar (255)**|アーティクルのスキーマ スクリプトです。|  
|**del_cmd**|**nvarchar (255)**|テーブル アーティクルの削除をレプリケートするときに使用されるレプリケーション コマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**description**|**nvarchar (255)**|この記事の説明エントリします。|  
|**dest_table**|**sysname**|対象テーブルの名前です。|  
|**filter**|**int**|ストアド プロシージャ ID は、水平的パーティション分割に使用します。|  
|**filter_clause**|**ntext**|フィルターによる行選択に使用する、アーティクルの WHERE 句です。|  
|**ins_cmd**|**nvarchar (255)**|テーブル アーティクルの挿入をレプリケートするときに使用するレプリケーション コマンドの種類。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**name**|**sysname**|パブリケーションの中で一意なアーティクルに関係する名前です。|  
|**objid**|**int**|パブリッシュするテーブル オブジェクト ID です。|  
|**pubid**|**int**|そのアーティクルが属するパブリケーションの ID です。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE、または TRUNCATE 事前作成コマンドです。<br /><br /> **0** = none。<br /><br /> **1** = ドロップします。<br /><br /> **2** = 削除します。<br /><br /> **3** = TRUNCATE です。|  
|**status**|**tinyint**|アーティクル オプションとステータスのビットマスクです。次に示す 1 つ以上の値のビットごとの論理和演算をとります。<br /><br /> **1** = アーティクルはアクティブです。<br /><br /> **8** = INSERT ステートメントに列名を含みます。<br /><br /> **16** = ステートメントをパラメーター化を使用します。<br /><br /> **24** = INSERT ステートメントに列名は、どちらも、パラメーター化されたステートメントを使用しています。<br /><br /> **64** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> たとえば、パラメーター化されたステートメントを使用するアクティブなアーティクルの値があります**17**この列にします。 値**0**アーティクルがアクティブでないと、追加のプロパティが定義されていないことを意味します。|  
|**sync_objid**|**int**|アーティクルの定義を表すテーブルまたはビューの ID です。|  
|**type**|**tinyint**|アーティクルのタイプです。<br /><br /> **1**ログベースのアーティクルを = です。<br /><br /> **3** = 手動フィルター付きログベースのアーティクルです。<br /><br /> **5** = 手動ビュー付きログベースのアーティクルです。<br /><br /> **7** = 手動フィルターおよび手動ビュー付きログベースのアーティクルです。<br /><br /> **8**ストアド プロシージャの実行を = です。<br /><br /> **24**シリアル化可能なストアド プロシージャの実行を = です。<br /><br /> **32** = ストアド プロシージャ (スキーマのみ)。<br /><br /> **64** = ビュー (スキーマのみ)。<br /><br /> **128** = 関数 (スキーマのみ)。|  
|**upd_cmd**|**nvarchar (255)**|テーブル アーティクルの更新プログラムをレプリケートするときに使用されるレプリケーション コマンドの種類。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**schema_option**|**binary(8)**|サブスクライバーに配信するため、アーティクルのスキーマの部分がスクリプト化を制御する、アーティクルのスキーマ生成オプションのビットマスク。 スキーマ オプションの詳細については、「[sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)」を参照してください。|  
|**dest_owner**|**sysname**|目的のデータベースにおけるテーブルの所有者です。|  
|**ins_scripting_proc**|**int**|登録したカスタム ストアド プロシージャまたはスクリプト、INSERT ステートメントがレプリケートされるときに実行されます。|  
|**del_scripting_proc**|**int**|登録したカスタム ストアド プロシージャまたは DELETE ステートメントがレプリケートされるときに実行されるスクリプト。|  
|**upd_scripting_proc**|**int**|UPDATE ステートメントがレプリケートされるときに実行される登録済みのカスタム ストアド プロシージャまたはスクリプトです。|  
|**custom_script**|**nvarchar(2048)**|DDL トリガーの最後に実行される登録済みのカスタム ストアド プロシージャまたはスクリプトです。|  
|**fire_triggers_on_snapshot**|**bit**|これらの値のいずれかを指定することができます、スナップショットが適用されるときにトリガーが実行されるレプリケートされたかどうかを示します。<br /><br /> **0** = トリガーは実行されません。<br /><br /> **1** = トリガーは実行されます。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)  
  
  
