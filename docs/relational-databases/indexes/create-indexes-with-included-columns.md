---
title: 付加列インデックスの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index size [SQL Server]
- index keys [SQL Server]
- index columns [SQL Server]
- size [SQL Server], indexes
- key columns [SQL Server]
- included columns
- nonclustered indexes [SQL Server], included columns
- designing indexes [SQL Server], included columns
- nonkey columns
ms.assetid: d198648d-fea5-416d-9f30-f9d4aebbf4ec
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c3ec437ccaaf3280be800ea6f80ac6ad38a0a1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024907"
---
# <a name="create-indexes-with-included-columns"></a>付加列インデックスの作成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用し、付加列 (非キー列) を追加して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]の非クラスター化インデックスの機能を拡張する方法について説明します。 非キー列を含めることにより、より多くのクエリをカバーする非クラスター化インデックスを作成できます。 これは、非キー列には次の利点があるためです。  
  
-   非キー列には、インデックス キー列として許可されていないデータ型を設定できる。  
-   インデックス キー列の数やインデックス キーのサイズを計算するときに、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では非キー列が考慮されない。  
  
 クエリ内のすべての列が、キー列または非キー列としてインデックスに含まれるているとき、非キー列を含むインデックスにより、クエリ パフォーマンスが大幅に向上します。 クエリ オプティマイザーではインデックス内のすべての列値を参照できるので、テーブルやクラスター化インデックスのデータにアクセスすることがなく、ディスク I/O 操作が少なくて済むため、パフォーマンスが向上します。  
  
> [!NOTE]  
> クエリによって参照されるすべての列がインデックスに含まれているときは、一般的に、そのインデックスは *クエリをカバーしている*と呼ばれます。  
   
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="DesignRecs"></a> 設計上の推奨事項  
  
-   検索や参照に使用される列のみがキー列になるように、大きなサイズのインデックス キーを使用して、非クラスター化インデックスを設計し直します。 クエリをカバーする他のすべての列を非キー列にします。 その結果、クエリをカバーするために必要なすべての列を含むことができますが、インデックス キー自体は小さく、効率的です。  
  
-   非クラスター化インデックスに非キー列を含め、現在のインデックス サイズの制限で (最大 32 個のキー列と、最大 1,700 バイトのインデックス キー サイズ) を超えないようにします ([!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] より前は、最大 16 個のキー列と最大 900 バイトのインデックス キーのサイズでした)。 インデックス キー列の数やインデックス キーのサイズを計算するときに、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では非キー列が考慮されません。  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   非キー列を定義できるのは、クラスター化されていないインデックスだけです。  
  
-   **text**、 **ntext**、 **image** を除くすべてのデータ型は、非キー列として使用できます。  
  
-   決定的な計算列は、正確かどうかに関係なく、非キー列にすることができます。 詳細については、「 [計算列のインデックス](../../relational-databases/indexes/indexes-on-computed-columns.md)」を参照してください。  
  
-   計算列が **image**、 **ntext**、 **text** の各データ型から派生している場合は、計算列のデータ型が非キー インデックス列として許可されている限り、非キー列にできます。  
  
-   インデックスを先に削除しない限り、非キー列をテーブルから削除できません。  
  
-   次の操作以外に、非キー列は変更できません。  
  
    -   列の NULL 値の許容を NOT NULL から NULL に変更する。  
  
    -   **varchar**、 **nvarchar**、または **varbinary** の各列の長さを拡張します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。 実行するには、 **sysadmin** 固定サーバー ロール、または **db_ddladmin** 固定データベース ロールおよび **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>非キー列を含むインデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、非キー列を含むインデックスの作成先となるテーブルが格納されているデータベースを、プラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、非キー列を含むインデックスの作成先となるテーブルを展開します。  
  
4.  **[インデックス]** フォルダーを右クリックし、 **[新しいインデックス]** をポイントし、 **[非クラスター化インデックス]** を選択します。  
  
5.  **[新しいインデックス]** ダイアログ ボックスの **[全般]** ページで、 **[インデックス名]** ボックスに新しいインデックスの名前を入力します。  
  
6.  **[インデックス キー列]** タブで、 **[追加...]** をクリックします。  
  
7.  _[table\_name_ **から列を選択]** ダイアログ ボックスで、インデックスに追加する 1 つまたは複数のテーブル列のチェック ボックスをオンにします。  
  
8.  **[OK]** をクリックします。  
  
9. **[付加列]** タブで、 **[追加...]** をクリックします。  
  
10. _[table\_name_ **から列を選択]** ダイアログ ボックスで、非キー列としてインデックスに追加する 1 つまたは複数のテーブル列のチェック ボックスをオンにします。  
  
11. **[OK]** をクリックします。  
  
12. **[新しいインデックス]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>非キー列を含むインデックスを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    -- Creates a nonclustered index on the Person.Address table with four included (nonkey) columns.   
    -- index key column is PostalCode and the nonkey columns are  
    -- AddressLine1, AddressLine2, City, and StateProvinceID.  
    CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
    GO  
    ```  

## <a name="related-content"></a>関連コンテンツ  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)    
[SQL Server インデックス デザイン ガイド](../../relational-databases/sql-server-index-design-guide.md)   
