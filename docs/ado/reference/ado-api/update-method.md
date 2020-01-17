---
title: メソッドの更新 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ce247905afd6ed34366424f5f905d57b42d988f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938842"
---
# <a name="update-method"></a>Update メソッド
現在の行に加えた変更を保存、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、または[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)のコレクションを[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Fields*  
 任意。 A**バリアント**を表す 1 つの名前または**バリアント**名または変更するフィールドの序数位置を表す配列。  
  
 *値*  
 任意。 A**バリアント**を表す 1 つの値または**バリアント**フィールドまたは新しいレコードのフィールドの値を表す配列。  
  
## <a name="remarks"></a>コメント  
  
## <a name="recordset"></a>レコードセット  
 使用して、**更新**の現在のレコードに加えた変更を保存する方法、**レコード セット**オブジェクトを呼び出した後、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)メソッドまたは内のフィールドの値を変更した後、既存のレコード。 **Recordset**オブジェクトは、更新プログラムをサポートする必要があります。  
  
 フィールドの値を設定するには、次のいずれかの操作を行います。  
  
-   値を割り当てる、[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクトの[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティと呼び出し、 **Update**メソッド。  
  
-   フィールドの名前と値を引数として渡す、 **Update**呼び出します。  
  
-   フィールド名の配列と値の配列を渡す、 **Update**呼び出します。  
  
 フィールドと値の配列を使用する場合は、両方の配列内の要素の数が等しい必要があります。 また、フィールド名の順序は、フィールドの値の順序と一致する必要があります。 フィールドと値の順序と数が一致しない場合は、エラーが発生します。  
  
 場合、 **Recordset**オブジェクトは、バッチ更新をサポートしているを呼び出すまで、ローカルでは、1 つまたは複数のレコードに複数の変更をキャッシュすることができます、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッド。 現在のレコードを編集または呼び出すときに新しいレコードを追加する場合、 **UpdateBatch**メソッド、ADO の呼び出しが自動的に、 **Update**メソッドの前に、現在のレコードに保留中の変更を保存するにはプロバイダーにバッチ処理された変更を送信します。  
  
 レコードから移動した場合の追加または編集する呼び出しの前に、 **Update**メソッド、ADO の呼び出しが自動的に**Update**変更を保存します。 呼び出す必要があります、 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)メソッド、現在のレコードに加えられた変更をキャンセルするか、新しく追加したレコードを破棄する場合。  
  
 現在のレコードを呼び出した後は、最新の状態、 **Update**メソッド。  
  
## <a name="record"></a>レコード  
 **Update**メソッドは、追加、削除、および内のフィールドに対する更新を終了、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)のコレクションを**レコード**オブジェクト。  
  
 削除されたフィールドなど、**削除**メソッドがすぐに削除対象としてマークがコレクションに残ります。 **Update**を実際には、プロバイダーのコレクションからこれらのフィールドを削除するメソッドを呼び出す必要があります。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Fields コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>関連項目  
 [Update および CancelUpdate メソッドの例 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update および CancelUpdate メソッドの例 (vc++)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew メソッド (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [CancelUpdate メソッド (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode プロパティ](../../../ado/reference/ado-api/editmode-property.md)   
 [UpdateBatch メソッド](../../../ado/reference/ado-api/updatebatch-method.md)
