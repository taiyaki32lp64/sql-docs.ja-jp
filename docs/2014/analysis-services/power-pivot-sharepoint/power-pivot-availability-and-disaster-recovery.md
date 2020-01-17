---
title: PowerPivot の可用性とディザスターリカバリー (SQL Server 2014) |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4aaf008c-3bcb-4dbf-862c-65747d1a668c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 731550d385d073c7b2f2e2758d4fcaf2353db746
ms.sourcegitcommit: 9b8b11961b33e66fc9f433d094fc5c0f9b473772
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74908994"
---
# <a name="powerpivot-availability-and-disaster-recovery-sql-server-2014"></a>PowerPivot の可用性と災害復旧 (SQL Server 2014)
  
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] の可用性とディザスター リカバリー計画は主に、SharePoint ファームの設計、さまざまなコンポーネントで許容されるダウンタイムの長さ、SharePoint の可用性を高めるために実装するツールとベスト プラクティスに依存します。 このトピックでは、展開の可用性とディザスターリカバリーを計画する際に考慮する必要[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]のあるトポロジ図の例を示し、テクノロジの概要を説明します。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Sharepoint 2013 &#124; sharepoint 2010|  
  
 **このトピックの内容:**  
  
-   [PowerPivot の高可用性に関連する SharePoint 2013 のトポロジの例](#bkmk_sharepoint2013)  
  
-   [PowerPivot の高可用性に関連する SharePoint 2010 のトポロジの例](#bkmk_sharepoint2010)  
  
-   [PowerPivot サービスアプリケーションデータベースと SQL Server の可用性と復旧のテクノロジ](#bkmk_sql_server_technologies)  
  
-   [詳細情報へのリンク](#bkmk_more_resources)  
  
##  <a name="bkmk_sharepoint2013"></a>PowerPivot の高可用性のための SharePoint 2013 トポロジの例  
 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 を配置するときに、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] の可用性を設計する方法に関してより大きな柔軟性を実現できます。 SharePoint 2013 では、SharePoint モードで配置された [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスは、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] サーバーとも呼ばれますが、SharePoint ファームの外部で実行され、別のサーバーにインストールすることもできます。 SharePoint モードにある [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の各インスタンスは、Excel Services に登録されます。 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] の共有サービスとサービス アプリケーションは、SharePoint アプリケーション サーバー上で実行されます。  
  
 次の図に、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 の配置に関する例を示します。 この例では、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] サービスの適切な可用性をサポートしており、データベースを定期的にバックアップすることを前提としています。  
  
 ![2013 での PowerPivot の可用性](../media/ssas-powerpivot-services-2013.png "2013 での PowerPivot の可用性")  
  
-   **(1)** Web フロントエンドサーバー。 各サーバーにデータ プロバイダーをインストールするには、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 のアドインを使用します。 詳細については、「 [SharePoint 2013&#41;&#40;PowerPivot for SharePoint アドインをインストールまたはアンインストールする](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)」を参照してください。  
  
-   **(2)** 共有[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]サービスは各アプリケーションサーバー**上で**実行され、サービスアプリケーションはアプリケーションサーバー**間で**実行できます。 そのため、1 台のアプリケーション サーバーがオフラインになったときでも、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] アプリケーションは引き続き使用できます。  
  
-   **(3)** Excel Calculation Services は、アプリケーションサーバーごとに1つずつ実行し、サービスアプリケーションをアプリケーションサーバー間で実行できるようにします。 そのため、1 台のアプリケーション サーバーがオフラインになったときでも、Excel Calculation Services は引き続き使用できます。  
  
-   **(4)** および **(6)** sharepoint モード[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスは、sharepoint ファームの外部にあるサーバー上で実行されます。これには、Windows サービス**SQL Server Analysis Services (POWERPIVOT)** が含まれます。 これらのインスタンスのそれぞれは、Excel Services **(3)** に登録されます。 Excel Services は、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] サーバーに対する要求の負荷分散を管理します。 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 アーキテクチャを活用して、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] に対応する複数のサーバーを用意することができ、その結果、必要に応じてより多くのインスタンスを追加できます。 詳細については、「 [Excel Services のデータ モデルの設定を管理する (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\).aspx)」を参照してください。  
  
-   **(5)** コンテンツ、構成、およびアプリケーションデータベースに使用される SQL Server データベース。 これには、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] サービス アプリケーション データベースが含まれます。 DR (災害復旧) 計画に、データベース層を含める必要があります。 この設計では、データベースは、 **(4)**[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] インスタンスのいずれかと同じサーバーで実行されます。 **(4)** と **(5)** を別々のサーバーに配置することもできます。  
  
-   **(7)** 何らかの形式の SQL Server データベースのバックアップまたは冗長性。  
  
##  <a name="bkmk_sharepoint2010"></a>PowerPivot の高可用性のための SharePoint 2010 トポロジの例  
 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 のアーキテクチャでは、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のすべてのコンポーネントを同じ SharePoint アプリケーション サーバーで実行することが必要です。 これには、SharePoint モードで配置された [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスと、2 つの共有サービスが含まれますが、後者は SharePoint 2013 の配置で 1 つのみが使用される点とは対照的です。  
  
 次の図に、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 の配置に関する例を示します。 この例では、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] サービスの適切な可用性をサポートしており、データベースを定期的にバックアップすることを前提としています。  
  
 ![SharePoint 2010 での PowerPivot の可用性](../media/ssas-powerpivot-services-2010.png "SharePoint 2010 での PowerPivot の可用性")  
  
-   **(1)** Web フロントエンドサーバー。 各サーバーにデータ プロバイダーをインストールします。 「 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)」を参照してください。  
  
-   **(2)** 2 つ[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]の共有サービスと **(4)** Windows Service **SQL Server Analysis Services (POWERPIVOT)** が SharePoint アプリケーションサーバーにインストールされます。  
  
     
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System サービスは **各** アプリケーション サーバー上で動作し、サービス アプリケーションが複数のアプリケーション サーバーに **またがって** 動作できるようにします。 1 台のアプリケーション サーバーがオフラインになったときでも、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] サービス アプリケーションは引き続き使用できます。  
  
     SharePoint 2010 で [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のキャパシティを向上させるには、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System サービスを実行する SharePoint アプリケーション サーバーをさらに配置します。  
  
-   **(3)** Excel Calculation Services は各アプリケーションサーバー上で実行され、サービスアプリケーションはアプリケーションサーバー間で実行できます。 そのため、1 台のアプリケーション サーバーがオフラインになったときでも、Excel Calculation Services は引き続き使用できます。  
  
-   **(5)** コンテンツ、構成、およびアプリケーションデータベースに使用される SQL Server データベース。 これには、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] サービス アプリケーション データベースが含まれます。 DR (災害復旧) 計画に、データベース層を含める必要があります。  
  
-   **(6)** 何らかの形式の SQL Server データベースのバックアップまたは冗長性。  
  
##  <a name="bkmk_sql_server_technologies"></a>PowerPivot サービスアプリケーションデータベースと SQL Server の可用性と復旧のテクノロジ  
 SharePoint の高可用性実現計画には、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] サービス アプリケーション データベースを加えてください。 データベースの既定の名前は、 `DefaultPowerPivotServiceApplicationDB-<GUID>`です。 以下の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースと組み合わせて使用される [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] の可用性テクノロジと推奨事項をまとめたものです。 詳細については、「 [サポートされている SharePoint データベース用の高可用性とディザスター リカバリーのオプション (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx)」を参照してください。  
  
||備考|  
|-|--------------|  
|
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] と [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] の同期ミラーリングを同じファーム内で行うことによる可用性の確保|サポートはされますが、推奨はされません。 AlwaysOn は同期コミットモードで使用することをお勧めします。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)]同期コミットモードの場合|サポートされ、なおかつ推奨されます。|  
|
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 非同期ミラーリングまたはログ配布を別のファームとの間で行うことによるディザスター リカバリー|サポートされています。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)]非同期コミットとディザスターリカバリー|サポートされています|  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログ配布  
  
 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]を含んだコールド スタンドバイのシナリオを計画する方法の詳細については、 [PowerPivot の災害復旧](https://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx)に関するページを参照してください。  
  
## <a name="verification"></a>確認  
 ディザスターリカバリーサイクルの前後にデプロイを[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]検証するためのガイダンスとスクリプトについては、「[チェックリスト: PowerShell を使用して PowerPivot for SharePoint を検証](../instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)する」を参照してください。  
  
##  <a name="bkmk_more_resources"></a>詳細情報へのリンク  
  
-   [SharePoint データベースのサポートされている高可用性とディザスターリカバリーのオプション (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx)  
  
-   [ディザスターリカバリーの計画 (SharePoint Server 2010)](https://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)  
  

  
  
