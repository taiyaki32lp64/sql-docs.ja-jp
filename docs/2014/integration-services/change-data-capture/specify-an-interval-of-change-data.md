---
title: 変更データの間隔を指定する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],specifying interval
ms.assetid: 17899078-8ba3-4f40-8769-e9837dc3ec60
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2c5509699945db857bd0b763192c7aea21ac90da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771220"
---
# <a name="specify-an-interval-of-change-data"></a>変更データの間隔を指定する
  変更データの増分読み込みを実行する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの制御フローにおいて、最初のタスクは、変更間隔のエンドポイントを計算することです。 このエンドポイントは `datetime` 値で、パッケージで後から使用するためにパッケージ変数に格納されます。  
  
> [!NOTE]  
>  制御フローをデザインするプロセス全体の説明については、「[変更データ キャプチャ &#40;SSIS&#41;](change-data-capture-ssis.md)」を参照してください。  
  
## <a name="set-up-package-variables-for-the-endpoints"></a>エンドポイントのパッケージ変数の設定  
 エンドポイントを計算するように SQL 実行タスクを構成する前に、エンドポイントを格納するパッケージ変数を定義する必要があります。  
  
#### <a name="to-set-up-package-variables"></a>パッケージ変数を設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、新しい [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  **[変数]** ウィンドウで、次の変数を作成します。  
  
    1.  間隔の開始時点を格納する `datetime` データ型の変数を作成します。  
  
         この例では、ExtractStartTime という名前の変数を使用します。  
  
    2.  間隔の終了時点を格納する `datetime` データ型の別の変数を作成します。  
  
         この例では、ExtractEndTime という名前の変数を使用します。  
  
 複数の子パッケージを実行するマスター パッケージのエンドポイントを計算する場合は、親パッケージ変数の構成を使用してその変数の値を各子パッケージに渡すことができます。 詳細については、「 [パッケージ実行タスク](../control-flow/execute-package-task.md) 」および「 [子パッケージでの変数およびパラメーターの値の使用](../use-the-values-of-variables-and-parameters-in-a-child-package.md)」を参照してください。  
  
## <a name="calculate-a-starting-point-and-an-ending-point-for-change-data"></a>変更データの開始時点と終了時点の計算  
 間隔のエンドポイントのパッケージ変数を設定したら、そのエンドポイントの実際の値を計算し、対応するパッケージ変数にマップできるようになります。 このエンドポイントは `datetime` 値なので、`datetime` 値を計算または操作できる関数を使用する必要があります。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 式言語と Transact-SQL の両方に、`datetime` 値を操作する関数が用意されています。  
  
 `datetime` 値を操作する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 式言語の関数  
 -   [DATEADD (SSIS 式)](../expressions/dateadd-ssis-expression.md)  
  
-   [DATEDIFF (SSIS 式)](../expressions/datediff-ssis-expression.md)  
  
-   [DATEPART (SSIS 式)](../expressions/datepart-ssis-expression.md)  
  
-   [DAY (SSIS 式)](../expressions/day-ssis-expression.md)  
  
-   [GETDATE (SSIS 式)](../expressions/getdate-ssis-expression.md)  
  
-   [GETUTCDATE (SSIS 式)](../expressions/getutcdate-ssis-expression.md)  
  
-   [MONTH (SSIS 式)](../expressions/month-ssis-expression.md)  
  
-   [YEAR (SSIS 式)](../expressions/year-ssis-expression.md)  
  
 `datetime` 値を操作する Transact-SQL の関数  
 [日付と時刻のデータ型および関数 (Transact-SQL)](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)。  
  
 これらの `datetime` 関数のいずれかを使用してエンドポイントを計算する前に、間隔が一定で定期的かどうかを判断する必要があります。 通常、ソース テーブルで行われた変更は、定期的に変換先テーブルに適用します。 たとえば、このような変更は、1 時間ごと、毎日、または毎週適用します。  
  
 変更間隔が一定かランダムかを把握したら、エンドポイントを計算できます。  
  
-   **開始日時の計算**。 前の読み込みの終了日時を現在の開始日時として使用します。 増分読み込みの間隔が一定である場合は、Transact-SQL または [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 式言語の `datetime` 関数を使用してこの値を計算できます。 一定でない場合は、実行のたびにエンドポイントを保存し、SQL 実行タスクまたはスクリプト タスクを使用して前のエンドポイントを読み込むことが必要になる場合があります。  
  
-   **終了日時の計算**。 増分読み込みの間隔が一定である場合は、現在の終了日時を開始日時からのオフセットとして計算します。 使用して、この値を計算する、もう一度、`datetime`または TRANSACT-SQL の関数、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]式言語です。  
  
 次の手順では、変更間隔が一定で、増分読み込みパッケージが例外なく毎日実行されることを前提としています。 それ以外の場合、対象外の間隔の変更データは失われます。 間隔の開始時点は一昨日の午前 0 時 (24 ～ 48 時間前) です。 間隔の終了時点は昨日の午前 0 時 (0 ～ 24 時間前の昨晩) です。  
  
#### <a name="to-calculate-the-starting-point-and-ending-point-for-the-capture-interval"></a>キャプチャ間隔の開始時点と終了時点を計算するには  
  
1.  **デザイナーの** [制御フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブで、SQL 実行タスクをパッケージに追加します。  
  
2.  **[SQL 実行タスク エディター]** を開いて、エディターの **[全般]** ページで次のオプションを選択します。  
  
    1.  **[ResultSet]** で **[単一行]** を選択します。  
  
    2.  ソース データベースへの有効な接続を構成します。  
  
    3.  **[SQLSourceType]** で **[直接入力]** を選択します。  
  
    4.  **[SQLStatement]** に、次の SQL ステートメントを入力します。  
  
        ```  
        SELECT DATEADD(dd,0, DATEDIFF(dd,0,GETDATE()-1)) AS ExtractStartTime,  
          DATEADD(dd,0, DATEDIFF(dd,0,GETDATE())) AS ExtractEndTime  
  
        ```  
  
3.  **[SQL 実行タスク エディター]** の **[結果セット]** ページで、ExtractStartTime の結果を ExtractStartTime パッケージ変数に、ExtractEndTime の結果を ExtractEndTime パッケージ変数にマップします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変数の値を設定する式を使用する場合は、変数の値にアクセスするたびに式が評価されます。  
  
## <a name="next-step"></a>次の手順  
 変更の範囲の開始時点と終了時点を計算したら、次の手順で、変更データが準備できているかどうかを判断します。  
  
 **次のトピック:** [変更データの準備ができているかどうかを判断する](determine-whether-the-change-data-is-ready.md)  
  
## <a name="see-also"></a>参照  
 [パッケージで変数を使用する](../use-variables-in-packages.md)   
 [Integration Services (SSIS) 式](../expressions/integration-services-ssis-expressions.md)   
 [SQL 実行タスク](../control-flow/execute-sql-task.md)   
 [スクリプト タスク](../control-flow/script-task.md)  
  
  
