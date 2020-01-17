---
title: MSreplmonthresholdmetrics (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
author: stevestein
ms.author: sstein
ms.openlocfilehash: b3e8b9c2443a6fa74e113dc1a3f25880ac753dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079941"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplmonthresholdmetrics**テーブルがレプリケーションを監視するためのメトリックを定義します。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|レプリケーション パフォーマンス基準を識別し、次の値のいずれかを指定できます。<br /><br /> **1**有効期限を =<br /><br /> **2**待機時間を =<br /><br /> **4** mergeexpiration を =<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** mergefastrunspeed を =<br /><br /> **8** mergeslowrunspeed を =|  
|**title**|**sysname**|レプリケーション パフォーマンス基準の名前。|  
|**warningbitstatus**|**int**|次のいずれかの基準に対応するしきい値違反の警告を示す、ビットごとの識別子です。<br /><br /> **1** = の有効期間 - トランザクション パブリケーションに対するサブスクリプションが保有期間のしきい値を超えるによって保有期間のパーセンテージを超えました。<br /><br /> **2** = 待機時間、トランザクション パブリッシャーからサブスクライバーへのデータのレプリケートにかかった時間 (秒)、しきい値を超えています。<br /><br /> **4** mergeexpiration = マージ パブリケーションに対するサブスクリプションが保有期間のしきい値を超えるによって、保有期間のパーセンテージを超えました。<br /><br /> **8** = mergefastrunduration - マージ サブスクリプションの同期の完了にかかった時間、高速ネットワーク接続経由で秒単位で、しきい値を超えています。<br /><br /> **16** = mergeslowrunduration - マージ サブスクリプションの同期の完了にかかった時間、低速またはダイヤルアップ ネットワーク接続経由で秒単位で、しきい値を超えています。<br /><br /> **32** = mergefastrunspeed - 配信率マージ サブスクリプションの同期中の行が高速ネットワーク接続経由でのしきい値の割合で、1 秒あたりの行を維持するために失敗しました。<br /><br /> **64** mergeslowrunspeed - 配信率 = マージ サブスクリプションの同期中の行が低速またはダイヤルアップ ネットワーク接続経由でのしきい値の割合で、1 秒あたりの行を維持するために失敗しました。|  
|**alertmessageid**|**int**|しきい値の警告が発生した場合に表示されるエラー メッセージの ID。|  
|**description**|**nvarchar(3000)**|レプリケーション パフォーマンス基準の説明|  
|**default_value**|**sql_variant**|レプリケーション パフォーマンス基準の既定値。|  
|**min_value**|**sql_variant**|境界のあるレプリケーションのパフォーマンス メトリックの最小値。|  
|**max_value**|**sql_variant**|境界のあるレプリケーションのパフォーマンス メトリックの最大値。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
