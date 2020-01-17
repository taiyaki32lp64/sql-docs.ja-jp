---
title: CancelUpdate メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa9e680e1626311f2cc10aa7c79fb583841fbc38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920113"
---
# <a name="cancelupdate-method-ado"></a>CancelUpdate メソッド (ADO)
現在のまたは新しい行に加えられた変更を取り消します、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、または[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)のコレクションを[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクトを呼び出す前に、 [Update](../../../ado/reference/ado-api/update-method.md)メソッド。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>コメント  
  
## <a name="recordset"></a>レコードセット  
 使用して、 **CancelUpdate**メソッド、現在の行に加えられた変更をキャンセルするかを新しく追加された行を破棄します。 呼び出した後は、現在の行または新しい行への変更を取り消すことはできません、 **Update**メソッドでは、変更をロールバックできるトランザクションの一部である場合を除き、 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)メソッド、または一部バッチ更新します。 バッチ更新を取り消すことができます、**更新**で、 **CancelUpdate**または[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッド。  
  
 呼び出すときに新しい行を追加するかどうか、 **CancelUpdate**メソッド、現在の行が前に、の現在の行、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)呼び出します。  
  
 編集モードにし、現在のレコードから移動する場合 (などを使用して、[移動](../../../ado/reference/ado-api/move-method-ado.md)、 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)、または[閉じる](../../../ado/reference/ado-api/close-method-ado.md)メソッド) を使用することができます**CancelUpdate**保留中の変更をキャンセルします。 更新プログラムは、データ ソースに正常に投稿できない場合に実行する必要があります。 たとえば、削除の試みが失敗する参照整合性違反が残ります、 **Recordset**呼び出しの後に編集モードで[削除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)します。  
  
## <a name="record"></a>レコード  
 **CancelUpdate**メソッドは、保留中の挿入または削除をキャンセル[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクト、および保留中の既存のフィールドの更新をキャンセルし、元の値に戻します。 [状態](../../../ado/reference/ado-api/status-property-ado-recordset.md)のすべてのフィールドのプロパティ、**フィールド**に設定されているコレクション**adfieldok で**します。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Fields コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>関連項目  
 [Update および CancelUpdate メソッドの例 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update および CancelUpdate メソッドの例 (vc++)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew メソッド (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel メソッド (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel メソッド (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch メソッド (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate メソッド (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [EditMode プロパティ](../../../ado/reference/ado-api/editmode-property.md)   
 [Update メソッド](../../../ado/reference/ado-api/update-method.md)
