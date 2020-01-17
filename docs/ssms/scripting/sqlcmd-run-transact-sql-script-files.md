---
title: sqlcmd を使用した Transact-SQL スクリプト ファイルの実行 | Microsoft Docs
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 46f4a1660fd2b33581482025cd5a9cf3bb16f770
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267646"
---
# <a name="sqlcmd---run-transact-sql-script-files"></a>sqlcmd - Transact-SQL スクリプトの実行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 **sqlcmd** を使用して Transact-SQL スクリプトを実行します。 Transact-SQL スクリプト ファイルは、Transact-SQL ステートメント、 **sqlcmd** コマンド、およびスクリプト変数を組み合わせて記述できるテキスト ファイルです。  

## <a name="create-a-script-file"></a>スクリプト ファイルの作成  
 メモ帳を使用して簡単な Transact-SQL スクリプト ファイルを作成するには、次の手順を実行します。  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[アクセサリ]** の順にポイントして、 **[メモ帳]** をクリックします。  
  
2.  次の Transact-SQL コードをコピーして、メモ帳に貼り付けます。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT p.FirstName + ' ' + p.LastName AS 'Employee Name',  
    a.AddressLine1, a.AddressLine2 , a.City, a.PostalCode   
    FROM Person.Person AS p   
       INNER JOIN HumanResources.Employee AS e   
            ON p.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.BusinessEntityAddress bea   
            ON bea.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.Address AS a   
            ON a.AddressID = bea.AddressID;  
    GO  
    ```  
  
3.  作成したファイルを **myScript.sql** という名前で C ドライブに保存します。  
  
## <a name="run-the-script-file"></a>スクリプト ファイルを実行する  
  
1.  コマンド プロンプト ウィンドウを開きます。  
  
2.  コマンド プロンプト ウィンドウで、「 **sqlcmd -S myServer\instanceName -i C:\myScript.sql**」と入力します。  
  
3.  Enter キーを押します。  
  
 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] の従業員名と住所の一覧がコマンド プロンプト ウィンドウに出力されます。  

## <a name="save-the-output-to-a-text-file"></a>出力をテキスト ファイルに保存する
  
1.  コマンド プロンプト ウィンドウを開きます。  
  
2.  コマンド プロンプト ウィンドウで、「 **sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt**」と入力します。  
  
3.  Enter キーを押します。  
  
 コマンド プロンプト ウィンドウには何も出力されません。 代わりに、EmpAdds.txt ファイルに出力されます。 EmpAdds.txt を開くと、この出力を確認できます。  
  
## <a name="see-also"></a>参照  
 [sqlcmd ユーティリティの起動](../../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)  
  
  
