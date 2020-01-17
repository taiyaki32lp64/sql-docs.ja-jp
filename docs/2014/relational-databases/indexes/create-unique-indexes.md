---
title: Unique インデックスの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- unique indexes
- designing indexes [SQL Server], unique
- clustered indexes, unique
- indexes [SQL Server], unique
- nonclustered indexes [SQL Server], unique
- unique indexes, design guidelines
ms.assetid: 56b5982e-cb94-46c0-8fbb-772fc275354a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cf786e48e6e76ca6a16a0a50a954a2a07d3f7a66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162356"
---
# <a name="create-unique-indexes"></a>一意のインデックスの作成
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、テーブルに一意のインデックスを作成する方法について説明します。 一意インデックスを使用すると、インデックス キーの値が重複することがないので、テーブルのすべての行を一意にすることができます。 UNIQUE 制約を作成することと、制約に依存しない一意インデックスを作成することの間に大きな違いはありません。 データ検証動作も同じ方式で行われます。また、クエリ オプティマイザーでは、制約によって作成された一意インデックスと手動で作成された一意インデックスは区別されません。 ただし、列に UNIQUE 制約を作成すると、インデックスの目的が明確になります。 UNIQUE 制約の詳細については、「 [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md)」を参照してください。  
  
 一意のインデックスを作成するとき、重複するキーを無視するオプションを設定できます。 このオプションを **[はい]** に設定して、複数行に影響するデータを INSERT ステートメントによって追加して重複キーを作成しようとすると、重複を含む行は追加されません。 **[いいえ]** に設定すると、この挿入操作全体が失敗となり、データはすべてロールバックされます。  
  
> [!NOTE]  
>  1 つの列の複数行に NULL がある場合は、その列には一意のインデックスを作成できません。 同様に、複数の列の複数行に NULL がある場合は、その列の組み合わせに一意のインデックスを作成することもできません。 インデックスを作成する場合、これらの NULL は重複した値として扱われます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [一意インデックスの利点](#Benefits)  
  
     [一般的な実装](#Implementations)  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してテーブルに一意のインデックスを作成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Benefits"></a> 一意インデックスの利点  
  
-   複数列の一意なインデックスにより、インデックス キーのそれぞれの値の組み合わせが一意であることが保証されます。 たとえば、 **LastName**列、 **FirstName**列、および **MiddleName** 列の組み合わせに一意インデックスを作成した場合、テーブル内の 2 つの行がこれらの列に対して同じ値の組み合わせを持つことはできません。  
  
-   列のデータが一意である場合、1 つのテーブルに 1 つの一意クラスター化インデックスと、複数の一意非クラスター化インデックスを作成できます。  
  
-   一意インデックスにより、定義された列のデータ整合性が保証されます。  
  
-   一意インデックスにより、より効率的な実行プランを生成できるクエリ オプティマイザーの役に立つ追加情報が提供されます。  
  
###  <a name="Implementations"></a> 一般的な実装  
 一意インデックスは、次のように実装されます。  
  
-   **PRIMARY KEY 制約または UNIQUE 制約**  
  
     PRIMARY KEY 制約を作成すると、テーブルにクラスター化インデックスが存在せず、一意の非クラスター化インデックスを指定しなかった場合、列に一意のクラスター化インデックスが自動的に作成されます。 主キー列には NULL 値を指定できません。  
  
     UNIQUE 制約を作成すると、既定では、一意な非クラスター化インデックスが作成され、UNIQUE 制約が適用されます。 テーブルにクラスター化インデックスが存在しない場合は、一意なクラスター化インデックスを指定できます。  
  
     詳細については、「 [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md) 」および「 [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md)」を参照してください。  
  
-   **制約に依存しないインデックス**  
  
     テーブルでは、一意の非クラスター化インデックスを複数定義できます。  
  
     詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)」を参照してください。  
  
-   **インデックス付きビュー**  
  
     インデックス付きビューを作成するには、1 つ以上のビュー列で一意のクラスター化インデックスを定義します。 このビューを実行すると、テーブル データがクラスター化インデックスに格納されるときと同じ方法で、結果セットがインデックスのリーフ レベルに格納されます。 詳細については、「 [インデックス付きビューの作成](../views/views.md)」を参照してください。  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   重複するキー値がデータに存在する場合は、一意インデックス、UNIQUE 制約、または PRIMARY KEY 制約を作成できません。  
  
-   一意非クラスター化インデックスには、付加非キー列を含めることができます。 詳細については、「 [付加列インデックスの作成](create-indexes-with-included-columns.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。 実行するには、 **sysadmin** 固定サーバー ロール、または **db_ddladmin** 固定データベース ロールおよび **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-unique-index-by-using-the-table-designer"></a>テーブル デザイナーを使用して一意のインデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、一意のインデックスを作成するテーブルが格納されているデータベースを展開します。  
  
2.  **[テーブル]** フォルダーを展開します。  
  
3.  一意のインデックスを作成するテーブルを右クリックし、 **[デザイン]** を選択します。  
  
4.  **[テーブル デザイナー]** メニューの **[インデックス/キー]** を選択します。  
  
5.  **[インデックス/キー]** ダイアログ ボックスで、 **[追加]** をクリックします。  
  
6.  **[選択された主/一意キーまたはインデックス]** ボックスで、新しいインデックスを選択します。  
  
7.  メイン グリッドの **[(全般)]** で、 **[種類]** を選択し、一覧から **[インデックス]** を選択します。  
  
8.  **[列]** を選択し、省略記号ボタン ( **[...]** ) をクリックします。  
  
9. **[インデックスの列]** ダイアログ ボックスの **[列名]** で、インデックスを作成する列を選択します。 16 列まで選択できます。 ただし、最適なパフォーマンスを得るには、1 つのインデックスにつき 1 列または 2 列に抑えます。 選択した各列の値の並べ方を昇順または降順のどちらかに指定できます。  
  
10. インデックスを作成するすべての列を選択したら、 **[OK]** をクリックします。  
  
11. グリッドの **[(全般)]** で、 **[一意である]** を選択し、一覧から **[はい]** を選択します。  
  
12. 省略可能:メイン グリッドで下**テーブル デザイナー**を選択します**重複するキーを無視する**選び、**はい**一覧から。 この操作は、一意のインデックスに重複キーが作成される可能性のあるデータを追加する操作を無視する場合に実行します。  
  
13. **[閉じる]** をクリックします。  
  
14. **[ファイル]** メニューの [_table_name_ **の保存**] をクリックします。  
  
#### <a name="create-a-unique-index-by-using-object-explorer"></a>オブジェクト エクスプ ローラーを使用して一意のインデックスを作成する  
  
1.  オブジェクト エクスプローラーで、一意のインデックスを作成するテーブルが格納されているデータベースを展開します。  
  
2.  **[テーブル]** フォルダーを展開します。  
  
3.  一意のインデックスを作成するテーブルを展開します。  
  
4.  **[インデックス]** フォルダーを右クリックし、 **[新しいインデックス]** をポイントし、 **[非クラスター化インデックス]** を選択します。  
  
5.  **[新しいインデックス]** ダイアログ ボックスの **[全般]** ページで、 **[インデックス名]** ボックスに新しいインデックスの名前を入力します。  
  
6.  **[一意]** チェック ボックスをオンにします。  
  
7.  **[インデックス キー列]** で、 **[追加]** をクリックします。  
  
8.  **table_name**_から列を選択_ ダイアログ ボックスで、一意のインデックスに追加する 1 つまたは複数のテーブル列のチェック ボックスをオンにします。  
  
9. **[OK]** をクリックします。  
  
10. **[新しいインデックス]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-unique-index-on-a-table"></a>テーブルに一意のインデックスを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named AK_UnitMeasure_Name and delete it if found  
    IF EXISTS (SELECT name from sys.indexes  
               WHERE name = N'AK_UnitMeasure_Name')   
       DROP INDEX AK_UnitMeasure_Name ON Production.UnitMeasure;   
    GO  
    -- Create a unique index called AK_UnitMeasure_Name  
    -- on the Production.UnitMeasure table using the Name column.  
    CREATE UNIQUE INDEX AK_UnitMeasure_Name   
       ON Production.UnitMeasure (Name);   
    GO  
    ```  
  
 詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)」を参照してください。  
  
  
