---
title: フィルター選択されたインデックスの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- filtered indexes [SQL Server], about filtered indexes
- designing indexes [SQL Server], filtered
- filtered indexes [SQL Server]
- nonclustered indexes [SQL Server], filtered
- indexes [SQL Server], filtered
ms.assetid: 25e1fcc5-45d7-4c53-8c79-5493dfaa1c74
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3cb02f0cbb395b8e3f730e62139eb7b7d89b4c96
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908105"
---
# <a name="create-filtered-indexes"></a>フィルター選択されたインデックスの作成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、フィルター選択されたインデックスを作成する方法について説明します。 フィルター選択されたインデックスは、最適化された非クラスター化インデックスであり、適切に定義されたデータのサブセットから選択するクエリに対応する際に特に適しています。 フィルター選択されたインデックスは、フィルター述語を使用して、テーブル内の一部の行にインデックスを作成します。 フィルター選択されたインデックスを適切にデザインすると、クエリのパフォーマンスが向上するだけでなく、テーブル全体のインデックスと比較してインデックスのメンテナンス コストおよびストレージ コストを削減できます。  
  
 フィルター選択されたインデックスは、テーブル全体のインデックスよりも次の点で優れています。  
  
-   **クエリのパフォーマンスとプランの品質の向上**  
  
     フィルター選択されたインデックスを適切にデザインすると、クエリのパフォーマンスと実行プランの品質が向上します。これは、このインデックスが、テーブル全体の非クラスター化インデックスよりも小さく、フィルター選択された統計情報を含むためです。 フィルター選択された統計情報は、フィルター選択されたインデックスの行のみを対象としているため、テーブル全体の統計情報よりも正確です。  
  
-   **インデックスのメンテナンス コストの削減**  
  
     インデックスのメンテナンスが行われるのは、データ操作言語 (DML) ステートメントがインデックス内のデータに影響を与える場合のみです。 フィルター選択されたインデックスにより、インデックスのメンテナンス コストは、テーブル全体の非クラスター化インデックスと比較して削減されます。これは、フィルター選択されたインデックスは小さく、インデックス内のデータが変更された場合にのみメンテナンスされるためです。 特に、含まれるデータの変更頻度が引く場合は、多数のフィルター選択されたインデックスを作成できます。 同様に、フィルター選択されたインデックスに頻繁に変更されるデータのみが含まれている場合は、インデックスのサイズを小さくすると、統計情報の更新コストが削減されます。  
  
-   **インデックスのストレージ コストの削減**  
  
     テーブル全体のインデックスが不要な場合は、フィルター選択されたインデックスを作成すると、非クラスター化インデックスのディスク ストレージを削減できます。 ストレージ要件をあまり増やすことなく、テーブル全体の非クラスター化インデックスを複数のフィルター選択されたインデックスに置き換えることができます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [デザインに関する考慮事項](#Design)  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してフィルター選択されたインデックスを作成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Design"></a> デザインに関する考慮事項  
  
-   クエリに関連する少数の値だけが列に含まれている場合、値のサブセットにフィルター選択されたインデックスを作成できます。 たとえば、列の値がほとんど NULL の場合に、クエリで常に NULL 以外の値を選択するときは、NULL 以外のデータ行にフィルター選択されたインデックスを作成できます。 作成したインデックスは、同じキー列に定義されているテーブル全体の非クラスター化インデックスよりも小さく、メンテナンス コストが少なくなります。  
  
-   テーブルに異種データの行が含まれている場合、1 つ以上のカテゴリのデータに対してフィルター選択されたインデックスを作成できます。 これにより、クエリのフォーカスをテーブルの特定の領域に狭めて、これらのデータに対するクエリのパフォーマンスを向上させることができます。 繰り返しになりますが、作成したインデックスは、テーブル全体の非クラスター化インデックスよりも小さく、メンテナンス コストが少なくなります。  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   フィルター選択されたインデックスをビューに作成することはできません。 ただし、クエリ オプティマイザーにとって、ビューで参照されているテーブルに定義されたフィルター選択されたインデックスは役立ちます。 クエリ オプティマイザーでは、クエリ結果が正しくなる場合、ビューから選択するクエリに対してフィルター選択されたインデックスが検討されます。

-   フィルター式でアクセスされる列が CLR データ型の場合、テーブルにフィルター選択されたインデックスを作成することはできません。
  
-   フィルター選択されたインデックスは、インデックス付きビューよりも次の点で優れています。  
  
    -   インデックスのメンテナンス コストの削減。 たとえば、インデックス付きビューを更新する場合よりもフィルター選択されたインデックスを更新する場合の方が、クエリ プロセッサで使用する CPU リソースが少なくなります。  
  
    -   プランの品質の向上。 たとえば、クエリのコンパイル時、同等のインデックス付きビューよりも多くの状況でフィルター選択されたインデックスを使用することがクエリ オプティマイザーで検討されます。  
  
    -   オンラインでのインデックス再構築。 フィルター選択されたインデックスは、クエリで使用可能なときに再構築できます。 オンラインでのインデックス再構築は、インデックス付きビューではサポートされていません。 詳細については、「[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)」の「REBUILD オプション」を参照してください。  
  
    -   一意ではないインデックス。 フィルター選択されたインデックスは一意ではないインデックスにすることができますが、インデックス付きビューは一意である必要があります。  
  
-   フィルター選択されたインデックスは 1 つのテーブルで定義され、単純な比較演算子のみをサポートします。 複数のテーブルを参照するフィルター式や複雑なロジックを含むフィルター式が必要な場合は、ビューを作成する必要があります。  
  
-   フィルター選択されたインデックスの式がクエリ述語と同じであり、フィルター選択されたインデックスの式の列がクエリ結果と共に返されない場合、その式の列を、フィルター選択されたインデックスの定義でキー列または付加列にする必要はありません。  
  
-   フィルター選択されたインデックスの式と異なるクエリ述語で比較に列が使用される場合は、フィルター選択されたインデックスの式の列を、フィルター選択されたインデックスの定義でキー列または付加列にする必要があります。  
  
-   フィルター選択されたインデックスの式の列がクエリ結果セットに含まれる場合、その列をフィルター選択されたインデックスの定義でキー列または付加列にする必要があります。  
  
-   テーブルのクラスター化インデックス キーは、フィルター選択されたインデックスの定義でキー列または付加列にする必要はありません。 クラスター化インデックス キーは、フィルター選択されたインデックスなど、すべての非クラスター化インデックスに自動的に含まれます。  
  
-   フィルター選択されたインデックスでは、その式に指定された比較演算子によって暗黙的または明示的なデータ変換が行われる場合、変換が比較演算子の左辺で行われると、エラーが発生します。 解決方法としては、比較演算子の右辺にデータ変換演算子 (CAST または CONVERT) を含む、フィルター選択されたインデックスの式を記述します。  

- [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md) 構文のフィルター選択されたインデックスの作成に必要な SET オプションを確認します。
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。 実行するには、 **sysadmin** 固定サーバー ロール、または **db_ddladmin** 固定データベース ロールおよび **db_owner** 固定データベース ロールのメンバーである必要があります。 フィルター選択されたインデックスの式を変更するには、CREATE INDEX WITH DROP_EXISTING を使用します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-filtered-index"></a>フィルター選択されたインデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、フィルター選択されたインデックスを作成するテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、フィルター選択されたインデックスを作成するテーブルを展開します。  
  
4.  **[インデックス]** フォルダーを右クリックし、 **[新しいインデックス]** をポイントし、 **[非クラスター化インデックス]** を選択します。  
  
5.  **[新しいインデックス]** ダイアログ ボックスの **[全般]** ページで、 **[インデックス名]** ボックスに新しいインデックスの名前を入力します。  
  
6.  **[インデックス キー列]** で、 **[追加]** をクリックします。  
  
7.  **[_table\_name_ から列を選択]** ダイアログ ボックスで、一意のインデックスに追加する 1 つまたは複数のテーブル列のチェック ボックスをオンにします。  
  
8.  **[OK]** をクリックします。  
  
9. **[フィルター]** ページで、 **[フィルター式]** に、フィルター選択されたインデックスの作成に使用する SQL 式を入力します。  
  
10. **[OK]** をクリックします。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-filtered-index"></a>フィルター選択されたインデックスを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Looks for an existing filtered index named "FIBillOfMaterialsWithEndDate"  
    -- and deletes it from the table Production.BillOfMaterials if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
        WHERE name = N'FIBillOfMaterialsWithEndDate'  
        AND object_id = OBJECT_ID (N'Production.BillOfMaterials'))  
    DROP INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials  
    GO  
    -- Creates a filtered index "FIBillOfMaterialsWithEndDate"  
    -- on the table Production.BillOfMaterials   
    -- using the columms ComponentID and StartDate.  
  
    CREATE NONCLUSTERED INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials (ComponentID, StartDate)  
        WHERE EndDate IS NOT NULL ;  
    GO  
    ```  
  
     上記のフィルター選択されたインデックスは、次のクエリに対して有効です。 クエリ実行プランを表示して、クエリ オプティマイザーでフィルター選択されたインデックスが使用されたかどうかを確認できます。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ProductAssemblyID, ComponentID, StartDate   
    FROM Production.BillOfMaterials  
    WHERE EndDate IS NOT NULL   
        AND ComponentID = 5   
        AND StartDate > '01/01/2008' ;  
    GO  
    ```  
  
#### <a name="to-ensure-that-a-filtered-index-is-used-in-a-sql-query"></a>フィルター選択されたインデックスが SQL クエリで使用されるようにするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
        WITH ( INDEX ( FIBillOfMaterialsWithEndDate ) )   
    WHERE EndDate IN ('20000825', '20000908', '20000918');   
    GO  
    ```  
  
 詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」を参照してください。  
  
  
