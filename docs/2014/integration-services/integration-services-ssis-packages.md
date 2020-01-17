---
title: Integration Services (SSIS) パッケージ | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, about packages
- packages [Integration Services], about packages
- SSIS packages, about packages
- SSIS packages
- SQL Server Integration Services packages
- containers [Integration Services], packages
- packages [Integration Services]
- Integration Services packages, about packages
- Integration Services packages
ms.assetid: 9266bc64-7e1a-4e78-913b-a8deaa9843bf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dccae9216609e80b0eb87582a78b94cd6e7b2f0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767691"
---
# <a name="integration-services-ssis-packages"></a>Integration Services (SSIS) パッケージ
  パッケージは、接続、制御フロー要素、データ フロー要素、イベント ハンドラー、変数、パラメーター、および構成の組み合わせとして構成されています。パッケージは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] に用意されているグラフィカル デザイン ツールを使用して作成するか、プログラムによって構築します。  完成したパッケージは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、 [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストア、またはファイル システムに保存します。または、ssISnoversion プロジェクトを [!INCLUDE[ssIS](../includes/ssis-md.md)] サーバーに配置することができます。 パッケージとは、取得、実行、および保存の対象となる作業単位のことです。  
  
 最初にパッケージを作成した時点では、パッケージは何も実行しない空のオブジェクトです。 パッケージに機能を追加するには、制御フロー、および任意で 1 つ以上のデータ フローを追加します。  
  
 次の図は、1 つの制御フローを含む簡単なパッケージを示しています。この制御フローには 1 つのデータ フロー タスクが含まれ、そのタスクの中に 1 つのデータ フローが含まれます。  
  
 ![制御フローとデータ フローを含むパッケージ](media/ssis-package.gif "制御フローとデータ フローを含むパッケージ")  
  
 基本パッケージを作成したら、ログ記録や変数などの拡張機能を追加して、パッケージの機能を拡張できます。 詳細については、パッケージ機能を拡張するオブジェクトに関するセクションを参照してください。  
  
 完成したパッケージは、セキュリティの実装、チェックポイントからのパッケージ再開の有効化、パッケージ ワークフローのトランザクションの組み込みなど、パッケージ レベルのプロパティを設定することにより構成できます。 詳細については、拡張機能をサポートするプロパティに関するセクションを参照してください。  
  
## <a name="package-content"></a>パッケージの内容  
 制御フローは、パッケージの実行時に実行される 1 つ以上のタスクとコンテナーで構成されます。 パッケージ制御フロー内で次に実行するタスクまたはコンテナーの順序を制御したり、実行条件を定義するには、優先順位制約を使用してパッケージ内のタスクやコンテナーを連結します。 タスクとコンテナーのサブセットをグループ化して、パッケージ制御フロー内の 1 つの単位として繰り返し実行することもできます。 詳細については、「 [Control Flow](control-flow/control-flow.md)」を参照してください。  
  
 データ フローは、データの抽出や読み込みの実行元と実行先、データの変更や拡張を行う変換、および実行元、変換、実行先にリンクするパスで構成されます。 データ フローをパッケージに追加するには、データ フロー タスクを事前にパッケージ制御フローに含める必要があります。 データ フロー タスクは [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ内の実行可能ファイルで、データ フローの作成、順序付け、および実行を行います。 パッケージ内の各データ フロー タスクに対し、データ フロー エンジンのインスタンスが個別に開きます。 詳細については、「 [データ フロー タスク](control-flow/data-flow-task.md) 」と「 [データ フロー](data-flow/data-flow.md)」を参照してください。  
  
 パッケージには通常、1 つ以上の接続マネージャーが含まれます。 接続マネージャーは、パッケージとデータ ソース間のリンクであり、パッケージ内のタスク、変換、およびイベント ハンドラーによって使用されるデータにアクセスするための接続文字列が定義されています。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、テキストや XML ファイル、リレーショナル データベース、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のデータベースやプロジェクトなどのデータ ソースに対する接続の種類が用意されています。 詳細については、「[Integration Services (SSIS) の接続](connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
## <a name="package-templates"></a>パッケージ テンプレート  
 パッケージは、基本的な共通した機能を持つパッケージを構築する際の基になるテンプレートとして使用されることがよくあります。 基本パッケージを構築してそれをコピーすることも、パッケージをテンプレートとして指定することもできます。 たとえば、ファイルをダウンロードおよびコピーしてからデータを抽出するパッケージでは、フォルダー内のファイルを列挙する ForEach ループに FTP タスクおよびファイル システム タスクを含めることができます。 また、データにアクセスするためのフラット ファイル接続マネージャーや、データを抽出するためのフラット ファイル ソースを含めることもできます。 データの抽出先はそれぞれ異なるので、基本パッケージからコピーした後、それぞれの新しいパッケージに抽出先を追加します。 パッケージを作成してから、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトに追加する新しいパッケージのテンプレートとしてそれらのパッケージを使用することもできます。 詳細については、「 [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md)」を参照してください。  
  
 プログラムまたは SSIS デザイナーを使用したパッケージの初回作成時には、パッケージの `ID` プロパティに GUID が追加され、`Name` プロパティに名前が追加されます。 既存のパッケージをコピーするかテンプレート パッケージを使用して新しいパッケージを作成した場合は、そのパッケージの名前および GUID もコピーされます。 この動作は、ログ記録を使用する場合に問題となることがあります。これは、ログに記録された情報が属するパッケージを識別するために、そのパッケージの GUID および名前がログに記録されるためです。 したがって、新しいパッケージをコピー元のパッケージと区別したり、ログ データ内でパッケージを正しく区別できるようにするには、新しいパッケージの名前と GUID を更新する必要があります。  
  
 パッケージの GUID を変更するには、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] の [プロパティ] ウィンドウで、`ID` プロパティの GUID を再生成します。 パッケージ名を変更するには、[プロパティ] ウィンドウの `Name` プロパティの値を更新します。 また、 **dtutil** コマンド プロンプトを使用したり、プログラムを使用して GUID と名前を更新したりすることもできます。 詳細については、「[パッケージのプロパティを設定する](set-package-properties.md)」と「[dtutil ユーティリティ](dtutil-utility.md)」を参照してください。  
  
## <a name="objects-that-extend-package-functionality"></a>パッケージ機能を拡張するオブジェクト  
 パッケージには、イベント ハンドラー、構成、ログ記録、変数など、拡張機能を提供したり既存の機能を拡張するためのオブジェクトを追加できます。  
  
### <a name="event-handlers"></a>イベント ハンドラー  
 イベント ハンドラーは、パッケージ、タスク、またはコンテナーによって発生したイベントに応答して実行されるワークフローです。 たとえば、イベント ハンドラーを使用すると、実行前のイベントが発生した場合にディスク領域を確認して空き領域を報告したり、エラーが発生した場合にエラー情報を報告したりする電子メール メッセージを管理者に送信できます。 イベント ハンドラーは、パッケージと同様、1 つの制御フローとオプションのデータ フローで構成されます。 イベント ハンドラーは、パッケージ内の個々のタスクまたはコンテナーに追加できます。 詳細については、「[Integration Services &#40;SSIS&#41; のイベント ハンドラー](integration-services-ssis-event-handlers.md)」を参照してください。  
  
### <a name="configurations"></a>構成  
 構成とは、パッケージが実行されるときの、パッケージおよびそのタスク、コンテナー、変数、およびイベント ハンドラーのプロパティを定義する、プロパティと値の組み合わせのことです。 構成を使用すると、パッケージを変更しなくてもプロパティを更新できます。 パッケージが実行されると、構成情報が読み込まれ、プロパティの値が更新されます。 たとえば、構成を使用して接続の接続文字列を更新できます。  
  
 パッケージを別のコンピューターにインストールすると、パッケージと共に構成が保存され、配置されます。 パッケージのインストールの際、別の環境でパッケージがサポートされるように、構成の値を更新できます。 詳細については、「 [パッケージ構成を作成する](../../2014/integration-services/create-package-configurations.md)」を参照してください。  
  
### <a name="logging-and-log-providers"></a>ログ記録とログ プロバイダー  
 ログとは、パッケージの実行時に収集される、パッケージに関する情報の集まりのことです。 たとえば、ログにはパッケージの実行開始時刻と終了時刻を記録できます。 ログ プロバイダーとは、パッケージとそのコンテナーおよびタスクが実行時の情報を記録するために使用する、記録先の種類と形式を定義するものです。 ログはパッケージに関連付けられますが、パッケージ内のタスクとコンテナーの情報は、任意のパッケージ ログに記録できます。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、ログ記録用の各種のログ プロバイダーが組み込まれています。 たとえば [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] およびテキスト ファイル用のログ プロバイダーが含まれます。 また、カスタム ログ プロバイダーを作成してログ記録用に使用することもできます。 詳細については、「[Integration Services (SSIS) のログ記録](performance/integration-services-ssis-logging.md)」をご覧ください。  
  
### <a name="variables"></a>変数:  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、システム変数とユーザー定義変数がサポートされます。 システム変数は、実行時のパッケージ オブジェクトに関する有益な情報を提供します。またユーザー定義変数を使用すると、パッケージのシナリオをユーザー独自でサポートできます。 どちらの種類の変数も、式、スクリプト、および構成の内部で使用できます。  
  
 パッケージ レベルの変数には、1 つのパッケージで使用できる定義済みのシステム変数と、パッケージの範囲を定めたユーザー定義変数が含まれます。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)」を参照してください。  
  
### <a name="parameters"></a>パラメーター  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パラメーターを使用すると、パッケージの実行時にパッケージ内のプロパティに値を割り当てることができます。 " *プロジェクト パラメーター* " はプロジェクト レベル、" *パッケージ パラメーター* " はパッケージ レベルで作成できます。 プロジェクト パラメーターは、プロジェクトが受け取る外部入力をプロジェクト内の 1 つまたは複数のパッケージに指定するために使用します。 パッケージ パラメーターを使用すると、パッケージを編集したり再配置したりせずにパッケージ実行を変更できます。 詳細については、[Integration Services &#40;SSIS&#41; のパラメーター](integration-services-ssis-package-and-project-parameters.md)に関する記事を参照してください。  
  
## <a name="package-properties-that-support-extended-features"></a>拡張機能をサポートするパッケージのプロパティ  
 パッケージ オブジェクトを構成して、チェックポイントでのパッケージの再開、デジタル証明書を使用したパッケージの署名、パッケージの保護レベルの設定、およびトランザクションを使用したデータ整合性の検証などの機能をサポートできます。  
  
### <a name="restarting-packages"></a>パッケージの再開  
 パッケージには、チェックポイント プロパティが含まれます。これを使用すると、1 つ以上のタスクが失敗した場合にパッケージを再開できます。 たとえば、異なる 2 つのテーブルを更新する 2 つのデータ フロー タスクがパッケージに含まれ、2 番目のタスクが失敗した場合、最初のデータ フロー タスクを繰り返さずにそのパッケージを再実行できます。 パッケージの再開を使用すると、実行時間が長いパッケージで時間を節約できます。 再開とは、パッケージ全体を再実行するのではなく、失敗したタスクからパッケージを開始できるということです。 詳細については、「 [Restart Packages by Using Checkpoints](packages/restart-packages-by-using-checkpoints.md)」を参照してください。  
  
### <a name="securing-packages"></a>パッケージの保護  
 デジタル署名を使用してパッケージに署名したり、パスワードまたはユーザー キーを使用してパッケージを暗号化できます。 デジタル署名により、パッケージのソースが認証されます。 ただし、パッケージの読み込み時にデジタル署名を確認するように [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] を構成する必要もあります。 詳細については、「[デジタル署名を使用してパッケージのソースを特定する](security/identify-the-source-of-packages-with-digital-signatures.md)」および「[パッケージ内の機微なデータへのアクセス制御](security/access-control-for-sensitive-data-in-packages.md)」を参照してください。  
  
### <a name="supporting-transactions"></a>トランザクションのサポート  
 パッケージ上のトランザクションの属性を設定すると、パッケージ内のタスク、コンテナー、および接続をトランザクションに結合できます。 トランザクションの属性により、パッケージとその要素が全体として成功または失敗するようにできます。 また、パッケージで他のパッケージを実行したり、トランザクション内に他のパッケージを含めることができるため、複数のパッケージを作業の 1 単位として実行できます。 詳細については、「[Integration Services のトランザクション](integration-services-transactions.md)」を参照してください。  
  
## <a name="custom-log-entries-available-on-the-package"></a>パッケージで使用できるカスタム ログ エントリ  
 次の表は、パッケージのカスタム ログ エントリの一覧です。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../../2014/integration-services/custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`PackageStart`|パッケージの実行が開始されたことを示します。<br /><br /> 注:このログ エントリは自動的にログに書き込まれます。 除外することはできません。|  
|`PackageEnd`|パッケージが完了したことを示します。<br /><br /> 注:このログ エントリは自動的にログに書き込まれます。 除外することはできません。|  
|`Diagnostic`|同時実行できる実行可能ファイル数など、パッケージの実行に影響するシステム構成に関する情報を提供します。|  
  
## <a name="configuration-of-packages"></a>パッケージの構成  
 プロパティを設定するには、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] の **[プロパティ]** ウィンドウで行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を使用してこれらのプロパティを設定する方法については、「 [パッケージのプロパティを設定する](set-package-properties.md)」を参照してください。  
  
 これらのプロパティのプログラムでの設定については、「 <xref:Microsoft.SqlServer.Dts.Runtime.Package>」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、パッケージを作成するための [!INCLUDE[ssIS](../includes/ssis-md.md)] オブジェクト モデルのほかに、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] デザイナーと [!INCLUDE[ssIS](../includes/ssis-md.md)] インポートおよびエクスポート ウィザードの、2 つのグラフィック ツールが含まれています。 詳細については、以下のトピックを参照してください。  
  
-   [SQL Server インポートおよびエクスポート ウィザードを実行する](import-export-data/start-the-sql-server-import-and-export-wizard.md)  
  
-   [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md)  
  
-   開発者ガイドの「**プログラムによるパッケージの作成**」を参照してください。  

  
  
