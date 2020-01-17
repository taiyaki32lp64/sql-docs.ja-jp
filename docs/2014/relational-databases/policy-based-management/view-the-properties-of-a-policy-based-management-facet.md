---
title: ポリシー ベースの管理ファセットのプロパティの表示 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c819fc7fb3b1cc73b67362a0eabd82ad33946fbc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676865"
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>ポリシー ベースの管理ファセットのプロパティの表示
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でポリシー ベースの管理ファセットのプロパティを表示する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
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
  
5.  プロパティを表示するファセットを右クリックし、 **[プロパティ]** をクリックします。 **[ファセットのプロパティ -** facet_name _]_ ダイアログ ボックスで使用可能なオプションの詳細については、「[[ファセットのプロパティ] ダイアログ ボックスの [全般] ページ](../../integration-services/general-page-of-integration-services-designers-options.md)」、「[[ファセットのプロパティ] ダイアログ ボックスの [依存ポリシー] ページ](facet-properties-dialog-box-dependent-policies-page.md)」、「[[ファセットのプロパティ] ダイアログ ボックスの [依存条件] ページ](facet-properties-dialog-box-dependent-conditions-page.md)」をご覧ください。  
  
6.  完了したら、 **[閉じる]** をクリックします。  
  
  
