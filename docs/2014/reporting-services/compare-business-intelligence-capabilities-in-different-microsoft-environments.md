---
title: さまざまな Microsoft 環境でのビジネスインテリジェンス機能の比較 |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 12/15/2019
ms.openlocfilehash: 3305e682f6ccbbee4ac9710e29ae522eb7339910
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241209"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>さまざまな Microsoft 環境での Business Intelligence 機能の比較

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と SharePoint Server、SharePoint Online、および Power BI for Office 365 などのさまざまな環境で配置できます。 このトピックでは、各環境でサポートされるコンポーネントと機能を比較します。  
  
SharePoint Server と SharePoint Online の比較に関する詳細については、「 [Compare SharePoint plans and options](https://products.office.com/SharePoint/compare-sharepoint-plans)」を参照してください。  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>BI レポートとダッシュボードの作成と管理  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online Plan 2|Office 365 用 BI 機能|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|BI サイト|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]デザイン|いいえ|Power BI サイト|  
|データ スチュワードシップおよびクエリの共有と管理|いいえ|いいえ|はい** <sup>1</sup>**|  
|Master Data Services (MDS) と Data Quality Services (DQS) との統合|はい|いいえ|いいえ|  
|定期データ更新|可 (ただし Power Query データを含むブックはサポートしない)|いいえ|はい|  
|自然言語クエリ (Q&A)|いいえ|いいえ|はい** <sup>2</sup>**|  
|予測される予測|いいえ|いいえ|はい** <sup>3</sup>**|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]結合|はい|いいえ|いいえ|  
|
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 統合 (多次元および表形式)|はい|いいえ|いいえ|  
|対話型の Power View ダッシュボードを PowerPoint プレゼンテーションにエクスポートする|はい|いいえ|いいえ|  
|ブラウザー内のダッシュ ボードの作成|はい|いいえ|いいえ|  
|利用状況の監視|はい|いいえ|はい|  
|
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] キューブの行ベースのセキュリティの活用|はい|いいえ|いいえ|  
|||||

 **<sup>1</sup>**  [データ管理とビデオにおけるデータスチュワードの役割について理解する](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US) [: Power BI 情報管理とデータ管理](https://www.youtube.com/watch?v=8dHOj68ts7c)。  
  
 **<sup>2</sup>**  [Power BI Q&a: Power BI ブック (クラウドモデリング) を最適化](https://powerbi.microsoft.com/nl-nl/blog/new-in-power-bi-cloud-modeling-for-q-and-a/)します。  
  
 **<sup>3</sup>**  [Office 365 の Power View の新しい予測機能について紹介](https://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx)します。  
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>BI データ、レポート、およびダッシュボードの表示と参照  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online Plan 2|Office 365 用 BI 機能|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|ブラウザーで Microsoft Excel ブックを表示する|可 (ブックのサイズが 2 GB より小さい場合)|可 (ブックのサイズが 10 MB より小さい場合)|可 (ブックのサイズが 250 MB より小さい場合)|  
|HTML5 でのブラウザー内のデータ探索|いいえ|いいえ|はい|  
|レポートとダッシュ ボードにリモートでアクセスするモバイル BI アプリ|いいえ|いいえ|はい** <sup>1</sup>**|  
|
  [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] をデータ ソースとする Excel ブック **<sup>2</sup>**|はい|いいえ|いいえ|  
|機能をさまざまなブラウザーやバージョンで使用するための機能|可 (Power View の視覚化以外の場合) **<sup>3</sup>**|可 (ブック ファイルのサイズが 10 MB より小さい場合) **<sup>3</sup>**|はい** <sup>3</sup>**|  
|||||

 **<sup>1</sup>**  [Microsoft Power BI](https://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba)。  
  
 **<sup>2</sup>**  [データソースとしての PowerPivot ブック](https://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**  [ビジネスインテリジェンス (BI) ツールでのモバイルサポート](https://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx)と、 [Reporting Services と Power View のブラウザーサポートの計画 (Reporting Services 2014)](https://msdn.microsoft.com/library/ms156511.aspx)」を参照してください。  
  
## <a name="more-information"></a>詳細  
  
- [Excel および Office 365 の BI 機能](https://support.office.com/article/BI-capabilities-in-Excel-and-Office-365-26c0548e-124c-4fd3-aab3-5f64568cb743)。  
  
- シノニムを使用するための要件の詳細については、「pragmaticworks.com での[シノニム & 言い回しを使用した Power BI Q&の最適化](https://blog.pragmaticworks.com/optimizing-power-bi-qa-with-synonyms-phrasing-using-cloud-modeling)」を参照してください。  
  
- [Office Online では、企業のソーシャルネットワーク (Yammer またはニュースフィード) を選択](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US)します。  
  
- [Power BI for Office 365](https://www.microsoft.com/powerbi/default.aspx)。  
  
- [Power BI 料金](https://www.microsoft.com/powerBI/pricing.aspx)。  
  
- [Microsoft ビジネス インテリジェンス (BI) ツールでの分析とレポート](../reporting-services/choosing-microsoft-business-intelligence-bi-tools-for-analysis-and-reporting.md)  
  
## <a name="community-content"></a>コミュニティ コンテンツ

