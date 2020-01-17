---
title: Index プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Index
helpviewer_keywords:
- Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba871d6d0e84b8068cb36a3ed2516a2665db28d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932435"
---
# <a name="index-property"></a>Index プロパティ
有効なインデックスを現在の名前を示します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**文字列**値で、インデックスの名前を指定します。  
  
## <a name="remarks"></a>コメント  
 指定したインデックス、**インデックス**プロパティする必要がありますが事前に宣言して基になるベース テーブルで、 **Recordset**オブジェクト。 つまり、インデックスする必要があります宣言されているプログラムで ADOX として[インデックス](../../../ado/reference/adox-api/index-object-adox.md)オブジェクト、またはベース テーブルの作成時にします。  
  
 インデックスを設定できない場合、実行時エラーが発生します。 **インデックス**プロパティは、次の条件下で設定できません。  
  
-   内で、 [WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)または**RecordsetChangeComplete**イベント ハンドラー。  
  
-   場合、 **Recordset**操作がまだ実行中 (で決定できますが、[状態](../../../ado/reference/ado-api/state-property-ado.md)プロパティ)。  
  
-   フィルターが設定されている場合、 **Recordset**で、[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティ。  
  
 **インデックス**プロパティは常に正常に設定できる場合、**レコード セット**が閉じているが、**レコード セット**が正常には開かれませんまたはインデックスは、使用できない場合、基になるプロバイダーは、インデックスをサポートしていません。  
  
 インデックスを設定できますが、現在の行位置は変更できます。 これにより、更新プログラム、 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)プロパティが起動し、 **WillChangeRecordset**、 **RecordsetChangeComplete**、 [WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)、および[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)イベント。  
  
 インデックスを設定する場合は、 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md)プロパティは**adLockPessimistic**または**adLockOptimistic**、し、暗黙[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)操作が実行されます。 これにより、現在および影響を受けるグループが解放されます。 任意の既存のフィルターがリリースされ、並べ替えられたの最初の行に現在の行位置が変更された**Recordset**します。  
  
 **インデックス**と共にプロパティが使用される、[シーク](../../../ado/reference/ado-api/seek-method.md)メソッド。 基になるプロバイダーがサポートされていない場合、**インデックス**プロパティ、つまり、**シーク**メソッドの使用を検討、[検索](../../../ado/reference/ado-api/find-method-ado.md)メソッド代わりにします。 決定かどうか、**レコード セット**オブジェクトのインデックスをサポートしている、[サポート](../../../ado/reference/ado-api/supports-method.md) **(adIndex)** メソッド。  
  
 組み込み**インデックス**プロパティが動的に関連しない[最適化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)プロパティ、インデックスを扱う、両方が。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Seek メソッドおよび Index プロパティの例 (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Index オブジェクト (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Seek メソッド](../../../ado/reference/ado-api/seek-method.md)
