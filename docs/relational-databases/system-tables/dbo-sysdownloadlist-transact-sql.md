---
title: dbo.sysdownloadlist (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdownloadlist
- sysdownloadlist_TSQL
- dbo.sysdownloadlist_TSQL
- sysdownloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sysdownloadlist system table
ms.assetid: 71087a4c-e829-488e-aa7d-a9476e2b4779
author: stevestein
ms.author: sstein
ms.openlocfilehash: 03e888cc3d36b909035247d5f1c16dd1ab61e0d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061194"
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  すべてのターゲット サーバーに対するダウンロード命令のキューを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|行の挿入順序を表す ID 列。|  
|**source_server**|**sysname**|ソース サーバーの名前。|  
|**operation_code**|**tinyint**|ジョブの操作コード。<br /><br /> **1**アドイン (挿入) を =<br /><br /> **2** UPD (更新) を =<br /><br /> **3** DEL (削除) を =<br /><br /> **4** = 開始<br /><br /> **5** = 停止|  
|**object_type**|**tinyint**|オブジェクトの種類のコード。|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|オブジェクト ID 番号。|  
|**target_server**|**sysname**|ターゲット サーバーの名前。|  
|**error_message**|**nvarchar(1024)**|ターゲット サーバーが特定の行を処理しているときにエラーが発生した場合のエラー メッセージ。|  
|**date_posted**|**datetime**|ジョブがターゲット サーバーに通知された日付と時刻。|  
|**date_downloaded**|**datetime**|ジョブが前回ダウンロードされた日付と時刻。|  
|**status**|**tinyint**|ジョブのステータス。<br /><br /> **0** = 未ダウンロード<br /><br /> **1** = 正常にダウンロードされました|  
|**deleted_object_name**|**sysname**|削除されたオブジェクトの名前。|  
  
 <sup>1</sup> 、 **object_id**列の値を指定できます **-1**、場合、すべての値に対応する、 **operation_code**列は、値は削除します。  
  
  
