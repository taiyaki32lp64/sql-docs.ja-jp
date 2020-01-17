---
title: パラメーターの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.parameterwindow.f1
ms.assetid: cd5d675b-dd5d-49cc-8b1f-dc717a973f99
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 639e31d8ec9282a948a7eda9050cc1a2025ac65e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060142"
---
# <a name="create-parameters"></a>Create Parameters
  プロジェクト パラメーターおよびパッケージ パラメーターを作成するには、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用します。 以下の手順では、パッケージ/プロジェクト パラメーターを作成する方法を詳細に説明します。  
  
> [!NOTE]  
>  以前のバージョンの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] を使用して作成したプロジェクトをプロジェクトの配置モデルに変換する場合は、**Integration Services プロジェクト変換ウィザード**を使用して、構成に基づいたパラメーターを作成できます。 詳細については、「 [Integration Services サーバーへのプロジェクトの配置](../../2014/integration-services/deploy-projects-to-integration-services-server.md)」を参照してください。  
  
### <a name="to-create-package-parameters"></a>パッケージ パラメーターを作成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] でパッケージを開き、SSIS デザイナーの **[パラメーター]** タブをクリックします。  
  
     ![パッケージの [パラメーター] タブ](media/denali-package-parameters.gif "パッケージの [パラメーター] タブ")  
  
2.  ツール バーの **[パラメーターの追加]** ボタンをクリックします。  
  
     ![ツール バーの [追加] ボタン](media/denali-parameter-add.gif "ツール バーの [追加] ボタン")  
  
3.  一覧で直接、または **[プロパティ]** ウィンドウを使用して、 **[名前]** 、 **[データ型]** 、 **[値]** 、 **[区別する]** 、 **[必須]** の各プロパティに値を入力します。 次の表では、これらのプロパティについて説明します。  
  
    |プロパティ|説明|  
    |--------------|-----------------|  
    |名前|パラメーターの名前。|  
    |データ型|パラメーターのデータ型です。|  
    |既定値|設計時に割り当てられたパラメーターの既定値。 これは設計時の既定値とも呼ばれます。|  
    |区別する|機密性の高いパラメーター値はカタログ内で暗号化され、Transact-SQL または SQL Server Management Studio で表示する際は NULL 値として表示されます。|  
    |必須|パッケージを実行する前に、設計上の既定値以外の値を指定する必要があります。|  
    |説明|管理しやすさを考慮した、パラメーターの説明。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、該当するパラメーター ウィンドウでパラメーターを選択したときに、Visual Studio プロパティ ウィンドウでパラメーターの説明を設定します。|  
  
    > [!NOTE]  
    >  プロジェクトをカタログに配置すると、いくつかのプロパティがプロジェクトに関連付けられます。 カタログ内のすべてのパラメーターのすべてのプロパティを表示するには、[catalog.object_parameters &#40;SSISDB Database&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database) ビューを使用します。  
  
4.  プロジェクトを保存して、変更をパラメーターに保存します。 パラメーターの値はプロジェクト ファイルに格納されます。  
  
    > [!WARNING]  
    >  リストで直接編集することも、 **[プロパティ]** ウィンドウを使用してパラメーターのプロパティの値を変更することもできます。 **[削除] \(X)** ツール バー ボタンを使用して、パラメーターを削除できます。 ツール バーの最後のボタンを使用すると、[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] でパッケージを実行するときにのみ使用されるパラメーターの値を指定できます。  
  
    > [!NOTE]  
    >  プロジェクトを [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で開かずにパッケージ ファイルを再度開くと、 **[パラメーター]** タブは空になり、無効になります。  
  
### <a name="to-create-project-parameters"></a>プロジェクト パラメーターを作成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] でプロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで **[Project.params]** を右クリックして **[開く]** をクリックするか、または **[Project.params]** をダブルクリックして開きます。  
  
     ![プロジェクト パラメーター ウィンドウ](media/denali-project-parameters.gif "プロジェクト パラメーター ウィンドウ")  
  
3.  ツール バーの **[パラメーターの追加]** ボタンをクリックします。  
  
     ![ツール バーの [追加] ボタン](media/denali-parameter-add.gif "ツール バーの [追加] ボタン")  
  
4.  **[名前]** 、 **[データ型]** 、 **[値]** 、 **[区別する]** 、 **[必須]** の各プロパティに値を入力します。  
  
    |プロパティ|説明|  
    |--------------|-----------------|  
    |名前|パラメーターの名前。|  
    |データ型|パラメーターのデータ型です。|  
    |既定値|設計時に割り当てられたパラメーターの既定値。 これは設計時の既定値とも呼ばれます。|  
    |区別する|機密性の高いパラメーター値はカタログ内で暗号化され、Transact-SQL または SQL Server Management Studio で表示する際は NULL 値として表示されます。|  
    |必須|パッケージを実行する前に、設計上の既定値以外の値を指定する必要があります。|  
    |説明|管理しやすさを考慮した、パラメーターの説明。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] では、該当するパラメーター ウィンドウでパラメーターを選択したときに、Visual Studio プロパティ ウィンドウでパラメーターの説明を設定します。|  
  
5.  プロジェクトを保存して、変更をパラメーターに保存します。 パラメーター値はプロジェクト ファイルの構成に格納されます。 プロジェクト ファイルを保存して、パラメーター値の変更をディスクにコミットしてください。  
  
    > [!WARNING]  
    >  リストで直接編集することも、 **[プロパティ]** ウィンドウを使用してパラメーターのプロパティの値を変更することもできます。 **[削除] \(X)** ツール バー ボタンを使用して、パラメーターを削除できます。 ツール バーの最後のボタンを使用すると、 **[パラメーター値の管理]** ダイアログ ボックスを開いて、[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] でパッケージを実行するときにのみ使用されるパラメーターの値を指定できます。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41;パラメーター](integration-services-ssis-package-and-project-parameters.md)  
  
  
