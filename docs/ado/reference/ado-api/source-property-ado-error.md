---
title: ソースのプロパティ (ADO Error) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b55ebbe5a167b7d70cf606fc4e37e7ede36b486
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916900"
---
# <a name="source-property-ado-error"></a>Source プロパティ (ADO Error)
オブジェクトまたはアプリケーション エラーの発生源の名前を示します。  
  
## <a name="return-value"></a>戻り値  
 返します、**文字列**オブジェクトまたはアプリケーションの名前を示す値。  
  
## <a name="remarks"></a>コメント  
 使用して、**ソース**プロパティを[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクトまたはアプリケーション エラーの発生源の名前を決定するオブジェクト。 これは、オブジェクトのクラス名またはプログラム id です。 Ado エラーは、プロパティ値に**ADODB** 。_ObjectName_ここで、 *ObjectName*エラーを発生させたオブジェクトの名前を指定します。 ADOX と ADO MD の場合は、値になります**ADOX** 。_ObjectName_と**ADOMD** 。_ObjectName_、それぞれします。  
  
 エラー ドキュメントに基づく、**ソース**、[数](../../../ado/reference/ado-api/number-property-ado.md)、および[説明](../../../ado/reference/ado-api/description-property.md)プロパティの**エラー**オブジェクトの場合、コードを記述することができますエラーが適切に処理するされます。  
  
 **ソース**プロパティは読み取り専用の**エラー**オブジェクト。  
  
## <a name="applies-to"></a>適用対象  
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>参照  
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (vc++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description プロパティ](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext、HelpFile プロパティ](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number プロパティ (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source プロパティ (ADO Record)](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source プロパティ (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
