---
title: cdc. change_tables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.change_tables
- cdc.change_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.change_tables
ms.assetid: 3525a5f5-8d8b-46a8-b334-4b7cd9fb7c21
author: stevestein
ms.author: sstein
ms.openlocfilehash: 52f7a58c854d7081c13cfad606f71044361a02ab
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962447"
---
# <a name="cdcchange_tables-transact-sql"></a>cdc.change_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース内の変更テーブルごとに 1 行を返します。 変更テーブルは、ソース テーブルに対して変更データ キャプチャを有効にすると作成されます。 システムテーブルに対して直接クエリを実行しないことをお勧めします。 代わりに、 [sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)ストアドプロシージャを実行します。  

|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|変更テーブルの ID。 データベース内で一意です。|  
|**version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、この列は常に 0 を返します。|  
|**source_object_id**|**int**|変更データ キャプチャが有効になっているソース テーブルの ID です。|  
|**capture_instance**|**sysname**|インスタンス固有の追跡オブジェクトの名前を指定するために使用されるキャプチャインスタンスの名前。 既定では、ソーススキーマ名とソーステーブル名を*schemaname_sourcename*の形式で指定します。|  
|**start_lsn**|**binary(10)**|変更テーブル内の変更データを照会するときに、低いエンドポイントを表すログシーケンス番号 (LSN)。<br /><br /> NULL = 低いエンドポイントが確立されていません。|  
|**end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]の場合、この列は常に NULL を返します。|  
|**supports_net_changes**|**bit**|変更テーブルでは、差分変更のクエリのサポートが有効になっています。|  
|**has_drop_pending**|**bit**|キャプチャプロセスで、ソーステーブルが削除されたことを示す通知を受信しました。|  
|**role_name**|**sysname**|変更データへのアクセスをゲートするために使用されるデータベースロールの名前。<br /><br /> NULL = ロールは使用されません。|  
|**index_name**|**sysname**|ソーステーブル内の行を一意に識別するために使用されるインデックスの名前。 **index_name**は、ソーステーブルの主キーインデックスの名前、またはソーステーブルで変更データキャプチャを有効にしたときに指定された一意のインデックスの名前のいずれかになります。<br /><br /> NULL = 変更データキャプチャを有効にしたときに、ソーステーブルに主キーがありませんでした。変更データキャプチャが有効になっているときに、一意のインデックスが指定されていませんでした。<br /><br /> 注: 主キーが存在するテーブルで変更データキャプチャが有効になっている場合、変更データキャプチャ機能では、差分変更が有効になっているかどうかに関係なく、インデックスが使用されます。 変更データ キャプチャ機能を有効にした後は、主キーの変更ができません。 テーブルに主キーがない場合でも、変更データキャプチャを有効にすることはできますが、差分変更のみが false に設定されています。 変更データキャプチャを有効にすると、主キーを作成できるようになります。 変更データキャプチャでは主キーが使用されないため、主キーを変更することもできます。|  
|**filegroup_name**|**sysname**|変更テーブルが存在するファイルグループの名前。<br /><br /> NULL = 変更テーブルは、データベースの既定のファイルグループにあります。|  
|**create_date**|**datetime**|ソーステーブルが有効になった日付。|  
|**partition_switch**|**bit**|変更データキャプチャが有効になっているテーブルに対して**ALTER TABLE**の**SWITCH PARTITION**コマンドを実行できるかどうかを示します。 0は、パーティションの切り替えがブロックされていることを示します。 パーティション分割されていないテーブルは、常に1を返します。|  
  
## <a name="see-also"></a>参照  
 [sp_cdc_help_change_data_capture &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
