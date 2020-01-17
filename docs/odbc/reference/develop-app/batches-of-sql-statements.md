---
title: SQL ステートメントのバッチ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f7264b17c13d6b66bf1be24da81e96a4ca3e8a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122831"
---
# <a name="batches-of-sql-statements"></a>SQL ステートメントのバッチ
SQL ステートメントのバッチは、2 つ以上の SQL ステートメントまたは 2 つ以上の SQL ステートメントのグループと同じ効果を 1 つの SQL ステートメントのグループです。 一部の実装で、結果は利用する前にバッチ全体ステートメントを実行します。 これは多くの場合、ネットワーク トラフィックが低下することができ、データ ソースは、SQL ステートメントのバッチの実行を最適化できる場合がありますので、ステートメントを個別に送信するよりも効率的です。 呼び出す他の実装で**SQLMoreResults**バッチの次のステートメントの実行をトリガーします。 ODBC では、次の種類のバッチがサポートされています。  
  
-   **明示的なバッチ**、*明示的なバッチ*はセミコロン (;) で区切られた 2 つ以上の SQL ステートメント。 たとえば、SQL ステートメントの次のバッチには、新しい販売注文が表示されます。 これは、注文と行の両方のテーブルに行を挿入する必要があります。 最後のステートメントの後にセミコロンがないことに注意してください。  
  
    ```  
    INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
       VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 1, 1234, 10);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 2, 987, 8);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 3, 566, 17);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 4, 412, 500)  
    ```  
  
-   **プロシージャ**プロシージャには、複数の SQL ステートメントが含まれている場合に SQL ステートメントのバッチと見なされます。 たとえば、次の SQL Server に固有のステートメントは、顧客とその顧客の開いているすべての販売注文を含む結果セットに関する情報を含む結果セットを返すプロシージャを作成します。  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE PROCEDURE**ステートメント自体は、SQL ステートメントのバッチではありません。 ただし、作成手順では、SQL ステートメントのバッチが、します。 セミコロンで区切られていない 2 つ**選択**ステートメントのため、 **CREATE PROCEDURE**ステートメントは、SQL Server に固有と SQL Server には、で複数のステートメントを区切るにはセミコロンは不要**CREATE PROCEDURE**ステートメント。  
  
-   **パラメーターの配列の**パラメーターの配列は、一括操作を実行する効果的な方法として、パラメーター化された SQL ステートメントで使用できます。 パラメーターの配列を使用してに次の例では、**挿入**行のテーブルに 1 つの SQL ステートメントのみを実行中に複数の行を挿入するステートメント。  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     データ ソースがパラメーターの配列をサポートしていない場合、ドライバーをエミュレートできますそれらのパラメーターのセットごとに、SQL ステートメントを実行しています。 詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)と[パラメーター値の配列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)、このセクションで後述します。  
  
 相互運用可能な方法でさまざまな種類のバッチを混在させることはできません。 つまり、パラメーターの配列を使用して、明示的なバッチを呼び出すアプリケーションでプロシージャが含まれますが、明示的なバッチの実行結果を決定する方法とパラメーターの配列を使用するプロシージャの呼び出しは、ドライバー固有です。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [結果生成および結果解放ステートメント](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [バッチの実行](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [エラーおよびバッチ](../../../odbc/reference/develop-app/errors-and-batches.md)
