---
title: 'レッスン 2: 名前付け基準ポリシーの作成と適用'
description: このチュートリアルでは、SQL Server でポリシーベース管理に名前付け基準ポリシーを作成して適用する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87e51f4e-156c-4def-8572-76a15075d75e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ac5510320783c35c83f84118e9679da4fd351415
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558697"
---
# <a name="lesson-2-create-and-apply-a-naming-standards-policy"></a>レッスン 2: 名前付け基準ポリシーの作成と適用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
ポリシー ベースの管理の一部の種類のポリシーでは、ポリシーへの今後の準拠を適用するためのトリガーを作成することができます。 このレッスンでは、テーブルの名前付け基準を適用するポリシーを作成します。 その後に、ポリシーに違反するテーブルを作成してポリシーをテストします。  


## <a name="prerequisites"></a>前提条件
このチュートリアルを完了するには、SQL Server Management Studio と SQL Server を実行しているサーバーへのアクセスが必要です。

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールする。
  
## <a name="create-the-finance-database"></a>Finance データベースの作成  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でクエリ ウィンドウを開き、次のステートメントを実行します。  
  
    ```sql  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  オブジェクト エクスプローラーで、 **[データベース]** をクリックし、F5 キーを押してデータベースの一覧を更新します。  

## <a name="create-the-finance-tables-condition"></a>Finance テーブルの条件の作成 

1.  オブジェクト エクスプローラーで、 **[管理]** 、 **[ポリシー管理]** の順に展開し、 **[条件]** を右クリックして **[新しい条件]** をクリックします。 

   ![新しい条件](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-condition.png)
  
2.  **[新しい条件の作成]** ダイアログ ボックスで、 **[名前]** ボックスに「 **Finance のテーブル**」と入力します。  
    1. **[ファセット]** ボックスの一覧で **[マルチパート名]** を選択します。 
    1. すべてのテーブル名が文字列 **fintbl** で始まるように、 **[式]** 領域の **[フィールド]** ボックスで **\@Name** を選択し、 **[演算子]** ボックスで **[次のパターンに一致]** を選択し、 **[値]** ボックスに ```'fintbl%'``` と入力します。
    1. **[説明]** ページで、「 **Finance のテーブル名は必ず fintbl で始める**」と入力し、 **[OK]** をクリックして条件を作成します。  

    ![Finance テーブルの条件](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-tables-condition.png)
 
## <a name="create-the-finance-name-policy"></a>Finace Name ポリシーの作成  
  
1.  オブジェクト エクスプローラーで **[ポリシー]** を右クリックし、 **[新しいポリシー]** をクリックします。  

   ![新しいポリシー](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-policy.png)
  
2.  **[新しいポリシーの作成]** ダイアログ ボックスで、 **[名前]** ボックスに「 **Finance の名前**」と入力します。
    1. **[条件の確認]** ボックスの一覧で、 **[Finance のテーブル]** を選択します。 このボックスは **[マルチパート名]** 領域にあります。 
    1. **[対象]** 領域に、このポリシーを適用できるデータベース オブジェクトの一覧が表示されます。 **[すべてのテーブル]** のチェック ボックスをオンにします。
    1. **[有効]** チェック ボックスをオンにします ( **[要求時]** ポリシーには **[有効]** ボックスが適用されません)。
    1. **[評価モード]** の一覧で、 **[変更時: 回避]** を選択します。 これにより、Finance データベースでデータベース トリガーを作成することでポリシーが適用されるようになります。 
    1. **[サーバーの制限]** ボックスの一覧で **[なし]** を選択します。 
    1. **[説明]** ページで、'Table names in the Finance database must contain 'fintbl%' (Finance データベースのテーブル名には 'fintbl%' が含まれている必要があります。) の説明を追加します。 
    1. **[全般]** ページに戻り、 **[すべてのデータベース]** 領域で **[すべて]** を展開し、 **[新しい条件]** をクリックします。

    ![新しい Finance Name ポリシーの作成](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-policy-finance-name.png)
  
6.  **[新しい条件の作成]** ダイアログ ボックスで、 **[名前]** ボックスに「 **Finance データベース**」と入力します。
    1. **[式]** ボックスで、@Name = 'Finance' を追加して式を完成させ、 **[OK]** をクリックして条件ページを閉じます。 
  
    ![新しい 'finance database' 条件の作成](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-condition.png)

    > [!NOTE]  
    > Tab キーを押して **[値]** ボックスから移動しないと、 **[OK]** ボタンが有効にならない場合があります。  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="create-the-finance-policy-category"></a>Finance ポリシー カテゴリの作成  
  
1.  オブジェクト エクスプローラーで **[管理]** を展開し、 **[ポリシー管理]** を右クリックして、 **[カテゴリの管理]** をクリックします。  

   ![カテゴリの管理](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-categories.png)
  
2.  **[ポリシー カテゴリの管理]** ダイアログ ボックスで、 **[名前]** の下の空白のボックスに「 **Finance** 」と入力し、 **[データベースのサブスクリプションの要求]** チェック ボックスをオフにします。 **[データベースのサブスクリプションの要求]** では、インスタンス内のすべてのデータベースは、このポリシー カテゴリに属するポリシーをサブスクライブします。 このレッスンでは、Finance の名前ポリシーをサブスクライブするのは Finance データベースだけです。  

    ![ポリシー カテゴリの管理](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-policy-categories.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="subscribe-to-the-finance-policy-category"></a>Finance ポリシー カテゴリのサブスクライブ  
  
1.  オブジェクト エクスプローラーで **[データベース]** を展開し、 **[Finance]** を右クリックして、 **[ポリシー]** をポイントし、 **[カテゴリ]** をクリックします。 

   ![Finance ポリシー カテゴリ](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-categories.png)
  
2.  **Finance** カテゴリの **[サブスクライブ済み]** チェック ボックスをオンにします。  

   ![Finance ポリシーのサブスクライブ](Media/lesson-2-create-and-apply-a-naming-standards-policy/subscribe-to-finance.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="test-the-enforcement-of-the-finance-name-policy"></a>Finance Name ポリシーの強制のテスト  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でクエリ ウィンドウを開きます。 **Finance の名前** ポリシーに違反するテーブルの作成を試みる次のステートメントを実行します。 このテーブルは、テーブル名が文字列 **fintbl**で始まっていないため、ポリシーに違反します。  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    ポリシーにより、テーブルの作成が防止され、ポリシー名を含む情報メッセージが返されます。 

   ```
     Policy 'Finance Name' has been violated by 'SQLSERVER:\SQL\SQL\SQL2017\Databases\Finance\Tables\dbo.NewTable'.
     This transaction will be rolled back.
     Policy condition: '@Name LIKE 'fintbl%''
     Policy description: 'Tables names in the Finance database must contain 'fintbl%''.
     Additional help: '' : ''
     Statement: 'CREATE TABLE NewTable  
         (Col1 int)'.
     Msg 515, Level 16, State 2, Procedure msdb.sys.sp_syspolicy_execute_policy, Line 69 [Batch Start Line 2]
     Cannot insert the value NULL into column 'target_query_expression', table 'msdb.dbo.syspolicy_policy_execution_history_details_internal'; column does not allow nulls. INSERT fails.
     The statement has been terminated.
   ``` 
  
2.  有効な名前を指定するには、コードを次のように変更し、ステートメントを再度実行します。  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    今度はテーブルが作成されます。  
  
## <a name="apply-the-policy-to-the-whole-server"></a>サーバー全体へのポリシーの適用  
  
1.  現在、Finance ポリシー カテゴリをサブスクライブするのは Finance データベースだけです。 多くの場合、ポリシー カテゴリをサーバー全体に適用する方が簡単です。 オブジェクト エクスプローラーで **[管理]** を展開し、 **[ポリシー管理]** を右クリックして、 **[カテゴリの管理]** をクリックします。  
  
2.  **[ポリシー カテゴリの管理]** ダイアログ ボックスで Finance カテゴリを探し、Finance カテゴリの **[データベースのサブスクリプションの要求]** チェック ボックスをオンにします。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] これで Finance カテゴリがすべてのデータベースに適用されるようになります。ただし、作成した条件により、Finance の名前ポリシーは Finance データベースにのみ適用されることになります。 これは、条件を複雑に組み合わせることで、多数のサーバーに対して適切な方法でポリシーを適用できるということを示しています。  
  
## <a name="summary"></a>まとめ  
このチュートリアルでは、ポリシー ベースの管理の条件、ポリシー、およびポリシー グループを作成する方法と、フィルターを適用してポリシー ベースの管理対象がポリシーに準拠しているかどうかを調べる方法について学習しました。  
  
## <a name="next"></a>Next  
このチュートリアルはこれで終了です。 先頭に戻る場合は、「[チュートリアル:ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md)」に移動してください。  
  
チュートリアルの一覧については、「 [SQL Server 2016 チュートリアル](../../sql-server/tutorials-for-sql-server-2016.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
