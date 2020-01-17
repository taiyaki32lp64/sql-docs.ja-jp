---
title: Requery メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3626f91018714fa4d67304c92ce464d82fb5c8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917222"
---
# <a name="requery-method"></a>Requery メソッド
データを更新、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトをオブジェクトの基になるクエリを再実行しています。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>パラメーター  
 *[オプション]*  
 任意。 含むビットマスク[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)と[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)値がこの操作に影響します。  
  
> [!NOTE]
>  場合*オプション*に設定されている**adAsyncExecute**、この操作は非同期的に実行、 [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)と判断します。 ときにイベントが発行されます。 **ExecuteOpenEnum**値**adExecuteNoRecords**または**adExecuteStream**では使用できません**Requery**します。  
  
## <a name="remarks"></a>コメント  
 使用して、 **Requery**の内容全体を更新する方法、**レコード セット**元のコマンドをもう一度データを取得して、データ ソースからのオブジェクト。 呼び出しと同じですがこのメソッドを呼び出す、[閉じる](../../../ado/reference/ado-api/close-method-ado.md)と[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッドを連続しています。 現在のレコードを編集するか、新しいレコードを追加する、エラーが発生します。  
  
 中に、 **Recordset**オブジェクトを開くと、カーソルの特性を定義するプロパティ ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)、 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md)、 [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)、など) は読み取り専用です。 つまり、 **Requery**メソッドは、現在のカーソルのみを更新できます。 カーソルのプロパティのいずれかを変更し、結果を表示、使用する必要があります、[閉じる](../../../ado/reference/ado-api/close-method-ado.md)メソッド、プロパティが読み取り/書き込みをもう一度になるようにします。 プロパティの設定と呼び出しを変更することができますし、[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッドにカーソルを再度開きます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Execute、Requery、および Clear のメソッドの例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery、および Clear のメソッドの例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery、および Clear のメソッドの例 (vc++)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText プロパティ (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
