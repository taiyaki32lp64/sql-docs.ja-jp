---
title: 新しいポリシー ベースの管理条件の作成 | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policy conditions
ms.assetid: 8a612f7e-6c70-49db-a4de-48431e097cc5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 739d706749b24720861b7572bde7e29473f1d406
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901160"
---
# <a name="create-a-new-policy-based-management-condition"></a>新しいポリシー ベースの管理条件の作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でポリシー ベースの管理条件を作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **以下を使用して条件を作成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-condition"></a>条件を作成するには  
  
1.  **オブジェクト エクスプローラー**で、プラス記号をクリックして、ポリシー ベースの管理条件を作成するサーバーを展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  プラス記号をクリックして **[ファセット]** フォルダーを展開します。  
  
5.  新しい条件を作成するファセットを右クリックし、 **[新しい条件]** をクリックします。  
  
6.  **[新しい条件の作成]** ダイアログ ボックスで、 **[名前]** ボックスに新しい条件の名前を入力します。  
  
7.  **[ファセット]** ボックスの一覧で正しいファセットが選択されていることを確認します。正しくない場合は、別のファセットを選択します。  
  
8.  **[式]** の **[フィールド]** ボックスで、ファセット プロパティとそれに関連する演算子および値を選択して条件式を構築します。 複数の式を追加する場合は、 **And** または **Or**を使用して式を結合できます。 [新しい条件の作成] ダイアログ ボックスで使用可能なオプションの詳細については、「[[新しい条件の作成] または [条件を開く] ダイアログ ボックスの [全般] ページ](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md)」、「[[新しい条件の作成] または [条件を開く] ダイアログ ボックスの [説明] ページ](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-description-page.md)」、および 「[[高度な編集] &#40;条件&#41; ダイアログ ボックス](../../relational-databases/policy-based-management/advanced-edit-condition-dialog-box.md)」を参照してください。  
  
9. 完了したら、 **[OK]** をクリックします。  
  
  
