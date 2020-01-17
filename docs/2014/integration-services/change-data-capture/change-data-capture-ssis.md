---
title: 変更データ キャプチャ (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental loads [SQL Server change data capture]
- change data capture [SQL Server], Integration Services and
ms.assetid: c4aaba1b-73e5-4187-a97b-61c10069cc5a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 391bf9204beeb6222a6e736125e5630bd5b1565e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771702"
---
# <a name="change-data-capture-ssis"></a>変更データ キャプチャ (SSIS)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、変更データ キャプチャによって、ソース テーブルからデータ マートおよびデータ ウェアハウスへの増分読み込みを効率的に実行するための効果的なソリューションが実現します。  
  
## <a name="what-is-change-data-capture"></a>変更データ キャプチャとは  
 ソース テーブルは、時間の経過と共に変化します。 このようなテーブルに基づくデータ マートまたはデータ ウェアハウスは、その変化を反映する必要があります。 ただし、ソース全体のスナップショットを定期的にコピーする処理には、膨大な時間とリソースが必要です。 timestamp 列、トリガー、複雑なクエリなどの別の方法を使用すると、多くの場合、パフォーマンスが低下して処理が複雑になります。 ここで必要となるのは、対象となるデータ表現に対して簡単に適用できるように構成された変更データの確実なストリームです。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の変更データ キャプチャはこのソリューションを提供します。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の変更データ キャプチャ機能は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のテーブルに対して適用された挿入、更新、削除の各アクティビティをキャプチャし、変更の詳細を、利用しやすいリレーショナル形式で格納します。 変更データ キャプチャで使用される変更テーブルには、追跡されたソース テーブルの列構造をミラー化する列が、行われた変更を行ごとに理解するために必要なメタデータと共に含まれています。  
  
> [!NOTE]
>  変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
## <a name="how-change-data-capture-works-in-integration-services"></a>Integration Services における変更データ キャプチャのしくみ  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベース内の変更データを簡単に取得でき、データ ウェアハウスへの増分読み込みを効率的に実行できます。 ただし、[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] を使用して変更データを読み込む前に、管理者は、変更をキャプチャするデータベースおよびテーブルで変更データ キャプチャを有効にする必要があります。 データベースで変更データ キャプチャを構成する方法の詳細については、「[変更データ キャプチャの有効化と無効化 &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)」を参照してください。  
  
 データベースで変更データ キャプチャが有効になったら、変更データの増分読み込みを実行するパッケージを作成できます。 次の図は、1 つのテーブルから増分読み込みを実行するパッケージの作成手順を示しています。  
  
 ![変更データ キャプチャ パッケージの作成手順](../media/cdc-package-creation.gif "変更データ キャプチャ パッケージの作成手順")  
  
 上の図に示したように、変更データの増分読み込みを実行するパッケージを作成するには、次の手順を実行します。  
  
 **ステップ 1: 制御フローのデザイン**  
 パッケージの制御フローでは、次のタスクを定義する必要があります。  
  
-   取得するソース データに対する変更の間隔の開始と終了の `datetime` 値を計算します。  
  
     これらの値を計算するには、`datetime` 関数を指定した SQL 実行タスクまたは [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 式を使用します。 その後、これらのエンドポイントをパッケージで後から使用するためにパッケージ変数に格納します。  
  
     **詳細:** [変更データの間隔を指定する](specify-an-interval-of-change-data.md)  
  
-   選択した間隔の変更データが準備できているかどうかを判断します。 非同期キャプチャ プロセスが、選択したエンドポイントにまだ達していない可能性があるため、この手順が必要となります。  
  
     データが準備できているかどうかを判断するには、必要に応じて、選択した間隔の変更データが準備できるまで実行を遅延させる For ループ コンテナーをまず用意します。 ループ コンテナー内で SQL 実行タスクを使用して、変更データ キャプチャによって管理される時間マッピング テーブルに対するクエリを実行します。 その後、`Thread.Sleep` メソッドを呼び出すスクリプト タスク、または `WAITFOR` ステートメントを実行する別の SQL 実行タスクを使用して、必要に応じてパッケージの実行を一時的に遅延させます。 必要に応じて、エラー状態またはタイムアウトをログに記録する別のスクリプト タスクを使用します。  
  
     **詳細:** [変更データの準備ができているかどうかを判断する](determine-whether-the-change-data-is-ready.md)  
  
-   変更データのクエリに使用するクエリ文字列を準備します。  
  
     スクリプト タスクまたは SQL 実行タスクを使用して、変更をクエリで確認するために使用する SQL ステートメントを作成します。  
  
     **詳細:** [変更データのクエリを準備する](prepare-to-query-for-the-change-data.md)  
  
 **手順 2:変更データのクエリの設定**  
 データのクエリを実行するテーブル値関数を作成します。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してクエリを作成および保存します。  
  
 **詳細:** [変更データを取得および理解する](retrieve-and-understand-the-change-data.md)  
  
 **手順 3:データ フローのデザイン**  
 パッケージのデータ フローでは、次のタスクを定義する必要があります。  
  
-   変更テーブルから変更データを取得します。  
  
     データを取得するには、変換元コンポーネントを使用して、選択した間隔内の変更のクエリを変更テーブルに対して実行します。 事前に作成しておく必要がある Transact-SQL テーブル値関数が変換元によって呼び出されます。  
  
     **詳細:** [変更データを取得および理解する](retrieve-and-understand-the-change-data.md)  
  
-   変更を処理用に挿入、更新、および削除に分割します。  
  
     変更を分割するには、条件分割変換を使用して、適切な処理のために挿入、更新、および削除を異なる出力に送信します。  
  
     **詳細:** [挿入、更新、および削除を処理する](process-inserts-updates-and-deletes.md)  
  
-   挿入、削除、および更新を変換先に適用します。  
  
     変更を変換先に適用するには、変換先コンポーネントを使用して、挿入を変換先に適用します。 また、OLE DB コマンド変換とパラメーター化された UPDATE および DELETE ステートメントを使用して、更新と削除を変換先に適用します。 更新と削除は、変換先コンポーネントを使用して一時テーブルに行を保存することによって適用することもできます。 次に、SQL 実行タスクを使用して、一時テーブルから変換先に対して一括更新および一括削除操作を実行します。  
  
     **詳細:** [変換先に変更を適用する](apply-the-changes-to-the-destination.md)  
  
### <a name="change-data-from-multiple-tables"></a>複数のテーブルの変更データ  
 上の図と手順で説明したプロセスでは、1 つのテーブルから増分読み込みを実行しています。 複数のテーブルから増分読み込みを実行する必要がある場合も、全体的に同じプロセスになります。 ただし、複数のテーブルの処理に対応できるようにパッケージのデザインを変更する必要があります。 複数のテーブルから増分読み込みを実行するパッケージの作成方法の詳細については、「 [複数のテーブルの増分読み込みを実行する](perform-an-incremental-load-of-multiple-tables.md)」を参照してください。  
  
## <a name="samples-of-change-data-capture-packages"></a>変更データ キャプチャ パッケージのサンプル  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、パッケージで変更データ キャプチャを使用する方法を紹介したサンプルが 2 つ用意されています。 詳細については、次の各トピックを参照してください。  
  
-   [Change Data Capture for Specified Interval パッケージ サンプルの Readme](https://go.microsoft.com/fwlink/?LinkId=133507)  
  
-   [Change Data Capture since Last Request パッケージ サンプルの Readme](https://go.microsoft.com/fwlink/?LinkId=133508)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [変更データの間隔を指定する](specify-an-interval-of-change-data.md)  
  
-   [変更データの準備ができているかどうかを判断する](determine-whether-the-change-data-is-ready.md)  
  
-   [変更データのクエリを準備する](prepare-to-query-for-the-change-data.md)  
  
-   [変更データを取得する関数を作成する](create-the-function-to-retrieve-the-change-data.md)  
  
-   [変更データを取得および理解する](retrieve-and-understand-the-change-data.md)  
  
-   [挿入、更新、および削除を処理する](process-inserts-updates-and-deletes.md)  
  
-   [変換先に変更を適用する](apply-the-changes-to-the-destination.md)  
  
-   [複数のテーブルの増分読み込みを実行する](perform-an-incremental-load-of-multiple-tables.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 sqlblog.com のブログ投稿「[SSIS Design Pattern - Incremental Load](https://go.microsoft.com/fwlink/?LinkId=217679)」(SSIS のデザイン パターン - 増分読み込み)  
  
  
