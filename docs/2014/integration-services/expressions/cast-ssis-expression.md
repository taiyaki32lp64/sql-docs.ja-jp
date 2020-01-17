---
title: Cast (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CAST function
- cast operator
- converting data types [Integration Services]
- data types [Integration Services], expressions
- data types [Integration Services], converting
ms.assetid: d4e915cc-1c7b-4b2e-93b0-13a8b0cb9242
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6549e2ad8faca23e32621e1cc871a62870c9effb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62899040"
---
# <a name="cast-ssis-expression"></a>Cast (SSIS 式)
  式のあるデータ型を別のデータ型に明示的に変換します。 キャスト演算子は、切り捨て演算子としても機能できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
(type_spec) expression  
  
```  
  
## <a name="arguments"></a>引数  
 *type_spec*  
 有効な [!INCLUDE[ssIS](../../includes/ssis-md.md)] データ型です。  
  
 *式 (expression)*  
 有効な式です。  
  
## <a name="result-types"></a>戻り値の型  
 *type_spec*のデータ型です。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="remarks"></a>コメント  
 次の図は、有効なキャスト演算を示しています。  
  
 ![データ型間の有効および無効なキャスト](../media/data-conversion.gif "データ型間の有効および無効なキャスト")  
  
 一部のデータ型にキャストする場合、パラメーターが必要となります。 次の表に、パラメーターが必要なデータ型とそのパラメーターの一覧を示します。  
  
|データ型|パラメーター|例|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252) は、1252 コード ページを使用して、30 バイトまたは 30 文字を DT_STR データ型にキャストします。|  
|DT_WSTR|*Charcount*|(DT_WSTR,20) は、20 バイト ペアまたは 20 Unicode 文字を DT_WSTR データ型にキャストします。|  
|DT_BYTES|*Bytecount*|(DT_BYTES,50) は、50 バイトを DT_BYTES データ型にキャストします。|  
|DT_DECIMAL|*Scale*|(DT_DECIMAL,2) は、数値を小数点以下 2 桁の DT_DECIMAL データ型にキャストします。|  
|DT_NUMERIC|*有効桁数*<br /><br /> *Scale*|(DT_NUMERIC,10,3) は、数値を有効桁数 10 桁で小数点以下 3 桁の DT_NUMERIC データ型にキャストします。|  
|DT_TEXT|*Codepage*|(DT_TEXT,1252) は、1252 コード ページを使用して、値を DT_TEXT データ型にキャストします。|  
  
 文字列を DT_DATE にキャストする場合、またはその逆のキャストを行う場合、変換のロケールが使用されます。 ただし、ロケール設定で ISO 形式を使用するかどうかにかかわらず、日付は YYYY-MM-DD の ISO 形式となります。  
  
> [!NOTE]  
>  文字列を DT_DATE 以外の日付データ型に変換するには、「 [Integration Services のデータ型](../data-flow/integration-services-data-types.md)」を参照してください。  
  
 コード ページがマルチバイト文字の場合、バイト数と文字数は異なる場合があります。 DT_WSTR データ型から同じ *charcount* 値の DT_STR データ型にキャストすると、変換された文字列で最後の文字が切り捨てられる場合があります。 変換先のテーブルの列で十分なストレージが使用できる場合、 *charcount* パラメーターの値は、マルチバイト コード ページで必要となるバイト数を反映するように設定します。 たとえば、936 コード ページを使用して、文字データを DT_STR データ型にキャストする場合、データに含まれると考えられる文字数の 2 倍の値を *charcount* に設定する必要があります。また、UTF-8 コード ページを使用して文字データをキャストする場合、 *charcount* は、予想される文字数の 4 倍の値に設定する必要があります。  
  
 日付データ型の構造の詳細については、「 [Integration Services のデータ型](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="ssis-expression-examples"></a>SSIS 式の例  
 この例では、数値を整数にキャストします。  
  
```  
(DT_I4) 3.57  
```  
  
 この例では、1252 コード ページを使用して整数を文字列にキャストします。  
  
```  
(DT_STR,1,1252)5  
```  
  
 この例では、3 文字の文字列を 2 バイト文字にキャストします。  
  
```  
(DT_WSTR,3)"Cat"  
```  
  
 この例では、整数を小数点以下 2 桁の 10 進数にキャストします。  
  
```  
(DT_DECIMAl,2)500  
```  
  
 この例では、整数を有効桁数 7 桁で小数点以下 3 桁の数値にキャストします。  
  
```  
(DT_NUMERIC,7,3)4000  
```  
  
 この例では、 **nvarchar** データ型で定義され、長さが 50 の **FirstName** 列の値を、1252 コード ページを使用して文字列にキャストします。  
  
```  
(DT_STR,50,1252)FirstName  
```  
  
 この例では、DT_DBDATE 型の **DateFirstPurchase** 列の値を、長さ 20 の Unicode 文字列にキャストします。  
  
```  
(DT_WSTR,20)DateFirstPurchase  
```  
  
 この例は、文字リテラル "True" をブール型にキャストします。  
  
```  
(DT_BOOL)"True"  
```  
  
 この例では、文字列リテラルを DT_DBDATE にキャストします。  
  
```  
(DT_DBDATE) "1999-10-11"  
```  
  
 この例では、秒の小数部に 5 桁を使用する DT_DBTIME2 データ型に文字列リテラルをキャストします (DT_DBTIME2 データ型では、秒の小数部に 0 ～ 7 桁まで指定できます)。  
  
```  
(DT_DBTIME2, 5) "16:34:52.12345"  
```  
  
 この例では、秒の小数部に 4 桁を使用する DT_DBTIMESTAMP2 データ型に文字列リテラルをキャストします (DT_DBTIMESTAMP2 データ型では、秒の小数部に 0 ～ 7 桁まで指定できます)。  
  
```  
(DT_DBTIMESTAMP2, 4) "1999-10-11 16:34:52.1234"  
```  
  
 この例では、秒の小数部に 7 桁を使用する DT_DBTIMESTAMPOFFSET データ型に文字列リテラルをキャストします (DT_DBTIMESTAMPOFFSET データ型では、秒の小数部に 0 ～ 7 桁まで指定できます)。  
  
```  
(DT_DBTIMESTAMPOFFSET, 7) "1999-10-11 16:34:52.1234567 + 5:35"  
```  
  
## <a name="see-also"></a>参照  
 [演算子の優先順位と結合規則](operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](operators-ssis-expression.md)   
 [Integration Services &#40;SSIS&#41; 式](integration-services-ssis-expressions.md)   
 [式における Integration Services データ型](integration-services-data-types-in-expressions.md)  
  
  
