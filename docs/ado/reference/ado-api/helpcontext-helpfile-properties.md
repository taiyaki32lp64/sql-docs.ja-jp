---
title: HelpContext、HelpFile プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetHelpContext
- Error::GetHelpFile
- Error::get_HelpFile
- Error::get_HelpContext
- Error::HelpContext
- Error::HelpFile
helpviewer_keywords:
- HelpContext property [ADO]
- HelpFile property [ADO]
ms.assetid: 2b9ef441-993c-44d4-8f87-fac0979dac1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba441a52958e423308e648f15dd36e14d6d1d895
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918478"
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext、HelpFile プロパティ
ヘルプ ファイルと関連付けられているトピックを示します、[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。  
  
## <a name="return-values"></a>戻り値  
  
-   **ヘルプ コンテキスト Id**として、コンテキスト ID を返します、**長い**トピックでは、ヘルプ ファイル内の値。  
  
-   **HelpFile**返します、**文字列**ヘルプ ファイルへの完全に解決されたパスに評価される値。  
  
## <a name="remarks"></a>コメント  
 ヘルプ ファイルがで指定されている場合、 **HelpFile**プロパティ、 **HelpContext**プロパティが自動的に識別するヘルプ トピックを表示するために使用します。 使用可能な関連するヘルプ トピックがない場合、 **HelpContext**プロパティは 0 を返します、 **HelpFile**プロパティは、長さ 0 の文字列を返します ("")。  
  
## <a name="applies-to"></a>適用対象  
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>参照  
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (vc++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description プロパティ](../../../ado/reference/ado-api/description-property.md)   
 [Number プロパティ (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source プロパティ (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
