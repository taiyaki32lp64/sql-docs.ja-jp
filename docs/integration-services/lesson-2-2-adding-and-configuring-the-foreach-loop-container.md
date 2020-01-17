---
title: 手順 2:Foreach ループ コンテナーを追加して構成する | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a5a0b804cb1e5bf130179c7a91ec04fa0d064f12
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296047"
---
# <a name="lesson-2-2-add-and-configure-the-foreach-loop-container"></a>レッスン 2-2:Foreach ループ コンテナーを追加して構成する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



このタスクでは、フラット ファイルのフォルダー全体にループ機能を付加し、レッスン 1 のデータ フロー変換と同じ変換を各フラット ファイルに適用します。 そのためには、Foreach ループ コンテナーを制御フローに追加して、構成します。  
  
Foreach ループ コンテナーを追加したら、フォルダー内の各フラット ファイルに接続できるようにする必要があります。 フォルダー内のファイルはすべて同じ形式なので、Foreach ループ コンテナーは、どのファイルに接続する場合でも同じフラット ファイル接続マネージャーを使用できます。 コンテナーで使用するフラット ファイル接続マネージャーは、レッスン 1 で作成したものです。  
  
レッスン 1 で作成したフラット ファイル接続マネージャーは、現在、1 つのフラット ファイルにのみ接続しています。 フォルダーの各フラット ファイルに 1 つずつ接続するには、Foreach ループ コンテナーとフラット ファイル接続マネージャーをそれぞれ次のように構成します。  
  
-   **Foreach ループ コンテナー:** このコンテナーの列挙値をユーザー定義のパッケージ変数にマップします。 ForEach ループ コンテナーでは、この変数を使用して、フラット ファイル接続マネージャーの **ConnectionString** プロパティを動的に変更しながら、フォルダー内の各フラット ファイルに順番に接続します。  
  
-   **フラット ファイル接続マネージャー:** ユーザー定義変数を使用して、レッスン 1 で作成した接続マネージャーの **ConnectionString** プロパティに値を設定します。  
  
このタスクの手順では、ForEach ループ コンテナーを作成し、ユーザー定義パッケージ変数を使用するように変更する方法、およびデータ フロー タスクをこのループに追加する方法を説明します。 次のタスクでは、ユーザー定義変数を使用するようにフラット ファイル接続マネージャーを変更します。  
  
上記のように変更した後でこのパッケージを実行すると、Foreach ループ コンテナーによって、Sample Data フォルダー内のすべてのファイルが反復的に処理されます。 条件と一致するファイルが検出されるたびに、新しい変数にそのファイルの名前が取り込まれ、Sample Currency Data フラット ファイル接続マネージャーの **ConnectionString** プロパティにマップされます。さらに、そのファイルに対してデータ フローが実行されます。 このようにして、Foreach ループの反復処理が実行されるたびに、データ フロー タスクではそれぞれ異なるフラット ファイルが使用されます。  
  
> [!NOTE]  
> [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では制御フローとデータ フローが分離されているので、制御フローにループを追加した場合でも、データ フローを修正する必要はありません。 したがって、レッスン 1 のデータ フローを変更する必要はありません。  
  
## <a name="add-a-foreach-loop-container"></a>ForEach ループ コンテナーを追加する  
  
1.  **SQL Server Data Tools** で **[制御フロー]** タブを選択します。  
  
2.  **SSIS ツールボックス**で **[コンテナー]** を展開し、 **[ForEach ループ コンテナー]** を **[制御フロー]** タブのデザイン画面にドラッグします。  
  
3.  新しい **ForEach ループ コンテナー**を右クリックし、 **[編集]** を選択します。  
  
4.  **[Foreach ループ エディター]** ダイアログの **[全般]** ページで、 **[名前]** に「**Foreach File in Folder**」と入力します。 **[OK]** を選択します。  
  
5.  Foreach ループ コンテナーを右クリックして **[プロパティ]** を選択し、 **[プロパティ]** ウィンドウで **LocaleID** プロパティが **[英語 (米国)]** に設定されていることを確認します。  
  
## <a name="configure-the-enumerator-for-the-foreach-loop-container"></a>ForEach ループ コンテナーの列挙子を構成する  
  
1.  **Foreach File in Folder** をダブルクリックして、 **[Foreach ループ エディター]** をもう一度開きます。  
  
2.  **[コレクション]** を選択します。  
  
3.  **[コレクション]** ページで、 **[Foreach File 列挙子]** を選択します。  
  
4.  **[列挙子の構成]** で、 **[参照]** を選択します。  
  
5.  **[フォルダーの参照]** ダイアログ ボックスで、サンプル データに含まれる Currency_*.txt ファイルが保存されている、コンピューター上のフォルダーに移動します。

6.  **[ファイル]** ボックスに「**Currency_\*.txt**」と入力します。  
  
## <a name="map-the-enumerator-to-a-user-defined-variable"></a>ユーザー定義の変数に列挙子をマップする  
  
1.  **[変数のマッピング]** を選択します。  
  
2.  **[変数のマッピング]** ページで、 **[変数]** 列の空いているセルをクリックし、 **[\<新しい変数...>]** を選択します。  
  
3.  **[変数の追加]** ダイアログ ボックスで、 **[名前]** ボックスに「**varFileName**」と入力します。  
  
    > [!NOTE]  
    > 変数名の大文字と小文字は区別されます。  
  
4.  **[OK]** を選択します。  
  
5.  再び **[OK]** を選択し、 **[Foreach ループ エディター]** ダイアログを閉じます。  
  
## <a name="add-the-data-flow-task-to-the-loop"></a>データ フロー タスクをループに追加する  
  
-   **Extract Sample Currency Data** データ フロー タスクを、**Foreach File in Folder** Foreach ループ コンテナーにドラッグします。  
  
## <a name="go-to-next-task"></a>次のタスクに進む  
[ステップ 3:フラット ファイル接続マネージャーの変更](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
## <a name="see-also"></a>参照  
[Foreach ループ コンテナーを構成する](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
  
