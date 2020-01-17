---
title: パッケージ実行タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executepackagetask.f1
- sql13.dts.designer.executepackagetask.package.f1
- sql13.dts.designer.executepackagetask.parameter.F1
- sql13.dts.designer.executepackagetask.general.f1
helpviewer_keywords:
- Execution Package task [Integration Services]
- child packages
- parent packages [Integration Services]
ms.assetid: 042d4ec0-0668-401c-bb3a-a25fe2602eac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dcd1e0912f1bf0adcbae79da1f1d34f92233f467
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294187"
---
# <a name="execute-package-task"></a>パッケージ実行タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  パッケージ実行タスクは、パッケージのワークフローの一部として他のパッケージを実行できるようにすることで、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のエンタープライズ用機能を拡張します。  
  
 パッケージ実行タスクは、次の目的で使用されます。  
  
-   複雑なパッケージ ワークフローを分割します。 このタスクによりワークフローを複数のパッケージに分割できるため、読み取り、テスト、管理が容易になります。 たとえば、スター スキーマにデータを読み込む場合、個別のパッケージを構築して各ディメンション テーブルおよびファクト テーブルを設定できます。  
  
-   パッケージのパーツを再利用します。 パッケージ ワークフローのパーツを他のパッケージで再利用できます。 たとえば、各種パッケージからの呼び出しが可能なデータ抽出モジュールを作成できます。 抽出モジュールを呼び出す各パッケージは、各種データのスクラビング、フィルターによる選択、集計操作を実行します。  
  
-   作業単位をグループ化します。 作業単位を個別のパッケージにカプセル化し、トランザクション コンポーネントとして親パッケージのワークフローに結合できます。 たとえば、親パッケージはアクセサリ パッケージを実行し、その実行の成否に基づいてトランザクションをコミットまたはロールバックします。  
  
-   パッケージのセキュリティを管理します。 パッケージ作成者がアクセスを必要とするのは、マルチパッケージ ソリューションの一部のみです。 パッケージを複数パッケージに分割することにより、作成者に関連パッケージのみへのアクセス権を与えることができるため、セキュリティ レベルを高めることができます。  
  
 通常、他のパッケージを実行するパッケージは親パッケージと呼ばれ、親ワークフローで実行されるパッケージは子パッケージと呼ばれます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、実行可能ファイルやバッチ ファイルの実行などの、ワークフロー処理を実行するタスクが含まれています。 詳細については、「 [プロセス実行タスク](../../integration-services/control-flow/execute-process-task.md)」を参照してください。  
  
## <a name="running-packages"></a>パッケージの実行  
 パッケージ実行タスクでは、親パッケージと同じプロジェクトに含まれる子パッケージを実行できます。 子パッケージをプロジェクトから選択するには、 **ReferenceType** プロパティを **[プロジェクト参照]** に設定し、 **PackageNameFromProjectReference** プロパティを設定します。  
  
> [!NOTE]  
>  **[ReferenceType]** オプションは読み取り専用であり、対象パッケージを含むプロジェクトがプロジェクト配置モデルに変換されていない場合は **[外部参照]** に設定されます。 [Integration Services (SSIS) プロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
 パッケージ実行タスクでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb データベース内に格納されたパッケージ、およびファイル システム内に格納されたパッケージも実行できます。 タスクは OLE DB 接続マネージャーを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続するか、ファイル接続マネージャーを使用してファイル システムにアクセスします。 詳細については、「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md) 」および「 [フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)」を参照してください。  
  
 パッケージ実行タスクでは、データベース メンテナンス プランを実行することもできます。これを実行すると、同じ [!INCLUDE[ssIS](../../includes/ssis-md.md)] ソリューション内の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージとデータベース メンテナンス プランの両方を管理できます。 データベース メンテナンス プランは [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージに似ていますが、プランはデータベース メンテナンス タスクのみを含むことができ、常に msdb データベース内に格納される点が異なります。  
  
 ファイル システム内に格納されたパッケージを選択する場合、パッケージの名前と格納場所を指定する必要があります。 パッケージはファイル システム内の任意の場所に格納できます。親パッケージと同じフォルダー内にある必要はありません。  
  
 子パッケージは、親パッケージのプロセス内で実行することも、独自のプロセス内で実行することもできます。 子パッケージを独自のプロセス内で実行する場合、より多くのメモリを必要としますが、柔軟性はより高くなります。 たとえば、子プロセスが失敗した場合でも親プロセスを続行できます。  
  
 また、親パッケージと子パッケージが 1 つの単位として共に失敗する方が良い場合や、別のプロセスで追加のオーバーヘッドが発生しない方が良い場合もあります。 たとえば、子プロセスが失敗し、パッケージの親プロセス内の次の処理が、子プロセスが成功した場合に行われる場合、子パッケージは親パッケージのプロセス内で実行される必要があります。  
  
 既定では、パッケージ実行タスクの ExecuteOutOfProcess プロパティは **False**に設定されるので、子パッケージは親パッケージと同じプロセス内で実行されます。 このプロパティを **True**に設定すると、子パッケージは別のプロセスで実行されます。 これにより、子パッケージの起動が遅くなる場合があります。 また、このプロパティを **True**に設定した場合、ツールのみのインストールではパッケージをデバッグできません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]をインストールする必要があります。 詳細については、「 [Integration Services のインストール](../../integration-services/install-windows/install-integration-services.md)」を参照してください。  
  
## <a name="extending-transactions"></a>トランザクションの拡張  
 親パッケージで使用するトランザクションを子パッケージに拡張できます。このため、両方のパッケージで実行される作業をコミットまたはロールバックできます。 たとえば、親パッケージで実行されるデータベースの挿入は、子パッケージで実行されるデータベースの挿入に基づいてコミットまたはロールバックできます。その逆も同様です。 詳細については、「 [トランザクションの継承](https://msdn.microsoft.com/library/90db5564-d41e-4cfe-8c9e-4e68d41eff1c)」を参照してください。  
  
## <a name="propagating-logging-details"></a>ログ記録の詳細の設定  
 パッケージ実行タスクで実行される子パッケージでログ記録を使用するように構成する場合でも、そうでない場合でも、子パッケージは、ログ記録の詳細を常に親パッケージに転送します。 パッケージ実行タスクがログ記録を使用するように構成されている場合、子パッケージからの詳細がログ記録されます。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
## <a name="passing-values-to-child-packages"></a>子パッケージへの値の引き渡し  
 子パッケージは、子パッケージを呼び出す別のパッケージ (通常は、親パッケージ) によって子パッケージに渡された値を使用することがあります。 親パッケージから渡される値を使用することは、次のようなシナリオで役に立ちます。  
  
-   大規模なワークフローの一部が各種パッケージに割り当てられている場合。 たとえば、特定のパッケージで毎夜データをダウンロードし、データを要約し、要約データの値を変数に割り当て、その値を別のパッケージに渡して、さらにデータを処理する場合などです。  
  
-   親パッケージが子パッケージのタスクを動的に調整する場合。 たとえば、親パッケージで現在の月の日数を決定し、その数値を変数に割り当て、子パッケージでその数値の回数だけタスクを実行する場合などです。  
  
-   親パッケージによって動的に抽出されたデータに、子パッケージがアクセスする必要がある場合。 たとえば、親パッケージでテーブルからデータを抽出し、行セットを変数に読み込んで、子パッケージでさらにそのデータを処理する場合などです。  
  
 次のいずれかの方法を使用して、子パッケージに値を渡すことができます。  
  
-   **パッケージ構成**  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、親パッケージ変数という種類の構成を使用して、親パッケージの値を子パッケージに渡すことができます。 この設定は子パッケージ上で構築され、親パッケージ内の変数を使用します。 構成は、子パッケージ内の変数、または子パッケージ内のオブジェクトのプロパティにマップされます。 また、スクリプト タスクまたはスクリプト コンポーネントで使用されるスクリプト内でも変数を使用できます。  
  
-   **パラメーター**  
  
     親パッケージの変数またはパラメーター、またはプロジェクトのパラメーターを子パッケージのパラメーターにマップするように、パッケージ実行タスクを構成できます。 プロジェクトはプロジェクト配置モデルを使用し、子パッケージが親パッケージと同じプロジェクトに含まれている必要があります。 詳細については、「 [パッケージ実行タスク エディター](../../integration-services/control-flow/execute-package-task-editor.md)」を参照してください。  
  
    > [!NOTE]  
    >  機密性が高くない子パッケージのパラメーターが、機密性の高い親パラメーターにマップされる場合は、子パッケージの実行に失敗します。  
    >   
    >  サポートされているマッピングの条件は次のとおりです。  
    >   
    >  機密性の高い子パッケージのパラメーターは、機密性の高い親パラメーターにマップされます。  
    >   
    >  機密性の高い子パッケージのパラメーターは、機密性が高くない親パラメーターにマップされます。  
    >   
    >  機密性が高くない子パッケージのパラメーターは、機密性が高くない親パラメーターにマップされます。  
  
 親パッケージの変数は、パッケージ実行タスクのスコープ内、またはパッケージなどの親コンテナー内で定義できます。 同じ名前の変数が複数ある場合、パッケージ実行タスクのスコープ内で定義された変数、またはタスクのスコープ内で最も近い変数が使用されます。  
  
 詳細については、「 [子パッケージでの変数およびパラメーターの値の使用](../../integration-services/packages/legacy-package-deployment-ssis.md#child)」を参照してください。  
  
### <a name="accessing-parent-package-variables"></a>親パッケージの変数へのアクセス  
 子パッケージではスクリプト タスクを使用して、親パッケージの変数にアクセスできます。 **スクリプト タスク エディター**で **[スクリプト]** ページに親パッケージ変数の名前を入力するときは、変数名に **User:** を含めないでください。 そうしないと、親パッケージを実行したときに子パッケージで変数が見つかりません。  
  
## <a name="configuring-the-execute-package-task"></a>パッケージ実行タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="configuring-the-execute-package-task-programmatically"></a>プログラムによるパッケージ実行タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   [N:Microsoft.SqlServer.Dts.Tasks.ExecutePackageTask](https://technet.microsoft.com/library/microsoft.sqlserver.dts.tasks.executepackagetask\(v=sql.110\).aspx)  
  
## <a name="execute-package-task-editor"></a>パッケージ実行タスク エディター
  パッケージ実行タスクを構成するには、パッケージ実行タスク エディターを使用します。 パッケージ実行タスクは、パッケージのワークフローの一部として他のパッケージを実行できるようにすることで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のエンタープライズ用機能を拡張します。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [パッケージ実行タスク エディターを開く](#open)  
  
-   [[全般] ページのオプションを設定する](#general)  
  
-   [[パッケージ] ページのオプションを設定する](#package)  
  
-   [[パラメーター バインド] ページのオプションを設定する](#parameter)  
  
###  <a name="open"></a> パッケージ実行タスク エディターを開く  
  
1.  パッケージ実行タスクが含まれる [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] で開きます。  
  
2.  SSIS デザイナーでタスクを右クリックし、 **[編集]** をクリックします。  
  
###  <a name="general"></a> [全般] ページのオプションを設定する  
 **[名前]**  
 パッケージ実行タスクの一意な名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 パッケージ実行タスクの説明を入力します。  
  
###  <a name="package"></a> [パッケージ] ページのオプションを設定する  
 **ReferenceType**  
 プロジェクト内の子パッケージの場合は **[プロジェクト参照]** をクリックします。 パッケージの外部にある子パッケージの場合は **[外部参照]** をクリックします。  
  
> [!NOTE]  
>  **[ReferenceType]** オプションは読み取り専用であり、対象パッケージを含むプロジェクトがプロジェクト配置モデルに変換されていない場合は **[外部参照]** に設定されます。 [Integration Services (SSIS) プロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
 **パスワード**  
 子パッケージがパスワードで保護されている場合は、子パッケージのパスワードを入力するか、参照ボタン [...] をクリックして子パッケージの新しいパスワードを作成します。  
  
 **ExecuteOutOfProcess**  
 子パッケージが親パッケージのプロセス内で実行するか、または別のプロセスで実行するかを指定します。 既定では、パッケージ実行タスクの ExecuteOutOfProcess プロパティは **False**に設定されるので、子パッケージは親パッケージと同じプロセス内で実行されます。 このプロパティを **true**に設定すると、子パッケージは別のプロセスで実行されます。 これにより、子パッケージの起動が遅くなる場合があります。 また、プロパティを **true**に設定した場合、ツールのみのインストールではパッケージをデバッグできません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 製品をインストールする必要があります。 詳細については、「 [Integration Services のインストール](../../integration-services/install-windows/install-integration-services.md)」を参照してください。  
  
#### <a name="referencetype-dynamic-options"></a>[ReferenceType] の動的オプション  
  
##### <a name="referencetype--external-reference"></a>ReferenceType = 外部参照  
 **場所**  
 子パッケージの場所を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**SQL Server**|場所を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに設定します。|  
|**ファイル システム**|場所をファイル システムに設定します。|  
  
 **[接続]**  
 子パッケージの格納場所の種類を選択します。  
  
 **PackageNameReadOnly**  
 パッケージ名が表示されます。  
  
##### <a name="referencetype--project-reference"></a>ReferenceType = プロジェクト参照  
 **PackageNameFromProjectReference**  
 プロジェクトに含まれるパッケージで子パッケージにするものを選択します。  
  
#### <a name="location-dynamic-options"></a>[Location] の動的オプション  
  
##### <a name="location--sql-server"></a>Location = SQL Server  
 **[接続]**  
 OLE DB 接続マネージャーを一覧から選択するか、[\<**新しい接続...>** ] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
 **PackageName**  
 子パッケージの名前を入力するか、[...] をクリックし、パッケージを指定します。  
  
##### <a name="location--file-system"></a>Location = ファイル システム  
 **[接続]**  
 ファイル接続マネージャーを一覧から選択するか、\< **[新しい接続...]** をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)  
  
 **PackageNameReadOnly**  
 パッケージ名が表示されます。  
  
###  <a name="parameter"></a> [パラメーター バインド] ページのオプションを設定する  
 親パッケージまたはプロジェクトから子パッケージに値を渡すことができます。 プロジェクトはプロジェクト配置モデルを使用し、子パッケージが親パッケージと同じプロジェクトに含まれている必要があります。  
  
 プロジェクト配置モデルへのプロジェクトの変換に関する詳細については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  
  
 **子パッケージのパラメーター**  
 子パッケージのパラメーターの名前を入力または選択します。  
  
 **バインドするパラメーターまたは変数**  
 子パッケージに渡す値を含むパラメーターまたは変数を選択します。  
  
 **[追加]**  
 パラメーターまたは変数を子パッケージのパラメーターにマップする場合にクリックします。  
  
 **[削除]**  
 パラメーターまたは変数と子パッケージのパラメーターの間のマッピングを削除する場合にクリックします。  
  
  
