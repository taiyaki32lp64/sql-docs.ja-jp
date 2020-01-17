---
title: TOKEN (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9fdd06bf-5bc9-445c-95bf-709e0ca5989b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af82c187fce638ddd1f28ab98a5109898f7cad25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768708"
---
# <a name="token--ssis-expression"></a>TOKEN (SSIS 式)
  文字列内のトークンを区切る指定された区切り記号、および返されるトークンを表すトークン数に基づいて、文字列からトークン (サブストリング) を返します。  
  
## <a name="syntax"></a>構文  
  
```  
TOKEN(character_expression, delimiter_string, occurrence)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 区切り記号で区切られたトークンを含む文字列です。  
  
 *delimiter_string*  
 区切り記号を含む文字列です。 たとえば、"; ," には 3 つの区切り記号 (セミコロン、空白、コンマ) が含まれています。  
  
 *occurrence*  
 返されるトークンを指定する符号付きまたは符号なし整数。 たとえば、このパラメーターの値として 3 を指定すると、文字列内の 3 番目のトークンが返されます。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>コメント  
 この関数は、<character_expression> 文字列を <delimiter_string> で指定された区切り記号で区切ったトークンのセットに分割した後、N 番目のトークンを返します。N は\<occurrence> パラメーターで指定されたトークンの発生回数です。 この関数のサンプルについては、「使用例」のセクションを参照してください。  
  
 TOKEN 関数には次の解説が適用されます。  
  
-   区切り記号には 1 つ以上の区切り文字を含めることができます。  
  
-   \<occurrence> パラメーターの値が文字列内のトークンの合計数より大きい場合、この関数は NULL を返します。  
  
-   先頭の区切り記号はスキップされます。  
  
-   TOKEN は、DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、TOKEN による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。  
  
-   character_expression が NULL の場合、TOKEN は NULL を返します。  
  
-   式のすべての引数で、変数および列を値として使用できます。  
  
## <a name="expression-examples"></a>式の例  
 次の例では、TOKEN 関数は "a" を返します。 文字列 "a little white dog" には、区切り記号 " " (空白文字) で区切られた 4 つのトークン、"a"、"little"、"white"、"dog" があります。 2 番目の引数である区切り記号は、入力文字列をトークンに分割するときに使用される 1 つの区切り記号 (空白文字) のみを指定します。 最後の引数である 1 は、返される最初のトークンを指定します。 この文字列のサンプルでは、最初のトークンは "a" です。  
  
```  
TOKEN("a little white dog"," ",1)  
```  
  
 次の例では、TOKEN 関数は "dog" を返します。 この例では、5 つの区切り記号が指定されています。 入力文字列には 4 つのトークン ("a"、"little"、"white"、および "dog") が含まれています。  
  
```  
TOKEN("a:little|white dog","| ,.:",4)  
```  
  
 次の例では、TOKEN 関数は "" (空の文字列） を返します。これは、文字列に 99 のトークンがないためです。  
  
```  
TOKEN("a little white dog"," ",99)  
```  
  
 次の例では、TOKEN 関数は完全な文字列を返します。 関数は区切り記号に対応する入力文字列を解析しますが、文字列には区切り記号が含まれていないため、文字列全体を最初のトークンとして加算します。  
  
```  
TOKEN("a little white dog","|",1)  
```  
  
 次の例では、TOKEN 関数は "a" を返します。 先頭の空白文字はすべて無視されます。  
  
```  
TOKEN("        a little white dog", " ", 1)  
```  
  
 次の例では、TOKEN 関数は日付文字列から年を返します。  
  
```  
TOKEN("2009/01/01", "/"), 1  
```  
  
 次の例では、TOKEN 関数は指定されたパスからファイル名を返します。 たとえば、User::Path の値が "c:\program files files\data\myfile.txt" の場合、TOKEN 関数は "myfile.txt" を返します。 TOKENCOUNT 関数は 4 を返し、TOKEN 関数は 4 番目のトークン "myfile.txt" を返します。  
  
```  
TOKEN(@[User::Path], "\\", TOKENCOUNT(@[User::Path], "\\"))  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
