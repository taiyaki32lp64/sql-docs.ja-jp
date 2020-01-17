---
title: FieldStatusEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldStatusEnum
helpviewer_keywords:
- FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3ad005a4c26a033f6c97d97def4cd55d867c14e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918666"
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
指定します、[状態](../../../ado/reference/ado-api/status-property-ado-field.md)の[フィールド オブジェクト](../../../ado/reference/ado-api/field-object.md)します。  
  
 **AdFieldPending\*** 値は、設定されていない状態の原因し、その他の状態値と組み合わせることもなった操作を示します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|指定したフィールドが既に存在することを示します。|  
|**adFieldBadStatus**|12|ADO から OLE DB プロバイダーに、無効な状態の値が送信されたことを示します。 考えられる原因は、OLE DB 1.0 または 1.1 プロバイダー、または不適切な組み合わせた[値](../../../ado/reference/ado-api/value-property-ado.md)と[状態](../../../ado/reference/ado-api/status-property-ado-field.md)します。|  
|**adFieldCannotComplete**|20|によって、サーバーの URL が指定されていることを示します[ソース](../../../ado/reference/ado-api/source-property-ado-record.md)操作を完了できませんでした。|  
|**adFieldCannotDeleteSource**|23|示します、移動操作中にツリーまたはサブツリーは、新しい場所に移動された、ソースを削除できませんでした。|  
|**adFieldCantConvertValue**|2|フィールドを取得またはデータの損失なしで保存できないことを示します。|  
|**adFieldCantCreate**|7|プロバイダーが許可されているフィールドの数) などの制限を超えているためは、フィールドを追加できませんでしたを示します。|  
|**adFieldDataOverflow**|6|プロバイダーから返されるデータが、フィールドのデータ型がオーバーフローしたことを示します。|  
|**adFieldDefault**|13|データを設定するときに、フィールドの既定値が使用されたことを示します。|  
|**adFieldDoesNotExist**|16|指定されたフィールドが存在しないことを示します。|  
|**adFieldIgnore**|15|ソースの値をデータを設定する場合に、このフィールドがスキップされたことを示します。 プロバイダーには、値は設定されていません。|  
|**adFieldIntegrityViolation**|10|計算された、または派生エンティティであるフィールドを変更できないことを示します。|  
|**adFieldInvalidURL**|17|データ ソースの URL に無効な文字が含まれていることを示します。|  
|**adFieldIsNull**|3|プロバイダーに VT_ 型のバリアント値が返されることと、フィールドが空でないことを示します。|  
|**adFieldOK**|0|既定値です。 フィールドが正常に追加または削除することを示します。|  
|**adFieldOutOfSpace**|22|プロバイダーが、移動が完了または操作をコピーするための十分な記憶域スペースを取得できないことを示します。|  
|**adFieldPendingChange**|0x40000|いずれかを示します、フィールドが削除され、再追加されました、おそらくさまざまなデータ型、またはをされている状態を持っていた、フィールドの値の**adfieldok で**が変更されました。 フィールドの最終形式を変更、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)後のコレクション、 [Update](../../../ado/reference/ado-api/update-method.md)メソッドが呼び出されます。|  
|**adFieldPendingDelete**|0x20000|示します、**削除**操作の原因となった状態を設定します。 削除、フィールドがマークされて、**フィールド**後のコレクション、 **Update**メソッドが呼び出されます。|  
|**adFieldPendingInsert**|0x10000|示します、 **Append**操作の原因となった状態を設定します。 **フィールド**に追加するのにはなって、**フィールド**後のコレクション、 **Update**メソッドが呼び出されます。|  
|**adFieldPendingUnknown**|これに対して、0x80000|プロバイダーがどのような操作の原因となったフィールドの状態を設定する判断できないことを示します。|  
|**adFieldPendingUnknownDelete**|0x100000|どのような操作には、フィールドの状態を設定して、フィールドがから削除されることが原因となったプロバイダーが判断できないことを示します、**フィールド**後のコレクション、 **Update**メソッドが呼び出されます。|  
|**adFieldPermissionDenied**|9|読み取り専用として定義されているため、フィールドを変更できないことを示します。|  
|**adFieldReadOnly**|24|読み取り専用データ ソースのフィールドが定義されていることを示します。|  
|**adFieldResourceExists**|19|プロバイダーが送信先 URL にオブジェクトが既にし、オブジェクトを上書きできないため、操作を実行できなかったことを示します。|  
|**adFieldResourceLocked**|18|プロバイダーがデータ ソースが 1 つ以上の他のアプリケーションまたはプロセスによってロックされているため、操作を実行できなかったことを示します。|  
|**adFieldResourceOutOfScope**|25|送信元または送信先の URL が現在のレコードの範囲外にことを示します。|  
|**adFieldSchemaViolation**|11|値が、フィールドのデータ ソース スキーマの制約に違反したことを示します。|  
|**adFieldSignMismatch**|5|プロバイダーによって返されるデータ値が署名された ADO フィールドの値のデータ型が署名されていないことを示します。|  
|**adFieldTruncated**|4|データ ソースから読み取るときに、可変長のデータが切り捨てられたことを示します。|  
|**adFieldUnavailable**|8|エントリのデータ ソースから読み取るときに、プロバイダーでした値が決定しないことを示します。 たとえば、行が作成した、列の既定値が使用可能なおよび新しい値が指定されていません。|  
|**adFieldVolumeNotFound**|21|プロバイダーが、URL で示される記憶域ボリュームを検出することであることを示します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 これらの定数には、ADO と WFC 対応はありません。  
  
## <a name="applies-to"></a>適用対象  
 [Status プロパティ (ADO Field)](../../../ado/reference/ado-api/status-property-ado-field.md)
