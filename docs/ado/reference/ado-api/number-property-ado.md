---
title: Number プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce027747c843e02998f4845db7075e70cf8733b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917996"
---
# <a name="number-property-ado"></a>Number プロパティ (ADO)
一意に識別する番号を示します、[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 返します、**長い**値のいずれかに対応している可能性がありますが、 [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)定数。  
  
## <a name="remarks"></a>コメント  
 使用して、**数**プロパティのエラーが発生しました。 プロパティの値は、エラー状態に対応する一意の番号です。  
  
 [エラー](../../../ado/reference/ado-api/errors-collection-ado.md)コレクションは、16 進数形式 (たとえば、0x80004005) または long 型の値 (たとえば、: 2147467259) のいずれかの HRESULT を返します。 これらの Hresult は、OLE DB または自体でも OLE などの基になるコンポーネントで生成されます。 これらの番号の詳細については、次を参照してください。[エラー (OLE DB)](https://msdn.microsoft.com/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd)で、 [OLE DB プログラマーズ リファレンス](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)*します。*  
  
## <a name="applies-to"></a>適用対象  
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>参照  
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (vc++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description プロパティ](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext、HelpFile プロパティ](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Source プロパティ (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
