---
title: 手順 2:パッケージ インストール ウィザードの実行 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f91fbb89-4626-4c47-b96d-56052dc45861
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b380b56611e72bfd6b0c249792843a6a684813b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283327"
---
# <a name="lesson-3-2---running-the-package-installation-wizard"></a>レッスン 3-2 - パッケージ インストール ウィザードの実行

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


この実習では、パッケージ インストール ウィザードを実行して、Deployment Tutorial プロジェクトから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスにパッケージを配置します。 msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースの sysssispackages テーブルにインストールできるのはパッケージだけです。配置バンドルに含まれるサポート ファイルは、ファイル システムに配置されます。  
  
パッケージ インストール ウィザードを使用すると、手順に従ってパッケージのインストールと構成を行うことができます。 配置先のコンピューター (配置バンドルをコピーするコンピューター) の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスにパッケージをインストールします。 また、C:\DeploymentTutorialInstall フォルダーも作成します。このフォルダーには、パッケージ以外のファイルがインストールされます。  
  
前のレッスンで、構成を使用するようにチュートリアルのパッケージを変更しました。 パッケージ インストール ウィザードを使用してこれらの構成を編集し、インストール先の環境でパッケージを正常に実行できるようにします。  
  
### <a name="to-install-the-packages"></a>パッケージをインストールするには  
  
1.  インストール先のコンピューターの配置バンドルを見つけます。  
  
    配置ユーティリティの場所として既定値の bin\Deployment を使用した場合は、Deployment Tutorial プロジェクト内にある Deployment フォルダーが配置バンドルです。  
  
2.  Deployment フォルダーで、マニフェスト ファイルの Deployment Tutorial.SSISDeploymentManifest をダブルクリックします。  
  
3.  パッケージ インストール ウィザードの初期画面で、 **[次へ]** をクリックします。  
  
4.  [SSIS パッケージの配置] ページで、 **[SQL Server に配置]** オプションを選択し、 **[インストール後にパッケージを検証する]** チェック ボックスをオンにして、 **[次へ]** をクリックします。  
  
5.  [インストール先の SQL Server の指定] ページで、 **[サーバー名]** ボックスに **(local)** と指定します。  
  
6.  SQL Server のインスタンスが Windows 認証をサポートしている場合は、 **[Windows 認証を使用]** を選択します。サポートしていない場合は、 **[SQL Server 認証を使用]** を選択し、ユーザー名とパスワードを入力します。  
  
7.  **[暗号化をサーバー ストレージに依存する]** チェック ボックスがオフになっていることを確認します。  
  
8.  **[次へ]** をクリックします。  
  
9. [インストール フォルダーの選択] ページの **[参照]** をクリックします。  
  
10. **[フォルダーの参照]** ダイアログ ボックスで、 **[マイ コンピューター]** を展開し、 **[ローカル ディスク (C:)]** をクリックします。  
  
11. **[新しいフォルダーの作成]** をクリックし、新しいフォルダーの既定の名前 **[新しいフォルダー]** の代わりに「 **DeploymentTutorialInstall**」と入力します。  
  
    > [!IMPORTANT]  
    > この名前は、構成が使用する環境変数の値で参照されます。 フォルダーと参照の名前が一致しなければ、パッケージを実行できません。  
  
12. **[OK]** をクリックします。  
  
13. [インストール フォルダーの選択] ページで、[フォルダー] ボックスに **C:\DeploymentTutorialInstall** と表示されていることを確認し、 **[次へ]** をクリックします。  
  
14. [インストールの確認] ページで、 **[次へ]** をクリックします。  
  
    パッケージがインストールされます。 インストールが完了すると、[パッケージの構成] ページが表示されます。  
  
15. [パッケージの構成] ページで、 **[構成ファイル]** ボックスに datatransferconfig.dtsconfig と loadxmldataconfig.dtsconfig が表示されていることを確認します。  
  
16. **[構成ファイル]** ボックスの一覧で、 **[datatransferconfig.dtsconfig]** をクリックし、 **[構成]** ボックスの **[パス]** 列のプロパティを展開して、 **[値]** 列を次の値で更新します。  
  
    |プロパティ|[値]|更新後の値|  
    |------------|---------|-----------------|  
    |\Package.Connections[Deployment Tutorial Log].Properties[ConnectionString]|C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Completed Packages\Deployment Tutorial Log|C:\DeploymentTutorialInstall\Deployment Tutorial Log|  
    |\Package.Connections[NewCustomers].Properties[ConnectionString]|C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Sample Data\NewCustomers.txt|C:\DeploymentTutorialInstall\NewCustomers.txt|  
  
17. **[構成ファイル]** ボックスの一覧で、[loadxmldataconfig.dtsconfig] をクリックし、 **[構成]** ボックスの **[パス]** 列のプロパティを展開して、 **[値]** 列を次の値で更新します。  
  
    |プロパティ|[値]|更新後の値|  
    |------------|---------|-----------------|  
    |\Package.LoadXMLData.Properties[[XML Source].[XMLData]]|C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Sample Data\orders.xml|C:\DeploymentTutorialInstall\orders.xml|  
    |\Package.LoadXMLData.Properties[[XML Source].[XMLSchemaDefinition]]|C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Sample Data\orders.xsd|C:\DeploymentTutorialInstall\orders.xsd|  
  
18. [パッケージの検証] ページで、インストールされた各パッケージの検証結果を表示し、 **[次へ]** をクリックします。  
  
    配置先コンピューターの環境変数の値は開発用コンピューターの環境変数の値と異なるため、[パッケージの検証] ページに複数の警告が表示されます。 次の 4 つの警告が表示されます。  
  
    -   構成ファイル: "C:\DeploymentTutorial\DataTransferConfig.dtsConfig" は有効ではありません。 構成ファイルの名前を確認してください。  
  
    -   パッケージの少なくとも 1 つの構成エントリを読み込めませんでした。 構成エントリとそれ以前に発生した警告を確認して、読み込めなかった構成に関する説明を参照してください。  
  
    -   構成ファイル: "C:\DeploymentTutorial\LoadXMLDataConfig.dtsConfig は有効ではありません。 構成ファイルの名前を確認してください。  
  
    -   パッケージの少なくとも 1 つの構成エントリを読み込めませんでした。 構成エントリとそれ以前に発生した警告を確認して、読み込めなかった構成に関する説明を参照してください。  
  
    これらの警告は、パッケージのインストールに影響しません。  
  
    [SSIS パッケージの配置] ページで **[インストール後にパッケージを検証する]** オプションを選択しなかった場合、[パッケージの検証] ページは表示されず、検証に関するインストール後の情報も表示されません。  
  
19. [パッケージ インストール ウィザードの完了] ページでインストールの概要を確認してから、 **[完了]** をクリックします。  
  
    > [!NOTE]  
    > パッケージの検証に使用する一時ログ ファイルが作成されます。 このファイルは、パッケージの実行時には使用されません。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
[ステップ 3:配置したパッケージのテスト](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="see-also"></a>参照  
[Integration Services サービス (SSIS サービス)](../integration-services/service/integration-services-service-ssis-service.md)  
