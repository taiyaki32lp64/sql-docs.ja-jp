---
title: Resync プロパティ-動的 (ADO) の更新 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed0e3ad8027c31a351ddb4506d3b420aa3a1124d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938804"
---
# <a name="update-resync-property-dynamic-ado"></a>Update Resync プロパティ - 動的 (ADO)
指定するかどうか、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッドの後に、暗黙的な[再同期](../../../ado/reference/ado-api/resync-method.md)メソッドの操作であれば、その操作のスコープ。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 1 つ以上を取得または設定、 [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)値。  
  
## <a name="remarks"></a>コメント  
 既に、残りの値の組み合わせを表す adResyncAll を除き、ADCPROP_UPDATERESYNC_ENUM の値を組み合わせることができます。  
  
 定数**adResyncConflicts** 、基になる値として再同期の値が格納されますが、保留中の変更を上書きしません。  
  
 **再同期の更新**に動的なプロパティが追加、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション時に、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) にプロパティを設定**adUseClient**します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
