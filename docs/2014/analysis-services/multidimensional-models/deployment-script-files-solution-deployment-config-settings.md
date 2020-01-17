---
title: ソリューションの配置に関する構成設定の指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, configuration settings
- input files [Analysis Services]
- configuration options [Analysis Services]
- Analysis Services deployments, configuration settings
- deploying [Analysis Services], configuration settings
ms.assetid: 953814a3-85ef-40cc-b46a-d532aa7a6569
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8addba32560e136f68e538240f4fce01f826355e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075265"
---
# <a name="specifying-configuration-settings-for-solution-deployment"></a>ソリューションの配置に関する構成設定の指定
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]展開ウィザードから、配置スクリプトで使用する展開オプション パーティションおよびロールを読み取り、 \<*プロジェクト名*> >.configsettings ファイル。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの作成時にこのファイルを作成します。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 現在のプロジェクトの構成設定を使用して、作成、 \<*プロジェクト名*> >.configsettings ファイル。  
  
## <a name="reviewing-the-configuration-settings-for-deployment"></a>配置に関する構成設定の確認  
 格納されている構成設定を次に、 \<*プロジェクト名*> >.configsettings ファイル。  
  
-   **データ ソース接続文字列** これは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトで指定されている値に基づいた各データ ソースの接続文字列です。 このファイルに接続文字列が保存される際には、常にユーザー ID とパスワードが削除されます。 ただし、配置ウィザードで Analysis Services インスタンスに直接配置を行う場合は、ウィザードで適切なユーザー ID とパスワードを入力して、配置するデータベースを正常に処理することができます。 配置ウィザードで配置スクリプトを保存する場合、この接続情報は配置スクリプト内に保存されません。  
  
-   **権限借用アカウント** この設定では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が各データ ソースでステートメントを実行するために使用するユーザー名を指定します。 権限借用アカウントが指定されていない場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のログオン アカウントを使用してステートメントが実行されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ログオン アカウントがデータ ソース内で権限を直接与えられている場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのすべてのデータベース内のデータベース管理者は、だれでもそのログオン アカウントを使用してデータ ソースにアクセスできます。 ユーザー アカウントとパスワードが指定された場合、このファイルに権限借用情報が保存される前に常にこの情報は削除されます。 ただし、配置ウィザードで Analysis Services インスタンスに直接配置を行う場合は、ウィザードで適切なユーザー ID とパスワードを入力して、配置するデータベースを正常に処理することができます。 配置ウィザードで配置スクリプトを保存する場合、この権限借用情報は配置スクリプト内に保存されません。  
  
-   **キーのエラー ログ ファイル** この設定では、データベース内の各キューブ、メジャー グループ、パーティション、およびディメンションのキー エラー ログ ファイルのファイル名とパスを指定します。  
  
-   **ストレージの場所** この設定では、データベース内の各キューブ、メジャー グループ、およびパーティションのストレージの場所を指定します。 オブジェクトの値が指定されていない場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードではオブジェクトの既定の場所が使用されます。 たとえば、パーティションにはメジャー グループの場所が使用され、メジャー グループにはキューブの場所が使用され、キューブには [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのオブジェクトの既定の場所が使用されます。 ストレージの場所には、ローカルまたは汎用名前付け規則 (UNC) のどちらかのパスを指定できます。  
  
-   **レポート サーバー** この設定では、データベース内の各キューブで定義されている各レポート アクションのレポート サーバーとフォルダーの場所を指定します。  
  
## <a name="modifying-the-configuration-settings-for-deployment"></a>配置に関する構成設定の変更  
 場合によっては、展開する必要があります、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]プロジェクトに格納されているものと異なる構成設定を使用して、 \<*プロジェクト名*> >.configsettings ファイル。 たとえば、1 つまたは複数のデータ ソースへの接続文字列を変更するか、特定のパーティションまたはメジャー グループのストレージの場所を指定する必要が生じることがあります。  
  
 パーティションおよびロールの配置を変更する、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]プロジェクト内のこの情報を変更する必要があります、 \<*プロジェクト名*> >.configsettings ファイルを次の手順で説明します。 に、プロジェクト内のパーティションおよびロールの設定を変更することはできません、 *\<プロジェクト名 >* **プロパティ ページ** ダイアログ ボックスで[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]これらのオプションは表示されません。  
  
> [!NOTE]  
>  構成設定は、すべてのオブジェクトに適用することも、新たに作成したオブジェクトのみに適用することもできます。 以前に配置した [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに追加のオブジェクトを配置し、既存のオブジェクトを上書きしないようにする場合は、新たに作成したオブジェクトのみに構成設定を適用します。 構成設定がすべてのオブジェクトに適用またはのみ新たに作成した、このオプションで設定するかどうかを指定する、 \<*プロジェクト名*> >.deploymentoptions ファイル。 詳細については、「 [パーティションおよびロールの配置オプションの指定](deployment-script-files-partition-and-role-deployment-options.md)」を参照してください。  
  
#### <a name="to-change-configuration-settings-after-the-input-files-have-been-generated"></a>入力ファイルの生成後に構成設定を変更するには  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードを対話形式で実行し、 **[構成設定]** ページで配置するオブジェクトの構成設定を指定します。  
  
     \- または -  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードをコマンド プロンプトで実行し、ウィザードを応答ファイル モードで実行するように設定します。 応答ファイル モードの詳細については、「 [Analysis Services 配置ウィザードの実行](running-the-analysis-services-deployment-wizard.md)」を参照してください。  
  
     \- または -  
  
-   変更、 \<*プロジェクト名*> 任意のテキスト エディターを使用して、>.configsettings ファイル。  
  
## <a name="see-also"></a>関連項目  
 [インストール先の指定](deployment-script-files-specifying-the-installation-target.md)   
 [パーティションおよびロールの配置オプションの指定](deployment-script-files-partition-and-role-deployment-options.md)   
 [処理オプションの指定](deployment-script-files-specifying-processing-options.md)  
  
  
