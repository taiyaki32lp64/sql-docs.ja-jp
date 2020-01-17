---
title: プロシージャのパラメーター |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f85512a1686df26cad739dc906e49cc5499f62e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912303"
---
# <a name="procedure-parameters"></a>プロシージャのパラメーター
プロシージャ呼び出しのパラメーター入力として使用できる、入力/出力、または出力パラメーター。 これは、すべての他の SQL ステートメントで、入力パラメーターでは常にパラメーターと異なります。  
  
 プロシージャに値を送信する入力パラメーターが使用されます。 たとえば、部品テーブルに PartID、説明、および価格の列があるとします。 InsertPart プロシージャ、テーブル内の各列の入力パラメーターがあります。 例:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 ドライバーはまで入力バッファーの内容を変更しないでください**SQLExecDirect**または**SQLExecute** SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または sql_no_data が返されます。 入力バッファーの内容を変更しないでください、 **SQLExecDirect**または**SQLExecute** SQL_STILL_EXECUTING SQL_NEED_DATA を返します。  
  
 入力/出力パラメーターは、プロシージャに値を送信し、プロシージャから値を取得の両方に使用されます。 入力と出力パラメーターの両方として、同じパラメーターを使用して、混乱になる傾向があります、避ける必要があります。 たとえば、手順は、注文 ID を受け入れるし、顧客の ID を返します。 これは、1 つの入力/出力パラメーターを定義できます。  
  
```  
{call GetCustID(?)}  
```  
  
 2 つのパラメーターを使用する方がよいことが考えられます: 注文 ID と出力または顧客の ID の入力/出力パラメーターの入力パラメーター。  
  
```  
{call GetCustID(?, ?)}  
```  
  
 プロシージャの戻り値を取得して、プロシージャの引数から値を取得する出力パラメーターを使用します。値を返すプロシージャとも呼ばれる*関数*します。 たとえば、 **GetCustID**先ほど説明した手順は、注文を検索できたかどうかを示す値を返します。 次の呼び出しで最初のパラメーターは、出力パラメーターをプロシージャの戻り値を取得するために使用、2 番目のパラメーターは入力パラメーターの順序の ID を指定するために使用および 3 番目のパラメーターが出力パラメーター、顧客 ID を取得するために使用します。  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 ドライバーの入力値の処理、入力/出力プロシージャのパラメーターいいえ他の SQL ステートメントでは入力パラメーターとは異なります。 変数の値を取得するステートメントが実行されたときにこれらのパラメーターにバインドし、データ ソースに送信します。  
  
 ステートメントが実行された後に、ドライバーは、これらのパラメーターにバインドされた変数に、入力/出力の返された値と出力パラメーターを格納します。 これらの値が、プロシージャによって返されるすべての結果がフェッチされた後までに設定する保証はありませんが返されますと**SQLMoreResults** SQL_NO_DATA が返されます。 ステートメントを実行すると、エラーが発生、入力/出力パラメーターのバッファーまたは出力パラメーターのバッファーの内容は未定義です。  
  
 アプリケーションを呼び出す**SQLProcedure**をプロシージャに戻り値を持つかどうかを判断します。 呼び出す**SQLProcedureColumns**プロシージャの各パラメーターの種類 (戻り値、入力、入力/出力、または出力) を判断します。
