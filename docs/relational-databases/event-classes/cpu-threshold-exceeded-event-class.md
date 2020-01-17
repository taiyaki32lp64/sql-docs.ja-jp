---
title: CPU Threshold Exceeded イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- CPU Threshold Exceeded Event Class
ms.assetid: eb106f7d-baa3-4a2b-96b2-f9fe0844057d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d74d1907b0f96275658c716a7a08061f0eec8995
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999565"
---
# <a name="cpu-threshold-exceeded-event-class"></a>CPU Threshold Exceeded イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  CPU Threshold Exceeded イベント クラスは、REQUEST_MAX_CPU_TIME_SEC に指定されている CPU しきい値を超えるクエリがリソース ガバナーによって検出されたことを示します。  
  
> [!NOTE]  
>  このイベントの検出間隔は 5 秒です。 クエリが指定の制限を超えた時間が 5 秒以上の場合は、このイベントの生成が保証されます。 クエリが指定のしきい値を超えた時間が 5 秒未満の場合、クエリのタイミングと前回の検出スイープの時間によっては検出されない場合もあります。  
  
## <a name="cpu-threshold-exceeded-data-columns"></a>CPU Threshold Exceeded のデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|CPU|**int**|CPU 使用率 (ミリ秒単位)。|18|はい|  
|EventClass|**int**|214|27|いいえ|  
|EventSubClass|**int**|CPU 制限違反。|21|はい|  
|GroupID|**int**|違反が発生したグループ ID。|66|はい|  
|OwnerID|**int**|違反の原因となったプロセスの SPID。|58|はい|  
|SPID|**int**|このイベントを発生させたサーバー プロセスの ID。<br /><br /> 注:システム スレッドが CPU 使用率をバックグラウンド タスクとして検証する場合は、この ID が実際のユーザー SPID と異なることがあります。|12|はい|  
|StartTime|**datetime**|このイベントが発生した時刻。|14|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
