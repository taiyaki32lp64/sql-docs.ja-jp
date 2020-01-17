---
title: カスタム オブジェクトのビルド、配置、デバッグ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 112a925c051b5345933ee4c8fc1fb3b1147c2e48
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297314"
---
# <a name="building-deploying-and-debugging-custom-objects"></a>カスタム オブジェクトのビルド、配置、およびデバッグ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 用カスタム オブジェクトのコードを記述したら、アセンブリをビルドして配置し、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに統合してパッケージで使用できるようにし、テストとデバッグを行う必要があります。  
  
##  <a name="top"></a> Integration Services 用カスタム オブジェクトのビルド、配置、およびデバッグ手順  
 オブジェクトのカスタム機能は既に記述しました。 次に、オブジェクトをテストし、ユーザーが使用できるようにする必要があります。 そのための手順は、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 用に作成できるカスタム オブジェクトのすべての種類でほぼ同じです。  
  
 ビルド、配置、およびテストの手順を以下に示します。  
  
1.  生成するアセンブリに厳密な名前で[署名](#signing)します。  
  
2.  アセンブリを[ビルド](#building)します。  
  
3.  適切な [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] フォルダーに移動またはコピーすることにより、アセンブリを[配置](#deploying)します。  
  
4.  グローバル アセンブリ キャッシュ (GAC) にアセンブリを[インストール](#installing)します。  
  
     オブジェクトは自動的にツールボックスに追加されます。  
  
5.  必要に応じて、配置の[トラブルシューティング](#troubleshooting)を行います。  
  
6.  コードの[テスト](#testing)とデバッグを行います。  
  
 SQL Server Data Tools (SSDT) で SSIS デザイナーを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のさまざまなバージョンをターゲットとするパッケージを作成、管理、および実行できるようになりました。 この機能強化がカスタム拡張機能に与える影響に関する詳細については、「[Getting your SSIS custom extensions to be supported by the multi-version support of SSDT 2015 for SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)」 (SSIS のカスタム拡張機能を SSDT 2015 for SQL Server 2016 用 SSDT 2015 の複数バージョン サポートでサポートされるようにする) を参照してください。  
  
##  <a name="signing"></a> アセンブリへの署名  
 アセンブリを共有することを目的としている場合は、アセンブリをグローバル アセンブリ キャッシュにインストールする必要があります。 グローバル アセンブリ キャッシュに追加されたアセンブリは、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] などのアプリケーションで使用できるようになります。 グローバル アセンブリ キャッシュの要件として、アセンブリに厳密な名前で署名する必要があります。これにより、アセンブリがグローバルに一意であることが保証されます。 厳密な名前が付けられたアセンブリは、アセンブリの名前、カルチャ、公開キー、およびバージョン番号を含む完全修飾名を持ちます。 ランタイムはこの情報を使用して、アセンブリを検索し、同じ名前の他のアセンブリと区別します。  
  
 アセンブリに厳密な名前で署名するには、公開キーと秘密キーのペアを保持しているか、または作成する必要があります。 この暗号化用の公開キーと秘密キーのペアがビルド時に使用され、厳密な名前のアセンブリが作成されます。  
  
 厳密な名前と、アセンブリへの署名に必要な手順の詳細については、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK のドキュメントの次のトピックを参照してください。  
  
-   厳密な名前付きアセンブリ  
  
-   キー ペアの作成  
  
-   厳密な名前でのアセンブリへの署名  
  
 アセンブリには、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] でビルド時に厳密な名前を使用して簡単に署名できます。 **[プロジェクトのプロパティ]** ダイアログ ボックスで、 **[署名]** タブをクリックします。 **[アセンブリの署名]** を選択し、キー (.snk) ファイルのパスを指定します。  
  
##  <a name="building"></a> アセンブリのビルド  
 プロジェクトに署名したら、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] の **[ビルド]** メニューで使用可能なコマンドを使用して、プロジェクトまたはソリューションを、ビルドまたはリビルドする必要があります。 ソリューションには、カスタム ユーザー インターフェイス用の独立したプロジェクトが含まれている場合があります。このプロジェクトにも厳密な名前で署名する必要があり、同時にビルドすることが可能です。  
  
 アセンブリの配置とグローバル アセンブリ キャッシュへのインストールを実行するための最も便利な方法は、これらの手順を [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] でビルド後のイベントとしてスクリプト処理することです。 ビルド イベントは、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] プロジェクトのプロジェクト プロパティの **[コンパイル]** ページ、および C# プロジェクトの **[ビルド イベント]** ページから使用できます。 **gacutil.exe** などのコマンド プロンプト ユーティリティは、完全なパスで指定する必要があります。 スペースを含むパスと、スペースを含むパスに展開される $(TargetPath) などのマクロは、引用符で囲む必要があります。  
  
 カスタム ログ プロバイダーのビルド後に実行するコマンド ラインの例を次に示します。  
  
```cmd
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\130\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a> アセンブリの配置  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインストール時に作成される一連のフォルダー内で検索されたファイルを列挙することにより、パッケージで使用できるカスタム オブジェクトを検索します。 既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール設定を使用した場合、この一連のフォルダーは **C:\Program Files\Microsoft SQL Server\130\DTS** の下にあります。 ただし、カスタム オブジェクトのセットアップ プログラムを作成する場合は、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\Setup\DtsPath** レジストリ キーの値をチェックしてこのフォルダーの場所を確認してください。  
  
> [!NOTE]  
>  SQL Server Data Tools の複数バージョンのサポートでうまく機能するカスタム コンポーネントを配置する方法の詳細については、「[Getting your SSIS custom extensions to be supported by the multi-version support of SSDT 2015 for SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)」 (SSIS のカスタム拡張機能を SSDT 2015 for SQL Server 2016 用 SSDT 2015 の複数バージョン サポートでサポートされるようにする) を参照してください。  
  
 アセンブリをフォルダーに配置する方法は 2 つあります。  
  
-   コンパイル済みのアセンブリをビルド後に適切なフォルダーに移動またはコピーします (ビルド後のイベントにコピー コマンドを含めると便利です)。  
  
-   適切なフォルダーでアセンブリを直接ビルドします。  
  
 **C:\Program Files\Microsoft SQL Server\130\DTS** にある次の配置フォルダーは、さまざまな種類のカスタム オブジェクトに使用されます。  
  
|カスタム オブジェクト|配置フォルダー|  
|-------------------|-----------------------|  
|タスク|処理手順|  
|[ODBC 入力元エディター]|接続|  
|ログ プロバイダー|LogProviders|  
|カスタム データ フロー コンポーネント|PipelineComponents|  
  
> [!NOTE]  
>  アセンブリは、使用可能なタスクや接続マネージャーなどの列挙をサポートするために、これらのフォルダーにコピーされます。 したがって、カスタム オブジェクトのカスタム ユーザー インターフェイスのみを含むアセンブリをこれらのフォルダーに配置する必要はありません。  
  
##  <a name="installing"></a> グローバル アセンブリ キャッシュへのアセンブリのインストール  
 タスク アセンブリをグローバル アセンブリ キャッシュ (GAC) にインストールするには、コマンド ライン ツール **gacutil.exe** を使用するか、アセンブリを `%system%\assembly` ディレクトリにドラッグします。 便宜上、**gacutil.exe** への呼び出しもビルド後のイベントに含めることができます。  
  
 次のコマンドでは、**gacutil.exe** を使用して *MyTask.dll* という名前のコンポーネントを GAC にインストールします。  
  
 `gacutil /iF MyTask.dll`  
  
 カスタム オブジェクトの新しいバージョンをインストールしたら、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーを閉じて再度開く必要があります。 グローバル アセンブリ キャッシュに以前のバージョンのカスタム オブジェクトをインストールしている場合は、新しいバージョンをインストールする前に以前のバージョンを削除する必要があります。 アセンブリをアンインストールするには、**gacutil.exe** を実行し、`/u` オプションを使用してアセンブリ名を指定します。  
  
 グローバル アセンブリ キャッシュの詳細については、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ツールのグローバル アセンブリ キャッシュ ツール (Gactutil.exe) を参照してください。  
  
##  <a name="troubleshooting"></a> 配置のトラブルシューティング  
 カスタム オブジェクトが **[ツールボックス]** または使用可能なオブジェクトの一覧に表示されるのに、パッケージに追加できない場合は、次の操作を試してください。  
  
1.  グローバル アセンブリ キャッシュにコンポーネントの複数のバージョンがないか検索します。 グローバル アセンブリ キャッシュにコンポーネントの複数のバージョンがある場合、デザイナーはコンポーネントを読み込めないことがあります。 アセンブリのすべてのインスタンスをグローバル アセンブリ キャッシュから削除し、アセンブリを再度追加してください。  
  
2.  配置フォルダーに存在するアセンブリのインスタンスが 1 つだけであることを確認します。  
  
3.  ツールボックスを更新します。  
  
4.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] を **devenv.exe** にアタッチし、ブレークポイントを設定して初期化コードを実行し、例外が発生しないことを確認します。  
  
##  <a name="testing"></a> コードのテストとデバッグ  
 カスタム オブジェクトの実行時のメソッドをデバッグするための最も簡単な方法は、カスタム オブジェクトのビルド後に [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] から **dtexec.exe** を起動し、コンポーネントを使用するパッケージを実行することです。  
  
 **Validate** メソッドなど、コンポーネントのデザイン時のメソッドをデバッグする場合は、コンポーネントを使用するパッケージを [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の 2 番目のインスタンスで開き、**devenv.exe** プロセスにアタッチします。  
  
 パッケージを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで開いて実行しているときに、コンポーネントの実行時のメソッドもデバッグする場合は、**DtsDebugHost.exe** プロセスにもアタッチできるようにパッケージの実行を一時停止する必要があります。  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>dtexec.exe にアタッチしてオブジェクトの実行時のメソッドをデバッグするには  
  
1.  デバッグ構成でプロジェクトへの署名とビルドを行い、プロジェクトを配置し、このトピックで説明したようにグローバル アセンブリ キャッシュにインストールします。  
  
2.  **[プロジェクトのプロパティ]** の **[デバッグ]** タブで、 **[開始動作]** として **[外部プログラムの開始]** を選択し、**dtexec.exe** を探します。これは、既定では C:\Program Files\Microsoft SQL Server\130\DTS\Binn にインストールされています。  
  
3.  **[開始オプション]** の **[コマンド ライン オプション]** テキスト ボックスに、コンポーネントを使用するパッケージを実行するために必要なコマンド ライン引数を入力します。 多くの場合、コマンド ライン引数は /F[ILE] スイッチと、それに続く .dtsx ファイルのパスおよびファイル名で構成されます。 詳細については、「 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)」を参照してください。  
  
4.  コンポーネントの実行時のメソッド内の適切な位置のソース コードに、ブレークポイントを設定します。  
  
5.  プロジェクトを実行します。  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>SQL Server データ ツールにアタッチしてカスタム オブジェクトのデザイン時のメソッドをデバッグするには  
  
1.  デバッグ構成でプロジェクトへの署名とビルドを行い、プロジェクトを配置し、このトピックで説明したようにグローバル アセンブリ キャッシュにインストールします。  
  
2.  カスタム オブジェクトのデザイン時のメソッド内の適切な位置のソース コードに、ブレークポイントを設定します。  
  
3.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の 2 番目のインスタンスを開き、カスタム オブジェクトを使用するパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを読み込みます。  
  
4.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の最初のインスタンスから、 **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックして、パッケージが読み込まれる **devenv.exe** の 2 番目のインスタンスにアタッチします。  
  
5.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の 2 番目のインスタンスからパッケージを実行します。  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>SQL Server データ ツールにアタッチしてカスタム オブジェクトの実行時のメソッドをデバッグするには  
  
1.  上記の一覧にある手順を完了したら、**DtsDebugHost.exe** にアタッチできるようにパッケージの実行を一時停止します。 ここで強制的に一時停止するには、ブレークポイントを **OnPreExecute** イベントに追加します。または、スクリプト タスクをプロジェクトに追加し、モーダル メッセージ ボックスを表示するスクリプトを入力します。  
  
2.  パッケージを実行します。 実行が一時停止されたら、コンポーネント プロジェクトが開かれている [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のインスタンスに切り替え、 **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックします。 **[x86]** としてのみ一覧に表示されているインスタンスではなく、必ず、 **[型]** 列で **[マネージド, x86]** として表示されている **DtsDebugHost.exe** のインスタンスにアタッチします。  
  
3.  一時停止したパッケージに戻り、ブレークポイント以降を続行します。または、 **[OK]** をクリックしてスクリプト タスクが生成したメッセージ ボックスを破棄し、パッケージの実行とデバッグを続けます。  
  
## <a name="see-also"></a>参照  
 [Integration Services 用のカスタム オブジェクトの開発](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)   
 [カスタム オブジェクトの永続化](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [パッケージ開発のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
