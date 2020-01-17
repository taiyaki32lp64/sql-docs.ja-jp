---
title: Name プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a919bb377eee2da1c3c1a65e85ddfb9807ed8d50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918036"
---
# <a name="name-property-ado"></a>Name プロパティ (ADO)
オブジェクトの名前を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**文字列**オブジェクトの名前を示す値。  
  
## <a name="remarks"></a>コメント  
 使用して、**名前**に名前を割り当てるまたはの名前を取得するプロパティを**コマンド**、**プロパティ**、**フィールド**、または**パラメーター**オブジェクト。  
  
 読み取り/書き込みするには、値、**コマンド**オブジェクトおよび読み取り専用で、**プロパティ**オブジェクト。  
  
 **フィールド**オブジェクト、**名前**は通常読み取り専用です。 ただし、新規の**フィールド**に追加されたオブジェクト、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)のコレクションを[レコード](../../../ado/reference/ado-api/record-object-ado.md)、**名前**は読み取り/書き込みにした場合のみ[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティを**フィールド**が指定されているデータ プロバイダーからその新しいが正常に追加し、**フィールド**呼び出すことによって、 [Update](../../../ado/reference/ado-api/update-method.md)のメソッド、**フィールド**コレクション。  
  
 **パラメーター**にオブジェクトが追加されていない、[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md) 、コレクション、**名前**読み取り/書き込みプロパティです。 追加の**パラメーター**オブジェクトとその他のすべてのオブジェクト、**名前**プロパティは読み取り専用です。 名は、コレクション内で一意である必要はありません。  
  
 取得することができます、**名前**名前で直接その後、オブジェクトを参照できます、序数参照によってオブジェクトのプロパティ。 たとえば場合、`rstMain.Properties(20).Name`生成`Updatability`、としてこのプロパティを後で参照できます`rstMain.Properties("Updatability")`します。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Field オブジェクト](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter オブジェクト](../../../ado/reference/ado-api/parameter-object.md)|[Property オブジェクト (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>関連項目  
 [属性と Name プロパティの例 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [属性と Name プロパティの例 (vc++)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
