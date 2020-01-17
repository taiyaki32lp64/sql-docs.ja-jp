---
title: Analysis Services | で使用されるツールとアプリケーションMicrosoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c04742d0e0a84dd35e300bace9107685685ef75b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228902"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Analysis Services で使用するツールとアプリケーション
  Analysis Services モデルの構築および Analysis Services インスタンス上で関連付けられているデータベースの管理に必要なツールやアプリケーションを検索します。  
  
## <a name="analysis-services-model-designers"></a>Analysis Services モデルのデザイナー  
 テーブル モデルおよび多次元モデルは、Visual Studio シェル内で構築されたソリューションのプロジェクト テンプレートから作成されます。 このプロジェクト テンプレートには、Analysis Services ソリューションを構成するモデル、キューブ、ディメンション、ロールを作成するためのデザイナーが用意されています。  
  
### <a name="download-sql-server-data-tools-for-business-intelligence-ssdt-bi"></a>SQL Server Data Tools for Business Intelligence (SSDT-BI) のダウンロード  
 以前は Business Intelligence Development Studio (BIDS) と呼ばれていた、ビジネス インテリジェンス用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] (SSDT-BI) を使用して、Analysis Services モデル、Reporting Services レポート、および Integration Services パッケージを作成できます。 次の場所から SSDT-BI をダウンロードできます。  
  
-   [SSDT-BI for Visual Studio 2013 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=396526)  
  
-   [SSDT-BI for Visual Studio 2012 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkID=273673)  
  
 SSDT-BI または BIDS の以前のバージョンをコンピューターにインストールしていた場合は、新しいバージョンが以前のバージョンと共にサイド バイ サイドでインストールされます。 サーバーの特定のバージョンに関連付けられているプロジェクトとソリューションを変更できるように、1 台のワークステーションでデザイン ツールの新しいバージョンと以前のバージョンを実行することは一般的です。  
  
> [!NOTE]  
>  SSDT の Visual Studio 2012 バージョンと Visual Studio 2013 バージョンを入手できるダウンロード サイトは複数存在します。 ほとんどのダウンロードには、BI プロジェクト テンプレートが含まれていません。 上記のリンクを使用すると、適切なバージョンを取得できます。 [ビジネスインテリジェンスプロジェクトテンプレート] フォルダーが表示されている場合は、SSDT の正しいバージョンがあることがわかります。 このフォルダーには、Analysis Services、Reporting Services、および Integration Services 用のプロジェクト テンプレートが格納されています。 SSDT-BI をインストールした方法によっては、SQL Server データベース用の追加のプロジェクト テンプレートも表示されることがあります。  
  
 ![SSDT の新しいプロジェクト テンプレート](media/ssdt-biprojects.png "SSDT の新しいプロジェクト テンプレート")  
  
## <a name="administrative-tools"></a>管理ツール  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Management Studio は、Analysis Services を含むすべての SQL Server 機能用の主要な管理ツールです。 SQL Server Management Studio はオプションのコンポーネントです。 SQL Server Management Studio が他の SQL Server アプリケーションと一緒に Windows Server 2012 のアプリ ページに表示されない場合は、SQL Server セットアップを実行してインストールに追加します。  
  
### <a name="sql-server-profiler"></a>SQL Server プロファイラー  
 正式に非推奨とされていても、SQL Server Profiler は接続、MDX クエリの実行、および他のサーバー操作を簡単に監視する機能を提供します。 SQL Server Profiler は既定でインストールされます。 SQL Server アプリケーションと一緒に Windows Server 2012 のアプリ ページにあります。  
  
### <a name="powershell"></a>PowerShell  
 PowerShell コマンドを使用すると、多くの管理タスクを実行できます。 詳細については、「 [Analysis Services PowerShell](analysis-services-powershell.md) 」を参照してください。  
  
### <a name="community-and-third-party-tools"></a>コミュニティとサード パーティのツール  
 コミュニティ コードの例については、「 [Analysis Services Codeplex ページ](https://sqlsrvanalysissrvcs.codeplex.com/) 」を参照してください。 [フォーラム](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices)は、Analysis Services をサポートするサードパーティ製ツールの推奨事項を検索するときに役立ちます。  
