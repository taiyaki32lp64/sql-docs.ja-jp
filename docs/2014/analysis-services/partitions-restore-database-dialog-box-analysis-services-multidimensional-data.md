---
title: パーティション (復元データベース ダイアログ ボックス) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.partitions.f1
ms.assetid: 1ad4dde5-4651-4069-875c-7ab73cd8b4f4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0c28420d711fd009dfc2b1e36ef4a613b3ecfaf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072111"
---
# <a name="partitions-restore-database-dialog-box-analysis-services---multidimensional-data"></a>[パーティション] ([データベースの復元] ダイアログ ボックス) (Analysis Services - 多次元データ)
  **の** [データベースの復元] **ダイアログ ボックスの** [パーティション] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ページを使用すると、ローカル パーティションを復元する場所の指定、リモート パーティションを復元するかどうかの指定、リモート パーティションを復元する際に使用するリモート バックアップ ファイルの指定ができます。  
  
> [!IMPORTANT]  
>  バックアップ ファイルごとに、復元コマンドを実行するユーザーは、各ファイルに指定されたバックアップ場所から読み取る権限を持っている必要があります。 サーバーにインストールされていない [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースを復元する場合、ユーザーは、その [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスのサーバー ロールのメンバーであることも必要です。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースを上書きするには、ユーザーは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスのサーバー ロールのメンバーか、復元するデータベースに対してフル コントロール (管理者) 権限を持つデータベース ロールのメンバーのいずれかである必要があります。  
  
> [!NOTE]  
>  既存のデータベースを復元すると、データベースを復元したユーザーは、復元されたデータベースにアクセスできなくなる可能性があります。 バックアップの実行時に、ユーザーがサーバー ロールのメンバー、またはフル コントロール (管理者) 権限を持つデータベース ロールのメンバーではなかった場合、このようにアクセスできなくなることがあります。  
  
 **データベースの復元 ダイアログ ボックスで、パーティション ページを表示するには**  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]の **オブジェクト エクスプローラー** で、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスの **[データベース]** フォルダー、またはデータベースを右クリックし、 **[データベースの復元]** をクリックします。次に、 **[ページの選択]** で **[パーティション]** をクリックします。  
  
## <a name="options"></a>および  
 **[スクリプト]**  
 ダイアログ ボックスで選択したオプションに基づいた復元スクリプトを作成します。 復元用スクリプトは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] スクリプト言語 (ASSL) で記述されています。  
  
 **[スクリプト]** アイコンをクリックすると、既定では、新しいクエリ ウィンドウに復元スクリプトが送信されます。  
  
 **[スクリプト]** の矢印をクリックすると、復元スクリプトの送信先を次の中から選択できるメニューが表示されます。  
  
-   新しいクエリ ウィンドウ (既定)。  
  
-   ファイル。  
  
-   クリップボード。  
  
-   ジョブ。  
  
 **元の場所に復元します。**  
 選択すると、バックアップ ファイルに保存されているローカル パーティションを元の場所に復元します。  
  
 **別の場所を選択します。**  
 ローカル パーティションの復元先として別の場所を指定する場合に選択します。  
  
> [!NOTE]  
>  ローカル パーティションにキューブ内の既定の場所以外の場所が指定されている場合にのみ、そのパーティションの復元フォルダーを変更できます。  
  
 このオプションを選択した場合、次のグリッドが有効になります。これを使用して、各ローカル パーティションの復元フォルダーを指定します。  
  
|[列]|説明|  
|------------|-----------------|  
|**Cube**|ローカル パーティションが含まれているキューブの名前が表示されます。|  
|**メジャー グループ**|ローカル パーティションが含まれているメジャー グループの名前が表示されます。|  
|**パーティション**|ローカル パーティションの名前が表示されます。|  
|**[サイズ (MB)]**|ローカル パーティションのサイズ (MB) が表示されます。|  
|**元のフォルダー**|ローカル パーティションが収められていた元のフォルダーの名前が表示されます。|  
|**復元フォルダー**|ローカル パーティションの復元フォルダーの名前を入力するか、参照ボタン ( **[...]** ) をクリックして **[リモート フォルダーの参照]** ダイアログ ボックスを表示し、使用するフォルダーのパスを選択します。 **[リモート フォルダーの参照]** ダイアログ ボックスの詳細については、「[[リモート フォルダーの参照] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。|  
  
 **リモート パーティションを復元します。**  
 選択すると、リモート バックアップ ファイルに保存されているリモート パーティションを復元します。  
  
> [!NOTE]  
>  バックアップ ファイルにリモート パーティションへの参照が含まれている場合にのみ、このオプションが有効になります。  
  
 このオプションを選択した場合、次のグリッドが有効になります。これを使用して、各ローカル パーティションの復元フォルダーを指定します。  
  
|[列]|説明|  
|------------|-----------------|  
|**[サーバー]**|リモート パーティションを管理する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスの名前が表示されます。|  
|**Data Source**|バックアップ ファイル内のデータ ソースの名前が表示されます。これは、リモート パーティションを含むデータベースを表します。|  
|**バックアップ ファイル**|使用するリモート バックアップ ファイルの完全なパスとファイル名を入力するか、参照ボタン ( **[...]** ) をクリックして **[データベース ファイルの検索]** ダイアログ ボックスを表示し、使用するリモート バックアップ ファイルのパスとファイル名を選択します。 **[データベース ファイルの検索]** ダイアログ ボックスの詳細については、「[[データベース ファイルの検索] ダイアログ ボックス (Analysis Services - 多次元データ)](locate-database-files-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。|  
|**[...]**|クリックすると、 **[リモート パーティション - 詳細設定]** ダイアログ ボックスが表示され、リモート パーティションの復元に使用するデータ ソースの接続文字列などの詳細なオプションを変更できます。 **[リモート パーティション - 詳細設定]** ダイアログ ボックスの詳細については、「[[リモート パーティション - 詳細設定] ダイアログ ボックス (Analysis Services - 多次元データ)](remote-partitions-advanced-settings-dialog-analysis-services-multidimensional-data.md)」を参照してください。|  
  
## <a name="see-also"></a>関連項目  
 [[データベースの復元] ダイアログ ボックス (Analysis Services - 多次元データ)](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [一般的な&#40;データベースの復元 ダイアログ ボックス&#41; &#40;Analysis Services - 多次元データ&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Analysis Services データベースのバックアップと復元](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
