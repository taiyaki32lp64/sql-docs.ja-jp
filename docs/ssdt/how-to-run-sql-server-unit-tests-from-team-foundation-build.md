---
title: 方法:Team Foundation ビルドから SQL Server の単体テストを実行する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 24f5b85d-d6f9-415f-b09f-933b78dc0b67
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4c4008d88a2a353ead1ddd16f678c4167ff6714d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035090"
---
# <a name="how-to-run-sql-server-unit-tests-from-team-foundation-build"></a>方法:Team Foundation ビルドから SQL Server の単体テストを実行する
Team Foundation ビルドを使用すると、SQL Server の単体テストをビルド確認テスト (BVT) の一環として実行できます。 データベースを配置し、テスト データを生成して、選択したテストを実行するように単体テストを構成できます。 Team Foundation ビルドを使い慣れていない場合は、このトピックの手順を実行する前に、次の情報を確認してください。  
  
-   [SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
-   [方法: アプリケーションのビルド後にスケジュールされているテストを構成および実行する](https://msdn.microsoft.com/library/ms182465(VS.100).aspx)  
  
-   [基本的なビルド定義の作成](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
  
これらの手順を使用する前に、まず、次のタスクを実行することによって作業環境を構成する必要があります。  
  
-   Team Foundation ビルドと Team Foundation バージョン管理をインストールします。 Team Foundation ビルドと Team Foundation バージョン管理を異なるコンピューターにインストールすることが必要になる場合があります。  
  
-   Team Foundation ビルドと同じコンピューターに、MicrosoftSQL Server Data Tools のビルド ユーティリティをインストールします。 SQL Server Data Tools のビルド ユーティリティをインストールするには、まず管理インストール ポイントを作成します。 管理インストール ポイントについて詳しくは、「[SQL Server Data Tools のインストール](../ssdt/install-sql-server-data-tools.md)」をご覧ください。 次に、管理インストール ポイントに使用している場所 (/location) から、SSDTBuildUtilties.msi をビルド サーバーにインストールします。  
  
-   Visual Studio Team Foundation Server のインスタンスに接続します。  
  
作業環境を構成したら、次の手順を実行する必要があります。  
  
1.  データベース プロジェクトを作成します。  
  
2.  データベース プロジェクトのスキーマとオブジェクトをインポートまたは作成します。  
  
3.  ビルドと配置のためにデータベース プロジェクトのプロパティを構成します。  
  
4.  1 つ以上の単体テストを作成します。  
  
5.  データベース プロジェクトおよび単体テスト プロジェクトを含むソリューションをバージョン管理に追加し、すべてのファイルをチェックインします。  
  
このトピックの手順では、自動テストの実行の一環として単体テストを実行するためのビルド定義を作成する方法について説明します。  
  
1.  [x64 ビルド エージェントでデータベース単体テストを実行するようにテスト設定を構成する](#ConfigureX64)  
  
2.  [テストをテスト カテゴリに割り当てる (省略可能)](#CreateATestList)  
  
3.  [テスト プロジェクトを変更する](#ModifyTestProject)  
  
4.  [ソリューションをチェックインする](#CheckInTheTestList)  
  
5.  [ビルド定義を作成する](#CreateBuildDef)  
  
6.  [新しいビルド定義を実行する](#RunBuild)  
  
**ビルド コンピューター上での SQL Server の単体テストの実行**  
  
ビルド コンピューター上でデータベース単体テストを実行するときに、単体テストでデータベース プロジェクト ファイル (.sqlproj) が見つからない場合があります。 この問題は、app.config ファイルが相対パスを使用してこれらのファイルを参照していることが原因で発生します。 さらに、単体テストの実行に使用する SQL Server のインスタンスが見つからないと、単体テストに失敗することがあります。 この問題は、app.config ファイルに格納されている接続文字列がビルド コンピューターからの無効な文字列の場合に発生する可能性があります。  
  
これらの問題を解決するには、app.config 内の override セクションを指定して、Team Foundation 環境に固有の構成ファイルで app.config をオーバーライドする必要があります。 詳しくは、このトピックの「[テスト プロジェクトを変更する](#ModifyTestProject)」をご覧ください。  
  
## <a name="ConfigureX64"></a>x64 ビルド エージェントで SQL Server の単体テストを実行するようにテスト設定を構成する  
x64 ビルド エージェントで単体テストを実行するには、事前にテストの設定を構成してホスト プロセス プラットフォームを変更する必要があります。  
  
#### <a name="to-specify-the-host-process-platform"></a>ホスト プロセスのプラットフォームを指定するには  
  
1.  設定を構成するテスト プロジェクトが含まれているソリューションを開きます。  
  
2.  **ソリューション エクスプローラー**の **[ソリューション項目]** フォルダーにある **Local.testsettings** ファイルをダブルクリックします。  
  
    **[テストの設定]** ダイアログ ボックスが表示されます。  
  
3.  一覧の **[ホスト]** をクリックします。  
  
4.  詳細ウィンドウの **[ホスト プロセスのプラットフォーム]** で、 **[MSIL]** をクリックし、x64 ビルド エージェントで実行するテストを構成します。  
  
5.  **[適用]** をクリックします。  
  
## <a name="CreateATestList"></a>テストをテスト カテゴリに割り当てる (省略可能)  
単体テストを実行するためのビルド定義を作成するときに、通常は、1 つ以上のテスト カテゴリを指定します。 ビルドが実行されると、指定されたカテゴリ内のすべてのテストが実行されます。  
  
#### <a name="to-assign-tests-to-a-test-category"></a>テスト カテゴリにテストを割り当てるには  
  
1.  **[テスト ビュー]** ウィンドウを開きます。  
  
2.  テストを選択します。  
  
3.  プロパティ ペインで、 **[テスト カテゴリ]** をクリックしてから、右端の列にある参照ボタン ([...]) をクリックします。  
  
4.  **[テスト カテゴリ]** ウィンドウの **[新しいカテゴリの追加]** ボックスに、新しいテスト カテゴリの名前を入力します。  
  
5.  **[追加]** をクリックし、 **[OK]** をクリックします。  
  
    新しいテスト カテゴリがテストに割り当てられ、プロパティを介して他のテストに指定できるようになります。  
  
## <a name="ModifyTestProject"></a>テスト プロジェクトを変更する  
既定では、単体テスト プロジェクトのビルド時に、Team Foundation ビルドによって、プロジェクトの app.config ファイルから構成ファイルが作成されます。 データベース プロジェクトのパスは、app.config ファイルに相対パスとして保存されます。 Visual Studio で機能していた相対パスは機能しなくなります。Team Foundation ビルドでは、単体テストを実行する場所に関連した別の場所に作成済みファイルが配置されるためです。 さらに、app.config ファイルには、テスト対象のデータベースを指定する接続文字列が含まれています。 単体テストで、テスト プロジェクトの作成時に使用したものとは異なるデータベースに接続する必要がある場合は、Team Foundation ビルド用に別の app.config ファイルも必要です。 次の手順で変更を行うことにより、Team Foundation ビルドで別の構成が使用されるように、テスト プロジェクトとビルド サーバーを設定することができます。  
  
> [!IMPORTANT]  
> この手順は、テスト プロジェクト (.vbproj または .vsproj) ごとに実行する必要があります。  
  
#### <a name="to-specify-an-appconfig-file-for-team-foundation-build"></a>Team Foundation ビルドの app.config ファイルを指定するには  
  
1.  **ソリューション エクスプローラー**で、app.config ファイルを右クリックし、 **[コピー]** をクリックします。  
  
2.  テスト プロジェクトを右クリックし、 **[貼り付け]** をクリックします。  
  
3.  **"app.config のコピー"** というファイルを右クリックし、[名前の変更] をクリックします。  
  
4.  「_BuildComputer_ **.sqlunitttest.config**」と入力して、Enter キーを押します。*BuildComputer* は、ビルド エージェントが実行されるコンピューターの名前です。  
  
5.  *BuildComputer*.sqlunitttest.config をダブルクリックします。  
  
    構成ファイルがエディターで開きます。  
  
6.  Sources フォルダーのフォルダー レベル、およびソリューションと同じ名前のサブフォルダーを追加して、.sqlproj ファイルへの相対パスを変更します。 たとえば、構成ファイルで次のエントリが最初に含まれているとします。  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    この場合は、ファイルを次のように更新します。  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    完了すると、*BuildComputer*.sqlunitttest.config ファイルは次の例のようになります (Visual Studio 2010 の場合)。  
  
    ```  
    <SqlUnitTesting_VS2010>  
        <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
            Configuration="Debug" />  
        <DataGeneration ClearDatabase="true" />  
        <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
        <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
    </SqlUnitTesting_VS2010>  
    ```  
  
    Visual Studio 2012 を使用している場合は次のようになります。  
  
    ```  
    <SqlUnitTesting_VS2012>  
            <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
                Configuration="Debug" />  
            <DataGeneration ClearDatabase="true" />  
            <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
            <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
        </SqlUnitTesting_VS2012>  
    ```  
  
7.  ExecutionContext および PrivilegedContext の ConnectionString 属性を更新して、配置先データベースへの接続を指定します。  
  
8.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
9. ソリューション エクスプローラーで、app.config をダブルクリックします。  
  
10. エディターで、各 \<SqlUnitTesting_*VSVersion*> ノードに `AllowConfigurationOverride="true"` を追加します。 例:  
  
    ```  
    -- Update SqlUnitTesting_VS2010 node to:  
    <SqlUnitTesting_VS2010 AllowConfigurationOverride="true">   
  
    -- Update SqlUnitTesting_VS2012 node to:  
    <SqlUnitTesting_VS2012 AllowConfigurationOverride="true">  
    ```  
  
    この変更により、作成した代わりの構成ファイルを Team Foundation ビルドで使用できるようになります。  
  
11. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
    次に、Local.testsettings を更新して、カスタマイズした構成ファイルを含める必要があります。  
  
#### <a name="to-customize-localtestsettings-to-deploy-the-customized-configuration-file"></a>カスタマイズした構成ファイルを配置するように Local.testsettings をカスタマイズするには  
  
1.  ソリューション エクスプローラーで、Local.testsettings をダブルクリックします。  
  
    **[テストの設定]** ダイアログ ボックスが表示されます。  
  
2.  カテゴリの一覧で、 **[配置]** をクリックします。  
  
3.  **[配置を有効にする]** チェック ボックスをオンにします。  
  
4.  **[ファイルの追加]** をクリックします。  
  
5.  **[配置ファイルの追加]** ダイアログ ボックスで、作成した *BuildComputer*.sqlunitttest.config ファイルを指定します。  
  
6.  **[適用]** をクリックします。  
  
7.  **[閉じる]** をクリックします。  
  
8.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
    次に、ソリューションをバージョン管理にチェックインします。  
  
## <a name="CheckInTheTestList"></a>ソリューションをチェックインする  
この手順では、ソリューションのすべてのファイルをチェックインします。 これらのファイルには、テスト カテゴリの関連付けおよびテストを含む、ソリューションのテスト メタデータ ファイルが含まれます。 テストの内容を追加、削除、再構成、または変更すると、テスト メタデータ ファイルは自動的に更新され、これらの変更が反映されます。  
  
> [!NOTE]  
> この手順では、Team Foundation バージョン管理を使用している場合の手順について説明します。 別のバージョン管理ソフトウェアを使用している場合は、そのソフトウェアに適した手順に従う必要があります。  
  
#### <a name="to-check-in-the-solution"></a>ソリューションをチェックインするには  
  
1.  Team Foundation Server を実行しているコンピューターに接続します。  
  
    詳しくは、「[ソース管理エクスプローラーの使用](https://msdn.microsoft.com/library/ms181370(VS.100).aspx)」をご覧ください。  
  
2.  ソリューションがソース管理にまだ含まれていない場合は、ソース管理に追加します。  
  
    詳しくは、[バージョン管理へのプロジェクトまたはソリューションの追加に関するページ](https://msdn.microsoft.com/library/ms181374(VS.100).aspx)をご覧ください。  
  
3.  **[表示]** をクリックし、 **[保留中のチェックイン]** をクリックします。  
  
4.  ソリューションのすべてのファイルをチェックインします。  
  
    詳しくは、「[保留中の変更のチェックイン](https://msdn.microsoft.com/library/ms181411(VS.100).aspx)」をご覧ください。  
  
    > [!NOTE]  
    > 自動テストの作成方法および管理方法を制御する特定のチーム プロセスを用意することができます。 たとえば、ビルドをローカルで検証した後に、ビルドで実行されるテストと共にそのコードをチェックインすることを要求するプロセスもあります。  
  
    **ソリューション エクスプローラー**で、チェックインされている各ファイルの横には南京錠が表示されます。 詳しくは、「[バージョン管理ファイルとフォルダーのプロパティの表示](https://msdn.microsoft.com/library/ms245468(VS.100).aspx)」をご覧ください。  
  
    テストは、Team Foundation ビルドで使用できるようになります。 これで、実行するテストを含むビルド定義を作成できます。  
  
## <a name="CreateBuildDef"></a>ビルド定義を作成する  
  
#### <a name="to-create-a-build-definition"></a>ビルド定義を作成するには  
  
1.  チーム エクスプローラーで、チーム プロジェクトをクリックし、 **[ビルド]** ノードを右クリックして、 **[ビルド定義の新規作成]** をクリックします。  
  
    **[ビルド定義の新規作成]** ウィンドウが表示されます。  
  
2.  **[ビルド定義名]** に、ビルド定義に使用する名前を入力します。  
  
3.  ナビゲーション バーの **[ビルドの既定値]** をクリックします。  
  
4.  **[ビルド出力を次の格納フォルダーにコピーします (\\\server\share などの UNC パス)]** に、ビルド出力を格納するフォルダーを指定します。  
  
    ローカル コンピューター、またはビルド処理でアクセスできる任意のネットワークの場所にある共有フォルダーを指定できます。  
  
5.  ナビゲーション バーの **[プロセス]** をクリックします。  
  
6.  **[必須]** グループの **[ビルドする項目]** で、参照ボタン ([...]) をクリックします。  
  
7.  **[ビルド プロジェクト リスト エディター]** ダイアログ ボックスで、 **[追加]** をクリックします。  
  
8.  このチュートリアルでバージョン管理に追加したソリューション ファイル (.sln) を指定し、 **[OK]** をクリックします。  
  
    指定したソリューションが **[ビルドするソリューションまたはプロジェクト ファイル]** の一覧に表示されます。  
  
9. **[OK]** をクリックします。  
  
10. **[基本]** グループの **[自動テスト]** で、実行するテストを指定します。 既定では、ソリューションの \*test\*.dll という名前のファイルに含まれているテストが実行されます。  
  
11. **[ファイル]** メニューの ***[ProjectName* の保存]** をクリックします。  
  
    ビルド定義が作成されました。 次に、テスト プロジェクトを変更します。  
  
## <a name="RunBuild"></a>新しいビルド定義を実行する  
  
#### <a name="to-run-the-new-build-type"></a>新しいビルドの種類を実行するには  
  
1.  チーム エクスプローラーで、チーム プロジェクトのノード、[ビルド] ノードの順に展開し、実行するビルド定義を右クリックして、[新しいビルドをキューに配置] をクリックします。  
  
    **[ビルド {** _TeamProjectName_ **} をキューに配置]** ダイアログ ボックスが表示され、既存のすべてのビルドの種類の一覧が表示されます。  
  
2.  必要に応じて、 **[ビルド定義]** で、新しいビルド定義をクリックします。  
  
3.  **[ビルド定義]** 、 **[ビルド エージェント]** 、 **[このビルドの格納フォルダー]** の各フィールドの値がすべて適切であることを確認し、 **[キューに登録]** をクリックします。  
  
    **ビルド エクスプローラー**の **[キューに挿入済み]** タブが表示されます。 詳しくは、「[完了したビルドの管理と表示 (Visual Studio 2010)](https://msdn.microsoft.com/library/ms181730(VS.100).aspx)」または「[ビルド エクスプローラーでのビルドの管理 (Visual Studio 2012)](https://msdn.microsoft.com/library/ms181732.aspx)」をご覧ください。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの実行](../ssdt/running-sql-server-unit-tests.md)  
[基本的なビルド定義の作成](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
[ビルドをキューに配置する](https://msdn.microsoft.com/library/ms181722(VS.100).aspx)  
[実行中のビルドの進行状況の監視](https://msdn.microsoft.com/library/ms181724(VS.100).aspx)  
  
