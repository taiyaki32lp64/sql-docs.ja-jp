---
title: ユーザー定義関数名の変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: c2695a5c-9cc5-4b18-8771-53027ca9a9af
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3419faca26d9d252610c07cb994ab5faa738f937
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211700"
---
# <a name="rename-user-defined-functions"></a>ユーザー定義関数名の変更
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してユーザー定義関数の名前を変更できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **ユーザー定義関数の名前を変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   関数名は、 [識別子](../databases/database-identifiers.md)の規則に従っている必要があります。  
  
-   ユーザー定義関数の名前を変更しても、 **sys.sql_modules** カタログ ビューの定義列にある、対応するオブジェクトの名前は変更されません。 したがって、このオブジェクトの種類の名前を変更しないことをお勧めします。 代わりに、ストアド プロシージャを削除して新しい名前で再作成してください。  
  
-   ユーザー定義関数の名前または定義を変更すると、依存オブジェクトを更新してその関数に加えられた変更を反映しなければ、その依存オブジェクトが失敗する可能性があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 関数を削除するには、関数が属するスキーマに対する ALTER 権限、または関数に対する CONTROL 権限が必要です。 関数を再作成するには、データベースの CREATE FUNCTION 権限と、関数を作成するスキーマの ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-rename-user-defined-functions"></a>ユーザー定義関数の名前を変更するには  
  
1.  **オブジェクト エクスプローラー**で、名前を変更する関数が格納されているデータベースの横にあるプラス記号をクリックします。  
  
2.  **Programmability** フォルダーの横にあるプラス記号をクリックします。  
  
3.  名前変更する次の関数を含むフォルダーの横にあるプラス記号をクリックします。  
  
    -   Table-valued Function  
  
    -   スカラー値関数  
  
    -   集計関数  
  
4.  名前を変更する関数を右クリックし、 **[名前の変更]** を選択します。  
  
5.  関数の新しい名前を入力します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **ユーザー定義関数の名前を変更するには**  
  
 Transact-SQL ステートメントを使用して、このタスクを実行することはできません。 Transact-SQL を使用してユーザー定義関数の名前を変更するには、まず既存の関数を削除してから、新しい定義を使用して再作成する必要があります。 関数の古い名前を使用していたすべてのコードおよびアプリケーションが、新しい名前を使用していることを確認します。  
  
 詳細については、「[CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)」および「[DROP FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-function-transact-sql)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)   
 [ユーザー定義関数の表示](user-defined-functions.md)  
  
  
