---
title: ポリシーベースの管理ファセットのプロパティの表示
description: SQL Server Management Studio (SSMS) を使用し、SQL Server のポリシーベースの管理ファセットのプロパティを表示する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3a5a938928817b8ffb5282b2af7d2a505b442302
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558097"
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>ポリシー ベースの管理ファセットのプロパティの表示
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でポリシー ベースの管理ファセットのプロパティを表示する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してファセットのプロパティを表示するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-the-properties-of-a-facet"></a>ファセットのプロパティを表示するには  
  
1.  **オブジェクト エクスプローラー**で、プロパティを表示するファセットを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  プラス記号をクリックして **[ファセット]** フォルダーを展開します。  
  
5.  プロパティを表示するファセットを右クリックし、 **[プロパティ]** をクリックします。 **[ファセットのプロパティ -** facet_name _]_ ダイアログ ボックスで使用可能なオプションの詳細については、「[[ファセットのプロパティ] ダイアログ ボックスの [全般] ページ](../../relational-databases/policy-based-management/facet-properties-dialog-box-general-page.md)」、「[[ファセットのプロパティ] ダイアログ ボックスの [依存ポリシー] ページ](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-policies-page.md)」、「[[ファセットのプロパティ] ダイアログ ボックスの [依存条件] ページ](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-conditions-page.md)」をご覧ください。  
  
6.  完了したら、 **[閉じる]** をクリックします。  

