---
title: 実行時に構築された SQL ステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8333000c9bb806116244ac6d4f654fa195205868
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107463"
---
# <a name="sql-statements-constructed-at-run-time"></a>実行時に構築された SQL ステートメント
よくアド ホック分析を実行するアプリケーションは、実行時に SQL ステートメントを作成します。 たとえば、スプレッドシート データの取得元となる列を選択するユーザーを許可する可能性があります。  
  
```  
// SQL_Statements_Constructed_at_Run_Time.cpp  
#include <windows.h>  
#include <stdio.h>  
#include <sqltypes.h>  
  
int main() {  
   SQLCHAR *Statement = 0, *TableName = 0;  
   SQLCHAR **TableNamesArray, **ColumnNamesArray = 0;  
   BOOL *ColumnSelectedArray = 0;  
   BOOL  CommaNeeded;  
   SQLSMALLINT i = 0, NumColumns = 0;  
  
   // Use SQLTables to build a list of tables (TableNamesArray[]). Let the  
   // user select a table and store the selected table in TableName.  
  
   // Use SQLColumns to build a list of the columns in the selected table  
   // (ColumnNamesArray). Set NumColumns to the number of columns in the  
   // table. Let the user select one or more columns and flag these columns  
   // in ColumnSelectedArray[].  
  
   // Build a SELECT statement from the selected columns.  
   CommaNeeded = FALSE;  
   Statement = (SQLCHAR*)malloc(8);  
   strcpy_s((char*)Statement, 8, "SELECT ");  
  
   for (i = 0 ; i = NumColumns ; i++) {  
      if (ColumnSelectedArray[i]) {  
         if (CommaNeeded)  
            strcat_s((char*)Statement, sizeof(Statement), ",");  
         else  
            CommaNeeded = TRUE;  
         strcat_s((char*)Statement, sizeof(Statement), (char*)ColumnNamesArray[i]);  
      }  
   }  
  
   strcat_s((char*)Statement, 15, " FROM ");  
   // strcat_s((char*)Statement, 100, (char*)TableName);  
  
   // Execute the statement . It will be executed once, do not prepare it.  
   // SQLExecDirect(hstmt, Statement, SQL_NTS);  
}  
```  
  
 通常 SQL ステートメントの実行時に作成するアプリケーションの別のクラスとは、アプリケーションの開発環境です。 ただしを作成するステートメントでは場所が通常が最適化され、テスト、ビルド、アプリケーションにハードコーディングします。  
  
 実行時に SQL ステートメントを作成するアプリケーションは、ユーザーに大きな柔軟性を提供できます。 前の例などの一般的な操作がさらにサポートされていませんでしたからわかるように**場所**句、 **ORDER BY**句、または結合、実行時に SQL ステートメントの作成が大幅に複雑ハード コーディングするステートメント。 さらに、このようなアプリケーションのテストは問題になります任意の数の SQL ステートメントを作成することができます。  
  
 実行時に SQL ステートメントの構築の潜在的な欠点は、ハード コーディングされたステートメントを使用してよりも、ステートメントを構築するまでに時間がかかることです。 さいわい、問題ではほとんどありません。 このようなアプリケーションは、大量のユーザー インターフェイスと、アプリケーションが費やした時間を傾向がある SQL ステートメントの構築は通常小さいと比べると、ユーザーが入力の条件に要する時間。
