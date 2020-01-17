---
title: R + T-SQL のチュートリアル:データの探索
description: チュートリアルでは、R 関数を使用して SQL Server データを探索および視覚化する方法を示しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 213db5ee9b88f7af34e3d000fc0f3b241d8e5791
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73725227"
---
# <a name="lesson-1-explore-and-visualize-the-data"></a>レッスン 1:データの探索および視覚化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事は、SQL Server で R を使用する方法に関する SQL 開発者向けのチュートリアルの一部です。

この手順では、サンプル データを確認し、[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) からの [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) と base R の汎用 [Hist](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist) 関数を使用して、プロットをいくつか生成します。これらの R 関数は、既に [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] に含まれています。

このレッスンの主な目的は、ストアド プロシージャの [!INCLUDE[tsql](../../includes/tsql-md.md)] から R 関数を呼び出し、結果をアプリケーション ファイル形式で保存する方法を示すことです。

+ **RxHistogram** を使用してストアド プロシージャを作成し、varbinary データとして R プロットを生成します。 **bcp** を使用して、バイナリ ストリームをイメージ ファイルにエクスポートします。
+ **Hist** を使用してストアド プロシージャを作成し、結果を JPG および PDF 出力として保存します。

> [!NOTE]
> 視覚化はデータの形状と分布を理解するための強力なツールであるため、R には、ヒストグラム、散布図、ボックス プロット、および他のデータ探索グラフを生成するための幅広い関数とパッケージが用意されています。 R は、通常、グラフィカル出力用の R デバイスを使用してイメージを作成します。これをキャプチャし、アプリケーションでレンダリングするために **varbinary** データ型として保存することができます。 また、任意のサポート ファイル形式 (.JPG、.PDF など) に画像を保存することもできます。

## <a name="review-the-data"></a>データを確認する

データ科学ソリューションの開発には、通常、集中的なデータの探索とデータの視覚化が伴います。 最初に、サンプル データを確認してください (まだ確認していない場合)。

元のパブリック データセットでは、タクシーの識別情報と乗車レコードが別々のファイルに入力されていました。 ですが、サンプル データの利用を簡単にするために、_medallion_、 _hack\_license_、_pickup\_datetime_ 列で元のデータセットを結合しました。  レコードもサンプリングされており、元のレコード数の 1% だけが取得されています。 結果的にダウンサンプリングされたデータセットは 1,703,957 行と 23 列です。

**タクシーの識別子**
  
-   _medallion_ 列はタクシーの一意の ID を表します。
  
-   _hack\_license_ 列には、タクシー運転手の運転免許証番号が含まれます (匿名にしてあります)。
  
**乗車と料金の記録**
  
-   各乗車記録には、乗車場所、降車場所、走行距離が含まれています。
  
-   各料金記録には、支払の種類、支払の合計額、チップ額など、支払情報が含まれています。
  
-   最後の 3 つの列はさまざまな機械学習タスクに利用できます。 _tip\_amount_ 列には連続する数値が含まれ、回帰分析用の **label** 列として利用できます。 _tipped_ 列には yes/no 値のみが含まれ、二項分類に利用されます。 _tip\_class_ 列には複数の**クラス ラベル**が含まれ、複数クラスの分類タスク用のラベルとして利用できます。
  
    このチュートリアルでは、二項分類タスクのみを紹介します。他の 2 つの機械学習タスク (回帰と複数クラスの分類) でもモデルの構築をお試しください。
  
-   ラベル列に使用される値はすべて _tip\_amount_ 列に基づき、次のようなビジネス ルールが適用されます。
  
    |派生列名|Rule|
    |-|-|
     |tipped|tip_amount > 0 の場合、tipped = 1、それ以外では tipped = 0|
    |tip_class|クラス 0: tip_amount = $0<br /><br />クラス 1: tip_amount > $0 および tip_amount <= $5<br /><br />クラス 2: tip_amount > $5 および tip_amount <= $10<br /><br />クラス 3: tip_amount > $10 および tip_amount <= $20<br /><br />クラス 4: tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>rxHistogram を使用してデータをプロットするストアド プロシージャを作成する

プロットを作成するには、[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) で提供されている拡張 R 関数の 1 つである [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) を使用します。 この手順では、[!INCLUDE[tsql](../../includes/tsql-md.md)] クエリのデータに基づいてヒストグラムをプロットします。 この関数は、ストアド プロシージャでラップすることができます。これには、**PlotRxHistogram** を使用します。

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、オブジェクト エクスプローラーで、**NYCTaxi_Sample** データベースを右クリックし、**[新しいクエリ]** を選択します。

2. 次のスクリプトに貼り付けて、ヒストグラムをプロットするストアド プロシージャを作成します。 この例には、**RPlotRxHistogram* という名前が付けられています。

    ```sql
    CREATE PROCEDURE [dbo].[RxPlotHistogram]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM nyctaxi_sample'  
      EXECUTE sp_execute_external_script @language = N'R',  
                                         @script = N'  
       image_file = tempfile();  
       jpeg(filename = image_file);  
       #Plot histogram  
       rxHistogram(~tipped, data=InputDataSet, col=''lightgreen'',   
       title = ''Tip Histogram'', xlab =''Tipped or not'', ylab =''Counts'');  
       dev.off();  
       OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
       ',  
       @input_data_1 = @query  
       WITH RESULT SETS ((plot varbinary(max)));  
    END
    GO
    ```

このスクリプトで理解する重要なポイントは、次のとおりです。 
  
+ 変数 `@query` によりクエリ テキスト (`'SELECT tipped FROM nyctaxi_sample'`) が定義され、スクリプト入力変数 `@input_data_1`の引数として R スクリプトに渡されます。 外部プロセスとして実行する R スクリプトの場合、スクリプトへの入力と、SQL Server で R セッションを開始する [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) システム ストアド プロシージャへの入力の間に 1 対 1 のマッピングが必要です。
  
+ R スクリプト内では、イメージを格納するための変数 (`image_file`) が定義されています。 

+ RevoScaleR ライブラリからの **rxHistogram** 関数は、プロットを生成するために呼び出されます。
  
+ このコマンドを SQL Server で外部スクリプトとして実行しているため、R デバイスは**オフ**に設定されています。 R では通常、高レベルのプロット コマンドを送るとき、R は *device* という名前のグラフィックス ウィンドウを開きます。 ファイルに書き込む場合や、出力を他の方法で処理する場合は、デバイスの電源をオフにすることができます。
  
+ R グラフィックス オブジェクトは、出力のために R data.frame にシリアル化されます。

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>ストアド プロシージャを実行し、bcp を使用してバイナリ データをイメージ ファイルにエクスポートする

ストアド プロシージャは varbinary データのストリームとして画像を返し、直接見ることはできません。 ただし、 **bcp** ユーティリティを利用すれば、varbinary データを取得し、クライアント コンピューターに画像ファイルとして保存できます。
  
1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で、次のステートメントを実行します。
  
    ```sql
    EXEC [dbo].[RxPlotHistogram]
    ```
  
    **結果**
    
    *plot* *0xFFD8FFE000104A4649...*
  
2. PowerShell コマンド プロンプトを開き、次のコマンドを実行します。引数として適切なインスタンス名、データベース名、ユーザー名、資格情報を指定します。 Windows ID を使用する場合は、**-U** や **-P** を **T**に置き換えることができます。
  
    ```powershell
    bcp "exec RxPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
    ```

    > [!NOTE]
    > bcp のコマンド スイッチでは大文字と小文字が区別されます。
  
3. 接続に成功した場合は、グラフィック ファイル形式に関する詳細情報を入力するように求められます。 

   プロンプトのたびに ENTER キーを押し、初期設定を適用します。ただし、次については変更します。
    
   + **フィールド プロットのプレフィックス長**に「0」を入力します。
  
   + 後で再利用するために出力パラメーターを保存する場合、「 **Y** 」を入力します。
  
    ```powershell
    Enter the file storage type of field plot [varbinary(max)]: 
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **結果**
    
    ```powershell
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > フォーマット情報をファイル (bcp.fmt) に保存する場合、 **bcp** ユーティリティによりフォーマット定義が生成されます。それを今後、同様のコマンドに適用できます。グラフィック ファイル フォーマットの選択を求められません。 フォーマット ファイルを使用するには、 `-f bcp.fmt` をコマンド行の終わりに追加します。パスワード引数の後です。
  
4.  出力ファイルは、PowerShell コマンドを実行した同じディレクトリに作成されます。 プロットを表示するには、ファイル plot.jpg を開きます。
  
    ![チップをもらったタクシー乗車とチップをもらわなかったタクシー乗車](media/rsql-devtut-tippedornot.jpg "チップをもらったタクシー乗車とチップをもらわなかったタクシー乗車")  
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>Hist および複数の出力形式を使用してストアド プロシージャを作成する

一般的に、データ サイエンティストはデータ視覚化を複数行い、さまざまな観点からデータを考察します。 この例では、**RPlotHist** というストアド プロシージャを作成し、ヒストグラム、その他の R グラフィックスを .JPG および .PDF 形式で書き込みます。

このストアド プロシージャは、**Hist** 関数を使用してヒストグラムを作成し、.JPG、.PDF、および .PNG などの一般的な形式でバイナリ データをエクスポートします。 

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、オブジェクト エクスプローラーで、**NYCTaxi_Sample** データベースを右クリックし、**[新しいクエリ]** を選択します。

2. 次のスクリプトに貼り付けて、ヒストグラムをプロットするストアド プロシージャを作成します。 この例には、**RPlotHist** という名前が付けられています。
  
    ```sql
    CREATE PROCEDURE [dbo].[RPlotHist]  
    AS  
    BEGIN  
      SET NOCOUNT ON;  
      DECLARE @query nvarchar(max) =  
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'  
      EXECUTE sp_execute_external_script @language = N'R',  
      @script = N'  
       # Set output directory for files and check for existing files with same names   
        mainDir <- ''C:\\temp\\plots''  
        dir.create(mainDir, recursive = TRUE, showWarnings = FALSE)  
        setwd(mainDir);  
        print("Creating output plot files:", quote=FALSE)
        
        # Open a jpeg file and output histogram of tipped variable in that file.  
        dest_filename = tempfile(pattern = ''rHistogram_Tipped_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.jpg'',sep="")  
        print(dest_filename, quote=FALSE);  
        jpeg(filename=dest_filename);  
        hist(InputDataSet$tipped, col = ''lightgreen'', xlab=''Tipped'',   
            ylab = ''Counts'', main = ''Histogram, Tipped'');  
         dev.off();  

        # Open a pdf file and output histograms of tip amount and fare amount.   
        # Outputs two plots in one row  
        dest_filename = tempfile(pattern = ''rHistograms_Tip_and_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=7);  
        par(mfrow=c(1,2));  
        hist(InputDataSet$tip_amount, col = ''lightgreen'',   
            xlab=''Tip amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram, Tip amount'', xlim = c(0,40), 100);  
        hist(InputDataSet$fare_amount, col = ''lightgreen'',   
            xlab=''Fare amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram,   
            Fare amount'',   
            xlim = c(0,100), 100);  
       dev.off();  
  
        # Open a pdf file and output an xyplot of tip amount vs. fare amount using lattice;  
        # Only 10,000 sampled observations are plotted here, otherwise file is large.  
        dest_filename = tempfile(pattern = ''rXYPlots_Tip_vs_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=4);  
        plot(tip_amount ~ fare_amount,   
            data = InputDataSet[sample(nrow(InputDataSet), 10000), ],   
            ylim = c(0,50),   
            xlim = c(0,150),   
            cex=.5,   
            pch=19,   
            col=''darkgreen'',    
            main = ''Tip amount by Fare amount'',   
            xlab=''Fare Amount ($)'',   
            ylab = ''Tip Amount ($)'');   
        dev.off();',  
     @input_data_1 = @query  
     END
    ```
  
+ ストアド プロシージャ内の SELECT クエリの出力が既定の R データ フレーム `InputDataSet`に保存されます。 さまざまな R プロット関数を呼び出し、実際のグラフィックス ファイルを生成できます。 埋め込み R スクリプトのほとんどがそのようなグラフィックス関数のオプションを表します。 `plot` や `hist`などです。
  
+ すべてのフォルダーがローカル フォルダー C:\temp\Plots に保存されます。 宛先フォルダーはストアド プロシージャの一部として R スクリプトに渡された引数により定義されます。  変数 `mainDir`の値を変更して宛先フォルダーを変更できます。

+ ファイルを別のフォルダーに出力するには、ストアド プロシージャに埋め込まれている R スクリプトの `mainDir` 変数の値を変更します。 スクリプトを変更し、さまざまなフォーマットを出力したり、出力するファイルを増やしたりできます。

### <a name="execute-the-stored-procedure"></a>ストアド プロシージャを実行する

次のステートメントを実行して、バイナリ プロット データを JPEG および PDF ファイル形式にエクスポートします。

```sql
EXEC RPlotHist
```

**結果**
    
```sql
STDOUT message(s) from external script:
[1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 

C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]

C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
```

ファイル名の数値はランダムに生成され、既存のファイルに書き込もうとしたときに、エラーが発生しないようにします。

### <a name="view-output"></a>出力を表示する 

プロットを表示するには、宛先フォルダーを開き、ストアド プロシージャの R コードにより作成されたファイルを確認します。

1. STDOUT メッセージで示されているフォルダーに進みます (この例では、これは C:\temp\plots\)

2. `rHistogram_Tipped.jpg` を開いて、チップをもらった乗車の数とチップをもらわなかった乗車の数を比較して表示します。 (このヒストグラムは、前の手順で生成したヒストグラムに似ています。)

3. `rHistograms_Tip_and_Fare_Amount.pdf` を開き、料金に対してプロットされた、チップの金額の分布を表示します。
    
  ![tip_amount と fare_amount を示すヒストグラム](media/rsql-devtut-tipamtfareamt.PNG "tip_amount と fare_amount を示すヒストグラム")

4. `rXYPlots_Tip_vs_Fare_Amount.pdf` を開き、x 軸を料金、y 軸をチップ額とする散布図を表示します。

   ![料金に対してプロットされたチップ額](media/rsql-devtut-tipamtbyfareamt.PNG "料金に対してプロットされたチップ額")

## <a name="next-lesson"></a>次のレッスン

[レッスン 2:T-SQL を使用してデータ機能を作成する](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>前のレッスン

[NYC タクシーのデモ データを設定する](demo-data-nyctaxi-in-sql.md)
