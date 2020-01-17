---
title: Delete メソッド (ADO Recordset) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b978e3d885e3ff06dda18859384f88eb4c564254
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919123"
---
# <a name="delete-method-ado-recordset"></a>Delete メソッド (ADO Recordset)
現在のレコードまたはレコードのグループを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>パラメーター  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)レコードの数を決定する値、**削除**メソッドに影響されます。 既定値は**adAffectCurrent**します。  
  
> [!NOTE]
>  **adAffectAll**と**呼び出します**に有効な引数ではなく**削除**します。  
  
## <a name="remarks"></a>コメント  
 使用して、**削除**メソッドは、現在のレコードまたはレコードのグループを示します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトを削除します。 場合、 **Recordset**オブジェクトは、レコードの削除を許可しないエラーが発生します。 即時更新モードの場合は、削除はすぐに、データベースで発生します。 呼び出しの後に、レコードが編集モードのままは場合 (たとえば、データベース整合性違反) のため、レコードを正常に削除することはできません、 [Update](../../../ado/reference/ado-api/update-method.md)します。 これで更新を取り消す必要があることを意味[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)現在のレコードから移動する前に (たとえば、[閉じる](../../../ado/reference/ado-api/close-method-ado.md)、[移動](../../../ado/reference/ado-api/move-method-ado.md)、または[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 バッチ更新モードの場合は、レコードがキャッシュからの削除とマークされてし、実際の削除の動作を呼び出すとき、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッド。 使用して、[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティを削除したレコードを表示します。  
  
 削除されたレコードからフィールドの値を取得するには、エラーが生成されます。 現在のレコードを削除すると、削除されたレコードを別のレコードに移動するまで最新の状態します。 移動すると、削除されたレコードはアクセスできません。  
  
 トランザクションで、入れ子にする場合で削除されたレコードを回復することができます、 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)メソッド。 バッチ更新モードの場合は、保留中の削除または保留中の削除でのグループをキャンセルすることができます、 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッド。  
  
 基になるデータとの競合レコードを削除する試行が失敗した場合 (たとえば、レコードが別のユーザーが既に削除されている場合)、プロバイダーに警告を返し、[エラー](../../../ado/reference/ado-api/errors-collection-ado.md)コレクション プログラムは停止されませんが、実行します。 要求されたすべてのレコードの競合がある場合にのみ、実行時エラーが発生します。  
  
 場合、[一意テーブル](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)動的プロパティを設定すると、および**レコード セット**は複数のテーブルに対して結合操作を実行した結果、**削除**メソッドは削除されるだけ指定したテーブルから行、[一意テーブル](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)プロパティ。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Delete メソッドの例 (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete メソッドの例 (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Delete メソッドの例 (vc++)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete メソッド (ADO Fields コレクション)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete メソッド (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord メソッド (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
