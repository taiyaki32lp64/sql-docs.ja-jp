---
title: 手順 4:レッスン 2 のチュートリアル パッケージのテスト |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1a9b8361c83201fa2e3c6aa0c6a091e09f7c12f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767488"
---
# <a name="step-4-testing-the-lesson-2-tutorial-package"></a>手順 4:レッスン 2 のチュートリアル パッケージのテスト
  Foreach ループ コンテナーとフラット ファイル接続マネージャーを構成したので、Lesson 2 のパッケージは、Sample Data フォルダー内の 14 個のフラット ファイルに対して反復処理を実行できるようになりました。 指定した条件を満たすファイル名が見つかるたびに、Foreach ループ コンテナーは、ユーザー定義変数にそのファイル名を取り込みます。 次に、この変数に基づいて、フラット ファイル接続マネージャーの ConnectionString プロパティを更新し、新しいフラット ファイルへの接続を確立します。 さらに、新しいフラット ファイル内のデータに対して未変更のデータ フロー タスクを実行してから、フォルダー内の次のファイルに接続します。  
  
 次の手順を実行して、パッケージに追加した新しいループ機能をテストします。  
  
> [!NOTE]  
>  レッスン 1 で作成したパッケージを実行した場合、このレッスンでパッケージを実行する前に、AdventureWorksDW2012 の dbo.FactCurrency からレコードを削除する必要があります。そうしないと、主キー制約違反を示すエラーが発生してパッケージが失敗します。 [デバッグ] メニューの [デバッグの開始] をクリックして (または F5 キーを押して) パッケージを実行すると、レッスン 1 とレッスン 2 の両方が実行されるため、同じエラーが発生します。 レッスン 2 では、レッスン 1 で既に挿入されたレコードを挿入しようとします。  
  
## <a name="checking-the-package-layout"></a>パッケージ レイアウトの確認  
 パッケージをテストする前に、次の図に示すオブジェクトがレッスン 2 のパッケージの制御フローとデータ フローに含まれていることを確認します。 データ フローはレッスン 1 のデータ フローと同じである必要があります。  
  
 **制御フロー**  
  
 ![パッケージ内の制御フロー](../../2014/tutorials/media/task4lesson2control.gif "パッケージ内の制御フロー")  
  
 **データ フロー**  
  
 ![パッケージ内のデータ フロー](../../2014/tutorials/media/task9lesson1data.gif "パッケージ内のデータ フロー")  
  
### <a name="to-test-the-lesson-2-tutorial-package"></a>レッスン 2 で作成したチュートリアル パッケージをテストするには  
  
1.  **ソリューション エクスプローラー**で **Lesson 2.dtsx** を右クリックし、 **[パッケージの実行]** をクリックします。  
  
     パッケージが実行されます。 各ループのステータスは [出力] ウィンドウで確認できます。または、 **[進行状況]** タブをクリックしても確認できます。たとえば、Currency_VEB.txt から 1097 個の行がディメンション テーブルに追加されたことがわかります。  
  
2.  パッケージの実行が完了したら、 **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 5: パッケージ配置モデルのパッケージ構成の追加](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
  
## <a name="see-also"></a>参照  
 [プロジェクトとパッケージの実行](packages/run-integration-services-ssis-packages.md)  
  
  
