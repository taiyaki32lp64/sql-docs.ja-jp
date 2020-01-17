---
title: オブジェクトをフィールド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04dbf3069896b9a7668d64a2f1d322f0b17ca5f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918684"
---
# <a name="field-object"></a>Field オブジェクト
一般的なデータ型のデータの列を表します。  
  
## <a name="remarks"></a>コメント  
 各**フィールド**オブジェクト内の列に対応して、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。 使用する、[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティの**フィールド**オブジェクトを設定または現在のレコードのデータを取得します。 機能によって、プロバイダーが公開していくつかのコレクション、メソッド、またはプロパティの**フィールド**オブジェクトを使用できない可能性があります。  
  
 コレクション、メソッド、およびプロパティの使用、**フィールド**オブジェクトを次を行うことができます。  
  
-   フィールドの名前を返す、[名前](../../../ado/reference/ado-api/name-property-ado.md)プロパティ。  
  
-   表示または変更が含まれるフィールドのデータ、**値**プロパティ。 **値**の既定のプロパティ、**フィールド**オブジェクト。  
  
-   フィールドの基本的な特性を返す、[型](../../../ado/reference/ado-api/type-property-ado.md)、[精度](../../../ado/reference/ado-api/precision-property-ado.md)、および[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)プロパティ。  
  
-   持つフィールドの宣言されたサイズを返す、 [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)プロパティ。  
  
-   特定のフィールドに、データの実際のサイズを返す、 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)プロパティ。  
  
-   指定されたフィールドにどのような種類の機能がサポートされているかを判断、[属性](../../../ado/reference/ado-api/attributes-property-ado.md)プロパティと[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。  
  
-   長のバイナリまたは文字の長いデータを格納するフィールドの値を操作、 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)と[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)メソッド。  
  
-   プロバイダーは、バッチ更新をサポートする場合は、フィールド値の矛盾を解決でバッチを更新中に、 [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)と[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)プロパティ。  
  
 すべてのメタデータ プロパティ (**名前**、**型**、 **DefinedSize**、**精度**、および**NumericScale**) が開く前に使用可能な**フィールド**オブジェクトの**Recordset**します。 その時点でそれらを設定することは、フォームを動的に構築するために便利です。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Field オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [フィールド コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
