---
title: 可能 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 233b2f84b6a60c7b5162edce6c1b76b63946ae81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931283"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
指定します、[状態](../../../ado/reference/ado-api/status-property-ado-recordset.md)バッチ更新およびその他の一括操作に関して、レコードの。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|操作が取り消されたために、レコードが保存されなかったことを示します。|  
|**adRecCantRelease**|0x400|既存のレコードがロックされていたために、新しいレコードが保存されなかったことを示します。|  
|**adRecConcurrencyViolation**|0x800|オプティミスティック同時実行制御を使用していたために、レコードが保存されなかったことを示します。|  
|**adRecDBDeleted**|0x40000|レコードがデータ ソースから既に削除されたことを示します。|  
|**adRecDeleted**|0x4|レコードが削除されたことを示します。|  
|**adRecIntegrityViolation**|0x1000|ユーザーが整合性制約に違反したため、レコードが保存されなかったことを示します。|  
|**adRecInvalid**|0x10|ブックマークが無効であるために、レコードが保存されなかったことを示します。|  
|**adRecMaxChangesExceeded**|0x2000|保留中の変更が多すぎますがあったために、レコードが保存されなかったことを示します。|  
|**adRecModified**|0x2|レコードが変更されたことを示します。|  
|**adRecMultipleChanges**|0x40|複数のレコードが影響している場合があるために、レコードが保存されなかったことを示します。|  
|**adRecNew**|0x1|レコードが新しいことを示します。|  
|**adRecObjectOpen**|0x4000|開いているストレージ オブジェクトの競合があるため、レコードが保存されていないことを示します。|  
|**adRecOK**|0|レコードが正常に更新されたことを示します。|  
|**adRecOutOfMemory**|0x8000|コンピューターのメモリが不足しているために、レコードが保存されなかったことを示します。|  
|**adRecPendingChanges**|0x80|保留中の挿入を参照しているために、レコードが保存されなかったことを示します。|  
|**adRecPermissionDenied**|0x10000|ユーザーに十分なアクセス許可がないために、レコードが保存されなかったことを示します。|  
|**adRecSchemaViolation**|0x20000|基になるデータベースの構造に違反しているために、レコードが保存されなかったことを示します。|  
|**adRecUnmodified**|0x8|レコードが変更されていないことを示します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 AdoEnums.RecordStatus します。  
  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.RecordStatus.CANCELED|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums.RecordStatus.CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums.RecordStatus.OUTOFMEMORY|  
|AdoEnums.RecordStatus.PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>適用対象  
 [Status プロパティ (ADO Recordset)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
