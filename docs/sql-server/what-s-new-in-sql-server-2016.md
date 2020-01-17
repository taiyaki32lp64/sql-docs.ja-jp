---
title: SQL Server 2016 の新機能
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
keywords:
- 新しい sql server
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 103f74b4a1be1ee2111f8ed3e983f8a468f8db2c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893032"
---
# <a name="whats-new-in-sql-server-2016"></a>SQL Server 2016 の新機能
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]  
 SQL Server 2016 では、メモリ内パフォーマンスや高度なセキュリティからデータベース内分析まで、すべてが組み込まれたスケーラブルなハイブリッド データベース プラットフォームを使って、インテリジェントでミッションクリティカルなアプリケーションをビルドできます。 SQL Server 2016 のリリースでは、さまざまな改善機能や拡張機能と共に、新しいセキュリティ機能、クエリ機能、Hadoop とクラウド統合、R 分析などが追加されています。 

このページでは、概要情報と、SQL Server 2016 の各 SQL Server コンポーネントの新機能に関する詳細情報へのリンクを提供します。 

![SQL Server 2016](../sql-server/media/sql-server-2016.png)

 **SQL Server 2016 をお試しください。** 
- **無料の** [**SQL Server 2016 Developer edition**](https://www.microsoft.com/cloud-platform/sql-server-editions-developers) をダウンロードしてください。
- 最新バージョンの [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) をダウンロードします。 
- Azure アカウントをすでにお持ちですか? [SQL Server 2016 がインストール済みの仮想マシン](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016)をすぐにご利用いただけます。

## <a name="sql-server-2016-database-engine"></a>SQL Server 2016 データベース エンジン
- SQL Server のインストールおよびセットアップ時に、**複数の tempDB** データベース ファイルを構成できます。
- 新しい**クエリ ストア**は、データベース内に、クエリ テキスト、実行プラン、およびパフォーマンス指標を格納するため、パフォーマンス問題の監視およびトラブルシューティングが容易になります。 ダッシュボードには、どのクエリが最も多くの時間、メモリまたは CPU リソースを消費しているのかが表示されます。
- **テンポラル テーブル**は、すべてのデータ変更とその発生日時を記録する履歴テーブルです。
- SQL Server に新しく組み込まれた **JSON サポート**は、JSON のインポート、エクスポート、解析および格納をサポートします。
- 新しい **PolyBase** クエリ エンジンは、Hadoop または Azure Blob Storage 内の外部データと SQL Server を統合します。 クエリの実行だけでなく、データをインポートおよびエクスポートすることができます。
- 新しい **Stretch Database** 機能を使用すれば、ローカル SQL Server データベースからクラウドの Azure SQL Database へ、動的かつ安全に、データをアーカイブすることができます。 SQL Server は、リンクされたデータベースのローカルとリモートの両方のデータに自動的にクエリを実行します。 
- **インメモリ OLTP:** 
    - 現在は、FOREIGN KEY、UNIQUE、CHECK などの制約、ネイティブ コンパイルされたストアド プロシージャの OR、NOT、SELECT DISTINCT、OUTER JOIN、および SELECT のサブクエリをサポートしています。
    - 最大テーブル 2 TB をサポートしています (256 GB 以上)。 
    - 並べ替えと Always On 可用性グループのサポートに対する列ストア インデックスの機能強化があります。
- 新しいセキュリティ機能
    - **Always Encrypted:** 有効にすると、暗号化キーを持つアプリケーションのみが、SQL Server 2016 データベースの暗号化された機密データにアクセスにできます。 キーが SQL Server に渡されることはありません。
    - **動的なデータ マスク:** テーブル定義で指定されている場合、マスクされたデータはほとんどのユーザーには非表示となり、UNMASK アクセス許可を持つユーザーのみがすべてのデータを参照できます。
    - **行レベル セキュリティ:** データ アクセスをデータベース エンジン レベルで制限できるため、ユーザーは自分に関係するもののみを参照できます。 

[データベース エンジン](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)に関する記事を参照してください。
## <a name="sql-server-2016-analysis-services-ssas"></a>SQL Server 2016 Analysis Services (SSAS)
SQL Server 2016 Analysis Services では、**1200 互換性レベル**に基づいて、表形式モデルのデータベースに対するパフォーマンス、オーサリング、データベース管理、フィルター、処理などが向上しています。
- **[SQL Server R サービス](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)** は、統計的分析に使用する R プログラミング言語を、SQL Server に統合します。 
- 新しい **Database Consistency Checker (DBCC)** は、潜在的なデータの破損の問題を検出するために、内部的に実行されます。
- **直接クエリ**は、最初に外部データをインポートするのではなく、ライブの外部データにクエリを実行します。直接クエリでは、Azure SQL、Oracle、Teradata を含む、より多くのデータ ソースがサポートされるようになりました。 
- 多数の新しい **DAX (Data Access Expressions) 関数**が追加されています。
- 新しい **[Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)** 名前空間は、表形式モードのインスタンスとモデルを管理します。 
- [Analysis Services Management Objects (AMO)](https://msdn.microsoft.com/library/mt436122.aspx) は、2 つ目のアセンブリ (**Microsoft.AnalysisServices.Core.dll**) を含めるためにリファクタリングされます。

[Analysis Services エンジン (SSAS)](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services) に関する記事を参照してください。 

## <a name="sql-server-2016-integration-services-ssis"></a>SQL Server 2016 Integration Services (SSIS)
- **Always On 可用性グループ**のサポート
- **パッケージの増分配置**
- **Always Encrypted** サポート
- 新しい **ssis_logreader** データベース レベルのロール
- 新しい**カスタム ログ記録レベル**
- データ フロー内の**エラー列の名前** 
- 新しい**コネクタ**
- **Hadoop ファイル システム (HDFS)** のサポート

[Integration Services (SSIS)](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md) を参照してください。

## <a name="sql-server-2016-master-data-services-mds"></a>SQL Server 2016 マスター データ サービス (MDS)
- 再帰的階層と多対多階層のサポートを含む**派生階層の機能強化**
- **ドメイン ベースの属性**フィルター
- モデルの間でエンティティ データを共有するための**エンティティ同期**
- **変更セット**を使用したワークフローの承認
- クエリ パフォーマンスを向上させる**カスタム インデックス**
- セキュリティの強化のための新しい**アクセス許可レベル**
- 再設計された**ビジネス ルール管理**エクスペリエンス

[マスター データ サービス (MDS)](../master-data-services/what-s-new-in-master-data-services-mds.md) を参照してください。

## <a name="sql-server-2016-reporting-services-ssrs"></a>SQL Server 2016 Reporting Services (SSRS)
Microsoft は、このリリースで Reporting Services を全面的に改良しました。 
- KPI 機能を持つ新しい **Web レポート ポータル**
- 新しい **Mobile Report Publisher**
- HTML5 をサポートする**再設計されたレポート表示エンジン** 
- 新しいツリー マップおよびサンバーストの**グラフの種類** 

[Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md) に関する記事を参照してください。

## <a name="next-steps"></a>次の手順   
- [SQL Server セットアップ](../database-engine/install-windows/installation-for-sql-server-2016.md)   
- [SQL Server 2016 リリース ノート](../sql-server/sql-server-2016-release-notes.md) 
- [SQL Server 2016 データシート](https://download.microsoft.com/download/C/5/3/C53C3AEF-653C-4598-8721-D522E8AC6A3A/SQL_Server_2016_Everything_Built-In_Datasheet_EN_US.pdf)
- [SQL Server の各エディションがサポートする機能](https://msdn.microsoft.com/library/cc645993.aspx)
- [SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [インストール ウィザードからの SQL Server 2016 のインストール](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [セットアップとサービスのインストール](https://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
- [新しい SQL PowerShell モジュール](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update/)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
