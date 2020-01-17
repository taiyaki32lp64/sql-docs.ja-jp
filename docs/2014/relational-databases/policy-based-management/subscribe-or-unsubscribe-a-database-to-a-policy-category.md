---
title: ポリシー カテゴリへのデータベースのサブスクライブまたはアンサブスクライブ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.groupsubscription.f1
ms.assetid: d2c31769-7098-428e-ad9c-ef56541b7c52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d0139376adc28b07877389a023b19310b06417ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68212133"
---
# <a name="subscribe-or-unsubscribe-a-database--to-a-policy-category"></a>ポリシー カテゴリへのデータベースのサブスクライブまたはアンサブスクライブ
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、ポリシー カテゴリにデータベースをサブスクライブまたはアンサブスクライブする方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **ポリシー カテゴリにデータベースをサブスクライブまたはアンサブスクライブするために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 db_owner 固定データベース ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-subscribe-or-unsubscribe-a-database-to-a-policy-category"></a>ポリシー カテゴリにデータベースをサブスクライブまたはアンサブスクライブするには  
  
1.  **オブジェクト エクスプローラー**で、カテゴリのサブスクリプションを管理するデータベースが格納されているサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[データベース]** フォルダーを展開します。  
  
3.  カテゴリのサブスクリプションを管理するデータベースを右クリックし、 **[ポリシー]** をポイントし、 **[カテゴリ]** をクリックします。  
  
     **[カテゴリ]** ダイアログ ボックスでは、次のオプションを使用できます。  
  
     [列の展開]  
     クリックすると、ポリシー カテゴリが展開され、 カテゴリに含まれているすべてのポリシーが一覧表示されます。  
  
     **名前**  
     ポリシー カテゴリの名前です。  
  
     **[サブスクライブ済み]**  
     対象がポリシー カテゴリにサブスクライブしているかどうかを示します。 このチェック ボックスが無効になっている場合、ポリシー カテゴリの **[データベースのサブスクリプションの要求]** が設定されています。 つまり、ポリシー カテゴリはサーバー上のすべてのデータベースに適用されます。  
  
     **[ポリシー]**  
     ポリシー グループを展開すると、ポリシー カテゴリ内のポリシーが表示されます。  
  
     **有効**  
     ポリシーが有効であるかどうかを示します。  
  
     **[実行モード]**  
     ポリシーの実行モードが表示されます。  
  
     **履歴**  
     ログ ファイル ビューアーを開いてポリシー履歴を確認するには、[履歴の表示] ハイパーリンクをクリックします。  
  
4.  ポリシー ベースの管理カテゴリにサブスクライブするには、 **[サブスクライブ済み]** 列の下のカテゴリのチェック ボックスをオンにします。 カテゴリからアンサブスクライブするには、チェック ボックスをオフにします。  
  
5.  完了したら、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-subscribe-a-database-to-a-policy-category"></a>ポリシー カテゴリにデータベースをサブスクライブするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    -- Adds a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_subscribe_to_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 詳細については、「[sp_syspolicy_subscribe_to_policy_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql)」を参照してください。  
  
#### <a name="to-unsubscribe-a-database-to-a-policy-category"></a>ポリシー カテゴリからデータベースをアンサブスクライブするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    -- Deletes a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_unsubscribe_from_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 詳細については、「[sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql)」を参照してください。  
  
  
