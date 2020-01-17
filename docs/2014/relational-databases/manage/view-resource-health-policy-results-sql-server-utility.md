---
title: リソース正常性ポリシーの結果の表示 (SQL Server ユーティリティ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 52137a6405090ca52f3a99f21b400a573e606dc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63065577"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>リソース正常性ポリシーの結果の表示 (SQL Server ユーティリティ)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のマネージド インスタンスおよびデータ層アプリケーションに関する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ユーティリティのリソース パラメーターを表示するには、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] でユーティリティのダッシュボードを使用します。 詳細については、「 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)」を参照してください。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="view-sql-server-utility-resource-health-policy-results"></a>SQL Server ユーティリティのリソース正常性ポリシーの結果の表示  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (SSMS) で、 **[表示]** をクリックし、 **[ユーティリティ エクスプローラー]** をクリックして、ユーティリティ エクスプローラーのナビゲーション ウィンドウを表示します。 コンテンツ ウィンドウを表示するには、 **[表示]** をクリックし、 **[ユーティリティ エクスプローラーのコンテンツ]** をクリックします。  
  
2.  ナビゲーション ウィンドウで、 **[ユーティリティへの接続]** ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility") をクリックします。 ユーティリティ コントロール ポイント (UCP) を作成していない場合、または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスまたはデータ層アプリケーションを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ユーティリティに登録していない場合は、「 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)」を参照してください。  
  
3.  UCP ノードをクリックし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マネージド インスタンスおよびデータ層アプリケーションの概要データを表示します (更新するには右クリックします)。 ダッシュボードのデータは、コンテンツ ウィンドウに表示されます。  
  
4.  **[マネージド インスタンス]** ノードをクリックし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] マネージド インスタンスのリスト ビュー データを表示します (更新するには右クリックします)。 リスト ビューのデータは、コンテンツ ウィンドウに表示されます。  
  
5.  **[配置済みのデータ層アプリケーション]** ノードをクリックし、データ層アプリケーションのリスト ビュー データを表示します (更新するには右クリックします)。 リスト ビューのデータは、コンテンツ ウィンドウに表示されます。  
  
## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)   
 [CPU 使用率のポリシーにおけるノイズの軽減 &#40;SQL Server ユーティリティ&#41;](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [マネージド インスタンスの詳細 &#40;SQL Server ユーティリティ&#41;](../../database-engine/managed-instance-details-sql-server-utility.md)   
 [ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](../../database-engine/utility-administration-sql-server-utility.md)  
  
  
