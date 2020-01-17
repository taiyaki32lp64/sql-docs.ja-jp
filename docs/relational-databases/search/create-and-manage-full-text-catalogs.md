---
title: フルテキスト カタログの作成と管理 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text search [SQL Server], using SQL Server Management Studio
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ed7e7f31da9cacaf4862c29ada9c98df9559f9c9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903860"
---
# <a name="create-and-manage-full-text-catalogs"></a>フルテキスト カタログの作成と管理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
フルテキスト カタログは、フルテキスト インデックスのグループの論理的なコンテナーです。 フルテキスト インデックスを作成する前に、フルテキスト カタログを作成する必要があります。

フルテキスト カタログは、ファイル グループに属さない仮想オブジェクトです。
  
##  <a name="creating"></a> フルテキスト カタログを作成する  

### <a name="create-a-full-text-catalog-with-transact-sql"></a>Transact SQL を使用してフルテキスト カタログを作成する
[CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) を使用します。 例:

```sql 
USE AdventureWorks;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
``` 

### <a name="create-a-full-text-catalog-with-management-studio"></a>Management Studio を使用してフルテキスト カタログを作成する
1.  オブジェクト エクスプローラーで、サーバーを展開し、 **[データベース]** を展開して、フルテキスト カタログを作成する対象のデータベースを展開します。  
  
2.  **[ストレージ]** を展開し、 **[フルテキスト カタログ]** を右クリックします。  
  
3.  **[新しいフルテキスト カタログ]** を選択します。  
  
4.  **[新しいフルテキスト カタログ]** ダイアログ ボックスで、再作成するカタログの情報を指定します。 詳細については、「[[新しいフルテキスト カタログ] &#40;[全般] ページ&#41;](/sql/database-engine/new-full-text-catalog-general-page)」を参照してください。  
  
    > [!NOTE]  
    >  フルテキスト カタログ ID は、00005 から始まり、新しいカタログが作成されるたびに 1 ずつ増加します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

##  <a name="props"></a>フルテキスト カタログのプロパティの取得  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数 **FULLTEXTCATALOGPROPERTY** を使用して、フルテキスト インデックスに関連するさまざまなプロパティの値を取得します。 詳細については、「[FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)」を参照してください。

たとえば、フルテキスト カタログ `Catalog1` 内のインデックスの数を取得するには、次のクエリを実行します。

```sql 
USE <database>;  
GO  
SELECT fulltextcatalogproperty('Catalog1', 'ItemCount');  
GO  
```  
  
次の表は、フルテキスト カタログに関連しているプロパティを示しています。 この情報は、フルテキスト検索の管理およびトラブルシューティングに役立ちます。 
  
|プロパティ|[説明]|  
|--------------|-----------------|  
|**AccentSensitivity**|アクセントの区別の設定。|
|**ImportStatus**|フルテキスト カタログがインポートされているかどうかを示します。|  
|**IndexSize**|フルテキスト カタログのサイズ (MB 単位)。| 
|**ItemCount**|現在フルテキスト カタログ内にあるフルテキスト インデックス項目の数。|  
|**MergeStatus**|マスター マージの実行状況を示します。| 
|**PopulateCompletionAge**|01/01/1990 00:00:00 から、最後のフルテキスト インデックス作成が完了した時刻までの時間 (秒単位)。| 
|**PopulateStatus**|作成状態。<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**UniqueKeyCount**|フルテキスト カタログ内にある一意のキーの数。| 

##  <a name="rebuildone"></a>フルテキスト カタログを再構築する  

Transact-SQL ステートメント [ALTER FULLTEXT CATALOG ...REBUILD](
../../t-sql/statements/alter-fulltext-catalog-transact-sql.md) を実行するか、SQL Server Management Studio (SSMS) で、次の処理を実行します。

1.  SSMS では、オブジェクト エクスプローラーで、サーバーを展開し、 **[データベース]** を展開して、再構築するフルテキスト カタログが格納されているデータベースを展開します。  
  
2.  **[ストレージ]** を展開し、 **[フルテキスト カタログ]** を展開します。  
  
3.  再構築するフルテキスト カタログの名前を右クリックし、 **[再構築]** を選択します。  
  
4.  **"フルテキスト カタログを削除して再構築しますか?"** という確認メッセージが表示されたら、 **[OK]** をクリックします。  
  
5.  **[フルテキスト カタログの再構築]** ダイアログ ボックスで、 **[閉じる]** をクリックします。  
   
##  <a name="rebuildall"></a>データベースのすべてのフルテキスト カタログの再構築  

1.  SSMS のオブジェクト エクスプローラーで、サーバーを展開し、 **[データベース]** を展開して、再構築するフルテキスト カタログが格納されているデータベースを展開します。  
  
2.  **[ストレージ]** を展開し、 **[フルテキスト カタログ]** を右クリックします。  
  
3.  **[すべて再構築]** を選択します。  
  
4.  **[すべてのフルテキスト カタログを削除して再構築しますか?]** という確認メッセージが表示されたら、 **[OK]** をクリックします。  
  
5.  **[すべてのフルテキスト カタログの再構築]** ダイアログ ボックスで、 **[閉じる]** をクリックします。  
  
  
  
##  <a name="removing"></a>データベースからフルテキスト カタログを削除する  

Transact-SQL ステートメント [DROP FULLTEXT CATALOG](
../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) を実行するか、SQL Server Management Studio (SSMS) で次の処理を実行します。

1.  SSMS のオブジェクト エクスプローラーで、サーバーを展開し、 **[データベース]** を展開して、削除するフルテキスト カタログを含むデータベースを展開します。  
  
2.  **[ストレージ]** を展開し、 **[フルテキスト カタログ]** を展開します。  
  
3.  削除するフルテキスト カタログを右クリックし、 **[削除]** を選択します。  
  
4.  **[オブジェクトの削除]** ダイアログ ボックスで **[OK]** をクリックします。  

## <a name="next-step"></a>次の手順
[フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)
