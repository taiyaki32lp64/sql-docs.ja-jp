---
title: 'レッスン 3: dta コマンドプロンプトユーティリティの使用 |Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 04179ee339f41dde1b9e90d7abc30a00e492f3cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034717"
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>レッスン 3 : dta コマンド プロンプト ユーティリティの使用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**dta** コマンド プロンプト ユーティリティは、データベース エンジン チューニング アドバイザーの機能以外にも機能があります。  
  
データベース エンジン チューニング アドバイザーの XML スキーマを使用すれば、使い慣れた XML ツールで、このユーティリティへの入力ファイルを作成できます。 このスキーマは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時にインストールされ、C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd に格納されます。  
  
データベース エンジン チューニング アドバイザーの XML スキーマは、 [Microsoft Web サイト](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)から入手することもできます。  
  
この XML スキーマにより、チューニング オプションをより柔軟に設定することができます。 たとえば、"what-if" 分析を実行できます。 "what-if" 分析とは、チューニングするデータベースに対して実在の物理設計構造と仮想の物理設計構造のセットを指定し、それをデータベース エンジン チューニング アドバイザーで分析する手法です。これにより、仮想的な物理設計がクエリ処理のパフォーマンスを向上させるかどうかを判断できます。 このタイプの分析には、実際に実装しなくても新しい構成を評価できるという利点があります。 仮想的な物理構造により十分にパフォーマンスが向上しなくとも、十分な結果が得られる構成になるまで再び構造を変えて分析するのは容易です。  
  
また、データベース エンジン チューニング アドバイザーの XML スキーマと **dta** コマンド プロンプト ユーティリティを使用すると、データベース エンジン チューニング アドバイザーの機能をスクリプトに組み込み、そのスクリプトを他のデータベース設計ツールで使用することもできます。  
  
データベース エンジン チューニング アドバイザーの XML 入力機能の使用方法は、このレッスンでは扱いません。  
  
ここでは、 **dta** ユーティリティを起動してヘルプを表示した後、同ユーティリティを使用してコマンド プロンプトからワークロードをチューニングします。 このユーティリティは、データベース エンジン チューニング アドバイザーのグラフィカル ユーザー インターフェイス (GUI) の実習「[ワークロードのチューニング](lesson-2-using-database-engine-tuning-advisor.md#tuning-a-workload)」で作成したワークロード MyScript.sql を使用します。  
  
このチュートリアルでは、AdventureWorks2017 サンプルデータベースを使用します。 セキュリティ上の理由から、既定ではサンプル データベースがインストールされません。 サンプル データベースをインストールするには、「 [SQL Server のサンプルとサンプル データベースのインストール](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)」を参照してください。  
  
この後の実習では、コマンド プロンプトを開き、 **dta** コマンド プロンプト ユーティリティを起動して、構文ヘルプを表示します。さらに、「 [ワークロードのチューニング](../../tools/dta/lesson-1-1-tuning-a-workload.md)」で作成した簡単なワークロード MyScript.sql をチューニングします。  

## <a name="prerequisites"></a>Prerequisites 

このチュートリアルを実行するには、SQL Server Management Studio、SQL Server を実行しているサーバーへのアクセス、および AdventureWorks データベースが必要です。

- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールします。
- [AdventureWorks2017 サンプル データベース](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)をダウンロードします。


SSMS でデータベースを復元する手順については、[データベースの復元](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017)に関するページをご覧ください。

  >[!NOTE]
  > このチュートリアルは、SQL Server Management Studio と基本的なデータベース管理タスクの使用に慣れているユーザーを対象としています。 

## <a name="access-dta-command-prompt-utility-help-menu"></a>DTA コマンドプロンプトユーティリティの [ヘルプ] メニューにアクセスする
  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[アクセサリ]** の順にポイントして、 **[コマンド プロンプト]** をクリックします。  
  
2.  コマンド プロンプトで以下を入力し、Enter キーを押します。  
  
    ```  
    dta -? | more  
    ```  
  
    このコマンドの `| more` の部分は省略可能です。 これを指定した場合は、ユーティリティの構文ヘルプが 1 画面ずつ表示されます。 ヘルプを 1 行ずつ表示するには Enter キーを押し、1 ページずつ表示するにはスペース キーを押します。  

  ![DTA cmd utility で help を使用する](media/dta-tutorials/dta-cmd-help.png)

## <a name="tune-simple-workload-using-the-dta-command-prompt-utility"></a>DTA コマンドプロンプトユーティリティを使用して簡単なワークロードをチューニングする  


  
1.  コマンド プロンプトで、MyScript.sql ファイルが保存されているディレクトリに移動します。  
  
2.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押します (コマンドの解釈時には大文字と小文字が区別される点に注意してください)。コマンドが実行され、チューニング セッションが開始されます。  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
    ここで、 `-S` には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースがインストールされているサーバーおよび [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] インスタンスの名前を指定します。 設定 `-E` は、Windows ドメイン アカウントで接続している場合に、適切なインスタンスへの信頼できる接続を使用することを指定します。 設定 `-D` にはチューニングするデータベース名、 `-if` にはワークロード ファイル名、 `-s` にはセッション名を指定します。 `-of` には [!INCLUDE[tsql](../../includes/tsql-md.md)] の推奨設定スクリプトを書き込むファイルを指定し、 `-ox` には XML 形式で推奨設定を書き込むファイルを指定します。 最後の 3 つのスイッチは次のチューニング オプションを指定しています。 `-fa IDX_IV` は、インデックスとインデックス付きビューの追加のみを考慮するように指定します (クラスター化インデックス、非クラスター化インデックスが共に考慮されます)。 `-fp NONE` は、分析時にパーティション分割ストラテジを考慮しないように指定します。 `-fk NONE` は、データベース エンジン チューニング アドバイザーが推奨設定を作成する際に、データベースの既存の物理設計構造を保持しないように指定しています。  

  ![DTA での CMD の使用](media/dta-tutorials/dta-cmd.png)
  
3.  データベース エンジン チューニング アドバイザーによるワークロードのチューニングが完了すると、チューニング セッションが正常に完了したことを知らせるメッセージが表示されます。 チューニング結果を表示するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して MySession2OutputScript.sql および MySession2Output.xml を開きます。 また、データベース エンジン チューニング アドバイザーの GUI でチューニング セッション MySession2 を開き、その推奨設定とレポートを表示する方法もあります。これは、「 [チューニング推奨設定の表示](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md) 」および「 [チューニング レポートの表示](../../tools/dta/lesson-1-3-viewing-tuning-reports.md)」で行った操作と同様です。  
  
 
## <a name="after-you-finish-this-tutorial"></a>このチュートリアルが終了したら  
このチュートリアルのレッスンが終了したら、次のトピックを参照し、データベース エンジン チューニング アドバイザーの詳細を学習してください。  
  
-   このツールを使用した作業の実行方法の説明については、「[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) 」を参照してください。 
-   コマンド プロンプト ユーティリティおよびユーティリティの動作の制御に使用できるオプションの XML ファイルに関するリファレンス情報については、「[dta Utility](../../tools/dta/dta-utility.md) 」を参照してください。  
  
チュートリアルの開始に戻るには、「 [チュートリアル:データベース エンジン チューニング アドバイザー](../../tools/dta/tutorial-database-engine-tuning-advisor.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[データベース エンジンのチュートリアル](../../relational-databases/database-engine-tutorials.md)  
    
