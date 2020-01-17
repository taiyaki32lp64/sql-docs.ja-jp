---
title: 関数 (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- expressions [Integration Services], functions
- string functions
- SQL Server Integration Services, functions
- SSIS, functions
ms.assetid: e9a41a31-94f4-46a4-b737-c707dd59ce48
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a271b9dd9da2a4b21040a89145d9f2ab1fe84b68
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297590"
---
# <a name="functions-ssis-expression"></a>関数 (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  式言語には、式で使用するための関数セットが含まれています。 式で 1 つの関数を使用することもできますが、通常、式は関数と演算子を組み合わせて使用したり、複数の関数を使用します。  
  
 関数は、次の各グループに分類されます。  
  
-   数学関数。パラメーターとして渡された数値型の入力値に基づいて計算を実行し、数値を返します。  
  
-   文字列関数。文字列型または 16 進数の入力値に対して操作を実行し、文字列値または数値を返します。  
  
-   日付関数および時刻関数。日時の値に対して操作を実行し、文字列、数値、または日時の値を返します。  
  
-   システム関数。式に関する情報を返します。  
  
 式言語には、次の数学関数が用意されています。  
  
|機能|[説明]|  
|--------------|-----------------|  
|[ABS &#40;SSIS 式&#41;](../../integration-services/expressions/abs-ssis-expression.md)|数値式の正の絶対値を返します。|  
|[EXP &#40;SSIS 式&#41;](../../integration-services/expressions/exp-ssis-expression.md)|指定した式の e を基数とする指数を返します。|  
|[CEILING &#40;SSIS 式&#41;](../../integration-services/expressions/ceiling-ssis-expression.md)|数値式以上で最小の整数値を返します。|  
|[FLOOR &#40;SSIS 式&#41;](../../integration-services/expressions/floor-ssis-expression.md)|数値式以下で最大の整数を返します。|  
|[LN &#40;SSIS 式&#41;](../../integration-services/expressions/ln-ssis-expression.md)|数値式の自然対数を返します。|  
|[LOG &#40;SSIS 式&#41;](../../integration-services/expressions/log-ssis-expression.md)|数値式の常用対数を返します。|  
|[POWER &#40;SSIS 式&#41;](../../integration-services/expressions/power-ssis-expression.md)|指定された数値式の結果をべき乗値で返します。|  
|[ROUND &#40;SSIS 式&#41;](../../integration-services/expressions/round-ssis-expression.md)|指定された長さまたは有効桁数に丸めた数値式を返します。 。|  
|[SIGN &#40;SSIS 式&#41;](../../integration-services/expressions/sign-ssis-expression.md)|数値式の符号として正 (+)、負 (-)、ゼロ (0) のいずれかを返します。|  
|[SQUARE &#40;SSIS 式&#41;](../../integration-services/expressions/square-ssis-expression.md)|数値式の 2 乗値を返します。|  
|[SQRT &#40;SSIS 式&#41;](../../integration-services/expressions/sqrt-ssis-expression.md)|数値式の平方根を返します。|  
  
 式エバリュエーターには、次の文字列関数が用意されています。  
  
|機能|[説明]|  
|--------------|-----------------|  
|[CODEPOINT &#40;SSIS 式&#41;](../../integration-services/expressions/codepoint-ssis-expression.md)|文字式の左端の文字の Unicode コード値を返します。|  
|[FINDSTRING &#40;SSIS 式&#41;](../../integration-services/expressions/findstring-ssis-expression.md)|文字式内のある文字列が指定回数目に検出された場所を、1 を基点とするインデックスで返します。|  
|[HEX &#40;SSIS 式&#41;](../../integration-services/expressions/hex-ssis-expression.md)|整数の 16 進値を表す文字列を返します。|  
|[LEN &#40;SSIS 式&#41;](../../integration-services/expressions/len-ssis-expression.md)|文字式の文字数を返します。|  
|[LEFT &#40;SSIS 式&#41;](../../integration-services/expressions/left-ssis-expression.md)|指定された文字式の一番左の部分から指定された数の文字を返します。|  
|[LOWER &#40;SSIS 式&#41;](../../integration-services/expressions/lower-ssis-expression.md)|大文字が小文字に変換された状態の文字式を返します。|  
|[LTRIM &#40;SSIS 式&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)|先頭のスペースを削除した後の文字式を返します。|  
|[REPLACE &#40;SSIS &#41;](../../integration-services/expressions/replace-ssis-expression.md)|式に含まれている文字列を別の文字列または空の文字列で置き換えた文字式を返します。|  
|[REPLICATE &#40;SSIS 式&#41;](../../integration-services/expressions/replicate-ssis-expression.md)|指定された回数だけレプリケートされた文字式を返します。|  
|[REVERSE &#40;SSIS 式&#41;](../../integration-services/expressions/reverse-ssis-expression.md)|文字式を逆に並べ替えたものを返します。|  
|[RIGHT &#40;SSIS 式&#41;](../../integration-services/expressions/right-ssis-expression.md)|指定された文字式の一番右の部分から指定された数の文字を返します。|  
|[RTRIM &#40;SSIS 式&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)|末尾のスペースを削除した後の文字式を返します。|  
|[SUBSTRING &#40;SSIS 式&#41;](../../integration-services/expressions/substring-ssis-expression.md)|文字式の一部を返します。|  
|[TRIM &#40;SSIS 式&#41;](../../integration-services/expressions/trim-ssis-expression.md)|先頭および末尾のスペースを削除した後の文字式を返します。|  
|[UPPER &#40;SSIS 式&#41;](../../integration-services/expressions/upper-ssis-expression.md)|小文字が大文字に変換された状態の文字式を返します。|  
  
 式エバリュエーターには、次の日付と時刻関数が用意されています。  
  
|機能|[説明]|  
|--------------|-----------------|  
|[DATEADD &#40;SSIS 式&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)|指定された日付に日付または期間を加えて、新しい DT_DBTIMESTAMP 値を返します。|  
|[DATEDIFF &#40;SSIS 式&#41;](../../integration-services/expressions/datediff-ssis-expression.md)|指定された 2 つの日付間の差を、日付および時刻の単位で返します。|  
|[DATEPART &#40;SSIS 式&#41;](../../integration-services/expressions/datepart-ssis-expression.md)|ある日付の、特定の日付要素を整数で返します。|  
|[DAY &#40;SSIS 式&#41;](../../integration-services/expressions/day-ssis-expression.md)|指定された日付の日を整数で返します。|  
|[GETDATE &#40;SSIS 式&#41;](../../integration-services/expressions/getdate-ssis-expression.md)|システムの現在の日付を返します。|  
|[GETUTCDATE &#40;SSIS 式&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)|システムの現在の日付を UTC 時刻 (協定世界時またはグリニッジ標準時) で返します。|  
|[MONTH &#40;SSIS 式&#41;](../../integration-services/expressions/month-ssis-expression.md)|指定された日付の月を表す整数を返します。|  
|[YEAR &#40;SSIS 式&#41;](../../integration-services/expressions/year-ssis-expression.md)|指定された日付の年を表す整数を返します。|  
  
 式エバリュエーターには、次の NULL 関数が用意されています。  
  
|機能|[説明]|  
|--------------|-----------------|  
|[ISNULL &#40;SSIS 式&#41;](../../integration-services/expressions/isnull-ssis-expression.md)|式が NULL かどうかに基づいてブール型の結果を返します。|  
|[NULL &#40;SSIS 式&#41;](../../integration-services/expressions/null-ssis-expression.md)|要求されたデータ型の NULL 値を返します。|  
  
 式の名前は大文字で表示されますが、大文字と小文字は区別されません。 たとえば、"null" は "NULL" を使用した場合と同様に機能します。  
  
## <a name="see-also"></a>参照  
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)   
 [Integration Services 式の詳細の例](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Integration Services &#40;SSIS&#41; 式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
