---
title: sysmergepartitioninfo (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepartitioninfo_TSQL
- sysmergepartitioninfo
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfo system table
ms.assetid: 7429ad2c-dd33-4f7d-89cc-700e083af518
author: stevestein
ms.author: sstein
ms.openlocfilehash: c188cf1ad72033976136496914844c14c3a35867
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029830"
---
# <a name="sysmergepartitioninfo-transact-sql"></a>sysmergepartitioninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  各アーティクルのパーティションに情報を提供します。 ローカル データベースに定義されているマージ アーティクルごとに 1 行のデータを格納します。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**uniqueidentifier**|指定したアーティクルの一意な ID 番号です。|  
|**pubid**|**uniqueidentifier**|このパブリケーションの一意な識別番号パブリケーションが追加されたときに生成されます。|  
|**partition_view_id**|**int**|このテーブルに関するパーティション ビューの ID です。 記事の別のパーティション id に属している行ごとのマッピングを表示します。|  
|**repl_view_id**|**int**|追加されます。|  
|**partition_deleted_view_rule**|**nvarchar (4000)**|マージ レプリケーション トリガー内で、列の古い値に基づいて削除または更新された各行のパーティション ID を取得するために使用される SQL ステートメントです。|  
|**partition_inserted_view_rule**|**nvarchar (4000)**|マージ レプリケーション トリガー内で挿入または更新された各行のパーティション ID を取得するために使用する SQL ステートメントは、新しい列の値に基づいています。|  
|**membership_eval_proc_name**|**sysname**|内の行の現在のパーティション Id を評価するプロシージャの名前**MSmerge_contents**します。|  
|**column_list**|**nvarchar (4000)**|アーティクル内でレプリケートされた列のコンマ区切り一覧。|  
|**column_list_blob**|**nvarchar (4000)**|Binary Large Object の列を含む、アーティクル内でレプリケートされた列のコンマ区切りの一覧です。|  
|**expand_proc**|**sysname**|パーティションを新たに挿入された親行のすべての子行とすると、パーティションの変更が発生したかが削除された親行の Id を再評価するプロシージャの名前。|  
|**logical_record_parent_nickname**|**int**|論理レコード内の、指定されたアーティクルのトップレベルにある親のニックネームです。|  
|**logical_record_view**|**int**|それぞれの子の rowguid に対応する、トップレベルにある親アーティクルの rowguid を出力するビューです。|  
|**logical_record_deleted_view_rule**|**nvarchar (4000)**|ような**logical_record_view**を除き、it の"deleted"テーブル内の子行の update および delete トリガーを示しています。|  
|**logical_record_level_conflict_detection**|**bit**|競合を、論理レコード レベルと、行または列レベルのどちらで検出するかを示します。<br /><br /> **0** = 行レベルまたは列レベルの競合検出を使用します。<br /><br /> **1** = 論理レコードの競合検出を使用すると、パブリッシャーでの行の変更と、別の変更の同じ論理行レコードはサブスクライバー側では、競合として処理します。<br /><br /> この値が**1**、論理レコード レベルの競合解決だけを使用できます。|  
|**logical_record_level_conflict_resolution**|**bit**|競合を、論理レコード レベルと、行または列レベルのどちらで解決するかを示します。<br /><br /> **0** = 行レベルまたは列レベルの解決が使用されます。<br /><br /> **1** = 場合に、競合を優先されなかった論理レコード全体に優先されなかった論理レコード全体が上書きされます。<br /><br /> 値**1**両方論理レコード レベルの検出と、行または列レベルの検出に使用することができます。|  
|**partition_options**|**tinyint**|アーティクル内のデータをパーティション分割する方法を定義します。パーティション分割することにより、すべての行が 1 つのパーティションまたは 1 つのサブスクリプションに属している場合に、パフォーマンスを最適化できます。 *partition_options*値は次のいずれかを指定できます。<br /><br /> **0** =、フィルタ リング、情報の記事が静的か、つまり「重複する」パーティションまたは各パーティションのデータの一意なサブセットは生成されません。<br /><br /> **1** = パーティションが重複していると、サブスクライバーで実行された DML 更新は、行が属するパーティションを変更できません。<br /><br /> **2**記事、重複しないパーティションが得られますが、複数のサブスクライバーが同じパーティションを受け取ることができます = フィルター選択します。<br /><br /> **3** =、フィルタ リング、情報の記事には、サブスクリプションごとに固有の重複しないパーティションが得られます。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
