---
title: テーブルの作成 (チュートリアル) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating tables
ms.assetid: 653f2dd3-36a2-4bd5-8703-71a57d244661
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 2d4b110446ae27335f65e83958a1a153350ccbcb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62704558"
---
# <a name="creating-a-table-tutorial"></a>テーブルの作成 (チュートリアル)
  テーブルを作成するには、テーブルの名前と、テーブル内の各列の名前とデータ型を入力する必要があります。 また、各列でヌル値を許可するかどうかを指定することも推奨されます。  
  
 ほとんどのテーブルに、テーブルの 1 つ以上の列で構成された主キーがあります。 主キーは常に一意です。 [!INCLUDE[ssDE](../includes/ssde-md.md)]によって、主キーの値がテーブルで重複しないように制限されます。  
  
 データ型のリストと、それぞれの説明のリンクについては、「[データ型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../includes/ssde-md.md)]は、大文字と小文字を区別するか区別しないかを設定してインストールできます。 大文字と小文字を区別するように設定して [!INCLUDE[ssDE](../includes/ssde-md.md)] をインストールした場合は、オブジェクト名を常に大文字か小文字に統一する必要があります。 たとえば、OrderData という名前のテーブルと、ORDERDATA という名前のテーブルは別のテーブルです。 大文字と小文字を区別しないように設定して [!INCLUDE[ssDE](../includes/ssde-md.md)] をインストールした場合、この 2 つのテーブル名は同じテーブルと見なされるため、その名前は一度しか使用できません。  
  
### <a name="to-create-a-database-to-contain-the-new-table"></a>新しいテーブルを含めるデータベースを作成するには  
  
-   クエリ エディター ウィンドウに次のコードを入力します。  
  
    ```  
    USE master;  
    GO  
  
    --Delete the TestData database if it exists.  
    IF EXISTS(SELECT * from sys.databases WHERE name='TestData')  
    BEGIN  
        DROP DATABASE TestData;  
    END  
  
    --Create a new database called TestData.  
    CREATE DATABASE TestData;  
    Press the F5 key to execute the code and create the database.  
    ```  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>クエリ エディター接続から TestData データベースへの切り替え  
  
-   接続を `TestData` データベースに変更するには、クエリ エディターのウィンドウで次のコードを入力して実行します。  
  
    ```  
    USE TestData  
    GO  
    ```  
  
### <a name="to-create-a-table"></a>テーブルを作成するには  
  
-   クエリ エディターのウィンドウで、次のコードを入力して実行し、 `Products`という名前の単純なテーブルを作成します。 テーブルの列は `ProductID`、 `ProductName`、 `Price`、 `ProductDescription`という名前です。 `ProductID` 列がテーブルの主キーです。 `int`、 `varchar(25)`、 `money`、 `text` は、すべてデータ型です。 行を挿入または変更するときにデータを入力しなくてもよい列は、 `Price` と `ProductionDescription` のみです。 このステートメントには、スキーマというオプションの要素 (`dbo.`) が含まれています。 スキーマは、テーブルを所有するデータベース オブジェクトです。 管理者の場合は、 `dbo` が既定のスキーマです。 `dbo` はデータベース所有者を表します。  
  
    ```  
    CREATE TABLE dbo.Products  
       (ProductID int PRIMARY KEY NOT NULL,  
        ProductName varchar(25) NOT NULL,  
        Price money NULL,  
        ProductDescription text NULL)  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [テーブルのデータの挿入と更新 (チュートリアル)](../t-sql/lesson-1-3-inserting-and-updating-data-in-a-table.md)  
  
## <a name="see-also"></a>関連項目  
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)  
  
  
