---
title: FileTable の作成、変更、および削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], altering
- FileTables [SQL Server], dropping
- FileTables [SQL Server], creating
ms.assetid: 47d69e37-8778-4630-809b-2261b5c41c2c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 494eabcd54e7a8c28b3a68e99efca72ef80eb9e1
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811240"
---
# <a name="create-alter-and-drop-filetables"></a>FileTable の作成、変更、および削除
  新しい FileTable の作成や、既存の FileTable の変更または削除を行う方法について説明します。  
  
##  <a name="BasicsCreate"></a> FileTable の作成  
 FileTable は、定義済みおよび固定のスキーマがある特殊なユーザー テーブルです。 このスキーマは、FILESTREAM データ、ファイルとディレクトリの情報、およびファイルの属性を格納します。 FileTable スキーマの詳細については、「 [FileTable Schema](filetable-schema.md)」を参照してください。  
  
 Transact-SQL または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、新しい FileTable を作成することができます。 FileTable には固定スキーマがあるため、列の一覧を指定する必要はありません。 FileTable を作成するため、簡単な構文を指定することができます。  
  
-   ディレクトリ名。 FileTable フォルダー階層において、このテーブル レベルのディレクトリは、データベース レベルで指定されたデータベース ディレクトリの子になると同時に、テーブルに格納されるファイルまたはデータベースの親になります。  
  
-   FileTable の **Name** 列のファイル名に対して使用される照合順序の名前。  
  
-   自動的に作成される 3 つの主キーと一意の制約で使用する名前。  
  
###  <a name="HowToCreate"></a>方法:FileTable を作成する  
 **Transact-SQL を使用して FileTable を作成する**  
 FileTable を作成するには、**AS FileTable** オプションを指定して [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) ステートメントを呼び出します。 FileTable には固定スキーマがあるため、列の一覧を指定する必要はありません。 新しい FileTable には次の設定を指定できます。  
  
1.  **FILETABLE_DIRECTORY**。 FileTable に格納されたすべてのファイルおよびディレクトリのルート ディレクトリとなるディレクトリを指定します。 この名前は、データベース内のすべての FileTable ディレクトリ名の中で一意である必要があります。 一意性の比較では、現在の照合順序の設定とは関係なく、大文字と小文字は区別されません。  
  
    -   この値は、 **nvarchar(255)** のデータ型であり、 **Latin1_General_CI_AS_KS_WS**の固定の照合順序を使用します。  
  
    -   指定するディレクトリ名は、ファイル システムの有効なディレクトリ名に関する要件を満たしている必要があります。  
  
    -   この名前は、データベース内のすべての FileTable ディレクトリ名の中で一意である必要があります。 一意性の比較では、現在の照合順序の設定とは関係なく、大文字と小文字は区別されません。  
  
    -   FileTable を作成するときにディレクトリ名を指定しなかった場合は、FileTable そのものの名前がディレクトリ名として使用されます。  
  
2.  **FILETABLE_COLLATE_FILENAME**。 FileTable の **Name** 列に適用される照合順序の名前を指定します。  
  
    1.  指定した照合順序は、Windows のファイル名のセマンティクスに準拠するために、 **大文字と小文字を区別しない** 設定にする必要があります。  
  
    2.  **FILETABLE_COLLATE_FILENAME**の値を指定しない場合、または、 **database_default**を指定した場合は、現在のデータベースの照合順序が列に継承されます。 現在のデータベースの照合順序で大文字と小文字が区別される場合は、エラーが発生し、 **CREATE TABLE** 操作は失敗します。  
  
3.  自動的に作成される 3 つの主キーと一意の制約で使用する名前を指定することもできます。 名前を指定しなかった場合、このトピックで後述するように、システムで名前が自動生成されます。  
  
    -   **FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME**  
  
    -   **FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME**  
  
    -   **FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME**  
  
 **使用例**  
  
 次の例では、新しい FileTable を作成し、 **FILETABLE_DIRECTORY** と **FILETABLE_COLLATE_FILENAME**の両方に対してユーザー定義の値を指定します。  
  
```sql  
CREATE TABLE DocumentStore AS FileTable  
    WITH (   
          FileTable_Directory = 'DocumentTable',  
          FileTable_Collate_Filename = database_default  
         );  
GO  
```  
  
 次の例も、新しい FileTable を作成するものです。 ユーザー定義の値が指定されていないため、 **FILETABLE_DIRECTORY** の値が FileTable の名前に、 **FILETABLE_COLLATE_FILENAME** の値が database_default になります。また、主キーと一意の制約にはシステムで生成された名前が指定されます。  
  
```sql  
CREATE TABLE DocumentStore AS FileTable;  
GO  
```  
  
 **SQL Server Management Studio を使用して FileTable を作成する**  
 オブジェクト エクスプローラーで、選択したデータベースのオブジェクトを展開し、 **[テーブル]** フォルダーを右クリックして **[新しい FileTable]** をクリックします。  
  
 このオプションを選択すると、新しいスクリプト ウィンドウが開き、FileTable を作成するためにカスタマイズして実行できる Transact-SQL スクリプト テンプレートが表示されます。 **[クエリ]** メニューの **[テンプレート パラメーターの値の指定]** オプションを使用すると、スクリプトを簡単にカスタマイズできます。  
  
###  <a name="ReqCreate"></a> FileTable を作成するための要件と制限  
  
-   既存のテーブルは、変更して FileTable に変換することはできません。  
  
-   データベース レベルで前もって指定する親ディレクトリには、null ではない値を指定する必要があります。 データベースレベルのディレクトリを指定する方法については、「 [FileTable の前提条件の有効化](enable-the-prerequisites-for-filetable.md)」を参照してください。  
  
-   FileTable には、FILESTREAM 列が含まれているため、有効な FILESTREAM ファイル グループが必要です。 必要に応じて、FileTable を作成する **CREATE TABLE** コマンドの一部として、FILESTREAM ファイル グループを指定することもできます。 ファイル グループが指定されていない場合、FileTable はデータベースの既定の FILESTREAM ファイル グループを使用します。 データベースに FILESTREAM ファイル グループがない場合は、エラーが発生します。  
  
-   **CREATE TABLE...AS FILETABLE** ステートメントの一部としてテーブルの制約を作成することはできません。 ただし、制約を追加するには、後で **ALTER TABLE** ステートメントを使用します。  
  
-   **tempdb** データベースまたはその他のシステム データベースに FileTable を作成することはできません。  
  
-   一時テーブルとして、FileTable を作成することはできません。  
  
##  <a name="BasicsAlter"></a> FileTable の変更  
 FileTable は、定義済みおよび固定のスキーマがあるため、その列を追加または変更することはできません。 ただし、カスタム インデックス、トリガー、制約、およびその他のオプションを FileTable に追加することはできます。  
  
 ALTER TABLE ステートメントを使用して FileTable 名前空間 (システム定義の制約を含む) を有効または無効にする方法の詳細については、「 [FileTable の管理](manage-filetables.md)」を参照してください。  
  
###  <a name="HowToChange"></a> 方法:FileTable のディレクトリを変更する  
 **Transact-SQL を使用して FileTable のディレクトリを変更する**  
 ALTER TABLE ステートメントを呼び出し、有効な新しい値を **FILETABLE_DIRECTORY** SET オプションに指定します。  
  
 **例**  
  
```sql  
ALTER TABLE filetable_name  
    SET ( FILETABLE_DIRECTORY = N'directory_name' );  
GO  
```  
  
 **SQL Server Management Studio を使用して FileTable のディレクトリを変更する**  
 オブジェクト エクスプローラーで、FileTable を右クリックし、 **[プロパティ]** をクリックして、 **[テーブルのプロパティ]** ダイアログ ボックスを開きます。 **[FileTable]** ページで、 **[FileTable ディレクトリ名]** に新しい値を入力します。  
  
###  <a name="ReqAlter"></a> FileTable を変更するための要件と制限  
  
-   **FILETABLE_COLLATE_FILENAME**の値を変更することはできません。  
  
-   FileTable のシステムで定義された列を変更、削除、または無効にすることはできません。  
  
-   新しいユーザー列、計算列、または保存される計算列を FileTable に追加することはできません。  
  
##  <a name="BasicsDrop"></a> FileTable の削除  
 FileTable を削除するには、[DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql) ステートメントの通常の構文を使用します。  
  
 FileTable を削除すると、次のオブジェクトも削除されます。  
  
-   FileTable のすべての列に加え、インデックス、制約、トリガーなどテーブルに関連付けられているすべてのオブジェクトが削除されます。  
  
-   FileTable ディレクトリと、その下位にあったサブディレクトリも、データベースの FILESTREAM ファイルとディレクトリ階層から消失します。  
  
 FileTable のファイルの名前空間内に開いているファイル ハンドルがある場合、DROP TABLE コマンドは失敗します。 開いているハンドルを閉じる方法の詳細については、「 [FileTable の管理](manage-filetables.md)」を参照してください。  
  
##  <a name="BasicsOtherObjects"></a> FileTable を作成したときに作成されるその他のデータベース オブジェクト  
 新しい FileTable を作成すると、システム定義のインデックスと制約もいくつか作成されます。 これらのオブジェクトを変更または削除することはできません。これらは、FileTable 自体が削除されると一緒に削除されます。 これらのオブジェクトの一覧を表示するには、カタログ ビュー [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql) に対してクエリを実行します。  
  
```sql  
--View all objects for all filetables, unsorted  
SELECT * FROM sys.filetable_system_defined_objects;  
GO  
  
--View sorted list with friendly names  
SELECT OBJECT_NAME(parent_object_id) AS 'FileTable', OBJECT_NAME(object_id) AS 'System-defined Object'  
    FROM sys.filetable_system_defined_objects  
    ORDER BY FileTable, 'System-defined Object';  
GO  
```  
  
 **新しい FileTable を作成するときに作成されるインデックス**  
 新しい FileTable を作成すると、次に示すシステム定義のインデックスも作成されます。  
  
|||  
|-|-|  
|**列**|**インデックスの種類**|  
|[path_locator] ASC|主キー、非クラスター化|  
|[parent_path_locator] ASC、<br /><br /> [name] ASC|一意、非クラスター化|  
|[stream_id] ASC|一意、非クラスター化|  
  
 **新しい FileTable を作成するときに作成される制約**  
 新しい FileTable を作成すると、次に示すシステム定義の制約も作成されます。  
  
|制約|強制|  
|-----------------|--------------|  
|次の列の既定の制約<br /><br /> **creation_time** <br /> **is_archive** <br /> **is_directory** <br /> **is_hidden** <br /> **is_offline** <br /> **is_readonly** <br /> **is_system** <br /> **is_temporary** <br /> **last_access_time** <br /> **last_write_time** <br /> **path_locator** <br /> **stream_id**|システム定義の既定の制約によって、指定した列に既定値が適用されます。|  
|CHECK 制約|システム定義の CHECK 制約によって、次の要件が適用されます。<br /><br /> 有効なファイル名。<br /><br /> 有効なファイル属性。<br /><br /> 親オブジェクトをディレクトリにする。<br /><br /> 名前空間の階層は、ファイル操作中にロックされる。|  
  
 **システム定義の制約の名前付け規則**  
 上で説明したシステム定義の制約は、 **\<constraintType>_\<tablename>[\_\<columnname>]\_\<uniquifier>** という形式で名前が付けられます。  
  
-   *<constraint_type>* は CK (CHECK 制約)、DF (DEFAULT 制約)、FK (外部キー)、PK (主キー)、または UQ (一意制約) です。  
  
-   *\<uniquifier>* は、名前を一意にする、システムによって生成された文字列です。 この文字列には、通常、FileTable の名前と一意の識別子が含まれています。  
  
## <a name="see-also"></a>関連項目  
 [FileTable の管理](manage-filetables.md)  
  
  
