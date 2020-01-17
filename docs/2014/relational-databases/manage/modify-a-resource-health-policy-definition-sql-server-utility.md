---
title: リソース正常性ポリシーの定義の変更 (SQL Server ユーティリティ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.UE.UTILITY.ADMINISTRATION.F1
ms.assetid: 27bec0b6-92e9-448e-8c70-fe36802cf128
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2b489fda1c051ecd08b63f28d6232a0e213d9fcb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188875"
---
# <a name="modify-a-resource-health-policy-definition-sql-server-utility"></a>リソース正常性ポリシーの定義の変更 (SQL Server ユーティリティ)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でリソース正常性ポリシーの定義を変更する方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティでリソース使用率のポリシーを変更する前に、ユーティリティ コントロール ポイント (UCP) を作成する必要があります。 詳細については、「 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのリソース使用率のポリシーは、データ層アプリケーション、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のマネージド インスタンス用に構成できます。 リソース使用率のポリシーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで、データ層アプリケーション、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスすべてに対してグローバルに定義できます。また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで、データ層アプリケーションごと、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスごとに個別に定義することもできます。 さらに、グローバル ポリシーを実装し、個々のデータ層アプリケーションまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の個々のマネージド インスタンスを独自のポリシー定義を使用して構成することも可能です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="modify-global-resource-utilization-policies-in-a-sql-server-utility"></a>SQL Server ユーティリティによるグローバル リソース使用率のポリシーの変更  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で UCP に接続します。  
  
2.  ユーティリティ エクスプローラーのナビゲーション ウィンドウで、 **[ユーティリティ管理]** をクリックして、グローバルな監視ポリシーを表示または変更した後、ユーティリティ エクスプローラーのコンテンツ ウィンドウで **[ポリシー]** タブをクリックします。  
  
3.  ユーティリティ エクスプローラーのコンテンツ ウィンドウで、矢印またはポリシーの説明をクリックして、 **[グローバルなデータ層監視ポリシーの設定]** または **[グローバルなマネージド インスタンス監視ポリシーの設定]** を選択します。  
  
4.  ポリシーの説明の右側にあるコントロールを使用して、過小使用ポリシーまたは過大使用ポリシーのしきい値を設定します。  
  
5.  必要に応じて、 **[適用]** 、 **[破棄]** 、または **[既定値に戻す]** ボタンをクリックします。 ポリシーの変更は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのダッシュボードおよびリスト ビューの詳細に反映されるまで最大 15 分かかる場合があります。  
  
6.  データを更新するには、ユーティリティ エクスプローラーのナビゲーション ウィンドウで **[ユーティリティ管理]** ノードを右クリックし、 **[更新]** をクリックします。  
  
#### <a name="modify-resource-health-policy-definitions-for-an-individual-data-tier-application-or-an-individual-managed-instance-of-sql-server-in-a-sql-server-utility"></a>SQL Server ユーティリティによる個々のデータ層アプリケーションまたは SQL Server マネージド インスタンスのリソース正常性ポリシー定義の変更  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で UCP に接続します。  
  
2.  ユーティリティ エクスプローラーのナビゲーション ウィンドウで、 **[配置済みのデータ層アプリケーション]** または **[マネージド インスタンス]** をクリックして、個々のデータ層アプリケーションやマネージド インスタンスの監視ポリシーを表示または変更します。  
  
3.  ユーティリティ エクスプローラーのコンテンツ ウィンドウのリスト ビューで、ポリシーを変更するデータ層アプリケーションまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前をクリックし、 **[ポリシーの詳細]** タブをクリックします。  
  
4.  矢印またはポリシーの説明をクリックして、表示または変更するポリシーを選択します。 既定では、グローバル ポリシーが選択されます。  
  
5.  グローバル ポリシーをオーバーライドして、指定したデータ層アプリケーションに個別のポリシー定義を実装するには、 **[グローバル ポリシーをオーバーライド]** をクリックします。  
  
6.  ポリシーの説明の右側にあるコントロールを使用して、過小使用ポリシーまたは過大使用ポリシーのしきい値を設定します。  
  
7.  必要に応じて、 **[適用]** 、 **[破棄]** 、または **[既定値に戻す]** ボタンをクリックします。 ポリシーの変更は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのダッシュボードおよびリスト ビューの詳細に反映されるまで最大 15 分かかる場合があります。  
  
8.  データを更新するには、ユーティリティ エクスプローラーのナビゲーション ウィンドウで **[配置済みのデータ層アプリケーション]** ノードを右クリックし、 **[更新]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)   
 [リソース正常性ポリシーの結果の表示 &#40;SQL Server ユーティリティ&#40;](view-resource-health-policy-results-sql-server-utility.md)  
  
  
