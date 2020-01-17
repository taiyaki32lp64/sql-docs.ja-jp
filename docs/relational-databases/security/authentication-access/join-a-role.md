---
title: ロールの追加 | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.DATABASEUSER.MEMBERSHIP.F1
helpviewer_keywords:
- adding a member to a role
- join a role
ms.assetid: 05c8d10d-5823-46c6-8b1a-81722da6a42b
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 909a8156556cd4a654dcfd6406de2bd45826e31b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990487"
---
# <a name="join-a-role"></a>ロールの追加
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、ログインおよびデータベース ユーザーにロールを割り当てる方法について説明します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で権限を効率的に管理するには、ロールを使用します。 ロールに権限を割り当て、そのロールに対してユーザーとログインの追加および削除を行います。 ロールを使用すると、権限をユーザーごとに個別に管理する必要がありません。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、4 種類のロールをサポートしています。  
  
-   固定サーバー ロール  
  
-   ユーザー定義サーバー ロール  
  
-   固定データベース ロール  
  
-   ユーザー定義データベース ロール  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]では、固定ロールは自動的に使用可能になります。 固定ロールには、一般的なタスクを実行するのに必要な権限があります。 固定ロールの詳細については、次のリンクを参照してください。 ユーザー定義ロールはユーザーが作成するもので、権限を選択してカスタマイズできます。 ユーザー定義ロールの詳細については、次のリンクを参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **ログインおよびデータベース ユーザーにロールを割り当てるために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   データベース ロールの名前を変更しても、ロールの ID 番号、所有者、権限は変わりません。  
  
-   データベース ロールは、sys.database_role_members および sys.database_principals カタログ ビューで確認できます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する **ALTER ANY ROLE** アクセス許可、ロールに対する **ALTER** アクセス許可、または **db_securityadmin**のメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>固定サーバー ロールにメンバーを追加するには  
  
1.  オブジェクト エクスプローラーで、固定サーバー ロールを編集するサーバーを展開します。  
  
2.  **[セキュリティ]** フォルダーを展開します。  
  
3.  **[サーバー ロール]** フォルダーを展開します。  
  
4.  編集するロールを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[サーバー ロールのプロパティ - _server\_role\_name_]** ダイアログ ボックスの **[メンバー]** ページで、 **[追加]** をクリックします。  
  
6.  **[サーバー ログインまたはロールの選択]** ダイアログ ボックスで、 **[選択するオブジェクト名を入力してください (例)]** に、このサーバー ロールに追加するログインまたはサーバー ロールを入力します。 または、 **[参照...]** をクリックし、 **[オブジェクトの参照]** ダイアログ ボックスに表示されるいずれかのオブジェクトまたはすべてのオブジェクトを選択します。 **[OK]** をクリックして **[サーバー ロールのプロパティ - _server\_role\_name_]** ダイアログ ボックスに戻ります。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>ユーザー定義データベース ロールにメンバーを追加するには  
  
1.  オブジェクト エクスプローラーで、ユーザー定義のデータベース ロールを編集するサーバーを展開します。  
  
2.  **[データベース]** フォルダーを展開します。  
  
3.  ユーザー定義のデータベース ロールを編集するデータベースを展開します。  
  
4.  **[セキュリティ]** フォルダーを展開します。  
  
5.  **[ロール]** フォルダーを展開します。  
  
6.  **[サーバー ロール]** フォルダーを展開します。  
  
7.  編集するロールを右クリックし、 **[プロパティ]** をクリックします。  
  
8.  **[データベースロールのプロパティ - _database\_role\_name_]** ダイアログ ボックスの **[全般]** ページで、 **[追加]** をクリックします。  
  
9. **[データベース ユーザーまたはロールの選択]** ダイアログ ボックスで、 **[選択するオブジェクト名を入力してください (例)]** に、このデータベース ロールに追加するログインまたはデータベース ロールを入力します。 または、 **[参照...]** をクリックし、 **[オブジェクトの参照]** ダイアログ ボックスに表示されるいずれかのオブジェクトまたはすべてのオブジェクトを選択します。 **[OK]** をクリックして **[データベースロールのプロパティ - _database\_role\_name_]** ダイアログ ボックスに戻ります。  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>固定サーバー ロールにメンバーを追加するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    ALTER SERVER ROLE diskadmin ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 詳細については、「[ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md)」を参照してください。  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>ユーザー定義データベース ロールにメンバーを追加するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    ALTER ROLE Marketing ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 詳細については、「[sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [サーバー レベルのロール](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [データベース レベルのロール](../../../relational-databases/security/authentication-access/database-level-roles.md)   
 [アプリケーション ロール](../../../relational-databases/security/authentication-access/application-roles.md)  
  
  
