---
title: PreConnect:Completed イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- PreConnect:Completed Event Class
ms.assetid: 7ed2f620-6511-4985-9961-d2927c2b1759
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d674bf516dbdf25f940e9b14792d71c01d44806
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940661"
---
# <a name="preconnectcompleted-event-class"></a>PreConnect:Completed イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  PreConnect:Completed イベント クラスは、LOGON トリガーまたはリソース ガバナー分類関数の実行が終了したことを示します。  
  
## <a name="preconnectcompleted-event-class-data-columns"></a>PreConnect:Completed イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|216|27|いいえ|  
|SPID|**int**|このイベントを発生させるサーバー プロセスの ID。|12|はい|  
|EventSubClass|**int**|ユーザー定義の分類子関数の場合は 1。|21|はい|  
|StartTime|**datetime**|ユーザー定義の分類子関数が開始された時刻。|14|はい|  
|EndTime|**datetime**|ユーザー定義の分類子関数が開始された時刻。|15|はい|  
|Duration|**bigint**|分類子関数によって使用された時間 (マイクロ秒)。|13|はい|  
|ObjectID|**int**|ユーザー定義の分類オブジェクトの ID。|22|はい|  
|CPU|**int**|CPU 使用率 (ミリ秒単位)。|18|はい|  
|Reads|**int**|論理読み取りの数。|16|はい|  
|Writes|**int**|論理書き込みの数。|17|はい|  
|GroupID|**int**|分類されたワークロード グループの ID。|66|はい|  
|Error|**int**|ユーザー定義の分類子関数が実行に失敗した場合の最後のエラー番号。|31|はい|  
|状態|**int**|最後のエラーの状態。|30|はい|  
|TargetUserName|**sysname**|対応するアクティブなグループをシステムが見つけられない場合は、ユーザー定義の分類子関数の戻り値 (ワークロード グループ名)。 それ以外の場合は、この列は NULL に設定されます。|39|はい|  
|ObjectName|**nvarchar (256)**|ユーザー定義の分類子関数の 2 部構成の名前 (dbo.classifier など)。|34|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)   
 [PreConnect:Starting イベント クラス](../../relational-databases/event-classes/preconnect-starting-event-class.md)   
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)  
  
  
