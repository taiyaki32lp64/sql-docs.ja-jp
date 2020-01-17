---
title: TOKENCOUNT (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c0efed1-c2b3-4f20-a3a1-ad91283b7c0a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0fd9c3a09bf5e901591b2837fcd163534db5f52c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71288149"
---
# <a name="tokencount-ssis-expression"></a>TOKENCOUNT (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  指定された区切り記号で区切られたトークンを含んでいる文字列内のトークン数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
TOKENCOUNT(character_expression, delimiter_string)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 区切り記号で区切られたトークンを含む文字列です。  
  
 *delimiter_string*  
 区切り記号を含む文字列です。 たとえば、"; ," には 3 つの区切り記号 (セミコロン、空白、コンマ) が含まれています。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 TOKEN 関数には次の解説が適用されます。  
  
-   区切り記号には 1 つ以上の区切り文字を含めることができます。  
  
-   先頭の区切り記号はスキップされます。  
  
-   TOKENCOUNT は、DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、TOKEN による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。  
  
-   character_expression が NULL の場合、TOKENCOUNT は 0 (ゼロ) を返します。  
  
-   この式の引数として、変数と列を使用できます。  
  
## <a name="expression-examples"></a>式の例  
 次の例では、TOKENCOUNT 関数は 3 を返します。これは、文字列に 3 つのトークン ("01"、"12"、および "2011") が含まれているためです。  
  
```  
TOKENCOUNT("01/12/2011", "/")  
```  
  
 次の例では、TOKENCOUNT 関数は 4 を返します。これは、文字列に 4 つのトークン ("a"、"little"、"white"、および "dog") が含まれているためです。  
  
```  
TOKENCOUNT("a little white dog"," ")  
```  
  
 次の例では、TOKENCOUNT 関数は 1 を返します。 関数は区切り記号に対応する入力文字列を解析しますが、文字列には区切り記号が含まれていないため、文字列全体を最初のトークンとして加算します。  
  
```  
TOKENCOUNT("a little white dog","|")  
```  
  
 次の例では、TOKENCOUNT 関数は 4 を返します。 この例では、5 つの区切り記号が指定されています。 入力文字列には 4 つのトークン ("a"、"little"、"white"、および "dog") が含まれています。  
  
```  
TOKENCOUNT("a:little|white dog","| ,.:")  
```  
  
 次の例では、TOKENCOUNT 関数は 4 を返します。 先頭の空白文字はすべて無視されます。  
  
```  
TOKENCOUNT("        a little white dog", " ")  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
