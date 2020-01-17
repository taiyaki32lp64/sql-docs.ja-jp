---
title: 手順 4:レッスン 2 のチュートリアル パッケージのテスト | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b17fc99cc7746739f381ba22f55a973d55497a1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283555"
---
# <a name="lesson-2-4-test-the-lesson-2-tutorial-package"></a>レッスン 2 から 4:レッスン 2 で作成したチュートリアル パッケージのテスト

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Foreach ループ コンテナーとフラット ファイル接続マネージャーを構成したので、レッスン 2 のパッケージは、Sample Data フォルダー内の 14 個のフラット ファイルに対して反復処理を実行できるようになりました。 ファイル名が指定した条件と一致するたびに、Foreach ループ コンテナーは、ユーザー定義変数にそのファイル名を取り込みます。 次に、この変数に基づいて、フラット ファイル接続マネージャーの ConnectionString プロパティが更新され、フラット ファイルへの接続が確立されます。 さらに、Foreach ループ コンテナーは、そのフラット ファイル内のデータに対して未変更のデータ フロー タスクを実行します。  
  
> [!NOTE]  
> レッスン 1 のパッケージを実行している場合、このレッスンのパッケージを実行する前に、AdventureWorksDW2012 データベースの dbo.NewFactCurrencyRate テーブルのレコードを削除する必要があります。 レッスン 2 が、レッスン 1 で既に挿入されたレコードを挿入しようとし、それによってエラーが発生します。  
  
## <a name="check-the-package-layout"></a>パッケージ レイアウトを確認する  
パッケージをテストする前に、次の図に示すオブジェクトがレッスン 2 のパッケージの制御フローとデータ フローに含まれていることを確認します。 レッスン 2 のデータ フローは、レッスン 1 と同じです。  
  
**制御フロー**  
  
![パッケージ内の制御フロー](../integration-services/media/task4lesson2control.gif "パッケージ内の制御フロー")  
  
**データ フロー**  
  
![パッケージ内のデータ フロー](../integration-services/media/task9lesson1data.gif "パッケージ内のデータ フロー")  
  
## <a name="test-the-lesson-2-tutorial-package"></a>レッスン 2 で作成したチュートリアル パッケージのテスト  
  
1.  **ソリューション エクスプローラー**で **[Lesson 2.dtsx]** を右クリックし、 **[パッケージの実行]** を選択します。  
  
    パッケージが実行されます。 各ループのステータスは **[出力]** ウィンドウで確認できます。または、 **[進行状況]** タブを選択しても確認できます。たとえば、ファイル Currency_VEB.txt から 1,097 個の行が宛先のテーブルに追加されたことがわかります。  
  
2.  パッケージの実行が完了したら、 **[デバッグ]** メニューの **[デバッグの停止]** を選択します。  
  
## <a name="go-to-next-lesson"></a>次のレッスンに進む  
[レッスン 3:SSIS でのログ記録の追加](../integration-services/lesson-3-add-logging-with-ssis.md)  
  
## <a name="see-also"></a>参照  
[プロジェクトとパッケージの実行](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

