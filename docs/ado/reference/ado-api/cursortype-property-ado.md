---
title: CursorType プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4dc881b96a1e2641d4946340c9462455197f2043
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919253"
---
# <a name="cursortype-property-ado"></a>CursorType プロパティ (ADO)
使用するカーソルの種類を示す、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)値。 既定値は**adOpenForwardOnly**します。  
  
## <a name="remarks"></a>コメント  
 使用して、 **CursorType**プロパティを開くときに使用するカーソルの種類を指定する、 **Recordset**オブジェクト。  
  
 設定のみ**adOpenStatic**場合にサポートされていますが、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティに設定されて**adUseClient**します。 サポートされていない値が設定されている場合、エラーは発生しません。サポートされている最も近い**CursorType**が使用されます。  
  
 プロバイダーが、要求されたカーソルの種類をサポートしていない場合は、別のカーソルの種類を返すこと可能性があります。 **CursorType**プロパティは、実際のカーソルの種類に一致するように変更で使用するときに、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトが開いています。 返されるカーソルの特定の機能を確認するため、[サポート](../../../ado/reference/ado-api/supports-method.md)メソッド。 閉じた後、 **Recordset**、 **CursorType**プロパティは、元の設定に戻ります。  
  
 次の図は、プロバイダーの機能を示します (で識別される**サポート**メソッド定数) カーソルの種類ごとに必要な。  
  
|この CursorType のレコード セット|これらの定数のすべての True サポート メソッドを返す必要があります。|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adResync**|  
  
> [!NOTE]
>  **サポート**(**adUpdateBatch**) のバッチで更新プログラムを動的かつ順方向専用カーソルでは、true となる可能性、keyset または static カーソルに使用する必要があります。 設定、 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md)プロパティを**adLockBatchOptimistic**と**CursorLocation**プロパティを**adUseClient**カーソルを有効にするにはOLE DB、バッチ更新を必要とされるサービス。  
  
 **CursorType**プロパティが読み取り/書き込み時に、**レコード セット**が開いているときに閉じており、読み取り専用です。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**クライアント側で使用すると**レコード セット**オブジェクト、 **CursorType**にのみ設定できるプロパティ**adOpenStatic**。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [CursorType、LockType、EditMode プロパティの例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType、EditMode プロパティの例 (vc++)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports メソッド](../../../ado/reference/ado-api/supports-method.md)
