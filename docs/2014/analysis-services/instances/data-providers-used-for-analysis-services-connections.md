---
title: Analysis Services 接続に使用されるデータ プロバイダー |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16e691ab6c6a6fcff4cb59fe54884fbb1b52268e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080098"
---
# <a name="data-providers-used-for-analysis-services-connections"></a>Analysis Services 接続に使用するデータ プロバイダー
  Analysis Services では、サーバーとデータにアクセスするために 3 種類のデータ プロバイダーを用意しています。 Analysis Services に接続するすべてのアプリケーションでは、これらのプロバイダーのいずれかを使用します。 これらのプロバイダーのうち、ADOMD.NET および Analysis Services 管理オブジェクト (AMO) の 2 つは、マネージド データ プロバイダーです。 Analysis Services OLE DB Provider (MSOLAP DLL) は、ネイティブ データ プロバイダーです。  
  
 複数のバージョンの Analysis Services を運用している組織では、Analysis Services データに接続しているユーザー ワークステーションに、最新バージョンのデータ プロバイダーをインストールする必要が生じることがあります。 新しいバージョンの Analysis Services に接続するには、それと同じメジャー リリースのデータ プロバイダーが必要です。 たとえば、[!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] に接続するには、各ワークステーションに、2014 リリースのデータ プロバイダーが必要です。 Excel では、接続する必要のあるデータ プロバイダーがインストールされますが、提供されるプロバイダーは、使用している Analysis Services と比べて古いことがあります。  
  
 このトピックの内容は次のとおりです。  
  
 [サーバーのバージョンを確認する方法](#bkmk_ServVers)  
  
 [Analysis Services データ プロバイダーのバージョンを確認する方法](#bkmk_LibUpdate)  
  
 [新しいバージョンのデータ プロバイダーを入手する方法](#bkmk_downloadsite)  
  
 [Analysis Services OLE DB Provider](#bkmk_OLE)  
  
 [ADOMD.NET](#bkmk_ADOMD)  
  
 [AMO](#blkmk_AMO)  
  
##  <a name="bkmk_ServVers"></a> サーバーのバージョンを確認する方法  
 Analysis Services インスタンスのバージョンを把握しておくと、組織のワークステーションに新しいバージョンのデータ プロバイダーをインストールする必要があるかどうかを判断するのに役立ちます。  
  
-   SQL Server Management Studio で Analysis Services インスタンスに接続します。 チェック、 をポイントするインスタンスを右クリックして**レポート**、 をクリック**全般**します。 エディションとバージョンのビルド情報がレポートに表示されます。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の初回リリースのメジャー ビルド番号は 12.0.2000.9 です。  
  
 バージョンおよびビルド情報の取得の詳細については、次を参照してください。[バージョンとエディションの SQL Server とそのコンポーネントを確認する方法](https://support.microsoft.com/kb/321185)します。  
  
##  <a name="bkmk_LibUpdate"></a> Analysis Services データ プロバイダーのバージョンを確認する方法  
 データ プロバイダーは、Excel など、日常的に Analysis Services データベースに接続するクライアント アプリケーションによって、Analysis Services と共にインストールされます。  
  
 Office 2007 では SQL Server 2005 のデータ プロバイダーがインストールされます。 Office 2010 では SQL Server 2008 のデータ プロバイダーがインストールされます。 Office 2013 では SQL Server 2012 のデータ プロバイダーがインストールされます。 複数のバージョンの Office または SQL Server を使用しており、必要な接続または機能を使用できない場合は、新しいバージョンのデータ プロバイダーのインストールが必要になることがあります。 各データ プロバイダーの複数のメジャー バージョンは、同じコンピューター上でサイド バイ サイドで実行できます。  
  
#### <a name="find-the-file-version-of-the-oledb-provider"></a>OLEDB プロバイダーのファイル バージョンを確認する  
  
1.  \Program Files\Microsoft Analysis Services\AS OLEDB\120 に移動します。  
  
2.  Msolap120.dll を右クリックし、をクリックして**プロパティ**します。  
  
 この場所にファイルが見つからない場合、またはフォルダーのパスに "AS OLEDB\110" または "AS OLEDB\90" が含まれている場合は、使用しているプロバイダーが古いため、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]に接続するには、新しいバージョン (AS OLEDB\11) をインストールする必要があります。  
  
#### <a name="find-the-file-version-of-adomdnet-and-amo"></a>ADOMD.NET および AMO のファイル バージョンを確認する  
  
1.  C:\Windows\Assembly に移動します。  
  
2.  Microsoft.AnalysisServices.AdomdClient を右クリックし、 **[プロパティ]** をクリックします。 **[バージョン]** をクリックします。  
  
     AMO の場合は、Microsoft.AnalysisServices を右クリックします。  
  
 リリース別のバージョンおよびビルド番号の詳細については、次を参照してください。 [blogspot の SQL Server ビルド](http://sqlserverbuilds.blogspot.com)します。  
  
##  <a name="bkmk_downloadsite"></a> 新しいバージョンのデータ プロバイダーを入手する方法  
 クライアント コンピューターにインストールされているバージョンは、データを提供しているサーバーのメジャー バージョンと一致する必要があります。 インストールされているサーバーが、ネットワーク内のワークステーションにインストールされているデータ プロバイダーより新しい場合は、新しいプロバイダーのインストールが必要になることがあります。  
  
#### <a name="find-the-data-providers-on-the-download-site"></a>ダウンロード サイトでデータ プロバイダーを探す  
  
1.  [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?LinkID=296473)にアクセスします。  
  
2.  **[インストール方法]** を展開します。  
  
3.  Analysis Services コンポーネントに関するセクションまで下方向へスクロールします。 ADOMD.NET、OLE DB Provider、および AMO が一覧の 2 ～ 4 番目にあります。 各ライブラリには、32 ビット版と 64 ビット版が用意されています。 64 ビット オペレーティング システムを実行しているサーバーと新しいワークステーションには、64 ビット版が必要になります。  
  
##  <a name="bkmk_OLE"></a> Analysis Services OLE DB Provider  
 Analysis Services OLE DB Provider は、Analysis Services データベース接続に使用されるネイティブ プロバイダーです。 MSOLAP は、接続要求をデータ プロバイダーに委任するために、ADOMD.NET および AMO の両方で間接的に使用します。 また、アプリケーション コードから OLE DB プロバイダーを直接呼び出すこともできます。この操作は、ソリューションの要件によってマネージド API を使用できない場合などに行います。  
  
 Analysis Services OLE DB Provider は、Analysis Services データベースにアクセスするためによく使用される SQL Server セットアップ、Excel などのアプリケーションによって自動的にインストールされます。 これは、ダウンロード センターからダウンロードして、手動でインストールすることもできます。 既定では、このプロバイダーは \Program Files\Microsoft Analysis Services フォルダーに置かれています。 このプロバイダーは、Analysis Services データへのアクセスに使用されるすべてのワークステーションにインストールする必要があります。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]に付属する Analysis Services OLE DB プロバイダーのバージョンは、MSOLAP130.dll です。 最近のバージョンとしては、MSOLAP10.dll (SQL Server 2008 および 2008 R2) と MSOLAP90.dll (SQL Server 2005) があります。  
  
 OLE DB Provider は多くの場合、接続文字列で指定されます。 Analysis Services 接続文字列では、別の用語体系を使用して、OLE DB プロバイダーを参照してください。MSOLAP します。\<バージョン > .dll  
  
 Excel 2013 と同時にインストールされる最新の Analysis Services OLE DB Provider は、MSOLAP.5.dll です。 以前のバージョンの Excel を実行しているワークステーションでは、多くの場合、MSOLAP.4.dll や MSOLAP.3.dll など、以前のバージョンを使用しています。 PowerPivot アドインなど、一部の Analysis Services 機能では、特定のバージョンの OLE DB Provider が必要です。 詳細については、「[接続文字列プロパティ (Analysis Services)](connection-string-properties-analysis-services.md)」を参照してください。  
  
##  <a name="bkmk_ADOMD"></a> ADOMD.NET  
 ADOMD.NET は、Analysis Services データの照会に使用するマネージド データ プロバイダーです。 Excel では、特定の Analysis Services キューブに接続する場合に、ADOMD.NET を使用します。 Excel に表示される接続文字列は、ADOMD.NET 接続の接続文字列です。  
  
 SQL Server セットアップによりインストールされた ADOMD.NET を SQL Server クライアント アプリケーションが使用して、Analysis Services に接続します。 Excel からのデータ接続をサポートするために、Office にこのライブラリがインストールされます。 SQL Server に含まれる他のデータ プロバイダーと同様に、カスタム コードでこのプロバイダーを使用している場合は ADOMD.NET を再配布することができます。 新しいバージョンの AMO をダウンロードして手動でインストールすることもできます (このトピックの「 [Analysis Services データ プロバイダーのバージョンを確認する方法](#bkmk_LibUpdate) 」を参照)。  
  
 ファイルのバージョン情報を確認するには、グローバル アセンブリ キャッシュで ADOMD.NET を参照してください。グローバル アセンブリ キャッシュには `Microsoft.AnalysisServices.AdomdClient`という名前で記載されています。  
  
 データベースに接続する場合、3 つすべてのライブラリの接続文字列プロパティはほぼ同じです。 ADOMD.NET (<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>) 用に定義した接続文字列のほとんどは、AMO および Analysis Services OLE DB Provider にも使用できます。 詳細については、「[接続文字列プロパティ (Analysis Services)](connection-string-properties-analysis-services.md)」を参照してください。  
  
 プログラムからの接続の詳細については、「 [ADOMD.NET での接続の確立](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net)」を参照してください。  
  
##  <a name="blkmk_AMO"></a> AMO  
 AMO は、サーバー管理およびデータ定義に使用するマネージド データ プロバイダーです。 たとえば、SQL Server Management Studio では AMO を使用して Analysis Services に接続します。  
  
 SQL Server セットアップによりインストールされた AMO を SQL Server クライアント アプリケーションが使用して、Analysis Services に接続します。 カスタム コードで AMO を使用する際に、AMO をダウンロードして手動でインストールすることもできます (このトピックの「 [Analysis Services データ プロバイダーのバージョンを確認する方法](#bkmk_LibUpdate) 」を参照)。 AMO は、グローバル アセンブリ キャッシュに `Microsoft.AnalysisServices`という名前で記載されています。  
  
 AMO を使用して接続は通常ごくわずかで構成される"データ ソース =\<servername >"。 接続が確立されたら、API を使用して、データベース コレクションおよび主要なオブジェクトを操作します。 SSDT と SSMS では、どちらも AMO を使用して、Analysis Services インスタンスに接続します。  
  
 プログラムによる接続の詳細については、「 [AMO 基本オブジェクトのプログラミング](https://docs.microsoft.com/bi-reference/amo/programming-amo-fundamental-objects)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Analysis Services への接続](connect-to-analysis-services.md)  
  
  
