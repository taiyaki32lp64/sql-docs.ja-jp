---
title: Analysis Services 多次元モデリングチュートリアルのサンプルデータとプロジェクトをインストールする |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fc475b25-cbb2-408a-901f-9299299538c5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0be986ee50599c6e95222bca2eae217b088e2de3
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530821"
---
# <a name="install-sample-data-and-projects-for-the-analysis-services-multidimensional-modeling-tutorial"></a>Analysis Services 多次元モデリング チュートリアル用のサンプル データおよびプロジェクトのインストール
  このトピックに示す手順とリンクを使用して、Analysis Services チュートリアルで使用するすべてのデータとプロジェクト ファイルをインストールします。  
  
## <a name="step-1-install-sql-server-software"></a>手順 1:SQL Server ソフトウェアのインストール  
 このチュートリアルのレッスンでは、次のソフトウェアをインストール済みであることを前提としています。 次のソフトウェアはすべて、SQL Server のインストール メディアを使用してインストールされます。 配置を簡単にするために、すべての機能を 1 台のコンピューターにインストールできます。 これらの機能をインストールするには、SQL Server セットアップを実行して [機能の選択] ページから機能を選択します。 詳細については、[インストールウィザード&#40;のセットアップ&#41;から SQL Server 2014 をインストールする](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)」を参照してください。  
  
-   データベース エンジン  
  
-   Analysis Services  
  
     Analysis Services は、次のエディションでのみ使用できます。評価、エンタープライズ、ビジネスインテリジェンス、標準。  
  
     SQL Server Express エディションには、Analysis Services は含まれないことに注意してください。 無料でのソフトウェアの試用を希望する場合は、[Evaluation Edition をダウンロード](https://go.microsoft.com/fwlink/?LinkId=392824)してください。  
  
     既定では Analysis Services は、多次元のインスタンスとしてインストールされますが、インストール ウィザードのサーバー構成ページで表形式のサーバー モードを選択することによりオーバーライドできます。 両方のサーバー モードを実行する場合は、同じコンピューター上の SQL Server セットアップを再実行して、他方のモードで Analysis Services の第 2 のインスタンスをインストールします。  
  
-   SQL Server Management Studio  
  
 チュートリアルを進めていくと、多次元データを参照することがあるので、必要に応じて Excel のインストールを検討してください。 Excel をインストールすると、構築するキューブに接続されているピボットテーブル フィールド リストを使用して Excel を起動する、" **Excel で分析** " 機能が有効になります。 データと対話するためのピボット レポートをすばやく作成できるので、Excel を使用してデータを参照することをお勧めします。  
  
 また、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]に組み込まれている MDX クエリ デザイナーを使用してデータを参照することもできます。 クエリ デザイナーでも同じデータが返されますが、データがフラットな行セットとして表示される点が異なります。  
  
## <a name="step-2-download-sql-server-data-tools---business-intelligence-for-visual-studio-2012"></a>手順 2:SQL Server Data Tools のダウンロード-Visual Studio 2012 用ビジネスインテリジェンス  
 このリリースでは、SQL Server Data Tools を他の SQL Server 機能とは別にダウンロードしてインストールします。 BI レポートおよび BI モデルの作成に使用するデザイナーとプロジェクト テンプレートは、現在、Web から無償でダウンロードできます。  
  
-   [ビジネス インテリジェンス バージョンの SQL Server Data Tools をダウンロードしてください](https://go.microsoft.com/fwlink/p/?LinkID=322038)。 ファイルはダウンロード フォルダーに保存されます。 セットアップを実行してツールをインストールします。  
  
     コンピューターを再起動してインストールを完了します。  
  
## <a name="step-3-install-databases"></a>手順 3:データベースのインストール  
 Analysis Services 多次元モデルでは、リレーショナル データベース管理システムからインポートしたトランザクション データを使用します。 このチュートリアルでは、次のリレーショナル データベースをデータ ソースとして使用します。  
  
-   **AdventureWorksDW2012** -これは、データベースエンジンインスタンスで実行されるリレーショナルデータウェアハウスです。 このチュートリアルで構築して配置する Analysis Services データベースおよびプロジェクトで使用される元のデータを提供します。  
  
     このサンプル データベースは、 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] に加えて [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]でも使用できます。  
  
 このデータベースをインストールするには、次の操作を行います。  
  
1.  CodePlex の製品サンプル ページから [AdventureWorkDW2012](https://go.microsoft.com/fwlink/p/?LinkID=221770) データベースをダウンロードします。  
  
     データベース ファイル名は、AdvntureWorksDW2012_Data.mdf です。 ファイルは、コンピューターのダウンロード フォルダーにあります。  
  
2.  AdventureWorksDW2012_Data.mdf ファイルを、SQL Server データベース エンジンのローカル インスタンスのデータ ディレクトリにコピーします。 既定では、このファイルは C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data にあります。  
  
3.  Microsoft SQL Server Management Studio を起動し、データベース エンジン インスタンスに接続します。  
  
4.  [データベース] を右クリックし、 **[アタッチ]** をクリックします。  
  
5.  **[追加]** をクリックします。  
  
6.  **AdventureWorksDW2012_Data.mdf** データベース ファイルを選択し、 **[OK]** をクリックします。 一覧にファイルが表示されない場合は、このファイルが C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data フォルダーにあることを確認します。  
  
7.  データベースの詳細で、ログ ファイルのエントリを削除します。 このセットアップ プログラムでは、ログ ファイルが存在することが前提とされていますが、サンプルにログ ファイルは含まれていません。 データベースをアタッチすると、新しいログ ファイルが自動的に作成されます。 ログ ファイルを選択して **[削除]** をクリックし、 **[OK]** をクリックして、プライマリ データベース ファイルだけをアタッチします。  
  
## <a name="step-4-grant-database-permissions"></a>手順 4:データベースアクセス許可の付与  
 サンプル プロジェクトでは、データがインポートまたは処理されるときのセキュリティ コンテキストを指定する、データ ソースの権限借用設定を使用します。 既定の権限借用設定では、データにアクセスするための Analysis Services サービス アカウントを指定します。 この既定の設定を使用するには、Analysis Services サービスを実行するサービス アカウントに、 **AdventureWorksDW2012** データベースに対するデータ リーダー権限を与える必要があります。  
  
> [!NOTE]  
>  学習のために、既定のサービス アカウントによる権限借用オプションを使用し、SQL Server のサービス アカウントにデータ リーダー権限を与えることをお勧めします。 他の権限借用オプションも使用できますが、それらのすべてが処理操作に適しているわけではありません。 特に、現在のユーザーの資格情報を使用するためのオプションは、処理ではサポートされていません。  
  
1.  サービス アカウントを確認します。 アカウント情報は、SQL Server 構成マネージャーまたは [サービス] コンソール アプリケーションを使用して表示できます。 既定のアカウントを使用して Analysis Services を既定のインスタンスとしてインストールした場合、サービスは **NT Service\MSSQLServerOLAPService**として実行されています。  
  
2.  Management Studio で、データベース エンジン インスタンスに接続します。  
  
3.  [セキュリティ] フォルダーを展開し、[ログイン] を右クリックして **[新しいログイン]** をクリックします。  
  
4.  [全般] ページの [ログイン名] に、「 **NT Service\MSSQLServerOLAPService** 」(またはサービスを実行している任意のアカウント) を入力します。  
  
5.  **[ユーザー マッピング]** をクリックします。  
  
6.  **AdventureWorksDW2012** データベースの横にあるチェック ボックスをオンにします。 ロールのメンバーシップには、 **db_datareader** および **public**が自動的に含まれます。 **[OK]** をクリックして、既定値をそのまま使用します。  
  
## <a name="step-5-install-projects"></a>手順 5:プロジェクトのインストール  
 このチュートリアルには、完了した状態のプロジェクトと結果を比較したり、さらに後続のレッスンを開始したりできるように、サンプル プロジェクトが含まれています。  
  
 レッスン 4 のプロジェクト ファイルは、レッスン 4 だけでなく後続のすべてのレッスンの基盤となるため、特に重要です。 チュートリアルの手順を実行すると完了した状態のプロジェクト ファイルの正確なコピーが作成された、それ以前のプロジェクト ファイルと異なり、レッスン 4 のサンプル プロジェクトは、レッスン 1 ～ 3 で作成したモデルに含まれない新しいモデル情報を含んでいます。 レッスン 4 は、次のダウンロードで入手できるサンプル プロジェクト ファイルを使用して作業を開始することを前提としています。  
  
1.  CodePlex の製品サンプル ページで [Analysis Services Tutorial SQL Server 2012](https://go.microsoft.com/fwlink/p/?LinkID=221866) をダウンロードします。  
  
     2012 のチュートリアルは [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] リリースで有効です。  
  
     "Analysis Services チュートリアル SQL Server 2012 .zip" ファイルは、コンピューターのダウンロードフォルダーに保存されます。  
  
2.  .zip ファイルをルート ドライブ直下のフォルダー (たとえば、C:\Tutorial) に移動します。 この手順では、ダウンロードフォルダー内のファイルを解凍しようとした場合に発生することがある "パスが長すぎる" というエラーが軽減されます。  
  
3.  ファイルを右クリックし、 **[すべて展開]** をクリックして、サンプル プロジェクトを解凍します。 ファイルを抽出すると、次のプロジェクトがコンピューターにインストールされます。  
  
    -   Lesson 1 Complete  
  
    -   Lesson 2 Complete  
  
    -   Lesson 3 Complete  
  
    -   Lesson 4 Complete  
  
    -   Lesson 4 Start  
  
    -   Lesson 5 Complete  
  
    -   Lesson 6 Complete  
  
    -   Lesson 7 Complete  
  
    -   Lesson 8 Complete  
  
    -   Lesson 9 Complete  
  
    -   Lesson 10 Complete  
  
4.  これらのファイルの読み取り専用権限を削除します。 親フォルダーである [Analysis Services Tutorial SQL Server 2012] を右クリックし、 **[プロパティ]** をクリックして、 **[読み取り専用]** のチェックボックスをオフにします。 **[OK]** をクリックします。 このフォルダー、サブフォルダー、およびファイルへの変更を適用します。  
  
5.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を起動します。  
  
6.  使用するレッスンに対応するソリューション (.sln) ファイルを開きます。 たとえば、Lesson 1 Complete というフォルダーで Analysis Services Tutorial.sln ファイルを開きます。  
  
7.  ソリューションを配置して、データベース権限およびサーバーの場所の情報が正しく設定されていることを確認します。  
  
     Analysis Services とデータベース エンジンが既定のインスタンス (MSSQLServer) としてインストールされ、すべてのソフトウェアが同じコンピューターで実行されている場合は、[ビルド] メニューの **[ソリューションの配置]** をクリックするとサンプル プロジェクトがビルドされ、ローカルの Analysis Services インスタンスに配置されます。 配置するときに、データベース エンジンのローカル インスタンスから **AdventureWorksDW2012** データベースが処理 (またはインポート) されます。 データベース エンジンから取得されたデータを含む Analysis Services インスタンス上で新しい Analysis Services データベースが作成されます。  
  
     エラーが発生した場合は、データベース権限の設定に関する前の手順を確認してください。 さらに、サーバー名の変更も必要になる場合があります。 既定のサーバー名は localhost です。 サーバーがリモート コンピューター上で、または名前付きインスタンスとしてインストールされている場合、インストールに対して有効なサーバー名を使用するように既定値をオーバーライドする必要があります。 さらに、サーバーがリモート コンピューターにある場合は、サーバーへのアクセスを許可するように Windows ファイアウォールの構成が必要になることがあります。  
  
     データベース エンジンに接続するためのサーバー名は、ソリューション エクスプローラーに表示される多次元ソリューション (Adventure Works チュートリアル) の Data Source オブジェクトで指定されます。  
  
     Analysis Services に接続するためのサーバー名は、プロジェクトの [プロパティ ページ] の [配置] タブで指定され、ソリューション エクスプローラーにも表示されます。  
  
8.  [SQL Server Management Studio] を起動します。 SQL Server Management Studio で、Analysis Services に接続します。 **Analysis Services Tutorial** という名前のデータベースがサーバーで実行されていることを確認します。  
  
## <a name="next-step"></a>次の手順  
 以上の操作で、チュートリアルを使用する準備が整いました。 開始方法の詳細については、「[多次元モデリング (Adventure Works チュートリアル)](multidimensional-modeling-adventure-works-tutorial.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [インストールウィザード&#40;から SQL Server 2014 をインストールする (セットアップ)&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [Configure the Windows Firewall to Allow Analysis Services Access](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)   
 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
