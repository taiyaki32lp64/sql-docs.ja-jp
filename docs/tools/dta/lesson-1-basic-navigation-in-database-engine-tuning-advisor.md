---
title: 'レッスン 1: データベース エンジン チューニング アドバイザーでの基本操作 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
ms.assetid: ad49b2e0-a5e3-49d2-80fd-9f4eaa3652cb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 39183d699bfa27430a35012d353b8f3bc70d6be0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034776"
---
# <a name="lesson-1-basic-navigation-in-database-engine-tuning-advisor"></a>レッスン 1: データベース エンジン チューニング アドバイザーでの基本操作
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
データベース エンジン チューニング アドバイザーでは、グラフィカル ユーザー インターフェイス (GUI) を使用して、チューニング セッションやチューニング推奨設定レポートを表示できます。 このレッスンでは、このツールの起動方法および操作画面の構成方法を説明します。 このレッスンを終了すると、ツールの起動と画面の構成を複数の方法で行い、日常的に実行するチューニング タスクに活用できるようになります。  

## <a name="prerequisites"></a>Prerequisites 

このチュートリアルを実行するには、SQL Server Management Studio、SQL Server を実行しているサーバーへのアクセス、および AdventureWorks データベースが必要です。

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールします。
- [AdventureWorks2017 サンプル データベース](https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017)をダウンロードします。


SSMS でデータベースを復元する手順については、[データベースの復元](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017)に関するページをご覧ください。

  >[!NOTE]
  > このチュートリアルは、SQL Server Management Studio と基本的なデータベース管理タスクの使用に慣れているユーザーを対象としています。 
  

## <a name="launch-database-tuning-advisor"></a>データベース チューニング アドバイザーを起動する 
まず、データベース エンジン チューニング アドバイザー (DTA) のグラフィカル ユーザー インターフェイス (GUI) を開きます。 初回起動時には、 **sysadmin** 固定サーバー ロールのメンバーがデータベース エンジン チューニング アドバイザーを起動し、アプリケーションを初期化する必要があります。 初期化が完了すると、 **db_owner** 固定データベース ロールのメンバーがデータベース エンジン チューニング アドバイザーを使用し、所有するデータベースをチューニングできるようになります。 データベース エンジン チューニング アドバイザーの初期化の詳細については、「 [データベース エンジン チューニング アドバイザーの起動および使用](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)」を参照してください。  
  
1. SQL Server Management Studio (SSMS) を起動します。 Windows の [**スタート] メニュー**の **[すべてのプログラム]** をポイントし、 **SQL Server Management Studio**を見つけます。 
2. SSMS が開いたら、 **[ツール]** メニューを選択し、 **[データベースチューニングアドバイザー]** を選択します。 

  ![SSMS から DTA を起動する](media/dta-tutorials/launch-dta.png)

3. データベースチューニングアドバイザーが起動し、 **[サーバーへの接続]** ダイアログボックスが開きます。 既定の設定を確認し、 **[接続]** を選択して SQL Server に接続します。  
  
既定では、次の図に示す構成でデータベース エンジン チューニング アドバイザーが開きます。  
  
![データベース エンジン チューニング アドバイザーの既定のウィンドウ](media/dta-tutorials/dta-default-gui.png)
  
> [!NOTE]  
> **[セッションモニター]** タブには、セッション名が表示されます。これは、接続されているユーザーと現在のデータの名前です。 
  
データベース エンジン チューニング アドバイザーの GUI を初めて開くと、2 つのメイン ペインが表示されます。  
  
-   左側のセッション モニターには、この [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで実行されたすべてのチューニング セッションが表示されます。 データベース エンジン チューニング アドバイザーを開くと、セッション モニターの最上部に新しいセッションが表示されます。 隣のペインで、このセッションに名前を付けることができます。 初期状態では既定のセッションのみが表示されます。 このセッションは、データベース エンジン チューニング アドバイザーが自動的に作成する既定のセッションです。 データベースのチューニングが完了すると、接続している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで実行されたすべてのチューニング セッションが、新しいセッションの下に一覧表示されます。 セッション名を変更する、セッションを閉じる、削除する、またはクローンを作成するときは、チューニング セッションを右クリックします。 リスト内で右クリックすると、名前順、状態順、または作成時間順にセッションを並べ替えることができます。新しいセッションも作成できます。 このペインの下部には、選択したチューニング セッションの詳細が表示されます。 **[項目別]** ボタンをクリックすると、詳細情報がカテゴリ別に分類され、表示されます。 **[アルファベット順]** ボタンをクリックすると、詳細情報がアルファベット順に表示されます。 このペインの右側の境界を左方向にドラッグすることで、セッション モニターを非表示にすることもできます。 再度表示するには、ペインの境界を右方向にドラッグします。 セッション モニターは以前のチューニング セッションを表示できるほか、似ている定義を使用して新しいセッションを作成するために使用できます。 また、セッション モニターを使用してチューニング推奨設定を評価することもできます。 詳細については、「 [データベース エンジン チューニング アドバイザーからの出力の表示および操作](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)」を参照してください。 このチュートリアルに戻るには、ブラウザーの **[戻る]** ボタンを使用します。  
  
-   右側のペインには、 **[全般]** タブと **[チューニング オプション]** タブがあります。 これらのタブでデータベース エンジン チューニング セッションを定義します。 **[全般]** タブでは、チューニング セッション名の入力、使用するワークロード ファイルまたはテーブルの指定、およびこのセッションでチューニングするデータベースとテーブルの選択を行います。 ワークロードとは、チューニングするデータベースに対して実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのセットです。 データベースをチューニングする際には、トレース ファイル、トレース テーブル、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト、または XML ファイルがワークロード入力として使用されます。 **[チューニング オプション]** タブでは、物理データベース設計構造 (インデックスまたはインデックス付きビュー) を選択し、その分析時に適用するパーティション分割方法を指定できます。 またこのタブでは、データベース エンジン チューニング アドバイザーがワークロードのチューニングにあてる最大時間を指定することもできます。 既定のワークロード チューニング時間は 1 時間です。  
  
> [!NOTE]
> [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ エディターから [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] スクリプトをインポートする場合、XML ファイルからスクリプトを取り込むことができます。 詳細については、「 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] データベース エンジン チューニング アドバイザーからの出力の表示および操作 [」の](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)クエリ エディターからデータベース エンジン チューニング アドバイザーを起動する方法に関するセクションを参照してください。  
  
## <a name="configure-tool-options-and-layout"></a>ツールのオプションとレイアウトを構成する 

1.  **[ツール]** メニューの **[オプション]** をクリックします。  

   ![DTA オプション](media/dta-tutorials/dta-settings.png) 
  
2.  **[オプション]** ダイアログ ボックスが開き、次のオプションが表示されます。  
  
    -   **[スタートアップ時]** ボックスの一覧には、データベース エンジン チューニング アドバイザーの起動時に表示されるアイテムが示されます。 既定では、 **[新しいセッションを表示します]** が選択されています。  
  
    -   データベースの一覧と **[全般]** タブのテーブルに表示できるフォントを確認するには、 **[フォント変更]** をクリックします。このオプションで選択したフォントは、データベース エンジン チューニング アドバイザーの推奨設定グリッドおよびチューニング実行後のレポートにも使用されます。 既定ではシステム フォントが使用されます。  
  
    -   **[最近使用した項目の一覧に表示する項目数]** には、 **1** ～ **10**の値を設定できます。 このオプションでは、 **[ファイル]** メニューの **[最新のセッション]** または **[最近使ったファイル]** をクリックしたときに表示される最大項目数を設定します。 既定では **4**に設定されています。  
  
    -   **[最後のチューニング オプションを保存する]** チェック ボックスをオンにした場合、既定では、最後のチューニング セッションで指定したチューニング オプションが次のチューニング セッションで使用されます。 データベース エンジン チューニング アドバイザーの既定のチューニング オプションを使用するには、このチェック ボックスをオフにします。 既定では、このオプションはオンになっています。  
  
    -   誤ってチューニング セッションを削除しないよう、既定では **[完全にセッションを削除する前に確認する]** がオンになっています。  
  
    -   データベース エンジン チューニング アドバイザーによるワークロードの分析が完了する前に、間違ってチューニング セッションを停止しないように、既定では **[セッションの分析を停止する前に確認する]** がオンになっています。  
  
## <a name="next-lesson"></a>次のレッスン  
[レッスン 2: データベース エンジン チューニング アドバイザーの使用](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
  
  
  
