---
title: IHarticles (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHarticles
- IHarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHarticles system table
ms.assetid: 773ef9b7-c993-4629-9516-70c47b9dcf65
author: stevestein
ms.author: sstein
ms.openlocfilehash: 45278a6d9501b75b624e11bbeb11d24d10e482c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056213"
---
# <a name="iharticles-transact-sql"></a>IHarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHarticles**システム テーブルにはから、SQL Server 以外のパブリッシャー、現在のディストリビューターを使用してがレプリケートされるアーティクルごとに 1 行が含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|アーティクルの一意な ID 番号を示す ID 列です。|  
|**name**|**sysname**|パブリケーションの中で一意なアーティクルに関係する名前です。|  
|**publication_id**|**smallint**|そのアーティクルが属するパブリケーションの ID です。|  
|**table_id**|**int**|パブリッシュされるテーブルの ID [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)します。|  
|**publisher_id**|**smallint**|非 SQL Server パブリッシャーの ID。|  
|**creation_script**|**nvarchar (255)**|アーティクルのスキーマ スクリプトです。|  
|**del_cmd**|**nvarchar (255)**|テーブル アーティクルの削除をレプリケートするときに使用されるレプリケーション コマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**filter**|**int**|このコラムでは使用されませんしするためだけに含まれている、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)の表示、 **IHarticles**と互換性のあるテーブル、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server の記事 (使用するビュー[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**filter_clause**|**ntext**|水平方向のフィルター処理に使用し、標準的な TRANSACT-SQL SQL 以外のパブリッシャーで解釈できるで記述された、アーティクルの WHERE 句です。|  
|**ins_cmd**|**nvarchar (255)**|テーブル アーティクルの挿入をレプリケートするときに使用するレプリケーション コマンドの種類。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**pre_creation_cmd**|**tinyint**|同じ名前のオブジェクトがサブスクライバーに既に存在する場合に、初期スナップショットが適用される前に実行するコマンドです。<br /><br /> **0** = なし - コマンドは実行されません。<br /><br /> **1** = DROP - 変換先テーブルを削除します。<br /><br /> **2** = 削除 - 変換先テーブルからデータを削除します。<br /><br /> **3** = 切り捨て - 変換先テーブルを切り捨てます。|  
|**status**|**tinyint**|アーティクル オプションとステータスのビットマスクです。次に示す 1 つ以上の値のビットごとの論理和演算をとります。<br /><br /> **0** = その他のプロパティはありません。<br /><br /> **1** = アクティブ。<br /><br /> **8** = INSERT ステートメントに列名を含みます。<br /><br /> **16** = ステートメントをパラメーター化を使用します。<br /><br /> たとえば、パラメーター化されたステートメントを使用するアクティブなアーティクルの場合、この列の値は 17 になります。 値 0 は、アーティクルが非アクティブであり、追加のプロパティが定義されていないことを表します。|  
|**type**|**tinyint**|アーティクルのタイプです。<br /><br /> **1**ログベースのアーティクルを = です。|  
|**upd_cmd**|**nvarchar (255)**|テーブル アーティクルの更新プログラムをレプリケートするときに使用されるレプリケーション コマンドの種類。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**schema_option**|**binary(8)**|指定されたアーティクルに対するスキーマ生成オプションのビットマップです。次に示す 1 つ以上の値のビットごとの論理和演算をとります。<br /><br /> **0x00** = スナップショット エージェントによるスクリプト作成を無効にしては、指定されたいる creationscript を使用します。<br /><br /> **0x01** = オブジェクトの作成 (CREATE TABLE、CREATE PROCEDURE など) を生成します。<br /><br /> **0x10** = 対応するクラスター化インデックスを生成します。<br /><br /> **0x40**生成に対応する非クラスター化インデックスを = です。<br /><br /> **0x80** Include の主キーに関する宣言参照整合性を = です。<br /><br /> **0x1000** = 列レベルの照合順序をレプリケートします。 注:このオプションは、既定では大文字小文字を区別する比較を有効にする Oracle パブリッシャーに対して設定されます。<br /><br /> **0x4000** = テーブル アーティクルで定義されている場合、一意なキーをレプリケートします。<br /><br /> **0x8000** = ALTER TABLE ステートメントを使用して、制約として主キーと、テーブルの一意のキーの記事をレプリケートします。|  
|**dest_owner**|**sysname**|目的のデータベースにおけるテーブルの所有者です。|  
|**dest_table**|**sysname**|対象テーブルの名前です。|  
|**tablespace_name**|**nvarchar (255)**|アーティクルのログ テーブルによって使用されるテーブルスペースを識別します。|  
|**objid**|**int**|このコラムでは使用されませんしするためだけに含まれている、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)の表示、 **IHarticles**と互換性のあるテーブル、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server の記事 (使用するビュー[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**sync_objid**|**int**|このコラムでは使用されませんしするためだけに含まれている、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)の表示、 **IHarticles**と互換性のあるテーブル、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server の記事 (使用するビュー[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**description**|**nvarchar (255)**|この記事の説明エントリします。|  
|**publisher_status**|**int**|パブリッシュされたアーティクルを定義するビューを呼び出すことによって定義されているかどうかを示すために使用が[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)します。<br /><br /> **0** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)が呼び出されました。<br /><br /> **1** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)呼び出されていません。|  
|**article_view_owner**|**nvarchar (255)**|ログ リーダー エージェントによって使用されるパブリッシャー上の同期オブジェクトの所有者です。|  
|**article_view**|**nvarchar (255)**|ログ リーダー エージェントによって使用されるパブリッシャー上の同期オブジェクトです。|  
|**ins_scripting_proc**|**int**|このコラムでは使用されませんしするためだけに含まれている、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)の表示、 **IHarticles**と互換性のあるテーブル、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server の記事 (使用するビュー[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**del_scripting_proc**|**int**|このコラムでは使用されませんしするためだけに含まれている、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)の表示、 **IHarticles**と互換性のあるテーブル、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server の記事 (使用するビュー[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**upd_scripting_proc**|**int**|このコラムでは使用されませんしするためだけに含まれている、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)の表示、 **IHarticles**と互換性のあるテーブル、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server の記事 (使用するビュー[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**custom_script**|**int**|このコラムでは使用されませんしするためだけに含まれている、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)の表示、 **IHarticles**と互換性のあるテーブル、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server の記事 (使用するビュー[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**fire_triggers_on_snapshot**|**bit**|このコラムでは使用されませんしするためだけに含まれている、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)の表示、 **IHarticles**と互換性のあるテーブル、 [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) SQL Server の記事 (使用するビュー[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**instance_id**|**int**|パブリッシュされたテーブルに対するアーティクル ログの現在のインスタンスを識別します。|  
|**use_default_datatypes**|**bit**|アーティクルが既定のデータ型マッピングを使用するかどうかを示す値**1**既定のデータ型マッピングを使用することを示します。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)  
  
  
