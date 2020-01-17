---
title: UpdateBatch メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e9d74fe938ce486a4cd15573af8166dbed12ba6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937840"
---
# <a name="updatebatch-method"></a>UpdateBatch メソッド
すべての保留中のバッチ更新プログラムをディスクに書き込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>パラメーター  
 *AffectRecords*  
 任意。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)レコードの数を示す値、 **UpdateBatch**メソッドに影響されます。  
  
 *PreserveStatus*  
 任意。 A**ブール**によって示されるローカルが変更されたかどうかを指定する値、[状態](../../../ado/reference/ado-api/status-property-ado-recordset.md)プロパティをコミットする必要があります。 この値設定されている場合**True**、**状態**更新が完了したら、各レコードのプロパティは変更されません。  
  
## <a name="remarks"></a>コメント  
 使用して、 **UpdateBatch**メソッドを変更する場合、**レコード セット**で行われたすべての変更を送信するバッチ更新モードでのオブジェクトを**レコード セット**基になるデータベース オブジェクト。  
  
 場合、 **Recordset**オブジェクトは、バッチ更新をサポートしているを呼び出すまで、ローカルでは、1 つまたは複数のレコードに複数の変更をキャッシュすることができます、 **UpdateBatch**メソッド。 現在のレコードを編集または呼び出すときに新しいレコードを追加する場合、 **UpdateBatch**メソッド、ADO の呼び出しが自動的に、 [Update](../../../ado/reference/ado-api/update-method.md)メソッドの前に、現在のレコードに保留中の変更を保存するにはプロバイダーにバッチ処理された変更を送信します。 バッチ更新を keyset または static カーソルのみを使用する必要があります。  
  
> [!NOTE]
>  指定する**adAffectGroup** 、現在のレコードの表示がない場合にエラーで、このパラメーターの値が結果として**Recordset** (レコードが一致しないフィルター) など。  
  
 基になるデータとの競合またはすべてのレコードの変更の転送に失敗した場合 (たとえば、レコードが別のユーザーが既に削除されている場合)、プロバイダーに警告を返し、[エラー](../../../ado/reference/ado-api/errors-collection-ado.md)コレクションと、実行時エラーが発生します。 使用して、[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティ (**adFilterAffectedRecords**) および[状態](../../../ado/reference/ado-api/status-property-ado-recordset.md)が競合しているレコードを検索するプロパティ。  
  
 バッチ更新保留中のすべてをキャンセルするには、使用、 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッド。  
  
 場合、[一意テーブル](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)と[Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)動的プロパティが設定されて、**レコード セット**は複数のテーブルに対して結合操作を実行した結果、実行、 **UpdateBatch**メソッドが暗黙的に続けて、[再同期](../../../ado/reference/ado-api/resync-method.md)の設定によって、メソッド、 [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)プロパティ。  
  
 データ ソースでのバッチの個々 の更新プログラムの実行順序は必ずしもそれらがローカルに実行された順序と同じ**Recordset**します。 更新順序は、プロバイダーによって異なります。 するは、insert または update に対する外部キー制約など、相互に関連する更新プログラムをコーディングするときなど、考慮します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [UpdateBatch および CancelBatch メソッドの例 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch および CancelBatch メソッドの例 (vc++)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CancelBatch メソッド (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear メソッド (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType プロパティ (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update メソッド](../../../ado/reference/ado-api/update-method.md)
