---
title: Enable Stretch Database for a table
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, enabling table
- enabling table for Stretch Database
ms.assetid: de4ac0c5-46ef-4593-a11e-9dd9bcd3ccdc
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 49d3f7fa266be69c767b0fb0450cc6898351f39b
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843806"
---
# <a name="enable-stretch-database-for-a-table"></a>Enable Stretch Database for a table
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database 用にテーブルを構成するには、SQL Server Management Studio でテーブルに対して **[ストレッチ]、[有効にする]** の順に選択し、 **[テーブルのストレッチの有効化]** ウィザードを開きます。 Transact-SQL を使用して、既存のテーブルで Stretch Database を有効にしたり、Stretch Database が有効になっている新しいテーブルを作成することもできます。  
  
-   コールド データを別のテーブルに保存している場合は、そのテーブル全体を移行できます。  
  
-   テーブルにホット データとコールド データの両方が含まれている場合は、移行する行を選択するフィルター関数を指定できます。    
 
 **前提条件**。 テーブルに対して **[ストレッチ]、[有効にする]** の順に選択した場合、データベースに対して Stretch Database がまだ有効になっていないと、ウィザードは最初に Stretch Database 用にデータベースを構成します。 この記事の手順ではなく、「[Stretch ウィザードに対するデータベースの有効化を実行して開始する](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)」の手順に従います。  
  
 **権限**: データベースまたはテーブルで Stretch Database を有効にするには、db_owner 権限が必要です。 テーブルで Stretch Database を有効にするには、テーブルに対する ALTER 権限も必要です。  

 > [!NOTE]
 > 後で、Stretch Database を無効にする場合は、テーブルまたはデータベースで Stretch Database を無効にしてもリモート オブジェクトは削除されないことに注意してください。 リモート テーブルまたはリモート データベースを削除する場合は、Azure 管理ポータルを使用して削除する必要があります。 リモート オブジェクトを手動で削除するまで、引き続き Azure ストレージのコストが発生します。
 
##  <a name="EnableWizardTable"></a> ウィザードを使用してテーブルで Stretch Database を有効にする  
 **ウィザードを起動する**  
 1.  SQL Server Management Studio のオブジェクト エクスプローラーで、ストレッチを有効にするテーブルを選択します。  
  
2.  右クリックして **[ストレッチ]** を選択し、 **[有効化]** を選択して、ウィザードを起動します。  
  
 **概要**  
 ウィザードの目的と前提条件を確認します。  
  
 **データベースのテーブルを選択する**  
 有効にするテーブルが表示され、選択されていることを確認します。  
  
 テーブル全体を移行することも、ウィザードで単純なフィルター関数を指定することもできます。 移行する行を選択するために別の種類のフィルター関数を使用する場合、次のいずれかの操作を行います。  
  
-   ウィザードを終了し、ALTER TABLE ステートメントを実行してテーブルの Stretch を有効にして、フィルター関数を指定します。  
  
-   ウィザードを終了した後、ALTER TABLE ステートメントを実行してフィルター関数を指定します。 必要な手順については、「 [Add a filter function after running the Wizard](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz)」 (ウィザードの実行後、フィルター関数を追加する) を参照してください。  
  
 ALTER TABLE 構文については、この記事で後ほど説明します。  
  
 **概要**  
 ウィザードで入力した値および選択したオプションを確認します。 次に、 **[完了]** を選択してストレッチを有効にします。  
  
 **結果**  
 結果を確認します。  
  
##  <a name="EnableTSQLTable"></a> Transact-SQL を使用してテーブルで Stretch Database を有効にする  
 Transact-SQL を使用して、既存のテーブルで Stretch Database を有効にしたり、Stretch Database が有効になっている新しいテーブルを作成したりできます。  
  
### <a name="options"></a>オプション  
 CREATE TABLE または ALTER TABLE を実行してテーブルで Stretch Database を有効にする場合は、次のオプションを使用します。  
  
-   テーブルにホット データとコールド データの両方が含まれている場合は、オプションで `FILTER_PREDICATE = <function>` 句を使用して、移行する行を選択する関数を指定します。 この述語でインライン テーブル値関数を呼び出す必要があります。 詳細については、「 [フィルター関数を使用して、移行する行を選択する](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)」を参照してください。 フィルター関数を指定しない場合、テーブル全体が移行されます。  
  
    > [!IMPORTANT]  
    > 指定したフィルター関数のパフォーマンスが低いと、データ移行のパフォーマンスも低くなります。 Stretch Database では、CROSS APPLY 演算子を使用してテーブルにフィルター関数を適用します。  
  
-   データ移行をすぐに開始する場合は `MIGRATION_STATE = OUTBOUND` を指定し、データ移行の開始を延期する場合は  `MIGRATION_STATE = PAUSED` を指定します。  
  
### <a name="enable-stretch-database-for-an-existing-table"></a>既存のテーブルに対して Stretch Database を有効にする  
 Stretch Database 用に既存のテーブルを構成するには、ALTER TABLE コマンドを実行します。  
  
 次に、テーブル全体を移行し、データ移行をすぐに開始する例を示します。  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 次に、 `dbo.fn_stretchpredicate` インライン テーブル値関数によって識別される行だけを移行し、データ移行を延期する例を示します。 フィルター関数の詳細については、「 [フィルター関数を使用して、移行する行を選択する](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)」を参照してください。  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
 GO
```  
  
 詳細については、「 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
### <a name="create-a-new-table-with-stretch-database-enabled"></a>Stretch Database が有効になっている新しいテーブルを作成する  
 Stretch Database が有効になっている新しいテーブルを作成するには、CREATE TABLE コマンドを実行します。  
  
 次に、テーブル全体を移行し、データ移行をすぐに開始する例を示します。  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name>
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 次に、 `dbo.fn_stretchpredicate` インライン テーブル値関数によって識別される行だけを移行し、データ移行を延期する例を示します。 フィルター関数の詳細については、「 [フィルター関数を使用して、移行する行を選択する](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)」を参照してください。  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name> 
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
GO  
```  
  
 詳細については、「 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  
