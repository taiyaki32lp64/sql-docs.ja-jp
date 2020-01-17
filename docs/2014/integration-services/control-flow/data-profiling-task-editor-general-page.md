---
title: '[データ プロファイル タスク エディター] ([全般] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataprofilingtask.general.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: eec15906-d757-4079-b2f6-aca4e52b3b4c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8462f85dc6c804020f12b9bc989d683c5a4ad0ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832226"
---
# <a name="data-profiling-task-editor-general-page"></a>[データ プロファイル タスク エディター] ([全般] ページ)
  **[データ プロファイル タスク エディター]** の **[全般]** ページを使用すると、次のオプションを構成できます。  
  
-   プロファイル出力の保存先を指定する。  
  
-   既定の設定を使用して、単一のテーブルまたはビューをプロファイルするタスクを簡素化する。  
  
 データ プロファイル タスクの使用方法の詳細については、「 [データ プロファイル タスクのセットアップ](data-profiling-task.md)」を参照してください。 Data Profile Viewer を使用してデータ プロファイル タスクの出力を分析する方法の詳細については、「 [Data Profile Viewer](data-profile-viewer.md)」を参照してください。  
  
 **[データ プロファイル タスク エディター] の [全般] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、データ プロファイル タスクを含む [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[制御フロー]** タブで、データ プロファイル タスクをダブルクリックします。  
  
3.  **[データ プロファイル タスク エディター]** で、 **[全般]** をクリックします。  
  
## <a name="data-profiling-options"></a>データ プロファイルに関するオプション  
 **Timeout**  
 データ プロファイル タスクがタイムアウトして実行を停止するまでの秒数を指定します。 既定値は 0 であり、タイムアウトしないことを示します。  
  
## <a name="destination-options"></a>転送先に関するオプション  
  
> [!IMPORTANT]  
>  出力ファイルには、データベースに関する機密データやデータベースに格納されているデータが含まれる場合があります。 このファイルの安全性を高める方法の推奨事項については、「 [パッケージで使用されるファイルへのアクセス](../access-to-files-used-by-packages.md)」をご覧ください。  
  
 **[DestinationType]**  
 データ プロファイル出力をファイルに保存するか変数に保存するかを指定します。  
  
|値|説明|  
|-----------|-----------------|  
|**[FileConnection]**|ファイル接続マネージャーで指定された場所にあるファイルにプロファイル出力を保存します。<br /><br /> 注:使用するファイル接続マネージャーは **[Destination]** オプションで指定します。|  
|**変数**|プロファイル出力をパッケージ変数に保存します。<br /><br /> 注:使用するパッケージ変数は **[Destination]** オプションで指定します。|  
  
 **変換先**  
 データ プロファイル出力を含むファイル接続マネージャーまたはパッケージ変数を指定します。  
  
-   **[DestinationType]** オプションが **[FileConnection]** に設定されている場合、 **[Destination]** オプションには使用可能なファイル接続マネージャーが表示されます。 これらの接続マネージャーのいずれかを選択するか、[\<新しいファイル接続>] を選択して新しいファイル接続マネージャーを作成します。  
  
-   **[DestinationType]** オプションが **[Variable]** に設定されている場合、 **[Destination]** オプションでは使用可能なパッケージ変数が **[Destination]** の一覧に表示されます。 これらの変数のいずれかを選択するか、[\<新しい変数>] を選択して新しい変数を作成します。  
  
 **[OverwriteDestination]**  
 出力ファイルが既に存在する場合に、その出力ファイルを上書きするかどうかを指定します。 既定値は **False**です。 このプロパティの値は、[DestinationType] オプションが [FileConnection] に設定されている場合にのみ使用されます。 [DestinationType] オプションが [Variable] に設定されている場合は、変数の以前の値が常に上書きされます。  
  
> [!IMPORTANT]  
>  出力ファイル名を変更せずに、または **OverwriteDestination** プロパティの値を **True**に変更せずに、データ プロファイル タスクを 2 回以上実行すると、出力ファイルが既に存在するというメッセージが表示され、タスクは失敗します。  
  
## <a name="other-options"></a>その他のオプション  
 **[クイック プロファイル]**  
 **[単一テーブル クイック プロファイル フォーム]** を表示します。 このフォームでは、既定の設定を使用することで、単一のテーブルまたはビューをプロファイルするタスクを簡素化します。 詳細については、「 [単一テーブル クイック プロファイル フォーム &#40;データ プロファイル タスク&#41;](single-table-quick-profile-form-data-profiling-task.md)」を参照してください。  
  
 **[プロファイル ビューアーを開く]**  
 Data Profile Viewer を開きます。 スタンドアロンの Data Profile Viewer は、データ プロファイル タスクのデータ プロファイル出力を表示します。 データ プロファイル出力は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ内でデータ プロファイル タスクを実行してデータ プロファイルを計算した後に表示できます。  
  
> [!NOTE]  
>  *\<ドライブ>* :\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn フォルダーの DataProfileViewer.exe を実行して、Data Profile Viewer を開くこともできます。  
  
## <a name="see-also"></a>参照  
 [単一テーブル クイック プロファイル フォーム &#40;データ プロファイル タスク&#41;](single-table-quick-profile-form-data-profiling-task.md)   
 [データ プロファイル タスク エディター &#40;[プロファイル要求] ページ&#41;](data-profiling-task-editor-profile-requests-page.md)  
  
  
