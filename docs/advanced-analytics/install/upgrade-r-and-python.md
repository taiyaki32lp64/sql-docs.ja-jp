---
title: R および Python コンポーネントのアップグレード
description: SQL Server Machine Learning Services または SQL Server R Services で sqlbindr.exe を使用して Machine Learning Server にバインドして、R と Python をアップグレードします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: abc14f78a969abd4adbbb2dcf12b4ee316614d23
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69634548"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>SQL Server のインスタンス内の機械学習 (R および Python) コンポーネントをアップグレードする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server での R および Python の統合には、オープンソースのパッケージと Microsoft 独自のパッケージが含まれます。 標準的な SQL Server サービスでは、パッケージは SQL Server のリリースサイクルに従って更新され、現在のバージョンの既存のパッケージに対するバグの修正がありますが、メジャーバージョンのアップグレードは行われません。 

しかし、多くのデータ科学者は、使用可能になった新しいパッケージを使用することに慣れています。 SQL Server Machine Learning Services (データベース内) と SQL Server R Services (データベース内) の両方について、**Microsoft Machine Learning Server** に*バインド*することで、[新しいバージョンの R および Python ](#version-map)を取得できます。 

## <a name="what-is-binding"></a>バインドとは

バインドは、R_SERVICES と PYTHON_SERVICES のフォルダーの内容を、[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index) の新しい実行可能ファイル、ライブラリ、およびツールを使用して交換するインストール プロセスです。

更新されたコンポーネントと共に、サービス モデルのスイッチが用意されています。 [SQL Server の製品ライフサイクル](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017)ではなく、[SQL Server の累積的な更新プログラム](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions)を使用して、サービスの更新は[モダン ライフサイクル](https://support.microsoft.com/help/30881/modern-lifecycle-policy)上の [Microsoft R Server および Machine Learning Server のサポート タイムライン](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)に準拠するようになりました。

コンポーネントのバージョンとサービスの更新を除き、バインドによってインストールの基本が変更されることはありません。R と Python の統合はデータベース エンジンのインスタンスの一部であるため、ライセンスは変更されません (バインドに関連する追加コストはありません)。また、データベース エンジンの SQL Server のサポート ポリシーも保持されます。 この記事の残りの部分では、バインド メカニズムと SQL Server の各バージョンでの動作について説明します。

> [!NOTE]
> バインドは、SQL Server のインスタンスにバインドされている (データベース内の) インスタンスにのみ適用されます。 バインドは、(スタンドアロン) のインストールには関係ありません。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
**SQL Server 2017 のバインドに関する考慮事項**

SQL Server Machine Learning Services については、Microsoft Machine Learning Server が既にインストールされているものよりも追加のパッケージ、または新しいバージョンを提供し始める場合にのみ、バインドを検討してください。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**SQL Server 2016 のバインドに関する考慮事項**

SQL Server 2016 R Services のお客様の場合、バインドで、更新された R パッケージ、元のインストールに含まれていない新しいパッケージ ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package))、および[事前にトレーニング済みのモデル](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)が提供されます。[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index) の新しいメジャーリリースとマイナーリリースで、これらすべてを最新の情報に更新することができます。 バインディングでは、Python のサポートは提供されません。これは SQL Server 2017 の機能です。
::: moniker-end

<a name="version-map"></a>

## <a name="version-map"></a>バージョン マップ

次のテーブルはバージョン マップで、リリース ツール全体のパッケージ バージョンを示しています。これにより、Microsoft Machine Learning Server (以前の、MLS 9.2.1で Python サポートが追加される前には Microsoft R Serverと呼ばれていました) にバインドするときに、可能性のあるアップグレード パスを確認できるようになります。 

バインドでは、R または Anaconda の最新バージョンが保証されないことに注意してください。 Microsoft Machine Learning Server (MLS) にバインドすると、セットアップを通じてインストールされた R または Python のバージョンが取得されますが、これは Web で利用可能な最新バージョンではない可能性があります。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

コンポーネント |最初のリリース | [Microsoft R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [Microsoft R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
R 上の Microsoft R Open (MRO) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| 該当なし | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[事前トレーニング済みモデル](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| 該当なし | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 該当なし | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 該当なし | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

コンポーネント |最初のリリース | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
R 上の Microsoft R Open (MRO) | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Python 3.5 上の Anaconda 4.2  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[事前トレーニング済みモデル](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |
::: moniker-end

## <a name="how-component-upgrade-works"></a>コンポーネントのアップグレードのしくみ 

R と Python のライブラリおよび実行可能ファイルは、R と Python の既存のインストールを Machine Learning Server にバインドするときにアップグレードされます。 バインドは、R または Python が統合された既存の SQL Server データベース エンジンのインスタンスでセットアップを実行するときに、[Microsoft Machine Learning Server のインストーラー](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)によって実行されます。 セットアップによって既存の機能が検出され、Machine Learning Server に再バインドするように求めるメッセージが表示されます。 

バインド中に、新しい実行可能ファイルとライブラリで `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` と `\PYTHON_SERVICES` の内容が、`C:\Program Files\Microsoft\ML Server\R_SERVER` と `\PYTHON_SERVER` に上書きされます。

同時に、サービスモデルも SQL Server の更新メカニズムから、Microsoft Machine Learning Server のより頻繁なメジャーおよびマイナー リリース サイクルにフリップされます。 サポートポリシーの切り替えは、ソリューションに新しい世代の R および Python モジュールを必要とするデータ サイエンス チームにとって魅力的な選択肢です。 

+ バインドを使用しない場合、SQL Server Service Pack または累積的な更新プログラム (CU) をインストールすると、R および Python のパッケージにバグ修正のための修正プログラムが適用されます。 
+ バインドを使用すると、新しいバージョンのパッケージをインスタンスに適用できます。これは CU リリース スケジュールとは独立し、[モダン ライフサイクル ポリシー](https://support.microsoft.com/help/30881/modern-lifecycle-policy)、および Microsoft Machine Learning Server のリリースの下で行われます。 モダン ライフサイクル サポート ポリシーでは、より短い 1 年間の有効期間に、より多くの更新が提供されます。 バインド後は、R と Python の今後の更新に MLS インストーラーを、Microsoft ダウンロード サイトから入手できるようになり次第、引き続き使用できます。

バインドは R および Python の機能にのみ適用されます。 つまり、R および Python の機能のオープンソース パッケージ (Microsoft R Open、Anaconda)、独自のパッケージ RevoScaleR、revoscalepy などです。 バインドすることで、データベース エンジンのインスタンスのサポート モデルは変更されず、また SQL Server のバージョンは変更されません。

バインドは元に戻すことができます。 [インスタンスのバインドを解除し](#bkmk_Unbind)、SQL Server データベース エンジンのインスタンスを修復することによって、SQL Server サービスに戻すことができます。

まとめると、バインドのステップは次のとおりです。

+ SQL Server R Services または SQL Server Machine Learning Services の既存の構成済みインストールを使用して開始します。
+ アップグレードされたコンポーネントを使用する Microsoft Machine Learning Server のバージョンを確認します。
+ そのバージョンのセットアップをダウンロードして実行します。 セットアップでは、既存のインスタンスが検出され、バインド オプションが追加され、互換性のあるインスタンスの一覧が返されます。
+ バインドするインスタンスを選択し、セットアップを完了してバインドを実行します。

ユーザー エクスペリエンスの観点から、テクノロジとその使用方法は変更されていません。 唯一の違いは、新しいバージョンのパッケージが存在し、場合によっては当初 SQL Server では利用できない追加パッケージが存在することです。

## <a name="bkmk_BindWizard"></a>セットアップを使用して MLS にバインドする

Microsoft Machine Learning のセットアップでは、既存の機能と SQL Server バージョンが検出され、SqlBindR.exe というユーティリティを呼び出してバインドが変更されます。 内部的には、SqlBindR はセットアップにチェーンされ、間接的に使用されます。 後で、SqlBindR をコマンド ラインから直接呼び出して、特定のオプションを実行することができます。

1. SSMS で `SELECT @@version` を実行して、サーバーが最小ビルド要件を満たしていることを確認します。 

   SQL Server 2016 R Services の場合、最小値は [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) および [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)です。

1. R ベース と RevoScaleR パッケージのバージョンを確認して、既存のバージョンが、それを置き換える予定のものよりも古いことを確認します。 

    ```sql
    EXECUTE sp_execute_external_script
    @language=N'R'
    ,@script = N'str(OutputDataSet);
    packagematrix <- installed.packages();
    Name <- packagematrix[,1];
    Version <- packagematrix[,3];
    OutputDataSet <- data.frame(Name, Version);'
    , @input_data_1 = N''
    WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
    ```

1. SSMS および SQL Server への接続が開いている他のツールをすべて閉じます。 バインドは、プログラム ファイルを上書きします。 SQL Server が開いているセッションがある場合、バインドが失敗し、バインド エラー コード 6 が表示されます。

1. アップグレードするインスタンスがあるコンピューターに Microsoft Machine Learning Server をダウンロードします。 [最新のバージョン](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)をお勧めします。

1. フォルダーを解凍し、MLSWIN93 の下にある ServerSetup.exe を起動します。

   ![Microsoft Machine Learning Server セットアップ ウィザード](media/mls-921-installer-start.PNG)

1. **インストールを構成する**で、アップグレードするコンポーネントを確認して、互換性のあるインスタンスの一覧をレビューします。 

   この手順は非常に重要です。

   左側で、保持またはアップグレードするすべての機能を選択します。 一部の機能のみをアップグレードすることはできません。 空のチェックボックスは、現在インストールされていることを前提として、その機能を削除します。 スクリーン ショットでは、SQL Server 2016 R Services (MSSQL13) のインスタンスがあり、R と事前トレーニング済みモデルの R のバージョンが選択されています。 SQL Server 2016 では R がサポートされますが Python はサポートされないため、この構成は有効です。

   SQL Server 2016 R Services のコンポーネントをアップグレードする場合は、Python の機能を選択しないでください。 SQL Server 2016 R Services に Python を追加することはできません。

   右側の、インスタンス名の横にあるチェックボックスをオンにします。 インスタンスが一覧に表示されない場合は、互換性のない組み合わせになっています。 インスタンスを選択しない場合は、Machine Learning Server の新しいスタンドアロン インストールが作成され、SQL Server ライブラリは変更されません。 インスタンスを選択できない場合は、[SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1) にない可能性があります。 

    ![インストール ステップの構成](media/mls-931-installer-mssql13.png)

1. **[ライセンス契約]** ページで、 **[次の使用条件に同意します]** を選択して Machine Learning Server のライセンス使用条件に同意します。 

1. 連続するページで、Microsoft R Open や Python Anaconda のディストリビューションなど、選択したオープンソース コンポーネントの追加のライセンス条件に同意します。

1. **[完了まであと少しです]** のページで、インストール フォルダーをメモしておきます。 既定のフォルダーは、\Program Files\Microsoft\ML Server です。

    インストール フォルダーを変更する場合は、 **[詳細]** をクリックして、ウィザードの最初のページに戻ります。 ただし、前の選択をすべて繰り返す必要があります。

インストールプロセス中に、SQL Server によって使用されている R または Python ライブラリはすべて置き換えられ、スタート パッドは新しいコンポーネントを使用するように更新されます。 その結果、インスタンスが以前に既定の R_SERVICES フォルダーでライブラリを使用していた場合、アップグレード後にこれらのライブラリが削除され、スタート パッド サービスのプロパティが新しい場所にあるライブラリを使用するように変更されます。

バインドは、次のフォルダーの内容に影響します。C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library は、C:\Program Files\Microsoft\ML Server\ R_SERVER の内容に置き換えられます。 2 番目のフォルダーとその内容は Microsoft Machine Learning Server のセットアップによって作成されます。 

アップグレードに失敗した場合、詳細については、[SqlBindR エラーコード](#sqlbindr-error-codes)を確認してください。

## <a name="confirm-binding"></a>バインドの確認

R と RevoScaleR のバージョンを再確認して、新しいバージョンがあることを確認します。 データベース エンジンのインスタンスで R パッケージと共に配布された R コンソールを使用して、パッケージ情報を取得します。

```sql
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Machine Learning Server 9.3 にバインドされている SQL Server 2016 R Services の場合、R ベース パッケージは 3.4.3、RevoScaleR は 9.3 である必要があります。また、Microsoft Ml 9.3 も必要です。 

事前にトレーニング済みのモデルを追加した場合、モデルは MicrosoftML ライブラリに埋め込まれ、MicrosoftML の関数を使用して呼び出すことができます。 詳細については、「[MicrosoftML のための R サンプル](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)」を参照してください。

## <a name="offline-binding-no-internet-access"></a>オフラインバインド (インターネットアクセスなし)

インターネットに接続されていないシステムでは、インストーラーと .cab ファイルをインターネットに接続されたコンピューターにダウンロードして、分離されたサーバーにファイルを転送できます。 

インストーラー (ServerSetup.exe) には、Microsoft のパッケージ (RevoScaleR、MicrosoftML、olapR、sqlRUtils) が含まれています。 .Cab ファイルには、他のコア コンポーネントが用意されています。 たとえば、"SRO" cab は R Open (Microsoft の配布するオープンソース R) を提供します。

次の手順では、オフライン インストール用のファイルを配置する方法について説明します。

1. インストーラーをダウンロードする 1つの zip 形式のファイルとしてダウンロードします。 [最新バージョン](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)をお勧めしますが、[以前のバージョン](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)をインストールすることもできます。

1. .Cab ファイルをダウンロードします。 9\.3 リリースのリンクは次のとおりです。 以前のバージョンが必要な場合は [Microsoft R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components) に追加のリンクがあります。 Python/Anaconda は SQL Server Machine Learning Services のインスタンスにのみ追加できることに注意してください。 事前にトレーニング済みのモデルは、R と Python の両方に存在します。 .cab は、使用している言語のモデルを提供します。

    | 機能 | ダウンロード |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | トレーニング済みモデル | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. .Zip ファイルと .cab ファイルをターゲット サーバーに転送します。

1. サーバーで、Run コマンドに `%temp%` と入力して、一時ディレクトリの物理的な場所を取得します。 物理パスはマシンによって異なりますが、通常は `C:\Users\<your-user-name>\AppData\Local\Temp` です。

1. .Cab ファイルを % temp% フォルダーに配置します。

1. インストーラーを実行します。

1. ServerSetup.exe を実行し、画面の指示に従ってインストールを完了します。

## <a name="bkmk_BindCmd"></a>コマンド ライン操作

Microsoft Machine Learning Server を実行すると、SqlBindR.exe というコマンド ライン ユーティリティが使用できるようになり、さらなるバインド操作に使用できるようになります。 たとえば、バインドを逆にする場合は、セットアップを再実行するか、コマンド ライン ユーティリティを使用します。 また、このツールを使用して、インスタンスの互換性と可用性を確認することもできます。

> [!TIP]
> SqlBindR が見つかりませんか。 セットアップを実行していない可能性があります。 SqlBindR は Machine Learning Server のセットアップを実行した後にのみ使用できます。

1. 管理者としてコマンド プロンプトを開き、sqlbindr.exe を含むフォルダーに移動します。 既定の場所は、C:\Program Files\Microsoft\MLServer\Setup です

2. 次のコマンドを入力して、使用可能なインスタンスの一覧を表示します。 `SqlBindR.exe /list`
  
   一覧表示されている完全なインスタンス名をメモしておきます。 たとえば、既定のインスタンスの場合、インスタンス名は MSSQL14.MSSQLSERVER または SERVERNAME.MYNAMEDINSTANCE のようになります。

3. */bind*引数を指定して **SqlBindR.exe** コマンドを実行し、前の手順で返されたインスタンス名を使用して、アップグレードするインスタンスの名前を指定します。

   たとえば、既定のインスタンスをアップグレードするには、次のように入力します。  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. アップグレードが完了したら、変更されたインスタンスに関連付けられているスタート パッド サービスを再起動します。

## <a name="bkmk_Unbind"></a>インスタンスを元に戻す、またはバインド解除する

バインドされたインスタンスを、SQL Server セットアップによって確立された R および Python コンポーネントの初期インストールに復元できます。 SQL Server サービスに戻すには、3つの部分があります。

+ [ステップ 1:Microsoft Machine Learning Server からのバインド解除](#step-1-unbind)
+ [ステップ 2:インスタンスを元の状態に復元する](#step-2-restore)
+ [ステップ 3:インストールに追加したパッケージを再インストールする](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>ステップ 1:バインドの解除

バインドをロールバックするには、2つのオプションがあります。セットアップを再実行するか、SqlBindR コマンドラインユーティリティを使用します。

#### <a name="bkmk_wizunbind"></a> セットアップを使用してバインドを解除する

1. Machine Learning Server のインストーラーを見つけます。 インストーラーを削除した場合は、再度ダウンロードしたり、別のコンピューターからコピーしたりすることが必要になる場合があります。
2. バインドを解除するインスタンスがあるコンピューターで、インストーラーを実行してください。
2. インストーラーによって、バインド解除の候補となるローカル インスタンスが識別されます。
3. 元の構成に戻すインスタンスの横にあるチェックボックスをオフにします。
4. ライセンス契約に同意します。 インストール中でも、ライセンス条項への同意を示す必要があります。
5. **[完了]** をクリックします。 処理には時間がかかります。

#### <a name="bkmk_cmdunbind"></a> コマンド ラインを使用したバインド解除

1. コマンド プロンプトを開き、前のセクションで説明したように **sqlbindr.exe** が含まれているフォルダーに移動します。

2. **SqlBindR.exe** コマンドを実行し、" */unbind*" 引数でインスタンスを指定します。

   次のコマンド ラインは既定のインスタンスを元に戻します。
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>ステップ 2:SQL Server のインスタンスを修復する

SQL Server セットアップを実行して、R および Python の機能を備えたデータベース エンジンのインスタンスを修復します。 既存の更新プログラムは保持されますが、R および Python パッケージへの SQL Server サービス更新プログラムを実行しなかった場合は、このステップで修正プログラムが適用されます。

また、より多くの作業が必要ですが、データベース エンジンのインスタンスを完全にアンインストールしてから再インストールし、すべてのサービス更新プログラムを適用することもできます。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>ステップ 3:サードパーティ製のパッケージを追加する

パッケージ ライブラリに、他のオープンソースまたはサードパーティのパッケージを追加している場合もあるでしょう。 バインドを逆にすると、既定のパッケージ ライブラリの保存先が切り替わります。そのため、現在 R および Python を保存しているライブラリにパッケージを再インストールする必要があります。 詳細については、「[R パッケージ情報](../package-management/r-package-information.md)」と「[インストール](../package-management/install-additional-r-packages-on-sql-server.md)」、および「[Python パッケージ情報](../package-management/python-package-information.md)および[インストール](../package-management/install-additional-python-packages-on-sql-server.md)」を参照してください。

## <a name="sqlbindrexe-command-syntax"></a>sqlbindr.exe コマンドの構文

### <a name="usage"></a>使用方法

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>パラメーター

|[オブジェクト名]|[説明]|
|------|------|
|*list*| 現在のコンピューター上にあるすべての SQL データベース インスタンスの ID を一覧表示します|
|*bind*| 指定された SQL データベース インスタンスを R Server の最新バージョンにアップグレードし、インスタンスが R Server の今後のアップグレードを自動的に取得するようにします|
|*unbind*|R Server の最新バージョンを指定した SQL データベース インスタンスからアンインストールし、R Server の今後のアップグレードがインスタンスに影響を与えないようにします|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>バインド エラー

MLS Installer と SqlBindR の両方で、次のエラー コードとメッセージが返されます。

|エラー コード  | メッセージ           | 詳細               |
|------------|-------------------|-----------------------|
|バインド エラー 0 | Ok (成功) | バインドがエラーなしで渡されました。 |
|バインド エラー 1 | 引数が無効です | 構文エラー。 |
|バインド エラー 2 | 無効なアクション | 構文エラー。 |
|バインド エラー 3 | 無効なインスタンス | インスタンスは存在しますが、バインドには無効です。 |
|バインド エラー 4 | バインドできません | |
|バインド エラー 5 | 既にバインドされています | *bind* コマンドを実行しましたが、指定したインスタンスは既にバインドされています。 |
|バインド エラー 6 | バインドに失敗しました | インスタンスのバインド解除中にエラーが発生しました。 このエラーは、機能を選択せずに MLS インストーラーを実行した場合に発生する可能性があります。 SQL Server インスタンスが 2017 であると仮定した場合、バインドには、MSSQL インスタンスと R および Python の両方を選択する必要があります。 このエラーは、SqlBindR が プログラム ファイル フォルダーに書き込むことができなかった場合にも発生します。 オープン セッションまたは SQL Server のハンドルによって、このエラーが発生します。 このエラーが発生した場合は、新しいセッションを開始する前に、コンピューターを再起動し、バインドの手順をやり直してください。|
|バインド エラー 7 | バインドされていません | データベース エンジンのインスタンスには、R Services または SQL Server Machine Learning Services があります。 インスタンスは Microsoft Machine Learning Server にバインドされていません。 |
|バインド エラー 8 | バインド解除の失敗 | インスタンスのバインド解除中にエラーが発生しました。 |
|バインド エラー 9 | No instances found (インスタンスが見つかりませんでした) | このコンピューターにはデータベース エンジンのインスタンスが見つかりませんでした。 |

## <a name="known-issues"></a>既知の問題

ここでは、SqlBindR.exe のユーティリティ使用に関する固有の問題、または Machine Learning Server のアップグレード時に SQL Server のインスタンスに影響する可能性があるものについて説明します。

### <a name="restoring-packages-that-were-previously-installed"></a>以前にインストールされたパッケージの復元

Microsoft R Server 9.0.1 にアップグレードした場合、そのバージョンの SqlBindR.exe のバージョンでは、元のパッケージまたは R コンポーネントを完全に復元できません。ユーザーはインスタンスで SQL Server の修復を実行し、すべてのサービス リリースを適用してからインスタンスを再起動する必要があります。

新しいバージョンの SqlBindR では、元の R 機能が自動的に復元されるため、R コンポーネントを再インストールしたり、サーバーを再パッチしたりする必要がなくなります。 ただし、初期インストール後に追加された可能性のある R パッケージの更新プログラムをインストールする必要があります。

パッケージ管理ロールを使用してパッケージをインストールして共有する場合、このタスクははるかに簡単です。R コマンドを使用すると、データベース内のレコードを使用して、インストールされているパッケージをファイル システムに同期できます。また、その逆も可能です。 詳細については、「[SQL Server の R パッケージ管理](../r/install-additional-r-packages-on-sql-server.md)」を参照してください。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>SQL Server からの複数のアップグレードに関する問題

以前に SQL Server 2016 R Services のインスタンスを 9.0.1 にアップグレードしている場合、Microsoft R Server 9.1.0 の新しいインストーラーを実行すると、すべての有効なインスタンスの一覧が表示され、既定で以前にバインドされたインスタンスが選択されます。 続行すると、バインド済みのインスタンスはバインド解除されます。 その結果、関連するパッケージも含めて、以前の 9.0.1 インストールは削除されますが、新しいバージョンの Microsoft R Server (9.1.0) はインストールされません。

この回避策として、既存の Microsoft R Server のインストールを次のように変更できます。
1. [コントロール] パネルで **[プログラムの追加と削除]** を開きます。
2. Microsoft R Server を見つけて、 **[変更]** をクリックします。
3. インストーラーが開始されたら、9.1.0 にバインドするインスタンスを選択します。

Microsoft Machine Learning Server 9.2.1 と 9.3 には、この問題はありません。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>バインドまたはバインド解除によって、複数の一時フォルダーが残される

場合によっては、バインドとバインド解除の操作で、一時フォルダーのクリーンアップに失敗することがあります。
次のような名前のフォルダーが見つかった場合は、インストールの完了後に削除できます。R_SERVICES_<guid>

> [!NOTE]
> インストールが完了するまでお待ちください。 1 つのバージョンに関連付けられている R ライブラリを削除してから、新しい R ライブラリを追加するには、長い時間がかかることがあります。 操作が完了すると、一時フォルダーが削除されます。

## <a name="see-also"></a>参照

+ [Windows 用 Machine Learning Server のインストール (インターネット接続あり)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Windows 用 Machine Learning Server のインストール (オフライン)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server の既知の問題](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [以前にリリースされた Microsoft R Server の機能に関するお知らせ](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [非推奨、廃止、または変更された機能](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
