---
title: データベース スキーマの作成 | Microsoft Docs
ms.custom: ''
ms.date: 07/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 980b179f39edc3e93e5cb0bc105b6b2f8d12bb58
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903751"
---
# <a name="create-a-database-schema"></a>データベース スキーマの作成
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、スキーマを作成する方法について説明します。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   新しいスキーマは、データベース ユーザー、データベース ロール、またはアプリケーション ロールのいずれかのデータベース レベルのプリンシパルが所有します。 スキーマ内に作成されるオブジェクトはスキーマの所有者が所有し、 **sys.objects** 内の **principal_id**は NULL になります。 スキーマが含まれるオブジェクトの所有権は、データベース レベルのプリンシパルに譲渡できますが、スキーマ内のオブジェクトに対する CONTROL 権限は常にスキーマ所有者が保持します。  
  
-   データベース オブジェクトを作成する場合に、有効なドメイン プリンシパル (ユーザーまたはグループ) をオブジェクト所有者として指定すると、ドメイン プリンシパルがスキーマとしてデータベースに追加されます。 新しいスキーマは、そのドメイン プリンシパルが所有します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
  
-   データベースに対する CREATE SCHEMA 権限が必要です。  
  
-   別のユーザーを、作成されるスキーマの所有者として指定する場合、呼び出し元は、そのユーザーに対する IMPERSONATE 権限を持っている必要があります。 データベース ロールを所有者として指定する場合、呼び出し元は、データベース ロールのメンバーシップまたはデータベース ロールに対する ALTER アクセス許可のいずれかを持っている必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
##### <a name="to-create-a-schema"></a>スキーマを作成するには  
  
1.  オブジェクト エクスプローラーで、 **[データベース]** フォルダーを展開します。  
  
2.  新しいデータベース スキーマを作成するデータベースを展開します。  
  
3.  **[セキュリティ]** フォルダーを右クリックし、 **[新規作成]** をポイントして、 **[スキーマ]** をクリックします。  
  
4.  **[スキーマ - 新規作成]** ダイアログ ボックスの **[全般]** ページで、 **[スキーマ名]** ボックスに新しいスキーマの名前を入力します。  
  
5.  **[スキーマの所有者]** ボックスに、スキーマを所有するデータベース ユーザーまたはロールの名前を入力します。 または、 **[検索]** をクリックして **[ロールとユーザーの検索]** ダイアログ ボックスを開きます。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

> [!NOTE]
> **Azure SQL Database** または **Azure SQL Data Warehouse** に対する SSMS を使用してスキーマを作成している場合、ダイアログ ボックスは表示されません。 生成されたスキーマ テンプレート作成 T-SQL ステートメントを実行する必要があります。
  
### <a name="additional-options"></a>追加オプション  
 **[スキーマ - 新規作成]** ダイアログ ボックスには次の 2 つのページもあり、それぞれにオプションが用意されています: **[権限]** 、 **[拡張プロパティ]** 。  
  
-   **[権限]** ページには、すべてのセキュリティ保護可能なリソースと、ログインに付与できる、セキュリティ保護可能なリソースに対する権限が一覧表示されます。  
  
-   **[拡張プロパティ]** ページでは、カスタム プロパティをデータベース ユーザーに追加できます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-schema"></a>スキーマを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例では、`Chains` という名前のスキーマを作成した後、`Sizes` という名前のテーブルを作成します。  
    ```sql  
    CREATE SCHEMA Chains;
    GO
    CREATE TABLE Chains.Sizes (ChainID int, width dec(10,2));
    ```

4.  追加オプションは、単一のステートメントで実行できます。 次の例では、Annik が所有するスキーマ `Sprockets` を作成します。このスキーマにはテーブル `NineProngs` が含まれます。 このステートメントは、Mandar に対して `SELECT` を許可し、Prasanna に対して `SELECT` を拒否します。  

    ```sql  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
5. このデータベースのスキーマを見るには、次のステートメントを実行します。

   ```sql
   SELECT * FROM sys.schemas;
   ```

 詳細については、「[CREATE SCHEMA &#40;Transact-SQL&#41;](../../../t-sql/statements/create-schema-transact-sql.md)」を参照してください。  
  
  
