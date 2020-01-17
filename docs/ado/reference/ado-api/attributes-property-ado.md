---
title: 属性のプロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b40b71dee32608756721d84a2e13f5f54f7bcbfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920541"
---
# <a name="attributes-property-ado"></a>Attributes プロパティ (ADO)
オブジェクトの 1 つまたは複数の特性を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**長い**値。  
  
 [接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト、**属性**プロパティが読み取り/書き込み、およびその値が 1 つまたは複数の合計を指定できます[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)値。 既定ではゼロ (0) です。  
  
 [パラメーター](../../../ado/reference/ado-api/parameter-object.md)オブジェクト、**属性**プロパティが読み取り/書き込み、およびその値が 1 つ以上の合計を指定できます[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)値。 既定値は**adParamSigned**します。  
  
 [フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクト、**属性**プロパティは、1 つまたは複数の合計を指定できます[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)値。 通常は読み取り専用をお勧めします。 ただし、新規の**フィールド**に追加されたオブジェクト、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)のコレクションを[レコード](../../../ado/reference/ado-api/record-object-ado.md)、**属性**は読み取り/書き込みのみ後に、[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティを**フィールド**が指定されていると、新しい**フィールド**データ プロバイダーによって、を呼び出すことによって正常に追加されました。[Update](../../../ado/reference/ado-api/update-method.md)のメソッド、**フィールド**コレクション。  
  
 [プロパティ](../../../ado/reference/ado-api/property-object-ado.md)オブジェクト、**属性**プロパティは読み取り専用とその値が 1 つ以上の合計を指定できます[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)値。  
  
## <a name="remarks"></a>コメント  
 使用して、**属性**プロパティを設定または取得の特性**接続**オブジェクト、**パラメーター**オブジェクト、**フィールド**オブジェクト、または**プロパティ**オブジェクト。  
  
 複数の属性を設定すると、適切な定数を合計できます。 互換性のない定数を含む合計にプロパティの値を設定すると、エラーが発生します。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**このプロパティはクライアント側で使用可能な**接続**オブジェクト。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Field オブジェクト](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter オブジェクト](../../../ado/reference/ado-api/parameter-object.md)|[Property オブジェクト (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>関連項目  
 [属性と Name プロパティの例 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [属性と Name プロパティの例 (vc++)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [AppendChunk メソッド (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans、CommitTrans、および RollbackTrans メソッド (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk メソッド (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
