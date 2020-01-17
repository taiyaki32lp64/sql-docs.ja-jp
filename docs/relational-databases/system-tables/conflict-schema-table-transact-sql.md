---
title: conflict_&lt;schema&gt;_&lt;table&gt;(Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/15/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- conflict_
- conflict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conflict_<schema>_<table>
ms.assetid: 15ddd536-db03-454e-b9b5-36efe1f756d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4725da28e9cd83df4979d1cc476cd60a488c0aa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084769"
---
# <a name="conflict_ltschemagt_lttablegt-transact-sql"></a>conflict _&lt;スキーマ&gt;_&lt;テーブル&gt;(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  conflict_\<schema>_\<table> テーブルには、ピア ツー ピア レプリケーションで競合する行に関する情報が含まれています。 競合テーブルはパブリケーション内のレプリケートされたテーブルごとに存在し、競合テーブルの名前にはスキーマとアーティクルの名前が付加されます。 このアーティクル固有の競合テーブルは、各パブリケーション データベースに保存されます。  
  
 ピア ツー ピア レプリケーションの場合、ディストリビューション エージェントは、競合を検出すると既定で停止します。 競合エラーはエラー ログに記録されますが、競合データは競合テーブルに記録されないため、競合データを表示できません。 ディストリビューション エージェントが実行の継続を許可されている場合は、競合が検出された各ノードで、競合がローカルでログに記録されます。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」の「競合の処理」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|__$originator_id|**int**|競合する変更が発生したノードの ID です。 Id の一覧は、実行[sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md)します。|  
|__$origin_datasource|**int**|競合する変更が発生したノードです。|  
|__$tranid|**nvarchar (40)**|__$origin_datasource で適用されたときの競合する変更のログ シーケンス番号 (LSN) です。|  
|__$conflict_type|**int**|競合の種類。次の値のいずれかです。<br /><br /> 1:ローカル行が別の更新プログラムまたはことによって変更されたために失敗しました。 更新プログラムが削除され、後に再挿入します。<br /><br /> 2:ローカル行が既に削除されて、更新に失敗しました。<br /><br /> 3:ローカル行が別の更新プログラムまたはことによって変更されたために失敗しました。 削除が削除され、後に再挿入します。<br /><br /> 4:ローカル行が既に削除されたために、削除が失敗しました。<br /><br /> 5:ローカル行が既に挿入されているかが、挿入し、更新、挿入が失敗しました。|  
|__$is_winner|**bit**|このテーブルの行が競合で優先されるかどうか (ローカル ノードに適用されるかどうか) を示します。|  
|__$pre_version|**varbinary (32)**|競合する変更が発生したデータベースのバージョンです。|  
|__$reason_code|**int**|競合の解決コード。 次のいずれかの値になります。<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> <br /><br /> 詳細については、次を参照してください。 **__$reason_text**します。|  
|__$reason_text|**nvarchar (720)**|競合の解決。 次のいずれかの値になります。<br /><br /> 解決 (1)<br /><br /> 未解決 (2)<br /><br /> 不明 (0)|  
|__$update_bitmap|**varbinary (** *n* **)** します。 サイズはコンテンツにより異なります。|更新 - 更新の競合が発生した場合にどの列が更新されたかを示すビットマップです。|  
|__$inserted_date|**datetime**|競合する行がこのテーブルに挿入された日時です。|  
|__$row_id|**timestamp**|競合の原因となった行に関連付けられている行バージョンです。|  
|__$change_id|**binary (8)**|ローカル行の場合、この値はローカル行と競合している挿入行の __$row_id に等しくなります。 挿入行の場合、この値は NULL です。|  
|\<ベース テーブルの列名 >|\<テーブル列の型を基本 >|この競合テーブルにはベース テーブルの列ごとに 1 行のデータが格納されます。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
