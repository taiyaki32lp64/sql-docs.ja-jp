---
title: 廃止された機能
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 14a5a6e38d4c9fcf306436374d80dd1c1c08b27e
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413043"
---
# <a name="discontinued-functionality-in-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) で廃止された機能

  このトピックでは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] で使用できなくなった [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]の機能について説明します。 特定のバージョンのオペレーティング システムまたは [!INCLUDE[msCoName](../includes/msconame-md.md)] インターネット インフォメーション サービス (IIS) で廃止されたサポートに関する告知事項は含まれていません。 システムの前提条件の詳細については、次を参照してください。 [Hardware and Software Requirements for Installing SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)します。  
  
 このトピックの内容  
  
- [SQL Server 2014 Reporting Services で廃止された機能](#bkmk_sql14)  
  
- [SQL Server 2012 Reporting Services で廃止された機能](#bkmk_rc0)  
  
- [SQL Server 2008 R2 Reporting Services で廃止された機能](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Reporting Services で廃止された機能

 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] で廃止された [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]機能はありません。  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Reporting Services で廃止された機能

 ここでは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] で廃止された [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]機能について説明します。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] で廃止された [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]機能はありません。  
  
##  <a name="bkmk_kj"></a> SQL Server 2008 R2 Reporting Services で廃止された機能

 ここでは、 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]で廃止された機能について説明します。  
  
> [!NOTE]  
> SQL Server 2008 R2 は SQL Server 2008 のマイナー バージョン アップグレードなので、SQL Server 2008 のセクションのコンテンツも確認することをお勧めします。
  
### <a name="64-bit-platform-support"></a>64 ビット プラットフォームのサポート

 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 以降の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] コンポーネントでは、Windows Server 2003 または Windows Server 2003 R2 を実行している Itanium ベースのサーバーがサポートされなくなりました。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Windows Server 2008 を itanium ベース システムと Windows Server 2008 R2 for Itanium-Based Systems など、他の 64 ビット オペレーティング システムをサポートし続けます。 Windows Server 2003 または Windows Server 2003 R2 の Itanium ベース システム エディションにインストールされた [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] を [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] にアップグレードするには、まずオペレーティング システムをアップグレードする必要があります。  
  
### <a name="data-source-credentials-in-url-access"></a>URL アクセスでのデータ ソース資格情報

 URL アクセス パラメーター文字列*dsu:datasourcename 値 =* と*dsp:datasourcename 値 =* は、廃止されました。 以前のバージョンでは、これらのパラメーター文字列は、セキュリティで保護されていないブラウザー キャッシュにプレーンテキストで保存されます。  
  
## <a name="next-steps"></a>次の手順

 - [新機能については&#40;Reporting Services&#41;](what-s-new-reporting-services.md)
 - [SQL Server 2014 における SQL Server Reporting Services の動作変更](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)
 - [SQL Server 2014 における SQL Server Reporting Services の非推奨の機能](deprecated-features-in-sql-server-reporting-services-ssrs.md)