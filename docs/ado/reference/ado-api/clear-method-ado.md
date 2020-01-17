---
title: Clear メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96bd13f130966b1830d07e49633842e4154b52b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920065"
---
# <a name="clear-method-ado"></a>Clear メソッド (ADO)
すべてを削除、[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクトから、[エラー](../../../ado/reference/ado-api/errors-collection-ado.md)コレクション。  
  
## <a name="syntax"></a>構文  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>コメント  
 使用して、**クリア**メソッドを[エラー](../../../ado/reference/ado-api/errors-collection-ado.md)既存のすべてを削除するコレクション[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクトをコレクションから。 エラーが発生すると、ADO は自動的にオフ、**エラー**コレクションを格納および**エラー**新しいエラーに基づいてオブジェクト。  
  
 プロパティとメソッドの一部として表示される警告を返す**エラー**内のオブジェクト、**エラー**コレクションが、プログラムの実行は停止しないでください。 呼び出す前に、[再同期](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)、または[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッド、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、 [を開く](../../../ado/reference/ado-api/open-method-ado-connection.md)メソッドを[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトまたは設定、[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティを**レコード セット**オブジェクトを呼び出し、 **をオフに**メソッドを**エラー**コレクション。 そうすることが読み取ることができます、[カウント](../../../ado/reference/ado-api/count-property-ado.md)のプロパティ、**エラー**コレクションをテストするには、警告が返されます。  
  
## <a name="applies-to"></a>適用対象  
 [Errors コレクション (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Execute、Requery、および Clear のメソッドの例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery、および Clear のメソッドの例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery、および Clear のメソッドの例 (vc++)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch メソッド (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete メソッド (ADO Fields コレクション)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete メソッド (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete メソッド (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [プロパティをフィルター処理します。](../../../ado/reference/ado-api/filter-property.md)   
 [Resync メソッド](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch メソッド](../../../ado/reference/ado-api/updatebatch-method.md)
