---
title: アプリケーション ロールの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.approle.general.f1
helpviewer_keywords:
- application roles [SQL Server], creating
ms.assetid: 6b8da1f5-3d8e-4f88-b111-b915788b06f1
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 032c371fd37bb66392761fff24bd30efb2bd5b37
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011949"
---
# <a name="create-an-application-role"></a>アプリケーション ロールの作成
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]でアプリケーション ロールを作成する方法について説明します。 アプリケーション ロールは、特定のアプリケーションを使用する場合を除き、データベースへのユーザー アクセスを制限します。 アプリケーション ロールにはユーザーが含まれないため、 **[アプリケーション ロール]** が選択されている場合には、 **[ロール メンバー]** の一覧は表示されません。  
  
> [!IMPORTANT]  
>  アプリケーション ロールのパスワードを設定するときには、パスワードの複雑性が確認されます。 アプリケーション ロールを呼び出すアプリケーションは、これらのパスワードを格納する必要があります。 アプリケーション ロールのパスワードは常に暗号化して保存する必要があります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **アプリケーション ロールを作成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER ANY APPLICATION ROLE 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
##### <a name="to-create-an-application-role"></a>アプリケーション ロールを作成するには  
  
1.  オブジェクト エクスプローラーで、アプリケーション ロールを作成するデータベースを展開します。  
  
2.  **[セキュリティ]** フォルダーを展開します。  
  
3.  **[ロール]** フォルダーを展開します。  
  
4.  **[アプリケーション ロール]** フォルダーを右クリックし、 **[新しいアプリケーション ロール...]** をクリックします。  
  
5.  **[アプリケーション ロール - 新規]** ダイアログ ボックスの **[全般]** ページで、 **[ロール名]** ボックスに、新しいアプリケーション ロールの名前を入力します。  
  
6.  **[既定のスキーマ]** ボックスで、オブジェクト名の入力によってこのロールが作成するオブジェクトを所有するスキーマを指定します。 または、省略記号 **[...]** をクリックして、 **[スキーマの検索]** ダイアログ ボックスを開きます。  
  
7.  **[パスワード]** ボックスに、新しいロールのパスワードを入力します。 **[パスワードの確認]** ボックスに、パスワードを再度入力します。  
  
8.  **[このロールが所有するスキーマ]** から、このロールが所有するスキーマを選択または表示します。 スキーマを所有できるのは、1 つのスキーマまたはロールのみです。  
  
9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>追加オプション  
 **アプリケーション ロール - 新しい**ダイアログ ボックスでは、2 つのページのオプションも提供されます。**セキュリティ保護可能な**と**拡張プロパティ**します。  
  
-   **[セキュリティ保護可能なリソース]** ページには、すべてのセキュリティ保護可能なリソースと、ログインに付与できる、セキュリティ保護可能なリソースに対する権限が一覧表示されます。  
  
-   **[拡張プロパティ]** ページでは、カスタム プロパティをデータベース ユーザーに追加できます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-an-application-role"></a>アプリケーション ロールを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Creates an application role called "weekly_receipts" that has the password "987Gbv876sPYY5m23" and "Sales" as its default schema.  
  
    CREATE APPLICATION ROLE weekly_receipts   
        WITH PASSWORD = '987G^bv876sPY)Y5m23'   
        , DEFAULT_SCHEMA = Sales;  
    GO  
    ```  
  
 詳細については、「[CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-application-role-transact-sql)」を参照してください。  
  
  
