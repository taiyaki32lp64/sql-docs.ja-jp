---
title: SQL Server ユーティリティの機能とタスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server utility [SQL Server]
- utility control point
- Utility growth rate
- Multiserver management
- UCP
- Multi-server management [SQL Server]
ms.assetid: 6e6cbd25-6b1c-4e21-9ade-4584e243fd8f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1d3f61904a1a820df58583212dcbd2e998dbabbd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63190429"
---
# <a name="sql-server-utility-features-and-tasks"></a>SQL Server ユーティリティの機能とタスク
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境全体をまとめて管理する必要があります。このリリースでは、この管理作業に対して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのアプリケーションとマルチサーバーの管理という発想で対応しています。  
  
## <a name="benefits-of-the-sql-server-utility"></a>SQL Server ユーティリティの利点  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティでは、組織の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関連のエンティティを統合ビューでモデル化します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SSMS) のユーティリティ エクスプローラーと [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ユーティリティのビューポイントを使用すると、管理者は、ユーティリティ コントロール ポイント (UCP) として機能する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを通じて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースの正常性を総合的に確認することができます。 過小使用ポリシーと過大使用ポリシーの両方、およびさまざまな主要パラメーターについて、概要データと詳細データを組み合わせて UCP に表示すると、リソースの統合の可能性とリソースの過大使用を簡単に特定することができます。 正常性ポリシーは、構成可能なため、リソース使用率のしきい値の上限または下限を変更して調整できます。 グローバルな監視ポリシーを変更したり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで管理されているエンティティごとに個別の監視ポリシーを構成したりできます。  
  
##  <a name="typical_scenarios"></a> SQL Server ユーティリティの概要  
 一般的なユーザー シナリオでは、まず、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの中心的な裏付けとなるポイントを確立する、ユーティリティ コントロール ポイント (UCP) を作成します。 UCP は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスから収集されたリソースの正常性を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティでまとめて表示します。 UCP の作成後は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録して UCP で管理できるようにします。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで管理される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各インスタンスおよびデータ層アプリケーションは、グローバルのポリシー定義または個々のポリシー定義に基づいて監視できます。  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの基礎知識については、次の各トピックを参照してください。  
  
|||  
|-|-|  
|**説明**|**トピック**|  
|ユーティリティ コレクション セットと非ユーティリティ コレクション セットを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の同じインスタンス上で実行するようにサーバーを構成する際の注意点について説明します。|[SQL Server の同じインスタンスでユーティリティ コレクション セットとユーティリティ以外のコレクション セットを実行する場合の考慮事項](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)|  
|SQL Server ユーティリティ コントロール ポイントを作成する方法について説明します。|[SQL Server ユーティリティ コントロール ポイントの作成 &#40;SQL Server ユーティリティ&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md)|  
|SQL Server ユーティリティに接続する方法について説明します。|[SQL Server ユーティリティへの接続](connect-to-a-sql-server-utility.md)|  
|SQL Server のインスタンスをユーティリティ コントロール ポイントに登録する方法について説明します。|[SQL Server のインスタンスの登録 &#40;SQL Server ユーティリティ&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md)|  
|ユーティリティ エクスプローラーを使用して SQL Server ユーティリティを管理する方法について説明します。|[ユーティリティ エクスプローラーを使用した SQL Server ユーティリティの管理](use-utility-explorer-to-manage-the-sql-server-utility.md)|  
|SQL Server ユーティリティで SQL Server のインスタンスを監視する方法について説明します。|[SQL Server ユーティリティでの SQL Server のインスタンスの監視](monitor-instances-of-sql-server-in-the-sql-server-utility.md)|  
|リソース正常性ポリシーの結果を表示する方法について説明します。|[リソース正常性ポリシーの結果の表示 &#40;SQL Server ユーティリティ&#40;](view-resource-health-policy-results-sql-server-utility.md)|  
|リソース正常性ポリシーの定義を変更する方法について説明します。|[リソース正常性ポリシーの定義の変更 &#40;SQL Server ユーティリティ&#41;](modify-a-resource-health-policy-definition-sql-server-utility.md)|  
|UCP データ ウェアハウスを構成する方法について説明します。|[ユーティリティ コントロール ポイント データ ウェアハウスの構成 &#40;SQL Server ユーティリティ&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)|  
|ユーティリティ正常性ポリシーを構成する方法について説明します。|[正常性ポリシーの構成 &#40;SQL Server ユーティリティ&#41;](configure-health-policies-sql-server-utility.md)|  
|CPU 使用ポリシーの減弱を調整する方法について説明します。|[CPU 使用率のポリシーにおけるノイズの軽減 &#40;SQL Server ユーティリティ&#41;](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)|  
|SQL Server のインスタンスを UCP から削除する方法について説明します。|[SQL Server ユーティリティからの SQL Server のインスタンスの削除](remove-an-instance-of-sql-server-from-the-sql-server-utility.md)|  
|SQL Server のマネージド インスタンスでユーティリティ コレクション セットのプロキシ アカウントを変更する方法について説明します。|[SQL Server のマネージド インスタンスにおけるユーティリティ コレクション セットのプロキシ アカウントの変更 &#40;SQL Server ユーティリティ&#41;](change-proxy-account-for-utility-collection-on-managed-sql-server.md)|  
|SQL Server のインスタンス間で UCP を移動する方法について説明します。|[SQL Server のインスタンス間での UCP の移動 &#40;SQL Server ユーティリティ&#41;](move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility.md)|  
|UCP を削除する方法について説明します。|[ユーティリティ コントロール ポイントの削除 &#40;SQL Server ユーティリティ&#41;](remove-a-utility-control-point-sql-server-utility.md)|  
|SQL Server ユーティリティのトラブルシューティングの方法について説明します。|[SQL Server ユーティリティのトラブルシューティング](../../database-engine/troubleshoot-the-sql-server-utility.md)|  
|SQL Server リソース正常性をトラブルシューティングする方法について説明します。|[SQL Server のリソース正常性のトラブルシューティング &#40;SQL Server ユーティリティ&#41;](troubleshoot-sql-server-resource-health-sql-server-utility.md)|  
|ユーティリティ エクスプローラーの F1 ヘルプ トピックを紹介します。|[ユーティリティ エクスプローラーの F1 ヘルプ](utility-explorer-f1-help.md)|  
  
  
