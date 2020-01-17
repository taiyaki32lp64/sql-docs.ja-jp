---
title: FetchProgress イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab93d8117a5fb3d2bbc95ea33bbacdc7fba3f151
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932829"
---
# <a name="fetchprogress-event-ado"></a>FetchProgress イベント (ADO)
**FetchProgress**に現在取得された複数行の数を報告する時間のかかる非同期操作中に定期的にイベントが呼び出される、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *[進行状況]*  
 A**長い**現在フェッチ操作によって取得されたレコードの数を示す値。  
  
 *MaxProgress*  
 A**長い**を取得するレコードの最大数を示す値が必要です。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。  
  
 *pRecordset*  
 A **Recordset**レコードが取得されているオブジェクトであるオブジェクト。  
  
## <a name="remarks"></a>コメント  
 使用する場合**FetchProgress**子を持つ**レコード セット**、注意してくださいを*進行状況*と*MaxProgress*パラメーターの値は派生基になるから[カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)行セット。 返される値は、基になる行セットの現在の章でレコードの数だけでなく、レコードの合計数を表します。  
  
> [!NOTE]
>  使用する**FetchProgress** Microsoft Visual Basic、Visual Basic 6.0 以降が必要です。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
