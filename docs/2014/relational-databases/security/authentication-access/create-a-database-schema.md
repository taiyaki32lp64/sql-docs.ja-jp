---
title: データベース スキーマの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3c3747149b23c6217f321eff9d19621189b89b66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011982"
---
# <a name="create-a-database-schema"></a>データベース スキーマの作成
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、スキーマを作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **スキーマを作成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   新しいスキーマは、データベース ユーザー、データベース ロール、またはアプリケーション ロールのいずれかのデータベース レベルのプリンシパルが所有します。 スキーマ内に作成されるオブジェクトはスキーマの所有者が所有し、 **sys.objects** 内の **principal_id**は NULL になります。 スキーマが含まれるオブジェクトの所有権は、データベース レベルのプリンシパルに譲渡できますが、スキーマ内のオブジェクトに対する CONTROL 権限は常にスキーマ所有者が保持します。  
  
-   データベース オブジェクトを作成する場合に、有効なドメイン プリンシパル (ユーザーまたはグループ) をオブジェクト所有者として指定すると、ドメイン プリンシパルがスキーマとしてデータベースに追加されます。 新しいスキーマは、そのドメイン プリンシパルが所有します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
  
-   データベースに対する CREATE SCHEMA 権限が必要です。  
  
-   別のユーザーを、作成されるスキーマの所有者として指定する場合、呼び出し元は、そのユーザーに対する IMPERSONATE 権限を持っている必要があります。 データベース ロールを所有者として指定する場合、呼び出し元は、データベース ロールのメンバーシップまたはデータベース ロールに対する ALTER 権限のいずれかを持っている必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
##### <a name="to-create-a-schema"></a>スキーマを作成するには  
  
1.  オブジェクト エクスプローラーで、 **[データベース]** フォルダーを展開します。  
  
2.  新しいデータベース スキーマを作成するデータベースを展開します。  
  
3.  **[セキュリティ]** フォルダーを右クリックし、 **[新規作成]** をポイントして、 **[スキーマ]** をクリックします。  
  
4.  **[スキーマ - 新規作成]** ダイアログ ボックスの **[全般]** ページで、 **[スキーマ名]** ボックスに新しいスキーマの名前を入力します。  
  
5.  **[スキーマの所有者]** ボックスに、スキーマを所有するデータベース ユーザーまたはロールの名前を入力します。 または、 **[検索]** をクリックして **[ロールとユーザーの検索]** ダイアログ ボックスを開きます。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>追加オプション  
 **[スキーマ - 新規作成]** ダイアログ ボックスには次の 2 つのページもあり、それぞれにオプションが用意されています:**[権限]**、**[拡張プロパティ]**。  
  
-   **[権限]** ページには、すべてのセキュリティ保護可能なリソースと、ログインに付与できる、セキュリティ保護可能なリソースに対する権限が一覧表示されます。  
  
-   **[拡張プロパティ]** ページでは、カスタム プロパティをデータベース ユーザーに追加できます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-schema"></a>スキーマを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the schema Sprockets owned by Annik that contains table NineProngs.   
    -- The statement grants SELECT to Mandar and denies SELECT to Prasanna.  
  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
  
 詳細については、「[CREATE SCHEMA &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-schema-transact-sql)」を参照してください。  
  
  
