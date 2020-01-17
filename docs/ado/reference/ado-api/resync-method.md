---
title: Resync メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e2f83a3637af8f0e89c4125d3207c8c54b86763
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917160"
---
# <a name="resync-method"></a>Resync メソッド
現在のデータを更新します[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、または[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)のコレクションを[レコード](../../../ado/reference/ado-api/record-object-ado.md)基になるデータベースからのオブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>パラメーター  
 *AffectRecords*  
 任意。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)レコードの数を決定する値、**再同期**メソッドに影響されます。 既定値は**adAffectAll**します。 この値で使用できますが、**再同期**のメソッド、**フィールド**のコレクションを**レコード**オブジェクト。  
  
 *ResyncValues*  
 任意。 A [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)基になる値を上書きするかどうかを指定する値。 既定値は**adResyncAllValues**します。  
  
## <a name="remarks"></a>コメント  
  
## <a name="recordset"></a>レコードセット  
 使用して、**再同期**メソッド、現在のレコードを再同期を**レコード セット**を基になるデータベース。 これは、機能は、基になるデータベースのすべての変更を表示するか、静的または順方向専用カーソルを使用している場合に便利です。  
  
 設定した場合、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**、**再同期**でのみ使用読み取り専用でない**レコード セット**オブジェクト。  
  
 異なり、 [Requery](../../../ado/reference/ado-api/requery-method.md)メソッド、**再同期**メソッドは再実行されません、 **Recordset**オブジェクトには、コマンドの基になります。 基になるデータベース内の新しいレコードには表示されません。  
  
 基になるデータの競合があるため、再同期の試行が失敗したかどうか (たとえば、レコードが削除された他のユーザーによって)、プロバイダーに警告を返し、[エラー](../../../ado/reference/ado-api/errors-collection-ado.md)コレクションと、実行時エラーが発生します。 使用して、[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティ (**競合**) および[状態](../../../ado/reference/ado-api/status-property-ado-recordset.md)が競合しているレコードを検索するプロパティ。  
  
 場合、[一意テーブル](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)と[Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)動的プロパティが設定されて、**レコード セット** 、複数のテーブルに対して結合操作の実行の結果を示します。**再同期**メソッドがで指定されたコマンドを実行、 **Resync Command**プロパティで指定したテーブルでのみ、**一意テーブル**プロパティ。  
  
## <a name="fields"></a>フィールド  
 使用して、**再同期**の値を再同期するメソッド、**フィールド**のコレクションを**レコード**基になるデータ ソースを持つオブジェクト。 [カウント](../../../ado/reference/ado-api/count-property-ado.md)プロパティがこのメソッドによって影響を受けません。  
  
 場合*ResyncValues*に設定されている**adResyncAllValues** (既定値)、 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)、[値](../../../ado/reference/ado-api/value-property-ado.md)、および[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)プロパティの[フィールド](../../../ado/reference/ado-api/field-object.md)コレクション内のオブジェクトが同期されます。 場合*ResyncValues*に設定されている**処理**、のみ、 **UnderlyingValue**プロパティが同期されています。  
  
 値、**状態**プロパティごとに**フィールド**の呼び出し時にオブジェクトの動作にも影響**再同期**します。 **フィールド**を持つオブジェクト**状態**値**adFieldPendingUnknown**または**adFieldPendingInsert**、**再同期**も何も起こりません。 **状態**の値**adFieldPendingChange**または**adFieldPendingDelete**、**再同期**フィールドの値のデータを同期します。データ ソースに存在します。  
  
 **再同期**は変更されません**状態**の値**フィールド**エラーが発生しない限り、オブジェクトと**再同期**が呼び出されます。 たとえば、フィールドが存在しない場合、プロバイダーが返されます、適切な**状態**値、**フィールド**などオブジェクト**adFieldDoesNotExist**します。 返される**状態**内の値、値を論理的に結合できます、**状態**プロパティ。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Fields コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>関連項目  
 [Resync メソッドの例 (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Resync メソッドの例 (vc++)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear メソッド (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [UnderlyingValue プロパティ](../../../ado/reference/ado-api/underlyingvalue-property.md)
