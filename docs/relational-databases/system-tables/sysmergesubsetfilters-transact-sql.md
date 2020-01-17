---
title: sysmergesubsetfilters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergesubsetfilters
- sysmergesubsetfilters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubsetfilters system table
ms.assetid: f91d1c6c-3132-47f6-926c-88f56848cafe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 84f9e2ce3026792b768d353e05b9e2299cf7ca5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029757"
---
# <a name="sysmergesubsetfilters-transact-sql"></a>sysmergesubsetfilters (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  パーティション分割されたアーティクルの結合フィルター情報を格納します。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**filtername**|**sysname**|アーティクルを作成するときに使用したフィルターの名前。|  
|**join_filterid**|**int**|結合フィルターを表すオブジェクトの ID。|  
|**pubid**|**uniqueidentifier**|パブリケーションの ID。|  
|**artid**|**uniqueidentifier**|アーティクルの ID。|  
|**art_nickname**|**int**|アーティクルのニックネーム。|  
|**join_articlename**|**sysname**|行が属しているかどうかを判断するために結合するテーブルの名前。|  
|**join_nickname**|**int**|行が属しているかどうかを判断する結合するテーブルのニックネームです。|  
|**join_unique_key**|**int**|一意なキーに基づいて結合を示します**join_tablename**:<br /><br /> 0 = 一意キーではない<br /><br /> 1 = 一意キー|  
|**expand_proc**|**sysname**|行を識別するために、マージ エージェントで使用するストアド プロシージャの名前を送信またはサブスクライバーから削除する必要があります。|  
|**join_filterclause**|**nvarchar(1000)**|フィルター句を結合に使用します。|  
|**filter_type**|**tinyint**|フィルターの種類。次のいずれかになります。<br /><br /> 1 = 結合フィルター。<br /><br /> 2 = 論理レコード リンクします。<br /><br /> 3 = 両方の結合フィルターと論理レコード リンクします。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
