---
title: MDSModelDeploy を使用したモデルの配置パッケージの配置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 81c87a7990c6c7125cbccbe99050cd5ee477e6d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483073"
---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>MDSModelDeploy を使用したモデルの配置パッケージの配置
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、MDSModelDeploy ツールを使用して、次のどちらかを含むパッケージを配置します。  
  
-   モデル オブジェクトのみ。  
  
-   モデル オブジェクトとデータ。  
  
 モデル オブジェクトのみを含むパッケージを配置する必要がある場合は、代わりに、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションのモデル配置ウィザードを使用できます。 詳細については、「 [ウィザードを使用したモデルの配置パッケージの展開](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)」を参照してください。  
  
> [!IMPORTANT]  
>  パッケージは、そのパッケージが作成されたエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にのみ配置できます。 つまり、 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] で作成されたパッケージを [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 以降に配置することはできません。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   ターゲット **環境の** [システム管理] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 機能領域にアクセスする権限が必要です。  
  
-   モデルの配置パッケージが必要です。 詳細については、「  [MDSModelDeploy を使用したモデルの配置パッケージの作成](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)」を参照してください。  
  
-   モデルを配置する環境の管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
-   モデルのデータを更新する場合、配置するバージョンは **ロック解除** することも、**コミット**することもできません。  
  
### <a name="to-deploy-a-model-deployment-package"></a>モデルの配置パッケージを配置するには  
  
1.  新しいモデルを配置するのか、モデルを複製するのか、以前に複製したモデルを更新するのかを決定します。 詳細については、「[モデル配置オプション (マスター データ サービス)](../../2014/master-data-services/model-deployment-options-master-data-services.md)」を参照してください。  
  
2.  コマンド プロンプトを開き、MDSModelDeploy.exe のある場所に移動します。  
  
    -   MDS を既定の場所にインストールする場合、ツールは*ドライブ*: SQL server \120\master Data Services\Configuration\MDSModelDeploy.exe \Program Files\Microsoft  
  
    -   MDS を既定の場所にインストールしなかった場合は、ローカル コンピューター内で MDSModelDeploy.exe を検索します。  
  
3.  任意。 オプションおよびヘルプを表示します。  
  
    -   使用可能なすべてのオプションを表示するには、「 `MDSModelDeploy` 」と入力し、Enter キーを押します。  
  
    -   オプションのヘルプを表示するには、「 *」と入力します。* OptionName `MDSModelDeploy help OptionName`はオプションの名前です。  
  
4.  任意。 Web アプリケーションが複数ある場合、次のコマンドを入力し、Enter キーを押して、配置するサービスの名前を確認します。  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     値の一覧が返されます (例: `MDS1, Default Web Site, MDS`)。 モデルを配置するには、この一覧の最初の値 (この例では、 `MDS1`) が必要です。  
  
5.  モデルを配置するのか、モデルを複製するのか、以前に複製したモデルを更新するのかに応じて、コマンド プロンプトに次のコマンドを入力し、Enter キーを押します。  
  
    -   新しいモデルを作成するには  
  
        ```  
        MDSModelDeploy deploynew -package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   モデルの複製を作成するには  
  
        ```  
        MDSModelDeploy deployclone -package PackageName  
        ```  
  
    -   既存のモデルとそのデータを更新するには  
  
        ```  
        MDSModelDeploy deployupdate -package PackageName -version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  MDSModelDeploy ツールを使用して既存のモデルとそのデータを更新するときに、配置先モデルに存在するエンティティ、属性、またはメンバーがパッケージに含まれていない場合は、MDSModelDeploy によって、そのエンティティ、属性、またはメンバーがモデルから削除されることはありません。  
  
     *PackageName* はパッケージ (.pkg) ファイルの名前、 *ModelName* は新しいモデルの名前、 *VersionName* はバージョンの名前、 *ServiceName* は前の手順で返されたサービスの名前です。 モデル名とバージョン名は大文字と小文字の違いも含めて正確に指定してください。  
  
6.  パッケージが正常に配置されると、"MDSModelDeploy 操作は正常に完了しました" というメッセージが表示されます。  
  
 **注**  
  
-   としてビューを作成する場合は、パッケージ内のサブスクリプション ビューでは、既存のモデルにサブスクリプション ビューと同じ名前が含まれる*modelname.subscriptionviewname*します。 この名前が既に使用されている場合、サブスクリプション ビューは作成されません。  
  
-   配置プロセスには、次の 4 つの手順があります。  
  
    1.  モデル オブジェクトが作成されます。  
  
    2.  ビジネス ルールが作成されます。  
  
    3.  サブスクリプション ビューが作成されます。  
  
    4.  マスター データが設定されます。  
  
-   新しいモデルまたは複製モデルを作成する場合、いずれかの手順の実行中にプロセスが失敗すると、モデルは削除されます。  
  
     モデルを更新する場合、最初の 3 つの手順の実行中にプロセスが失敗すると、そのプロセスは続行されません。ただし、既に行われた変更はロールバックされません。 手順 4. でプロセスが失敗すると、更新可能なメンバーが更新されます。  
  
## <a name="next-steps"></a>次の手順  
 ユーザー定義メタデータ、ファイル属性、ユーザーおよびグループの権限はモデル配置パッケージに含まれていません。 モデルを配置した後、これらを手動で更新する必要があります。 詳細については、以下をご覧ください。  
  
-   [メタデータの追加&#40;マスター データ サービス&#41;](../../2014/master-data-services/add-metadata-master-data-services.md)  
  
-   [モデル オブジェクト権限を割り当てる (マスター データ サービス)](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [モデルの配置 (マスター データ サービス)](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  
