---
title: Instr (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 201580b71086dfe39e669966070dae2dca72e3eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105303"
---
# <a name="instr-mdx"></a>Instr (MDX)


  別の 1 つの文字列の最初に見つかった位置を返します。  
  
## <a name="syntax"></a>構文  
  
```  
InStr([start, ]searched_string, search_string[, compare])  
```  
  
## <a name="arguments"></a>引数  
 *start*  
 (省略可能)各検索の開始位置を設定する数値式。 この値を省略すると、最初の文字位置から検索を開始します。 start が null の場合、関数の戻り値は未定義となります。  
  
 *searched_string*  
 検索する文字列式です。  
  
 *search_string*  
 文字列式を検索します。  
  
 *Compare*  
 (省略可) 整数値です。 この引数は常に無視されます。 その他の互換性のために定義されている**Instr**他の言語で機能します。  
  
## <a name="return-value"></a>戻り値  
 開始位置を表す整数値*String2*で*String1*します。  
  
 また、 **InStr**関数は、条件に応じて次の表に記載した値を返します。  
  
|条件|戻り値|  
|---------------|------------------|  
|String1 の長さが 0|ゼロ (0)|  
|String1 が NULL|未定義|  
|String2 が長さ 0|start|  
|String2 が NULL|未定義|  
|String2 が見つからない|ゼロ (0)|  
|start が len (string2) よりも大きい|ゼロ (0)|  
  
## <a name="remarks"></a>コメント  
  
> [!WARNING]  
>  **Instr**常に大文字と小文字を実行します。  
  
## <a name="example"></a>例  
 次の例では、使用状況、 **Instr**関数を示すさまざまなシナリオが発生します。  
  
```  
with   
    member [Date].[Date].[Results] as "Results"  
    member measures.[lowercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[uppercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "O")  
    member measures.[searched string is empty]            as InStr( "", "o")  
    member measures.[searched string is null]             as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[search string is empty]              as InStr( "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is empty start 10]     as InStr(10, "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is null]               as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[found from start 10]                 as InStr( 10, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NOT found from start 17]             as InStr( 17, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NULL start]                          as iif(IsError(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Error", iif(IsNull(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Null","Is undefined"))  
    member measures.[start greater than searched length]  as InStr( 170, "abcdefghijklmnñopqrstuvwxyz", "o")  
  
select  [Results] on columns,  
       { measures.[lowercase found in lowercase string]  
       , measures.[uppercase found in lowercase string]  
       , measures.[searched string is empty]  
       , measures.[searched string is null]  
       , measures.[search string is empty]  
       , measures.[search string is empty start 10]  
       , measures.[search string is null]  
       , measures.[found from start 10]  
       , measures.[NOT found from start 17]  
       , measures.[NULL start]   
       , measures.[start greater than searched length]  
       } on rows  
  
from [Adventure Works]  
```  
  
 取得した結果を次の表に示します。  
  
|||  
|-|-|  
||[結果]|  
|小文字の文字列で小文字を検索|16|  
|大文字を小文字の文字列で検索します。|16|  
|検索した文字列が空|0|  
|検索した文字列が null|未定義|  
|検索文字列が空|1|  
|検索する文字列が開始位置 10 から空|10|  
|検索する文字列が NULL|未定義|  
|開始位置 10 から検索|16|  
|開始位置 17 からが見つかりません|0|  
|NULL で開始|未定義|  
|検索した長さを超えて開始します。|0|  
  
  
