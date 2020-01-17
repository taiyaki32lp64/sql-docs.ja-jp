---
title: LockType プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7b50ab4a6fa31ec74371b86129f30abf11a1ba6c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932250"
---
# <a name="locktype-property-ado"></a>LockType プロパティ (ADO)
編集中に、レコードに置かれたロックの種類を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)値。 既定値は**adLockReadOnly**します。  
  
## <a name="remarks"></a>コメント  
 設定、 **LockType**プロパティを開く前に、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)を開くときに、プロバイダーのロックの種類を使用する必要がありますを指定します。 開くときに使用されているロックの種類を取得するプロパティを読み取る**Recordset**オブジェクト。  
  
 プロバイダーはすべてのロックの種類をサポートしていません。 プロバイダーをサポートして、要求された場合**LockType**設定すると、別の種類のロックで置き換えられます。 使用可能な実際のロック機能を決定する、**レコード セット**オブジェクトを使用して、[サポート](../../../ado/reference/ado-api/supports-method.md)メソッド**adUpdate**と**adUpdateBatch**.  
  
 **AdLockPessimistic**場合、設定がサポートされていません、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティに設定されて**adUseClient**します。 サポートされていない値が設定されている場合、エラーは発生しません。サポートされている最も近い**LockType**が使用されます。  
  
 **LockType**プロパティが読み取り/書き込み時に、**レコード セット**が開いているときに閉じており、読み取り専用です。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**クライアント側で使用すると**レコード セット**オブジェクト、 **LockType**プロパティのみ設定できます**adLockBatchOptimistic**します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [CursorType、LockType、EditMode プロパティの例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType、EditMode プロパティの例 (vc++)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch メソッド (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [UpdateBatch メソッド](../../../ado/reference/ado-api/updatebatch-method.md)
