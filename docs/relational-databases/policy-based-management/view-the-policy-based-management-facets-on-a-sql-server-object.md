---
title: オブジェクト上のポリシーベースの管理ファセットの表示
description: SQL Server Management Studio (SSMS) で特定の SQL Server オブジェクトに適用されているポリシーベースの管理ファセットをすべて表示する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facets
ms.assetid: 5f423b9f-a6c4-41a7-9d8d-8f4926ce1fb4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9284388a56014084b2478d6d805ff3fc917459d1
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558117"
---
# <a name="view-policy-based-management-facets-on-a-sql-server-object"></a>SQL Server オブジェクトのポリシーベースの管理ファセットの表示
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で特定の SQL Server オブジェクトに適用されているすべてのポリシー ベースの管理ファセットを表示する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してオブジェクトのすべてのファセットを表示するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-all-of-the-facets-in-an-object"></a>オブジェクトのすべてのファセットを表示するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス、インスタンス オブジェクト、データベース、またはデータベース オブジェクトを右クリックし、 **[ファセット]** をクリックします。  
  
2.  **[ファセットの表示 - _object_name_]** ダイアログ ボックスの **[ファセット]** ボックスの一覧で、プロパティを表示するファセットを選択します。 このダイアログ ボックスで利用可能なオプションの詳細については、「 [View Facets Dialog Box](../../relational-databases/policy-based-management/view-facets-dialog-box.md)」を参照してください。  
  
3.  完了したら、 **[OK]** をクリックします。  
  
  
