---
title: LTRIM (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- leading blanks
- LTRIM function
ms.assetid: d082f42a-d7e7-49f5-a503-ac44ba630832
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 541531de470991c84d04a60d6829e3333c78ae3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62897499"
---
# <a name="ltrim-ssis-expression"></a>LTRIM (SSIS 式)
  先頭のスペースを削除した後の文字式を返します。  
  
> [!NOTE]  
>  LTRIM では、タブや改行文字などの空白文字は削除されません。 Unicode には各種スペースを表すコード ポイントが用意されていますが、この関数では Unicode コード ポイント 0x0020 のみが認識されます。 Unicode に変換される 2 バイト文字セット (DBCS) の文字列には、0x0020 以外のスペース文字が含まれる場合があり、このようなスペースはこの関数で削除できません。 すべての種類のスペースを削除するには、スクリプト コンポーネントから実行するスクリプト内で、Microsoft Visual Basic .NET の LTrim メソッドを使用できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
LTRIM(character expression)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 スペースを削除する対象となる文字式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>コメント  
 LTRIM は、DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、LTRIM による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳しくは、「[Integration Services のデータ型](../data-flow/integration-services-data-types.md)」および「[Cast &#40;SSIS 式&#41;](cast-ssis-expression.md)」をご覧ください。  
  
 引数が NULL の場合、LTRIM は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例では、文字列リテラルから先頭のスペースが削除されます。 返される結果は "Hello" です。  
  
```  
LTRIM("    Hello")  
```  
  
 この例では、 **FirstName** 列から先頭のスペースが削除されます。  
  
```  
LTRIM(FirstName)  
```  
  
 この例では、 **FirstName** 変数から先頭のスペースが削除されます。  
  
```  
LTRIM(@FirstName)  
```  
  
## <a name="see-also"></a>参照  
 [RTRIM &#40;SSIS 式&#41;](trim-ssis-expression.md)   
 [TRIM &#40;SSIS 式&#41;](trim-ssis-expression.md)   
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
