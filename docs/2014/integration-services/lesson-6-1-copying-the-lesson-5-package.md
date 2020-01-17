---
title: 手順 1:レッスン 5 のパッケージのコピー |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ede34999b9ca7a18a2bb5ec997c4a93735b82be2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62890758"
---
# <a name="step-1-copying-the-lesson-5-package"></a>手順 1:レッスン 5 のパッケージのコピー
  ここでは、レッスン 5 で作成した Lesson 5.dtsx パッケージのコピーを作成します。 または、チュートリアルに含まれている、レッスン 5 を完了した状態のパッケージをプロジェクトに追加した後、コピーすることもできます。 レッスン 6 の実習では、このパッケージの新しいコピーを使用します。  
  
### <a name="to-copy-the-lesson-5-package"></a>レッスン 5 のパッケージをコピーするには  
  
1.  SQL Server Data Tools がまだ開いていない場合は、[スタート] ボタンをクリックし、[すべてのプログラム]、[Microsoft SQL Server 2012] の順にポイントして、[SQL Server Data Tools] をクリックします。  
  
2.  [ファイル] メニューの [開く] をクリックし、[プロジェクト/ソリューション] をクリックします。次に、[SSIS Tutorial] フォルダーをクリックして [開く] をクリックした後、SSIS Tutorial.sln をダブルクリックします。  
  
3.  ソリューション エクスプローラーで、Lesson 5.dtsx を右クリックし、[コピー] をクリックします。  
  
4.  ソリューション エクスプローラーで [SSIS パッケージ] を右クリックし、[貼り付け] をクリックします。  
  
     コピーしたパッケージの既定の名前は、Lesson 6.dtsx です。  
  
5.  ソリューション エクスプローラーで Lesson 6.dtsx をダブルクリックして、このパッケージを開きます。  
  
6.  [制御フロー] タブの背景上で任意の場所を右クリックし、[プロパティ] をクリックします。  
  
7.  [プロパティ] ウィンドウで、[Name] プロパティを「Lesson 6」に変更します。  
  
8.  ID プロパティのボックスをクリックし、ドロップダウン矢印をクリックして、順にクリックします\<Generate New ID >。  
  
### <a name="to-add-the-completed-lesson-5-package"></a>レッスン 5 を完了した状態のパッケージを追加するには  
  
1.  SQL Server Data Tools を開き、SSIS Tutorial プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで [SSIS パッケージ] を右クリックし、[既存のパッケージを追加] をクリックします。  
  
3.  [既存のパッケージのコピーを追加] ダイアログ ボックスの [パッケージの場所] で、[ファイル システム] をクリックします。  
  
4.  参照ボタン ([...]) をクリックし、コンピューター上の Lesson 5.dtsx に移動して、 **[開く]** をクリックします。  
  
     このチュートリアルのレッスン パッケージをすべてダウンロードするには、次の手順を実行します。  
  
    1.  「[Integration Services 製品サンプル](https://go.microsoft.com/fwlink/?LinkId=275027)」に移動します。  
  
    2.  **[ダウンロード]** タブをクリックします。  
  
    3.  SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip ファイルをクリックします。  
  
5.  前の手順の手順 3. ～ 8. の説明に従って、レッスン 5 パッケージをコピーして貼り付けます。  
  
     レッスン 5 パッケージをコピーした後で、ソリューション内に前のレッスンで使用したパッケージが現在存在している場合は、レッスン 1 ～ 5 の各パッケージを右クリックし、[プロジェクトから除外] をクリックします。 作業完了後は、ソリューション内にの Lesson 6.dtsx のみが存在しています。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [手順 2:プロジェクトをプロジェクト配置モデルに変換します。](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
  
