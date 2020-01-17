---
title: ポリシー ベースの管理条件のプロパティの表示または変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view policy conditions
- Policy-Based Management, modify policy conditions
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 340423e23037ae401b1e5749fbed38b1822cfb41
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62677021"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-condition"></a>ポリシー ベースの管理条件のプロパティの表示または変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でポリシー ベースの管理条件のプロパティを表示または変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **表示またはを使用して、条件のプロパティを変更します。**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-or-modify-a-conditions-properties"></a>条件のプロパティを表示または変更するには  
  
1.  **オブジェクト エクスプローラー**で、表示または変更する条件を含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  プラス記号をクリックして **[条件]** フォルダーを展開します。  
  
5.  表示または編集する条件を右クリックし、 **[プロパティ]** をクリックします。 使用できるオプションの詳細については、**条件を開く -** _condition_name_ダイアログ ボックスを参照してください[新しい条件の作成または開く条件 ダイアログ ボックス、[全般] ページ](../../integration-services/general-page-of-integration-services-designers-options.md)、[条件ダイアログ ボックスの 依存ポリシーページを開く](open-condition-dialog-box-dependent-policies-page.md)、[新しい条件または条件を開く ダイアログ ボックス、[説明] ページを作成](create-new-condition-or-open-condition-dialog-box-description-page.md)、および[編集を高度な&#40;条件&#41; ダイアログ ボックス](advanced-edit-condition-dialog-box.md)します。  
  
6.  完了したら、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-a-conditions-properties"></a>条件のプロパティを表示するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       description,  
       facet,  
       expression,  
       is_name_condition,  
       obj_name  
    FROM syspolicy_conditions;  
    GO  
  
    ```  
  
 詳細については、「[syspolicy_conditions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syspolicy-conditions-transact-sql)」を参照してください。  
  
  
