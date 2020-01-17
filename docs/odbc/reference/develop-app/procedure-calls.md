---
title: プロシージャの呼び出し |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 926ee91fae207d50248df4c82d1b82bb6424e239
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023256"
---
# <a name="procedure-calls"></a>プロシージャ呼び出し
A*プロシージャ*はデータ ソースに格納されている実行可能オブジェクトです。 これは通常、プリコンパイルされた 1 つ以上の SQL ステートメントです。 プロシージャの呼び出しのエスケープ シーケンスは、します。  
  
 **{** **[? =]** **呼び出す***プロシージャ名*[ **(** [*パラメーター*] [ **、** [*パラメーター*]. **)** ] **}**  
  
 場所*プロシージャ名*プロシージャの名前を指定し、*パラメーター*プロシージャのパラメーターを指定します。  
  
 プロシージャ呼び出しのエスケープ シーケンスの詳細については、次を参照してください[プロシージャの Call エスケープ シーケンス](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md)付録 c:。SQL 文法。  
  
 プロシージャには、0 個以上のパラメーターを指定できます。 省略可能なパラメーター マーカーで示されている値を返すことも **? =** 構文の先頭。 場合*パラメーター*が入力パラメーターまたは入力/出力パラメーター、リテラルまたはパラメーター マーカーを指定できます。 ただし、一部のデータ ソースがリテラル パラメーター値を受け入れないために、相互運用可能なアプリケーションはパラメーター マーカーを使用常にする必要があります。 場合*パラメーター*出力パラメーター、パラメーター マーカーをする必要があります。 パラメーター マーカーにバインドする必要があります**SQLBindParameter**プロシージャ呼び出しの前にステートメントが実行されます。  
  
 プロシージャ呼び出しでは、入力パラメーターと入出力パラメーターを省略できます。 かどうか、プロシージャが呼び出されたどのパラメーターもが、かっこで囲んでなど {呼び出す*プロシージャ名*()}、ドライバーは最初のパラメーターの既定値を使用するデータ ソースを指示します。 手順がすべてのパラメーターを持たない場合、プロシージャは失敗があります。 プロシージャがかっこがない場合などと呼ばれるかどうかは {呼び出す*プロシージャ名*}、ドライバーは、パラメーターの値を送信しません。  
  
 プロシージャ呼び出しでは、入力パラメーターや入出力パラメーターとしてリテラルを指定できます。 たとえば、プロシージャ**InsertOrder**が 5 つの入力パラメーター。 次の呼び出しに**InsertOrder**最初のパラメーターを省略して、リテラルは、2 番目のパラメーターおよびパラメーター マーカーを使用して、3 番目、4 番目、および 5 番目のパラメーター。  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 パラメーターを省略した場合、他のパラメーターを区切るコンマする必要がありますも表示に注意してください。 入力パラメーターまたは入出力パラメーターを省略すると、プロシージャはそのパラメーターの既定値を使用します。 長さ/インジケーター バッファーの値を設定するパラメーターまたは入力/出力パラメーターの既定値を指定する別の方法に SQL_DEFAULT_PARAM をパラメーターにバインドします。  
  
 入力/出力パラメーターを省略した場合、またはパラメーターのリテラルが指定されている場合は、ドライバーは出力値を破棄します。 同様に、プロシージャの戻り値のパラメーター マーカーを省略した場合、ドライバーは戻り値を破棄します。 最後に、値を返さないプロシージャに戻り値パラメーターを指定すると、ドライバーは、そのパラメーターにバインドされる長さ/インジケーター バッファーの値を SQL_NULL_DATA に設定します。  
  
 たとえば、PARTS_IN_ORDERS プロシージャは、特定の部品番号が含まれている注文の一覧を含む結果セットを作成します。 次のコードでは、部品番号 544 にこの手順を呼び出します。  
  
```  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_SLONG, SQL_INTEGER, 0, 0,  
                  &PartID, 0, PartIDInd);  
  
// Place the department number in PartID.  
PartID = 544;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "{call PARTS_IN_ORDERS(?)}", SQL_NTS);  
```  
  
 アプリケーションを呼び出すプロシージャをデータ ソースがサポートしているかどうかを判断する**SQLGetInfo** SQL_PROCEDURES オプションを使用します。  
  
 プロシージャの詳細については、次を参照してください。[プロシージャ](../../../odbc/reference/develop-app/procedures-odbc.md)します。
