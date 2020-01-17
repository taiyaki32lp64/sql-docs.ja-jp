---
title: リソース正常性ポリシーの結果の表示 (SQL Server ユーティリティ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3e10d2bcd280e1c353fb30613a6d65b715caf82e
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907524"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>リソース正常性ポリシーの結果の表示 (SQL Server ユーティリティ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスおよびデータ層アプリケーションに関する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのリソース パラメーターを表示するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でユーティリティのダッシュボードを使用します。 詳細については、「 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="view-sql-server-utility-resource-health-policy-results"></a>SQL Server ユーティリティのリソース正常性ポリシーの結果の表示  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で、 **[表示]** をクリックし、 **[ユーティリティ エクスプローラー]** をクリックして、ユーティリティ エクスプローラーのナビゲーション ウィンドウを表示します。 コンテンツ ウィンドウを表示するには、 **[表示]** をクリックし、 **[ユーティリティ エクスプローラーのコンテンツ]** をクリックします。  
  
2.  ナビゲーション ウィンドウで、![](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility") **[ユーティリティへの接続]** をクリックします。 ユーティリティ コントロール ポイント (UCP) を作成していない場合、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスまたはデータ層アプリケーションを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録していない場合は、「 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。  
  
3.  UCP ノードをクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスおよびデータ層アプリケーションの概要データを表示します (更新するには右クリックします)。 ダッシュボードのデータは、コンテンツ ウィンドウに表示されます。  
  
4.  **[マネージド インスタンス]** ノードをクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスのリスト ビュー データを表示します (更新するには右クリックします)。 リスト ビューのデータは、コンテンツ ウィンドウに表示されます。  
  
5.  **[配置済みのデータ層アプリケーション]** ノードをクリックし、データ層アプリケーションのリスト ビュー データを表示します (更新するには右クリックします)。 リスト ビューのデータは、コンテンツ ウィンドウに表示されます。  

## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [CPU 使用率のポリシーにおけるノイズの軽減 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)   
 [マネージド インスタンスの詳細 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)   
 [ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)  
  
  
