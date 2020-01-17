---
title: 名前空間の uri-から-QName (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 96edefd5409520109e2b2155507dd8879ed4b0d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946635"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>QNames に関係する関数 - namespace-uri-from-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  指定された QName の名前空間 uri を表す文字列を返します *$arg*します。 場合、結果は空のシーケンス *$arg*は空のシーケンスです。  
  
## <a name="syntax"></a>構文  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 名前空間 URI が返される QName です。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. QName からの名前空間 URI の取得  
 実際のサンプルでは、次を参照してください。 [QName のローカル名&#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md)します。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   **Namespace-uri-from-QName()** 関数は、xs:anyURI ではなく xs:string のインスタンスを返します。  
  
## <a name="see-also"></a>参照  
 [QNames に関係する関数&#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
