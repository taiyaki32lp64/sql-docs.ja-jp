---
title: オブジェクトのプロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43bfa816a9ca8a93cdc1188a98e54d3e0d9111b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917554"
---
# <a name="property-object-ado"></a>Property オブジェクト (ADO)
プロバイダーによって定義されている ADO オブジェクトの動的な特性を表します。  
  
## <a name="remarks"></a>コメント  
 ADO オブジェクトは、2 種類のプロパティを設定します。 組み込みおよび動的な。  
  
 組み込みのプロパティは、これらのプロパティを ADO では実装されていると、すぐに利用できる、新しいオブジェクトを使用して、`MyObject.Property`構文。 として表示されない**プロパティ**オブジェクトの内のオブジェクト[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション、ため、その値を変更できますが、その特性を変更することはできません。  
  
 動的プロパティは、基になるデータ プロバイダーによって定義されているし、に表示されます、**プロパティ**適切な ADO オブジェクトのコレクション。 場合など、プロバイダー固有のプロパティを示す可能性があります、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトは、トランザクションや更新をサポートしています。 これらの追加プロパティは、として表示されます**プロパティ**オブジェクト**レコード セット**オブジェクトの**プロパティ**コレクション。 動的プロパティを参照するには、コレクションを介してのみを使用して、`MyObject.Properties(0)`または`MyObject.Properties("Name")`構文。  
  
 プロパティのいずれかの種類を削除することはできません。  
  
 動的な**プロパティ**オブジェクトが、独自の 4 つの組み込みプロパティ。  
  
-   [名前](../../../ado/reference/ado-api/name-property-ado.md)プロパティは、プロパティを識別する文字列。  
  
-   [型](../../../ado/reference/ado-api/type-property-ado.md)プロパティは、プロパティのデータ型を指定する整数。  
  
-   [値](../../../ado/reference/ado-api/value-property-ado.md)プロパティは、プロパティの設定を含んでいるバリアント。 **値**の既定のプロパティは、**プロパティ**オブジェクト。  
  
-   [属性](../../../ado/reference/ado-api/attributes-property-ado.md)プロパティは、プロバイダーに固有のプロパティの特性を示す long 値。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Property オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [コマンド オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
