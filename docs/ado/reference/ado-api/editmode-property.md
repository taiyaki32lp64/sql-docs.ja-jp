---
title: EditMode プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0ffc6fb258799b0ab0bb03e7acbd922f6a67d1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918982"
---
# <a name="editmode-property"></a>EditMode プロパティ
現在のレコードの編集状態を示します。  
  
## <a name="return-value"></a>戻り値  
 返します、 [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)値。  
  
## <a name="remarks"></a>コメント  
 ADO では、現在のレコードに関連付けられている編集のバッファーを保持します。 このプロパティは、このバッファーに変更が加えられましたかどうか、または新しいレコードが作成されているかどうかを示します。 使用して、 **EditMode**プロパティを現在のレコードの編集状態を確認します。 編集プロセスが中断された場合は、保留中の変更をテストして使用する必要があるかどうかを判断、 [Update](../../../ado/reference/ado-api/update-method.md)または[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)メソッド。  
  
 *即時更新モード*、 **EditMode**プロパティをリセット**adEditNone**呼び出しに成功した後、**更新**メソッドが呼び出されます. 呼び出し時に[削除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)は正常に削除されませんレコードまたはデータ ソース内のレコード (たとえば、参照整合性違反の場合) のため、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)は、引き続き編集モード (**EditMode** = **adEditInProgress**)。 そのため、 **CancelUpdate**現在のレコードから移動する前に呼び出す必要があります (たとえば[移動](../../../ado/reference/ado-api/move-method-ado.md)、 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)、または[を閉じる](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 *バッチ更新モード*(をプロバイダーが複数の変更をキャッシュし、呼び出すときにのみ、基になるデータ ソースに書き込む、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッド) の値、 **EditMode**プロパティが変更されたは、最初の操作を実行するへの呼び出しではリセットされません、 **Update**メソッド。 後続の操作は、の値を変更しないで、 **EditMode**プロパティ、さまざまな操作が実行される場合でもです。 たとえば、最初の操作は、新しいレコードを追加して、2 つ目は、既存に変更を加える場合は、記録のプロパティは、 **EditMode**は引き続き**adEditAdd**します。 **EditMode**にプロパティがリセットされない**adEditNone**への呼び出し後まで**UpdateBatch**します。 どのような操作が実行されたかを確認する設定、[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティを[adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md)保留中の変更のレコードがだけが表示され、確認できるように、 [の状態](../../../ado/reference/ado-api/status-property-ado-recordset.md)データにどのような変更が加えを判断するには、各レコードのプロパティ。  
  
> [!NOTE]
>  **EditMode**現在のレコードがある場合にのみ、有効な値を返すことができます。 **EditMode**場合はエラーを返します[BOF または EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)が true の場合、現在のレコードが削除されている場合またはします。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [CursorType、LockType、EditMode プロパティの例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType、EditMode プロパティの例 (vc++)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew メソッド (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete メソッド (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [CancelUpdate メソッド (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update メソッド](../../../ado/reference/ado-api/update-method.md)
