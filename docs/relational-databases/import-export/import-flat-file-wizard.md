---
title: SQL にフラット ファイルをインポートする | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: data-movement
ms.topic: conceptual
f1_keywords:
- sql13.swb.importflatfile.f1
author: yualan
ms.author: alayu
ms.reviewer: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 792cb1bcef1097c3eddaa325519b43a229bcccb4
ms.sourcegitcommit: ba44730f5cc33295ae2ed1f281186dd266bad4ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74190799"
---
# <a name="import-flat-file-to-sql-wizard"></a>SQL のフラット ファイルのインポート ウィザード
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
> インポートおよびエクスポート ウィザードに関連するコンテンツについては、「[SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)」(SQL Server インポートおよびエクスポート ウィザード) を参照してください。

フラット ファイルのインポート ウィザードを使用すると、フラット ファイル (.csv、.txt) からデータベース内の新しいテーブルにデータを簡単にコピーできます。 この概要では、このウィザードを使用する理由、このウィザードを見つける方法、実行が簡単な例について説明します。

## <a name="why-would-i-use-this-wizard"></a>このウィザードを使用する理由
このウィザードは、Program Synthesis using Examples ([PROSE](https://microsoft.github.io/prose/)) と呼ばれるインテリジェント フレームワークを利用して現在のインポート操作を改善するために作成されました。 特殊なドメインの知識を持っていないユーザーの場合、データのインポートは複雑で、間違いやすく、面倒な作業になりがちです。 このウィザードでは、インポート プロセスが入力ファイルと一意のテーブル名を選択するだけの簡単な操作に整理され、後の処理は PROSE フレームワークが行います。

PROSE は、入力ファイルのデータ パターンを分析し、列の名前、型、区切り記号などを推定します。 このフレームワークはファイルの構造を学習し、ユーザーの代わりにすべての面倒な作業を実行します。

フラット ファイルのインポート ウィザードのユーザー エクスペリエンス改善の詳細については、このビデオをご覧ください。

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173/player?WT.mc_id=dataexposed-c9-niner]

## <a name="prerequisites"></a>前提条件
この機能は、SQL Server Management Studio (SSMS) v17.3 以降でのみ使用できます。 最新バージョンを使用していることを確認してください。 最新バージョンは[こちら](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)で入手できます。
 
## <a id="started"></a>はじめに
フラット ファイルのインポート ウィザードにアクセスするには、次の手順を実行します。

1. **SQL Server Management Studio** を開きます。
2. SQL Server Database Engine または localhost のインスタンスに接続します。
3. **[データベース]** を展開し、データベース (下の例では test) を右クリックし、 **[タスク]** をポイントして、[データのインポート] の上の **[フラット ファイルのインポート]** をクリックします。

![ウィザードのメニュー](media/import-flat-file-wizard/importffmenu.png)

ウィザードの各機能の詳細については、次のチュートリアルを参照してください。

## <a name="tutorial"></a>チュートリアル
このチュートリアルには、任意のフラット ファイルを使うことができます。 自分のファイルを使わない場合は、このチュートリアルでは次の Excel の CSV 形式のファイルを使用します。自由にコピーしてください。 この CSV を使用する場合は、**example.csv** という名前を付けて、デスクトップなどの簡単な場所に csv ファイルとして保存してください。

![Excel のウィザード](media/import-flat-file-wizard/importffexample.png)

### <a name="step-1-access-wizard-and-intro-page"></a>手順 1:ウィザードの [はじめに] ページにアクセスする
[こちら](#started)の手順に従ってウィザードにアクセスします。

ウィザードの最初のページは [ようこそ] ページです。 このページを再表示したくない場合は、 **[次回からこの開始ページを表示しない]** をクリックします。

![ウィザードの [はじめに]](media/import-flat-file-wizard/importffintro.png)

### <a name="step-2-specify-input-file"></a>手順 2:入力ファイルを指定する
[参照] をクリックして入力ファイルを選択します。 ウィザードの既定で、.csv ファイルと .txt ファイルが検索されます。 

新しいテーブル名は一意にする必要があります。一意ではない場合、ウィザードを次に進めることはできません。

![ウィザードの指定](media/import-flat-file-wizard/importffspecify.png)

### <a name="step-3-preview-data"></a>手順 3:データをプレビューする
プレビューが生成され、最初の 50 行を確認できます。 問題がある場合は [キャンセル] をクリックします。ない場合は、次のページに進みます。

![ウィザードのプレビュー](media/import-flat-file-wizard/importffpreview.png)

### <a name="step-4-modify-columns"></a>手順 4:列を変更する
ウィザードでは、列名、データ型などについて正しいと思われるものを特定します。ここでは、フィールドが正しくない場合に編集できます (たとえば、データ型が int ではなく float など)。

準備ができたら次に進みます。

![ウィザードの変更](media/import-flat-file-wizard/importffmodify.png)

### <a name="step-5-summary"></a>手順 5:まとめ
これは、現在の構成が表示される概要ページです。 問題がある場合は、前のセクションに戻ることができます。 問題がない場合は、[完了] をクリックします。インポート プロセスが開始されます。

![ウィザードの概要](media/import-flat-file-wizard/importffsummary.png)

### <a name="step-6-results"></a>手順 6:[結果]
このページには、インポートが成功したかどうかが表示されます。 緑のチェック マークが表示される場合は成功です。それ以外の場合は、構成や入力ファイルに誤りがないか確認する必要があります。

![ウィザードの結果](media/import-flat-file-wizard/importffresults.png)

## <a name="learn-more"></a>詳細情報

ウィザードの詳細については、以下を参照してください。
 
- **その他のリソースのインポートに関する詳細**。 複数のフラット ファイルをインポートする場合は、「[SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)」(SQL Server インポートおよびエクスポート ウィザード) を参照してください。
- **フラット ファイル ソースへの接続に関する詳細**。 フラット ファイル ソースへの接続の詳細については、「[Connect to a Flat File Data Source](https://docs.microsoft.com/sql/integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard)」(フラット ファイル データ ソースへの接続) を参照してください。
- **PROSE の詳細**。 このウィザードに使用されるインテリジェント フレームワークの概要については、「[PROSE SDK](https://microsoft.github.io/prose/)」を参照してください。

