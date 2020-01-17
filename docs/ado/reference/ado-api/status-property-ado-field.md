---
title: Status プロパティ (ADO Field) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d90eff53ef998a009aecd4d82fc3b502a487c01d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930834"
---
# <a name="status-property-ado-field"></a>Status プロパティ (ADO Field)
状態を示します、[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 返します、 [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)値。 既定値は**adfieldok で**します。  
  
## <a name="remarks"></a>コメント  
  
## <a name="record-field-status"></a>レコード フィールドの状態  
 値に変更を**フィールド**のフィールド コレクション内のオブジェクトを[レコード](../../../ado/reference/ado-api/record-object-ado.md)までオブジェクトのオブジェクトがキャッシュされる[Update](../../../ado/reference/ado-api/update-method.md)メソッドが呼び出されます。 その時点では、フィールドの値への変更には、エラーが発生しました、OLE DB エラーが発生、 **DB_E_ERRORSOCCURRED** (2147749409)。 いずれかの Status プロパティ、**フィールド**内のオブジェクト、**フィールド**エラーの原因となったコレクションから値が格納されます、 [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)の原因を説明します。問題を。  
  
 パフォーマンス、追加および削除を強化するために、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)のコレクション、**レコード**までオブジェクトがキャッシュされている、 **Update**メソッドが呼び出されると、および変更し、オプティミスティック更新プログラムのバッチで行われます。 場合、 **Update**メソッドが呼び出されなかったサーバーは更新されません場合、。 OLE DB プロバイダー エラー (DB_E_ERRORSOCCURRED) が返されるすべての更新に失敗した場合、**状態**プロパティを操作およびエラー状態コードの値の組み合わせを示します。 たとえば、 **adFieldPendingInsert OR adFieldPermissionDenied**します。 **状態**プロパティごとに**フィールド**原因を特定するために使用できる、**フィールド**されていない追加、変更、または削除します。  
  
 さまざまな種類の変更、または削除を追加する場合に発生する問題を**フィールド**を通じて報告されたが、**状態**プロパティ。 たとえば、ユーザーを削除した場合、**フィールド**からの削除とマークされた、**フィールド**コレクション。 場合、後続**Update**ため、ユーザーを削除しようとしましたエラーが返されます、**フィールド**、アクセス許可のない、**フィールド**必要があります、  **。ステータス**の**adFieldPermissionDenied OR adFieldPendingDelete**します。 呼び出す、 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)メソッドの復元元の値とセット、**状態**に**adfieldok で**します。  
  
 同様に、 **Update**メソッドはエラーを返す可能性がありますので、新しい**フィールド**追加され、不適切な値を指定します。 その場合、新しい**フィールド**になります、**フィールド**コレクションの状態であると**adFieldPendingInsert**とおそらく**adFieldCantCreate**(、プロバイダーによります)。 適切な値を指定するには、新しい**フィールド**を呼び出すと**Update**もう一度です。  
  
## <a name="recordset-field-status"></a>レコード セットのフィールドの状態  
 値に変更を**フィールド**いずれかのフィールド コレクション内のオブジェクトを[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)までオブジェクトのキャッシュは[Update](../../../ado/reference/ado-api/update-method.md)メソッドが呼び出されます。 その時点では、フィールドの値への変更には、エラーが発生しました、OLE DB エラーが発生、 **DB_E_ERRORSOCCURRED** (2147749409)。 いずれかの Status プロパティ、**フィールド**内のオブジェクト、**フィールド**エラーの原因となったコレクションから値が格納されます、 [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)の原因を説明します。問題を。  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>関連項目  
 [Status プロパティの例 (Field) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Status プロパティの例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
