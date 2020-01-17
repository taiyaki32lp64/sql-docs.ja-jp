---
title: ポリシーからのポリシー ベースの管理ポリシーの評価 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: 0b3214bd-d0ab-45ab-9281-3d95507abe54
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 60fdd81c94bba0f7a8c0e96fc5d2f39f33fbaf7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705369"
---
# <a name="evaluate-a-policy-based-management-policy-from-that-policy"></a>ポリシーからのポリシー ベースの管理ポリシーの評価
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でポリシーを使用してそのポリシーを評価する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **以下を使用してポリシーを評価するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-evaluate-a-policy"></a>ポリシーを評価するには  
  
1.  **オブジェクト エクスプローラー**で、評価するポリシーを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  プラス記号をクリックして **[ポリシー]** フォルダーを展開します。  
  
5.  評価するポリシーを右クリックして、 **[評価]** をクリックします。  
  
6.  **[評価の結果]**  ダイアログ ボックスに、ポリシーの評価結果が表示されます。 ポリシーに準拠せず、ポリシー ベースの管理で再構成可能なプロパティを持つ対象の場合は、 **[適用]** をクリックしてポリシーへの準拠を適用できます。 **[ポリシーの評価]** ダイアログ ボックスで使用可能なオプションの詳細については、「 [Evaluate Policies Dialog Box, Policy Selection Page](evaluate-policies-dialog-box-policy-selection-page.md) 」および「 [Evaluate Policies Dialog Box, Evaluation Results Page](evaluate-policies-dialog-box-evaluation-results-page.md)」を参照してください。  
  
7.  完了したら、 **[閉じる]** をクリックします。  
  
  
