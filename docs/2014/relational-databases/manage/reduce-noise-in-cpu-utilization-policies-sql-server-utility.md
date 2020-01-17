---
title: CPU 使用率のポリシーにおけるノイズの軽減 (SQL Server ユーティリティ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.SWB.UE.ReduceNoise.F1
ms.assetid: 94bf4d93-c0ff-4869-bde7-80c24866092e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ce41c287105f97ce4a9cc0ce92facf9919f7ad33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035793"
---
# <a name="reduce-noise-in-cpu-utilization-policies-sql-server-utility"></a>CPU 使用率のポリシーにおけるノイズの軽減 (SQL Server ユーティリティ)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのリソース使用率のポリシーでは、レポート ノイズや不要な違反を軽減するために、次の方法を使用します。  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-overutilized"></a>プロセッサ使用率にどのくらいの頻度で違反が生じると使用率が高いと報告されるか  
 違反の評価期間と許容範囲はどちらも、ユーティリティ エクスプローラーの **[ユーティリティ管理]** ノードの **[ポリシー]** タブの設定を使用して構成できます。 ポリシーを変更するには、ポリシーの説明の右側にあるスライダー コントロールを使用して、 **[適用]** をクリックします。 また、画面の下部にあるボタンを使用して、既定値を復元したり変更を破棄したりすることもできます。  
  
-   データ収集の間隔は 15 分です。 この値を構成することはできません。  
  
-   プロセッサ使用率ポリシーの既定のしきい値の上限は 70% です。 オプションの範囲は 0 ～ 100% です。  
  
-   プロセッサ過大使用に対する既定の評価期間は 1 時間です。 オプションの範囲は 1 時間 ～ 1 週間です。  
  
-   既定では、CPU の使用率が高いと報告されるのは、違反となるデータ ポイントの割合が 20% になった場合です。 オプションの範囲は 0 ～ 100% です。  
  
 たとえば、既定値に基づき、1 時間ごとに 4 つのデータ ポイントが収集され、ポリシーのしきい値は 20% とします。 この場合、既定では、1 時間の収集期間内に 1 件でも違反があれば、4 つのデータ ポイントの 25% が違反することになります。 既定値では、CPU の過大使用ポリシーのしきい値の違反が報告されます。  
  
 わずか 1 件の違反によって生成されるノイズを軽減するには、次の対策を検討してください。  
  
-   評価期間を 1 時間ずつ 6 時間まで延ばします。 6 時間で 1 件の違反は、データ ポイント サンプル 24 個のうちの 1 個です。 この場合、6 時間で、ポリシーのしきい値の 4 回の違反はポリシーが許容できる範囲ですが (データ ポイントの 16.7%)、6 時間の収集期間で、5 回またはそれ以上の違反で過大使用としてレポートされます (データ ポイントの 20% より大きい)。  
  
-   違反の割合に対する許容範囲を 1% ずつ 30% まで増やします。 1 時間で 1 件の違反は、データ ポイント サンプル 4 個のうちの 1 個です。 この場合、1 時間に 1 違反はポリシーの許容範囲ですが、1 時間の収集期間で 2 回、またはそれ以上の違反で過大使用としてレポートされます (データ ポイントの 30% より大きい)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスおよびデータ層アプリケーションのプロセッサ使用率のポリシーのしきい値を大きくします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスまたはデータ層アプリケーションのグローバルな CPU 使用率のポリシーを変更する方法については、「[ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](../../database-engine/utility-administration-sql-server-utility.md)」を参照してください。 個々の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの CPU 使用率のポリシーを変更する方法については、「[マネージド インスタンスの詳細 &#40;SQL Server ユーティリティ&#41;](../../database-engine/managed-instance-details-sql-server-utility.md)」を参照してください。 個々のデータ層アプリケーションの CPU 使用率のポリシーを変更する方法については、「[配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)」を参照してください。  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-underutilized"></a>プロセッサ使用率にどのくらいの頻度で違反が生じると使用率が低いと報告されるか  
 違反の評価期間と許容範囲はどちらも、ユーティリティ エクスプローラーの **[ユーティリティ管理]** ノードの **[ポリシー]** タブの設定を使用して構成できます。 ポリシーを変更するには、ポリシーの説明の右側にあるスライダー コントロールを使用して、 **[適用]** をクリックします。 また、画面の下部にあるボタンを使用して、既定値を復元したり変更を破棄したりすることもできます。  
  
-   データ収集の間隔は 15 分です。 この値を構成することはできません。  
  
-   プロセッサ使用率ポリシーの既定のしきい値の下限は 0% です。 オプションの範囲は 0 ～ 100% です。  
  
-   プロセッサ過小使用に対する既定の評価期間は 1 週間です。 オプションの範囲は 1 日 ～ 1 か月です。  
  
-   既定では、CPU の使用率が低いと報告されるのは、違反となるデータ ポイントの割合が 90% になった場合です。 オプションの範囲は 0 ～ 100% です。  
  
 既定値に基づき、毎週 672 個のデータ ポイントが収集されますが、ポリシーのしきい値は 0% です。 この場合、既定では、このポリシーによって、プロセッサの過小使用による違反が生成されることはありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスまたはデータ層アプリケーションのグローバルな CPU 使用率のポリシーを変更する方法については、「[ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](../../database-engine/utility-administration-sql-server-utility.md)」を参照してください。 個々の SQL Server インスタンスの CPU 使用率のポリシーを変更する方法については、「[マネージド インスタンスの詳細 &#40;SQL Server ユーティリティ&#41;](../../database-engine/managed-instance-details-sql-server-utility.md)」を参照してください。 個々のデータ層アプリケーションの CPU 使用率のポリシーを変更する方法については、「[配置済みのデータ層アプリケーションの詳細 &#40;SQL Server ユーティリティ&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [ユーティリティの管理 &#40;SQL Server ユーティリティ&#41;](../../database-engine/utility-administration-sql-server-utility.md)   
 [SQL Server ユーティリティでの SQL Server のインスタンスの監視](monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [リソース正常性ポリシーの定義の変更 &#40;SQL Server ユーティリティ&#41;](modify-a-resource-health-policy-definition-sql-server-utility.md)   
 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)  
  
  
