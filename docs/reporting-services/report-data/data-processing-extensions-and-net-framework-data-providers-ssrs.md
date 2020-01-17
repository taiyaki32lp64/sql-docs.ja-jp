---
title: データ処理拡張機能と .NET Framework データ プロバイダー (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
- report data [Report Builder], accessing
ms.assetid: 42a5afb5-f4c8-4957-b1fd-77bf39afa5be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 424dbb31ab96153dbf959c304456d8d1b2e4abd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573105"
---
# <a name="data-processing-extensions-and-net-framework-data-providers-ssrs"></a>データ処理拡張機能と .NET Framework データ プロバイダー (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能は、特定の種類のデータ ソースからのデータ取得や、レポート デザインやレポート処理をサポートする追加機能を提供することを目的として、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]と共にインストールされるコンポーネントです。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーは、特定の種類のデータ ソースからのデータの取得や変更を可能にする <xref:System.Data> インターフェイスをサポートするコンポーネントで、[!INCLUDE[msCoName](../../includes/msconame-md.md)] またはサード パーティ ソースから入手できます。  
  
## <a name="understanding-a-data-processing-extension"></a>データ処理拡張機能について  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能では、<xref:System.Data> インターフェイスのサブセットがサポートされています。 データ処理拡張機能には、データ ソースへの読み取り専用アクセスのみが必要です。書き込みおよび更新用のインターフェイスは実装されていません。 それぞれのデータ処理拡張機能では、レポート処理をサポートするカスタム機能を設定できます。 たとえば、データ処理拡張機能がサポートしている機能の種類は次のとおりです。  
  
-   資格情報を接続文字列とは別に管理  
  
-   複数値パラメーターのサポート  
  
-   データ ソースで計算されたサーバー集計の取得  
  
-   データ ソースからのデータ プロパティおよびデータ値の取得  
  
## <a name="understanding-a-data-provider"></a>データ プロバイダーについて  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダー (ドライバーと呼ばれることもある) では、データ ソースのデータを読み込み、書き込み、更新するための <xref:System.Data> インターフェイスの標準セットがサポートされています。 データ プロバイダーは、特定の種類のデータ ソースに対して使用できるデータ処理拡張機能がない場合に使用できます。 サード パーティの標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーは多数あります。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には拡張可能なデータ プロバイダー アーキテクチャがあるので、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能によって提供される追加機能を含めたカスタムのデータ処理拡張機能を構築することもできます。 詳細については、「 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)」を参照してください。 サード パーティのデータ処理拡張機能の詳細については、サード パーティのデータ処理拡張機能に付属するドキュメントを参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーまたはカスタム データ処理拡張機能を使用してデータ ソースのデータにアクセスするには、インストールと登録が事前に完了している必要があります。 レポートを作成するためのレポート クライアントと、パブリッシュされたレポートを表示するためのレポート サーバーの両方で、データ処理拡張機能をインストールおよび登録する必要があります。 すべてのデータ プロバイダーがサーバー環境で機能するように設計されているわけではありません。 詳細については、「[標準 .NET Framework データ プロバイダーを登録する &#40;SSRS&#41;](../../reporting-services/report-data/register-a-standard-net-framework-data-provider-ssrs.md)」と「[データ処理拡張機能の配置](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ処理拡張機能の概要](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)   
 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
