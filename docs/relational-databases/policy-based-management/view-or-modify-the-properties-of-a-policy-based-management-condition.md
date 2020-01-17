---
title: ポリシーベースの管理条件のプロパティの表示または変更
description: SQL Server Management Studio (SSMS) または Transact-SQL (T-SQL) を使用し、ポリシーベースの管理条件のプロパティを表示したり、変更したりする方法について説明します。
ms.custom: ''
ms.date: 10/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view policy conditions
- Policy-Based Management, modify policy conditions
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e9a628b725222d0e77ed7fcb55b80ec8de153a55
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558127"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-condition"></a>ポリシー ベースの管理条件のプロパティの表示または変更
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でポリシー ベースの管理条件のプロパティを表示または変更する方法について説明します。  
  

  
##  <a name="BeforeYouBegin"></a> はじめに  
  

  
####  <a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-or-modify-a-conditions-properties"></a>条件のプロパティを表示または変更するには  
  
1.  **オブジェクト エクスプローラー**で、表示または変更する条件を含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  プラス記号をクリックして **[条件]** フォルダーを展開します。  
  
5.  表示または編集する条件を右クリックし、 **[プロパティ]** をクリックします。 **[条件を開く - _condition_name_]** ダイアログ ボックスで使用可能なオプションの詳細については、「[[新しい条件の作成] または [条件を開く] ダイアログ ボックスの [全般] ページ](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md)」、「[[条件を開く] ダイアログ ボックス、[依存ポリシー] ページ](../../relational-databases/policy-based-management/open-condition-dialog-box-dependent-policies-page.md)」、「[[新しい条件の作成] または [条件を開く] ダイアログ ボックスの [説明] ページ](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-description-page.md)」、「[[高度な編集] &#40;条件&#41; ダイアログ ボックス](../../relational-databases/policy-based-management/advanced-edit-condition-dialog-box.md)」を参照してください。  
  
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
  
 詳細については、「[syspolicy_conditions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md)」を参照してください。  
  
  
