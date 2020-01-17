---
title: スカラー関数の呼び出し |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 37209a75c03a051e3def4d26fa0d4e7f85d0e91d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897746"
---
# <a name="scalar-function-calls"></a>スカラー関数の呼び出し
スカラー関数は、各行の値を返します。 たとえば、絶対値のスカラー関数は数値の列を引数として受け取りと、列の各値の絶対値を返します。 スカラー関数を呼び出すためのエスケープ シーケンスは、します。  
  
 **{fn** _スカラー関数_ **}**  
  
 ここで、*スカラー関数* は、[付録 e:スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md) ににリストされている関数の1つです。 スカラー関数のエスケープ シーケンスの詳細については、付録C：SQL文法の [スカラー関数エスケープ シーケンス](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) を参照してください。SQL 文法。  
  
 たとえば、次の SQL ステートメントは、名前、同じ結果セットの大文字の顧客の作成します。 最初のステートメントでは、エスケープ シーケンス構文を使用します。 2 番目のステートメントでは、OS/2 の Ingres のネイティブの構文を使用して、相互運用可能なではありません。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 アプリケーションは、ネイティブの構文を使用するスカラー関数の呼び出しと ODBC 構文を使用するスカラー関数の呼び出しに混在させることができます。 たとえば、姓、コンマ、および最初の名前として、従業員テーブル内の名前が格納されていることを想定しています。 次の SQL ステートメントでは、Employee テーブルに従業員の姓の結果セットを作成します。 ステートメントは、ODBC スカラー関数を使用して**SUBSTRING**と SQL Server のスカラー関数**CHARINDEX**と SQL Server でのみ正しく実行されます。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 相互運用性を最大に、アプリケーションを使用する必要があります、**CONVERT**スカラー関数、スカラー関数の出力が必要な型であることを確認します。 **CONVERT**関数は、1 つの SQL データ型のデータを指定した SQL データ型に変換します。 構文、**CONVERT**関数  
  
 **CONVERT (** _value_exp_ **、** _data_type_ **)**  
  
 場所*value_exp*列名、もう 1 つのスカラー関数、または、リテラル値の結果と*data_type*と一致するキーワード、 **#define**によって使用される名前、定義されている、SQL データ型識別子[付録 d:データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)します。 たとえば、次の SQL ステートメントを使用して、**CONVERT**ことを確認する関数の出力、 **CURDATE**関数は、タイムスタンプ列または文字データではなく、日付。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 データ ソースがサポートするスカラー関数を決定するには、アプリケーションを呼び出す**SQLGetInfo** SQL_CONVERT_FUNCTIONS、SQL_NUMERIC_FUNCTIONS、SQL_STRING_FUNCTIONS、SQL_SYSTEM_FUNCTIONS、SQL_TIMEDATE_ と関数のオプションです。 サポートされる変換操作を決定する、**CONVERT**関数の場合、アプリケーションを呼び出す**SQLGetInfo** SQL_CONVERT でを起動するオプションのいずれかにします。
