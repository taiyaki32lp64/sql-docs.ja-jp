---
title: カスタム ワークフローの作成
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8e4403e9-595c-4b6b-9d0c-f6ae1b2bc99d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 03e4c5c55610a0a6ac76b1183ae3cc43e72d028e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729323"
---
# <a name="create-a-custom-workflow-master-data-services"></a>カスタム ワークフローの作成 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] は、ビジネス ルールを使用して基本的なワークフロー ソリューションを作成します (たとえば、指定した条件に基づいてデータを自動的に更新および検証し、電子メール通知を送信するなど)。 組み込みのワークフロー アクションよりも複雑な処理が必要な場合は、カスタム ワークフローを使用します。 カスタム ワークフローは、ユーザーが作成する .NET アセンブリです。 作成したワークフロー アセンブリが呼び出された際には、記述したコードを通じて、状況に応じた任意のアクションを実行できます。 たとえば、複数階層の承認や複雑な意思決定ツリーなど、複雑なイベント処理を必要とするワークフローの場合は、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] を構成することで、データを分析し、データの承認のための送信先を決定するカスタム ワークフローを開始できます。  
  
## <a name="how-custom-workflows-are-processed"></a>カスタム ワークフローの処理方法  
 カスタム ワークフローの処理には、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーション、SQL Server MDS Workflow Integration Service、およびワークフロー ハンドラー アセンブリの 3 つの主要コンポーネントが関与します。 これらのコンポーネントは、カスタム ワークフローを次のように処理します。  
  
1.  ユーザーが [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] を使用して、ワークフローを開始するエンティティを検証します。  
  
2.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] は、ビジネス ルール条件を満たすメンバーを [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベース内の Service Broker キューに送ります。  
  
3.  SQL Server MDS Workflow Integration Service は、一定の間隔で [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベース内のストアド プロシージャを呼び出します。  
  
4.  このストアド プロシージャは、Service Broker キュー内にレコードを見つけると、それらを SQL Server MDS Workflow Integration Service に返します。  
  
5.  SQL Server MDS Workflow Integration Services は、それらのデータをワークフロー ハンドラー アセンブリにルーティングします。  
  
> [!NOTE]  
>  注: SQL Server MDS Workflow Integration Service は単純な処理をトリガーするためのものです。 カスタム コードで複雑な処理を行う必要がある場合は、個別のスレッド内か、またはワークフロー プロセスの外部で処理を完了してください。  
  
## <a name="configure-master-data-services-for-custom-workflows"></a>カスタム ワークフロー向けの Master Data Services の構成  
 カスタム ワークフローを作成するには、カスタム コードの記述と [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] の構成を行って、ワークフロー データをワークフロー ハンドラーに渡す必要があります。 カスタム ワークフロー処理を有効にするには、次の手順を実行します。  
  
1.  <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> を実装する .NET アセンブリ作成します。  
  
2.  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースに接続してワークフロー ハンドラーにタグを関連付けるよう、SQL Server MDS Workflow Integration Services を構成します。  
  
3.  SQL Server MDS Workflow Integration Service を開始します。  
  
4.  ワークフロー ハンドラーの名前でタグ付けされたワークフローを開始する [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 内で、ビジネス ルールを作成します。  
  
5.  そのビジネス ルールを、カスタム ワークフローをトリガーするメンバーに適用します。  
  
### <a name="create-the-workflow-handler-assembly"></a>ワークフロー ハンドラー アセンブリの作成  
 カスタム ワークフローは、<xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> インターフェイスを実装する .NET クラス ライブラリ アセンブリです。 SQL Server MDS Workflow Integration Service は、<xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> メソッドを呼び出してコードを実行します。 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> を実装するコードの例については、「[カスタム ワークフローの例 &#40;マスター データ サービス&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)」を参照してください。  
  
 カスタム ワークフローを処理するために SQL Server MDS Workflow Integration Service から呼び出すことができるアセンブリを、Visual Studio 2010 を使用して作成するには、次の手順を実行します。  
  
1.  Visual Studio 2010 で、任意の言語を使用する新しい **[クラス ライブラリ]** プロジェクトを作成します。 C# クラス ライブラリを作成するには、 **[Visual C#\Windows]** プロジェクト タイプを選択し、 **[クラス ライブラリ]** テンプレートを選択します。 プロジェクトの名前 (**MDSWorkflowTest** など) を入力し、 **[OK]** をクリックします。  
  
2.  Microsoft.MasterDataServices.WorkflowTypeExtender.dll への参照を追加します。 このアセンブリは、\<インストール フォルダー>\Master Data Services\WebApplication\bin にあります。  
  
3.  C# コード ファイルに、'using Microsoft.MasterDataServices.Core.Workflow;' を追加します。  
  
4.  クラス宣言で、<xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> を継承します。 クラス宣言は次のようになります: 'public class WorkflowTester : IWorkflowTypeExtender'  
  
5.  <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> インターフェイスを実装します。 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> メソッドは、ワークフローを開始するために SQL Server MDS Workflow Integration Service によって呼び出されます。  
  
6.  \<インストール フォルダー>\Master Data Services\WebApplication\bin 内にある SQL Server MDS Workflow Integration Service 実行可能ファイル (Microsoft.MasterDataServices.Workflow.exe) の場所に、アセンブリをコピーします。  
  
### <a name="configure-sql-server-mds-workflow-integration-service"></a>SQL Server MDS Workflow Integration Service の構成  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 構成ファイルを編集して、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベース用の接続情報を含め、ワークフロー ハンドラー アセンブリにタグを関連付けるには、次の手順を実行します。  
  
1.  \<インストール フォルダー>\Master Data Services\WebApplication\bin にある Microsoft.MasterDataServices.Workflow.exe.config を見つけます。  
  
2.  "ConnectionString" 設定に、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベース接続情報を追加します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールで大文字と小文字を区別する照合順序が使用されている場合、データベースの名前は、データベース内と同様の大文字/小文字で入力する必要があります。 たとえば、設定タグの全体は次のようになります。  
  
    ```xml  
    <setting name="ConnectionString" serializeAs="String">  
        <value>Server=myServer;Database=myDatabase;Integrated Security=True</value>  
    </setting>  
    ```  
  
3.  "ConnectionString" 設定下で "WorkflowTypeExtenders" 設定を追加して、ワークフロー ハンドラー アセンブリにタグ名を関連付けます。 例 :  
  
    ```xml  
    <setting name="WorkflowTypeExtenders" serializeAs="String">  
        <value>TEST=MDSWorkflowTestLib.WorkflowTester, MDSWorkflowTestLib</value>  
    </setting>  
    ```  
  
     \<value> タグの内部テキストは、\<ワークフロー タグ>=\<アセンブリ修飾型のワークフロー タイプ名> という形式になります。 \<ワークフロー タグ> は、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 内でビジネス ルールを作成する際に、ワークフロー ハンドラー アセンブリを識別するために使用する名前です。 \<アセンブリ修飾型のワークフロー タイプ名> は、名前空間で修飾されたワークフロー クラス名と、その後のコンマ、さらにその後の、アセンブリの表示名で指定します。 アセンブリに厳密な名前が指定されている場合は、バージョン情報と PublicKeyToken も含める必要があります。 異なる種類のワークフローを使用するために複数のワークフロー ハンドラーを作成した場合は、複数の \<setting> タグを含めることができます。  
  
> [!NOTE]  
>  サーバーの構成によっては、Microsoft.MasterDataServices.Workflow.exe.config ファイルを保存する際に、"アクセスが拒否されました" というエラーが返されることがあります。 その場合は、サーバー上のユーザー アカウント制御 (UAC) を一時的に無効にしてください。 これを行うには、コントロール パネルを開き、 **[システムとセキュリティ]** をクリックします。 **[アクション センター]** で、 **[ユーザー アカウント制御設定の変更]** をクリックします。 **[ユーザー アカウント制御の設定]** ダイアログで、スライダー バーを一番下まで下げ、通知が返されないようにします。 コンピューターを再起動し、上記の手順を繰り返して、構成ファイルを編集します。 ファイルを保存したら、UAC 設定を既定のレベルにリセットしてください。  
  
### <a name="start-sql-server-mds-workflow-integration-service"></a>SQL Server MDS Workflow Integration Service の開始  
 既定では、SQL Server MDS Workflow Integration Service はインストールされていません。 使用する前に、まずこのサービスをインストールする必要があります。 最大限のセキュリティを確保するため、このサービス用のローカル ユーザーを作成し、そのユーザーに対して、ワークフロー操作の実行に必要な権限のみを付与してください。 ユーザーを作成し、サービスをインストールして、サービスを開始するには、次の手順を実行します。  
  
1.  [ローカル ユーザーとグループ] マネージャーを使用して、ローカル ユーザー (この例では mds_workflow_service) を作成します。  
  
2.  SQL Server Management Studio を使用して、mds_workflow_service ユーザーに、[mdm].[udpExternalActionsGet] ストアド プロシージャを実行する権限を付与します。 これを行うには、mds_workflow_service アカウント用の新規ログインを作成し、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベース内に新規ユーザーを作成して、そのユーザーを mds_workflow_service ログインにマップした後、そのユーザーに、[mdm].[udpExternalActionsGet] ストアド プロシージャに対する EXECUTE 権限を付与します。  
  
3.  mds_workflow_service ユーザーに、ワークフロー ハンドラー アセンブリを実行する権限を付与します。 これを行うには、ワークフロー ハンドラー アセンブリの **[プロパティ]** の **[セキュリティ]** タブに mds_workflow_service ユーザーを追加し、その mds_workflow_service ユーザーに、READ および EXECUTE アクセス許可を付与します。  
  
4.  mds_workflow_service ユーザーに、SQL Server MDS Workflow Integration Service 実行可能ファイルを実行する権限を付与します。 これを行うには、Microsoft.MasterDataServices.Workflow.exe (**インストール フォルダー>\Master Data Services\WebApplication\bin 内) の** [プロパティ]**の**[セキュリティ]\< タブに mds_workflow_service ユーザーを追加し、その mds_workflow_service ユーザーに READ および EXECUTE アクセス許可を付与します。  
  
5.  .NET インストール ユーティリティ (InstallUtil.exe) を使用して、SQL Server MDS Workflow Integration Service をインストールします。 InstallUtil.exe は、.NET インストール フォルダー (C:\Windows\Microsoft.NET\Framework\v4.0.30319\\ など) にあります。 SQL Server MDS Workflow Integration Service は、管理者特権のコマンド プロンプトで次のコマンドを入力してインストールします。  
  
    ```  
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil Microsoft.MasterDataServices.Workflow.exe  
    ```  
  
     インストール中にユーザーの指定を求められたら、mds_workflow_service ユーザーを指定します。  
  
6.  サービス スナップインを使用して、SQL Server MDS Workflow Integration Service を開始します。 これを行うには、サービス スナップインで SQL Server MDS Workflow Integration Service を見つけて選択し、 **[開始]** リンクをクリックします。  
  
### <a name="create-a-workflow-business-rule"></a>ワークフロー ビジネス ルールの作成  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] を使用して、適用時にワークフローを開始するビジネス ルールを作成およびパブリッシュします。 ビジネス ルールには、属性値を変更するアクションを必ず含めて、そのルールが一度適用された後、false と評価されるようにしてください。 たとえば、Price 属性値が 500 より大きく、Approved 属性値が空白の場合に、true と評価されるビジネス ルールがあるとします。 その場合、そのルールに次の 2 つのアクションを含めることができます。1 つは、Approved 属性値を Pending に設定するアクション。もう 1 つは、ワークフローを開始するアクションです。 また、"が変更されている" 条件を使用するルールを作成し、追跡グループを変更するための属性を追加する方法もあります。 ビジネス ルールの詳細については、「[ビジネス ルール &#40;マスター データ サービス&#41;](../../master-data-services/business-rules-master-data-services.md)」を参照してください。  
  
 カスタム ワークフローを開始するビジネス ルールを [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] で作成するには、次の手順を実行します。  
  
1.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] のビジネス ルール エディターで、ビジネス ルールの条件を指定した後に、**ワークフローの開始**アクションを **[外部アクション]** ボックスの一覧から **[THEN]** ペインの **[アクション]** ラベルにドラッグします。  
  
2.  **[アクションの編集]** ペインの **[ワークフローの種類]** ボックスに、ワークフロー ハンドラー アセンブリを識別するタグを入力します。 これは、アセンブリの構成ファイルで指定したタグです (例: TEST)。  
  
3.  必要に応じて、 **[メッセージにメンバーのデータを含める]** チェック ボックスをオンにします。 これをオンにすると、ワークフロー ハンドラーに渡される XML に、属性の名前と値が含められます。  
  
4.  **[ワークフロー サイト]** ボックスに、Web サイトの名前を入力します。 これは、使用するカスタム ワークフローには該当しない場合がありますが、追加のコンテキスト用に使用できます。  
  
5.  **[ワークフロー名]** ボックスに、Visual Studio からのワークフローの名前を入力します。 これは、使用するカスタム ワークフローには該当しない場合がありますが、追加のコンテキスト用に使用できます。  
  
6.  ビジネス ルールを作成およびパブリッシュします。  
  
### <a name="apply-business-rules-to-start-a-workflow"></a>ビジネス ルールを適用してワークフローを開始する  
 データにビジネス ルールを適用して、ワークフローを開始します。 これを行うには、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] を使用して、検証するメンバーを含んだエンティティを編集します。 **[ビジネス ルールの適用]** をクリックします。 ビジネス ルールへの応答として、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] は、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースの Service Broker キューに値を設定します。 SQL Server MDS Workflow Integration Service は、キューをチェックすると、指定されたワークフロー ハンドラー アセンブリにデータを送信し、キューをクリアします。 ワークフロー ハンドラー アセンブリは、コードに記述された任意のアクションを実行します。  
  
## <a name="troubleshoot-custom-workflows"></a>カスタム ワークフローのトラブルシューティング  
 ワークフロー ハンドラー アセンブリがデータを受け取らなかった場合は、SQL Server MDS Workflow Integration Service をデバッグするか、または Service Broker キューを表示してみることができます。  
  
### <a name="debug-sql-server-mds-workflow-integration-service"></a>SQL Server MDS Workflow Integration Service のデバッグ  
 SQL Server Workflow Integration Service をデバッグするには、次の手順に従います。  
  
1.  サービス スナップインを使用して、サービスを停止します。  
  
2.  コマンド プロンプトを開き、サービスの場所に移動した後、コマンド Microsoft.MasterDataServices.Workflow.exe -console を入力してサービスをコンソール モードで実行します。  
  
3.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] で、メンバーを更新し、ビジネス ルールを再度適用します。 詳細なログがコンソール ウィンドウに表示されます。  
  
### <a name="view-the-service-broker-queue"></a>Service Broker キューの表示  
 ワークフローの一部として渡されるマスター データを含んだ Service Broker キューは、mdm.microsoft/mdm/queue/externalaction です。 キューは、SQL Management Studio の **[オブジェクト エクスプローラー]** で、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースの Service Broker ノードに表示されます。 ただし、サービスがキューを適切にクリアした場合、このキューは空になります。  
  
## <a name="see-also"></a>参照  
 [カスタム ワークフローの例 &#40;マスター データ サービス&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)   
 [カスタム ワークフロー XML の説明 &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md)  
  
  
