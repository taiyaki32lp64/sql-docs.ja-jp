---
title: プロパティの説明 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48b3a6987e6c7b6c3754f5041d90d248520345ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933087"
---
# <a name="description-property"></a>Description プロパティ
について説明します、[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 返します、**文字列**エラーの説明を表す値です。  
  
## <a name="remarks"></a>コメント  
 使用して、**説明**プロパティをエラーの簡単な説明を取得します。 ユーザーができない場合や、処理したくないエラーのアラートを生成するには、このプロパティを表示します。 文字列は、ADO またはプロバイダーから提供されます。  
  
 プロバイダーは、ADO に特定のエラー テキストを渡す責任を負います。 ADO の追加、[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクトを**エラー**コレクション プロバイダーごとにエラーまたは警告を受信します。 列挙、**エラー**プロバイダーに渡されるエラーをトレースするコレクション。  
  
## <a name="applies-to"></a>適用対象  
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>参照  
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、NativeError、数、ソース、および SQLState プロパティの例 (vc++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext、HelpFile プロパティ](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number プロパティ (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source プロパティ (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
