---
title: ワークロードのチューニング |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- workloads [SQL Server], tuning
ms.assetid: 6229bf3f-1182-4bc6-8451-cedc37f4b62e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3dd87c1e2bd08ce5bb1d05e9d51d92e3f62bcc7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110185"
---
# <a name="tuning-a-workload"></a>ワークロードのチューニング
  データベース エンジン チューニング アドバイザーでは、チューニング用に選択したデータベースおよびテーブルについて、最適なクエリ パフォーマンスが得られる物理データベース設計を見つけることができます。  
  
 このタスクでは [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースを使用します。 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。 サンプル データベースをインストールするには、「 [SQL Server のサンプルとサンプル データベースのインストール](http://sqlserversamples.codeplex.com)」を参照してください。  
  
### <a name="tune-a-workload-transact-sql-script-file"></a>ワークロード Transact-SQL スクリプト ファイルのチューニング  
  
1.  「 」の 「[SELECT の例 (Transact-SQL)](/sql/t-sql/queries/select-examples-transact-sql)」の「A. SELECT を使用して行および列を取得する」からサンプルの SELECT ステートメントをコピーし、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディターに貼り付けます。 このファイルを、探しやすいディレクトリに **MyScript.sql** という名前で保存します。  
  
2.  データベース エンジン チューニング アドバイザーを起動します。 「[データベース エンジン チューニング アドバイザーの起動](../../relational-databases/performance/database-engine-tuning-advisor.md)」を参照してください。  
  
3.  データベース エンジン チューニング アドバイザー GUI の右側ペインで、 **[セッション名]** に「 **MySession**」と入力します。  
  
4.  **[ワークロード]** で **[ファイル]** を選択し、 **[ワークロード ファイルを参照します。]** ボタンをクリックして、手順 1. で保存した **MyScript.sql** ファイルを指定します。  
  
5.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] [ワークロード分析用のデータベース] **ボックスの一覧で** を選択し、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] [チューニングするデータベースとテーブルの選択] **グリッドで** を選択します。 **[チューニング ログを保存する]** はオンのままにしておきます。 **[ワークロード分析用のデータベース]** では、データベース エンジン チューニング アドバイザーがワークロードのチューニング時に最初に接続するデータベースを指定します。 チューニングの開始後に、データベース チューニング アドバイザーは、ワークロードに含まれる `USE DATABASE` ステートメントで指定されたデータベースに接続します。  
  
6.  **[チューニング オプション]** タブをクリックします。この実習ではチューニング オプションを設定しませんが、既定のチューニング オプションをひととおり確認してください。 このタブ ページのヘルプを表示するには、F1 キーを押します。 詳細なチューニング オプションを表示するには、 **[詳細設定オプション]** をクリックします。 **[チューニング オプションの詳細設定]** ダイアログ ボックスに表示されているチューニング オプションの情報を表示するには、このダイアログ ボックスの **[ヘルプ]** をクリックします。 既定のオプションを選択したまま **[キャンセル]** をクリックし、 **[チューニング オプションの詳細設定]** ダイアログ ボックスを閉じます。  
  
7.  ツール バーの **[分析の開始]** ボタンをクリックします。 ワークロードの分析中は、 **[進行状況]** タブで実行状況を監視できます。チューニングが完了すると **[推奨設定]** タブが表示されます。  
  
     チューニング停止の日付と時刻に関してエラーが発生する場合は、 **[チューニング オプション]** タブの **[停止時刻]** の時間を確認します。 **[停止時刻]** の日付と時刻が現在の日付と時刻よりも後になっていることを確認し、必要に応じて変更します。  
  
8.  分析が完了したら、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [アクション] **メニューの** [推奨設定の保存] **をクリックし、推奨設定を** スクリプトとして保存します。 **[名前を付けて保存]** ダイアログ ボックスで推奨設定スクリプトを保存するディレクトリに移動し、ファイル名として「 **MyRecommendations**」と入力します。  
  
## <a name="summary"></a>まとめ  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで、簡単な SELECT ステートメントのワークロードをチューニングしました。 データベース エンジン チューニング アドバイザーでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のトレース ファイルとテーブルをチューニング ワークロードとして取り込むこともできます。 次の作業では、チューニングの実習で取得したチューニング推奨設定を表示し、解釈する方法について説明します。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [チューニング推奨設定の表示](lesson-1-2-viewing-tuning-recommendations.md)  
  
  
