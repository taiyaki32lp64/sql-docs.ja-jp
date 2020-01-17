---
title: フィールドのコレクション (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9c9216ee655e371633837c5653ebac56fac1a782
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918711"
---
# <a name="fields-collection-ado"></a>Fields コレクション (ADO)
すべてが含まれています、[フィールド](../../../ado/reference/ado-api/field-object.md)のオブジェクトを[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)または[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクト。  
  
## <a name="remarks"></a>コメント  
 A **Recordset**オブジェクトには、**フィールド**から成るコレクション**フィールド**オブジェクト。 各**フィールド**オブジェクト内の列に対応して、 **Recordset**します。 設定することができます、**フィールド**コレクションを開始する前に、**レコード セット**呼び出すことによって、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)コレクション メソッド。  
  
> [!NOTE]
>  参照してください、**フィールド**を使用する方法の詳細については、オブジェクト**フィールド**オブジェクト。  
  
 **フィールド**コレクションが、[追加](../../../ado/reference/ado-api/append-method-ado.md)メソッドでは、仮を作成し、追加、**フィールド**、コレクションにオブジェクトを**を更新**メソッドの追加または削除を終了します。  
  
 A**レコード**オブジェクトが 2 つの特別なフィールドでインデックスを作成できる[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)定数。 1 つの定数の既定のストリームを含むフィールドにアクセスする、**レコード**との絶対 URL 文字列を含むフィールドにアクセスする他、**レコード**します。  
  
 特定のプロバイダー (たとえば、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) メンバー関数の呼び出し、**フィールド**使用可能なフィールドのサブセットをコレクション、 **レコード**または**Recordset**します。 最初に名前で参照またはコードによってインデックスが作成されるまで、他のフィールドは、コレクションに追加されません。  
  
 存在しないフィールドの名前で参照しようとした場合、新しい**フィールド**オブジェクトに追加されます、**フィールド**使用して、コレクション、[状態](../../../ado/reference/ado-api/status-property-ado-field.md)の**adFieldPendingInsert**します。 呼び出すと[Update](../../../ado/reference/ado-api/update-method.md)ADO は、プロバイダーによって許可されている場合に、データ ソース内の新しいフィールドが作成されます。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [フィールド コレクションのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)
