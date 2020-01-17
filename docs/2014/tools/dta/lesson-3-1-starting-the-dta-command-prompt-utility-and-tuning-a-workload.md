---
title: dta コマンド プロンプト ユーティリティの起動とワークロードのチューニング | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: f34a5acf-1f3b-4484-a770-6470cb925ab0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf882bc731c8e435de808092e990b35ad23ce57e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110156"
---
# <a name="starting-the-dta-command-prompt-utility-and-tuning-a-workload"></a>dta コマンド プロンプト ユーティリティの起動とワークロードのチューニング
  ここでは、**dta** ユーティリティを起動してヘルプを表示した後、同ユーティリティを使用してコマンド プロンプトからワークロードをチューニングします。 このユーティリティは、データベース エンジン チューニング アドバイザーのグラフィカル ユーザー インターフェイス (GUI) の実習「 [ワークロードのチューニング](lesson-1-1-tuning-a-workload.md)」で作成したワークロード MyScript.sql を使用します。  
  
 このチュートリアルでは [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースを使用します。 セキュリティ上の理由から、既定ではサンプル データベースがインストールされません。 サンプル データベースをインストールするには、「 [SQL Server のサンプルとサンプル データベースのインストール](http://sqlserversamples.codeplex.com)」を参照してください。  
  
 この後の実習では、コマンド プロンプトを開き、 **dta** コマンド プロンプト ユーティリティを起動して、構文ヘルプを表示します。さらに、「 [ワークロードのチューニング](lesson-1-1-tuning-a-workload.md)」で作成した簡単なワークロード MyScript.sql をチューニングします。  
  
### <a name="to-start-the-dta-command-prompt-utility-and-view-help"></a>dta コマンド プロンプト ユーティリティを起動してヘルプを表示するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[アクセサリ]** の順にポイントして、 **[コマンド プロンプト]** をクリックします。  
  
2.  コマンド プロンプトで以下を入力し、Enter キーを押します。  
  
    ```  
    dta -? | more  
    ```  
  
     このコマンドの `| more` の部分は省略可能です。 これを指定した場合は、ユーティリティの構文ヘルプが 1 画面ずつ表示されます。 ヘルプを 1 行ずつ表示するには Enter キーを押し、1 ページずつ表示するにはスペース キーを押します。  
  
### <a name="to-tune-a-simple-workload-by-using-the-dta-command-prompt-utility"></a>dta コマンド プロンプト ユーティリティを使用して簡単なワークロードをチューニングするには  
  
1.  コマンド プロンプトで、MyScript.sql ファイルが保存されているディレクトリに移動します。  
  
2.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押します (コマンドの解釈時には大文字と小文字が区別される点に注意してください)。コマンドが実行され、チューニング セッションが開始されます。  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
     ここで、 `-S` には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースがインストールされているサーバーおよび [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] インスタンスの名前を指定します。 設定 `-E` は、Windows ドメイン アカウントで接続している場合に、適切なインスタンスへの信頼できる接続を使用することを指定します。 設定 `-D` にはチューニングするデータベース名、 `-if` にはワークロード ファイル名、 `-s` にはセッション名を指定します。 `-of` には [!INCLUDE[tsql](../../includes/tsql-md.md)] の推奨設定スクリプトを書き込むファイルを指定し、 `-ox` には XML 形式で推奨設定を書き込むファイルを指定します。 最後の 3 つのスイッチは次のチューニング オプションを指定しています。 `-fa IDX_IV` は、インデックスとインデックス付きビューの追加のみを考慮するように指定します (クラスター化インデックス、非クラスター化インデックスが共に考慮されます)。 `-fp NONE` は、分析時にパーティション分割ストラテジを考慮しないように指定します。 `-fk NONE` は、データベース エンジン チューニング アドバイザーが推奨設定を作成する際に、データベースの既存の物理設計構造を保持しないように指定しています。  
  
3.  データベース エンジン チューニング アドバイザーによるワークロードのチューニングが完了すると、チューニング セッションが正常に完了したことを知らせるメッセージが表示されます。 チューニング結果を表示するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して MySession2OutputScript.sql および MySession2Output.xml を開きます。 また、データベース エンジン チューニング アドバイザーの GUI でチューニング セッション MySession2 を開き、その推奨設定とレポートを表示する方法もあります。これは、「 [チューニング推奨設定の表示](lesson-1-2-viewing-tuning-recommendations.md) 」および「 [チューニング レポートの表示](lesson-1-3-viewing-tuning-reports.md)」で行った操作と同様です。  
  
## <a name="summary"></a>まとめ  
 **dta** ユーティリティを使用し、コマンド プロンプトから簡単なワークロードをチューニングしました。 このツールには、これ以外にも多数のチューニング オプションがあります。 詳細については、ヘルプ (**dta -?** ) および関連項目「 [dta ユーティリティ](dta-utility.md) 」を参照してください。  
  
## <a name="after-you-finish-this-tutorial"></a>このチュートリアルが終了したら  
 このチュートリアルのレッスンが終了したら、次のトピックを参照し、データベース エンジン チューニング アドバイザーの詳細を学習してください。  
  
-   このツールを使用した作業の実行方法の説明については、「[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) 」を参照してください。  
  
-   コマンド プロンプト ユーティリティおよびユーティリティの動作の制御に使用できるオプションの XML ファイルに関するリファレンス情報については、「[dta Utility](dta-utility.md) 」を参照してください。  
  
 チュートリアルの先頭に戻り、次を参照してください。[チュートリアル。データベース エンジン チューニング アドバイザー](tutorial-database-engine-tuning-advisor.md)します。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのチュートリアル](../../relational-databases/database-engine-tutorials.md)  
  
  
