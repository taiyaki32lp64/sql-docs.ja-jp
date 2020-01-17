---
title: MSmerge_contents (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_contents
- MSmerge_contents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_contents system table
ms.assetid: 8d68a61a-683f-4b20-92f9-c0a8d9ba0ad1
author: stevestein
ms.author: sstein
ms.openlocfilehash: a4be6cffcc7e4f13b88d8037b53d438d604b9650
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089945"
---
# <a name="msmerge_contents-transact-sql"></a>MSmerge_contents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_contents**テーブルには、発行された後に、現在のデータベースで変更された行ごとに 1 行が含まれています。 マージ プロセスはこのテーブルを使用して、変更された行を決定します。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|パブリッシュされたテーブルのニックネームです。|  
|**rowguid**|**uniqueidentifier**|特定の行の行識別子。|  
|**generation**|**bigint**|識別される行の生成、 **tablenick**と**rowguid**します。|  
|**partchangegen**|**bigint**|行がフィルター選択されたパブリケーションに属しているかどうかに変わる可能性がある最新のデータ変更に関連付けられているジェネレーション。|  
|**lineage**|**varbinary(501)**|サブスクライバーのニックネームとバージョン番号のペアのこの行に対する変更の履歴を保持するために使用します。|  
|**colvl**|**varbinary(7489)**|列バージョン情報です。|  
|**marker**|**uniqueidentifier**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|最上位レベル親行を識別**MSmerge_contents** (によって**rowguid**) 論理レコードの対応する子行はごとです。|  
|**logical_record_lineage**|**varbinary(501)**|サブスクライバーのニックネーム、論理レコードの最上位レベル親行に対する変更の履歴を維持するために使用されるバージョン番号のペア。 論理レコードのすべての子行に対しては、この値は NULL です。|  
|**logical_relation_change_gen**|**bigint**|既存の行が論理レコード内外に移動した、論理レコードの再調整の原因となった最後の変更に関連付けられた generation 値です。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
