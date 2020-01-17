---
title: '手順 2: Foreach ループ コンテナーの追加と構成 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 07c5118c654faccea2d9bab01040ce17b1d5699a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232467"
---
# <a name="step-2-adding-and-configuring-the-foreach-loop-container"></a>手順 2: Foreach ループ コンテナーの追加と構成
  この実習では、フラット ファイルのフォルダー全体にループ機能を付加し、レッスン 1 で使用したデータ フロー変換と同じ変換を各フラット ファイルに適用します。 そのためには、Foreach ループ コンテナーを制御フローに追加して、構成します。  
  
 Foreach ループ コンテナーを追加したら、フォルダー内の各フラット ファイルに接続できるようにする必要があります。 フォルダー内のファイルはすべて同じ形式なので、Foreach ループ コンテナーは、どのファイルに接続する場合でも同じフラット ファイル接続マネージャーを使用できます。 このループ コンテナーが使用するフラット ファイル接続マネージャーは、レッスン 1 で作成したフラット ファイル接続マネージャーと同じものです。  
  
 レッスン 1 で作成したフラット ファイル接続マネージャーは、現在、1 つのフラット ファイルにのみ接続しています。 フォルダーの各フラット ファイルに 1 つずつ接続するには、Foreach ループ コンテナーとフラット ファイル接続マネージャーをそれぞれ次のように構成します。  
  
-   **Foreach ループコンテナー:** コンテナーの列挙値をユーザー定義のパッケージ変数にマップします。 ForEach ループ コンテナーは、このユーザー定義の変数を使用して、フラット ファイル接続マネージャーの `ConnectionString` プロパティを動的に変更しながら、フォルダー内の各フラット ファイルへ順番に接続します。  
  
-   **フラットファイル接続マネージャー:** レッスン1で作成した接続マネージャーを変更するには、ユーザー定義変数を使用して接続マネージャーの`ConnectionString`プロパティを設定します。  
  
 この実習の手順では、ForEach ループ コンテナーを作成し、ユーザー定義パッケージ変数を使用するように変更する方法、およびデータ フロー タスクをこのループに追加する方法を説明します。 次の実習では、ユーザー定義変数を使用するようにフラット ファイル接続マネージャーを変更します。  
  
 上記のように変更した後でこのパッケージを実行すると、Foreach ループ コンテナーによって、Sample Data フォルダー内のすべてのファイルが反復的に処理されます。 条件と一致するファイルが検出されるたびに、ユーザー定義の変数にそのファイルの名前が取り込まれ、Sample Currency Data フラット ファイル接続マネージャーの `ConnectionString` プロパティにマップされます。さらに、そのファイルに対してデータ フローが実行されます。 つまり、Foreach ループの反復処理が実行されるたびに、データ フロー タスクではそれぞれ異なるフラット ファイルが使用されることになります。  
  
> [!NOTE]  
>  
  [!INCLUDE[msCoName](../includes/msconame-md.md)]
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では制御フローとデータ フローが分離されているので、制御フローにループを追加した場合でも、データ フローを修正する必要はありません。 したがって、レッスン 1 で作成したデータ フローは変更する必要がありません。  
  
### <a name="to-add-a-foreach-loop-container"></a>ForEach ループ コンテナーを追加するには  
  
1.  
  **SQL Server Data Tools**で **[制御フロー]** タブをクリックします。  
  
2.  
  **SSIS ツールボックス**で **[コンテナー]** を展開し、 **[ForEach ループ コンテナー]** を **[制御フロー]** タブのデザイン画面にドラッグします。  
  
3.  新しく追加した **[ForEach ループ コンテナー]** を右クリックし、 **[編集]** をクリックします。  
  
4.  [ **Foreach ループエディター** ] ダイアログボックスの **[全般**] ページで、[**名前**] `Foreach File in Folder`に「」と入力します。 [**OK**] をクリックすると、  
  
5.  [Foreach ループコンテナー] を右クリックし、[**プロパティ**] をクリックします。プロパティウィンドウ`LocaleID`で、プロパティが**英語 (米国)** に設定されていることを確認します。  
  
### <a name="to-configure-the-enumerator-for-the-foreach-loop-container"></a>ForEach ループ コンテナーの列挙子を構成するには  
  
1.  
  Foreach File in Folder をダブルクリックして、**[Foreach ループ エディター]** をもう一度開きます。  
  
2.  
  **[コレクション]** をクリックします。  
  
3.  
  **[コレクション]** ページで、 **[Foreach File 列挙子]** を選択します。  
  
4.  
  **[列挙子の構成]** で、 **[参照]** をクリックします。  
  
5.  
  **[フォルダーの参照]** ダイアログ ボックスで、Currency_*.txt ファイルが保存されている、コンピューター上のフォルダーに移動します。  
  
     このサンプル データは、 [!INCLUDE[ssIS](../includes/ssis-md.md)] のレッスン パッケージに含まれています。 サンプル データとレッスン パッケージをダウンロードするには、次の手順を実行します。  
  
    1.  「 [Integration Services 製品サンプル](https://go.microsoft.com/fwlink/?LinkId=275027)」に移動します。  
  
    2.  [ **ダウンロード** ] タブをクリックします。  
  
    3.  ハイパーリンク "https://msftisprodsamples.codeplex.com/downloads/get/578097" SQL2012 をクリックします。Integration_Services. Create_Simple_ETL_Tutorial .zip ファイル。  
  
6.  
  **[ファイル]** ボックスに「**Currency_\*.txt**」と入力します。  
  
### <a name="to-map-the-enumerator-to-a-user-defined-variable"></a>ユーザー定義の変数に列挙子をマップするには  
  
1.  
  **[変数のマッピング]** をクリックします。  
  
2.  [**変数のマッピング**] ページの [**変数**] 列で、空のセルをクリックし、[ ** \<新しい変数... >**] をクリックします。  
  
3.  [**変数の追加**] ダイアログボックスで、[**名前**] に「」と入力`varFileName`します。  
  
    > [!IMPORTANT]  
    >  変数名では大文字と小文字が区別されます。  
  
4.  [**OK**] をクリックすると、  
  
5.  再び **[OK]** をクリックし、 **[Foreach ループ エディター]** ダイアログ ボックスを閉じます。  
  
### <a name="to-add-the-data-flow-task-to-the-loop"></a>データ フロー タスクをループに追加するには  
  
-   [ **Extract Sample Currency data** ] データフロータスクを、名前を変更`Foreach File in Folder`した Foreach ループコンテナーにドラッグします。  
  
## <a name="next-lesson-task"></a>次のレッスンの作業  
 [手順 3: フラットファイル接続マネージャーの変更](lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
## <a name="see-also"></a>参照  
 [Foreach ループコンテナーの構成](control-flow/foreach-loop-container.md)   
 [パッケージで変数を使用する](use-variables-in-packages.md)  
  
