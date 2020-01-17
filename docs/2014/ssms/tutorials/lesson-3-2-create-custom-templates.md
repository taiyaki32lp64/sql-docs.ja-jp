---
title: カスタム テンプレートの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tql
- templates [Transact-SQL], creating
- templates [Transact-SQL]
ms.assetid: 41098e78-b482-410e-bfe8-2ac10769ac4a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 495b03b98e6c497bfd7a1527d9e2e2d81f25b762
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62805573"
---
# <a name="create-custom-templates"></a>カスタム テンプレートの作成
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 一般的な作業のためのテンプレートが多数用意されていますが、テンプレートの真価は、頻繁に作成する複雑なスクリプトに適したカスタム テンプレートを作成できる点にあります。 この演習では、2 ～ 3 のパラメーターを使用した簡単なスクリプトを作成しますが、規模が大きく、反復的なスクリプトを作成する場合にもテンプレートが役立ちます。  
  
## <a name="using-custom-templates"></a>カスタム テンプレートの使用  
  
#### <a name="to-create-a-custom-template"></a>カスタム テンプレートを作成するには  
  
1.  テンプレート エクスプローラーで **[SQL Server テンプレート]** を展開します。 **[Stored Procedure]** を右クリックし、 **[新規作成]** をポイントして **[フォルダー]** をクリックします。  
  
2.  新しいテンプレート フォルダーの名前として「 **Custom** 」と入力し、Enter キーを押します。  
  
3.  **[Custom]** を右クリックし、 **[新規作成]** をポイントして **[テンプレート]** をクリックします。  
  
4.  新しいテンプレートの名前として「 **WorkOrdersProc** 」と入力し、 **Enter**キーを押します。  
  
5.  **[WorkOrdersProc]** を右クリックし、 **[編集]** をクリックします。  
  
6.  **[データベース エンジンへの接続]** ダイアログ ボックスで接続情報を確認し、 **[接続]** をクリックします。  
  
7.  クエリ エディターに次のスクリプトを入力し、特定の部分 (この例では Blade) の命令を検索するストアド プロシージャを作成します (チュートリアル ウィンドウからコードをコピーして、貼り付けることができます)。  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersForBlade')  
       DROP PROCEDURE dbo.WorkOrdersForBlade;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersForBlade  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = 'Blade';  
    GO  
    ```  
  
8.  F5 キーを押してこのスクリプトを実行し、 **WorkOrdersForBlade** プロシージャを作成します。  
  
9. オブジェクト エクスプローラーでサーバーを右クリックし、 **[新しいクエリ]** をクリックします。 新しいクエリ エディター ウィンドウが開きます。  
  
10. クエリ エディターに「 **EXECUTE dbo.WorkOrdersForBlade**」と入力し、F5 キーを押してクエリを実行します。 **結果**ペインに、ブレードに対する作業命令の一覧が返されていることを確認します。  
  
11. テンプレート スクリプト (手順 7 でスクリプト) を編集して、製品名 Blade をパラメーターに置き換えて <strong> *<* product_name</strong>、 `nvarchar(50)`、<strong>名前 *>* </strong> 、4 つの場所にします。  
  
    > [!NOTE]  
    >  パラメーターには、置き換えるパラメーターの名前、パラメーターのデータ型、パラメーターの既定値の 3 つの要素が必要です。  
  
12. スクリプトは以下のようになります。  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersFor<product_name, nvarchar(50), name>')  
       DROP PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = '<product_name, nvarchar(50), name>';  
    GO  
    ```  
  
13. **[ファイル]** メニューの **[WorkOrdersProc.sql の保存]** をクリックし、テンプレートを保存します。  
  
#### <a name="to-test-the-custom-template"></a>カスタム テンプレートをテストするには  
  
1.  テンプレート エクスプローラーで **[Stored Procedure]** 、 **[Custom]** の順に展開し、 **[WorkOrderProc]** をダブルクリックします。  
  
2.  **[データベース エンジンへの接続]** ダイアログ ボックスで接続情報を指定し、 **[接続]** をクリックします。 新しいクエリ エディター ウィンドウが開き、 **WorkOrderProc** テンプレートの内容が表示されます。  
  
3.  **[クエリ]** メニューの **[テンプレート パラメーターの値の指定]** をクリックします。  
  
4.  **テンプレート パラメーターの置換** ダイアログ ボックスの`product_name`値には、入力**FreeWheel** (既定の内容を上書き) 順にクリックします**ok**を閉じる、**テンプレート パラメーターの置換** ダイアログ ボックスし、クエリ エディターでスクリプトを変更します。  
  
5.  F5&lt;/localizedText&gt; キーを押してクエリを実行し、プロシージャを作成します。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [プロジェクトまたはソリューションとしてスクリプトを保存する](lesson-3-3-save-scripts-as-projects-or-solutions.md)  
  
  
