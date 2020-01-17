---
title: CursorOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d5cc44950754c4b63e644d2d9210edcc94bd9ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933265"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
どのような機能を指定します、[サポート](../../../ado/reference/ado-api/supports-method.md)メソッドをテストする必要があります。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|では、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)新しいレコードを追加するメソッド。|  
|**adApproxPosition**|0x4000|では、 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)と[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)プロパティ。|  
|**adBookmark**|0x2000|では、[ブックマーク](../../../ado/reference/ado-api/bookmark-property-ado.md)特定のレコードにアクセスするプロパティ。|  
|**adDelete**|0x1000800|では、[削除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)レコードを削除するメソッド。|  
|**adFind**|これに対して、0x80000|サポート、[検索](../../../ado/reference/ado-api/find-method-ado.md)内の行を検索するメソッド、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)します。|  
|**adHoldRecords**|0x100|複数のレコードを取得または保留中のすべての変更をコミットしなくても、次の位置を変更します。|  
|**adIndex**|0x100000|サポート、[インデックス](../../../ado/reference/ado-api/index-property.md)プロパティにインデックスの名前します。|  
|**adMovePrevious**|0x200|サポート、 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)と[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)メソッド、および[移動](../../../ado/reference/ado-api/move-method-ado.md)または[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)に現在のレコードを移動する方法が後方移動ブックマークをせずにします。|  
|**adNotify**|0x40000|基になるデータ プロバイダーが通知をサポートしていることを示します (を決定するかどうか**Recordset**イベントがサポートされます)。|  
|**adResync**|0x20000|サポート、[再同期](../../../ado/reference/ado-api/resync-method.md)基になるデータベースに表示されているデータでカーソルを更新するメソッド。|  
|**adSeek**|0x200000|サポート、[シーク](../../../ado/reference/ado-api/seek-method.md)内の行を検索するメソッド、**レコード セット**します。|  
|**adUpdate**|0x1008000|サポート、[更新](../../../ado/reference/ado-api/update-method.md)メソッドを既存のデータを変更します。|  
|**adUpdateBatch**|0x10000|バッチ更新をサポートしています ([UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)と[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッド)、プロバイダーの変更のグループを送信します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.CursorOption.ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums.CursorOption.BOOKMARK|  
|AdoEnums.CursorOption.DELETE|  
|AdoEnums.CursorOption.FIND|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums.CursorOption.INDEX|  
|AdoEnums.CursorOption.MOVEPREVIOUS|  
|AdoEnums.CursorOption.NOTIFY|  
|AdoEnums.CursorOption.RESYNC|  
|AdoEnums.CursorOption.SEEK|  
|AdoEnums.CursorOption.UPDATE|  
|AdoEnums.CursorOption.UPDATEBATCH|  
  
## <a name="applies-to"></a>適用対象  
 [Supports メソッド](../../../ado/reference/ado-api/supports-method.md)
