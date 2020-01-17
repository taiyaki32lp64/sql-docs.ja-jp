---
title: Excel ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelsource.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 14153d38d53a87729231b60b2b2846dc12401fc1
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624355"
---
# <a name="excel-source"></a>Excel ソース
  Excel ソースは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel ブック内のワークシートまたは範囲からデータを抽出します。  
  
 Excel ソースでは、データを抽出するために、次の 4 つの異なるデータ アクセス モードが用意されています。  
  
-   テーブルまたはビュー。  
  
-   変数で指定されたテーブルまたはビュー。  
  
-   SQL ステートメントの結果。 クエリにはパラメーター化クエリを使用できます。  
  
-   変数に格納された SQL ステートメントの結果。  
  
> [!IMPORTANT]  
>  Excel でのワークシートまたは範囲は、テーブルまたはビューに相当します。 Excel ソース エディターと Excel 変換先エディターで使用できるテーブルの一覧では、既存のワークシート (Sheet1$ など、ワークシート名に $ 記号を付加して識別) と名前付き範囲 (MyRange など、$ 記号が付かないことで識別) が表示されます。 詳細については、「使用に関する注意点」を参照してください。  
  
 Excel ソースは、Excel 接続マネージャーを使用してデータ ソースに接続します。Excel 接続マネージャーでは、使用する Excel ブック ファイルを指定します。 詳しくは、「 [Excel Connection Manager](../connection-manager/excel-connection-manager.md)」をご覧ください。  
  
 Excel ソースは、1 つの標準出力と 1 つのエラー出力をとります。  
  
## <a name="usage-considerations"></a>使用に関する注意点  
 Excel 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 と、それによってサポートされる Excel ISAM (Indexed Sequential Access Method) ドライバーを使用して Excel データ ソースに接続し、データの読み取りおよび書き込みを行います。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報に含まれる資料の多くは、このプロバイダーおよびドライバーの処理に関するドキュメントです。これらの資料は [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] または従来のデータ変換サービスに固有のものではありませんが、予期しない結果が発生する可能性のある特定の動作について知っておくことをお勧めします。 Excel ドライバーの動作と使用の概要については、次を参照してください[HOWTO:。Visual Basic または VBA の Excel データで ADO を使用して](https://support.microsoft.com/kb/257819)します。  
  
 Jet プロバイダーを Excel ドライバーと共に使用した場合、次のような動作が原因で、Excel データ ソースのデータを読み取るときに予期しない結果が発生する場合があります。  
  
-   **データ ソース**。 Excel ブックの変換元データには、ワークシートまたは名前付き範囲 (MyRange など) を使用できます。ワークシート名には $ 記号を付加する必要があります (Sheet1$ など)。 SQL ステートメントでは、$ 記号による構文エラーを回避するため、ワークシートの名前を [Sheet1$] などのように区切る必要があります。 クエリ ビルダーは、これらの区切り記号を自動的に付加します。 ワークシートまたは範囲を指定した場合、ドライバーは、ワークシートまたは範囲の左上の空でない最初のセルから、連続したセルのブロックを読み取ります。 したがって、ソース データには、タイトル行またはヘッダー行とデータ行との間に空の行を入れることはできません。  
  
-   **不足している値**。 Excel ドライバーは、指定した変換元の特定の行数 (既定では 8 行) を読み取り、各列のデータ型を推測します。 1 つの列に複数のデータ型が混在している可能性がある場合、特に数値データとテキスト データが混合している場合に、Excel ドライバーは数が多い方のデータ型を優先して判定し、それ以外のデータ型のデータが含まれるセルについては NULL 値を返します (同数の場合は、数値型が優先されます)。Excel ワークシートでのセル書式のほとんどのオプションは、このデータ型の判定に影響しません。 Excel ドライバーのこの動作を変更するには、インポート モードを指定します。 インポート モードを指定する追加`IMEX=1`で Excel 接続マネージャーの接続文字列の拡張プロパティの値に、**プロパティ**ウィンドウ。 詳細については、次を参照してください[PRB:。DAO の OpenRecordset を使用して NULL として返される値を excel](https://support.microsoft.com/kb/194124)します。  
  
-   **切り捨てられたテキスト**。 Excel の列にテキスト データが含まているとドライバーが判定した場合、ドライバーはサンプリングした最も長い値に基づいて、データ型 (文字列またはメモ) を選択します。 ドライバーがサンプリングした行で 255 文字より長い値が検出されなかった場合、その列はメモ列ではなく、255 文字の文字列の列として扱われます。 このため、255 文字より長い値があると、切り捨てられる場合があります。 切り捨てを発生させずにメモ列からデータをインポートするには、サンプリングされた行のうち 1 行以上のメモ列に、255 文字より長い値が含まれている状態にする必要があります。または、そのような行が含まれるように、ドライバーがサンプリングする行数を増やす必要があります。 サンプリングする行数を増やすには、 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** レジストリ キーの **TypeGuessRows** の値を増やします。 詳細については、次を参照してください[PRB:。Jet 4.0 ole DB ソースからデータの転送エラーで失敗](https://support.microsoft.com/kb/281517)します。  
  
-   **データ型**。 Excel ドライバーでは、データ型の限定されたセットのみを認識します。 たとえば、すべての数値列は倍精度浮動小数点型 (DT_R8) として解釈され、すべての文字列の列 (メモ列以外) は 255 文字の Unicode 文字列 (DT_WSTR) として解釈されます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、Excel データ型を次のようにマップします。  
  
    -   Numeric - 倍精度浮動小数点数 (DT_R8)  
  
    -   Currency - 通貨 (DT_CY)  
  
    -   Boolean - ブール (DT_BOOL)  
  
    -   日付/時刻 - `datetime` (DT_DATE)  
  
    -   String - Unicode 文字列、長さ 255 (DT_WSTR)  
  
    -   Memo - Unicode テキスト ストリーム (DT_NTEXT)  
  
-   **データ型と長さの変換**。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、データ型の暗黙的な変換は行われません。 したがって、派生列変換またはデータ変換の変換を使用して、Excel データを明示的に変換してから Excel 以外の変換先に読み込むか、Excel データを Excel 以外のデータに変換してから Excel 変換先に読み込む必要があります。 この場合、初期パッケージを作成する際に、必要な変換を構成できるインポート ウィザードおよびエクスポート ウィザードを使用すると便利な場合があります。 必要な変換の例を次に示します。  
  
    -   特定のコードページを使用した Unicode Excel 文字列の列と Unicode 以外の文字列の列間の変換  
  
    -   255 文字の Excel 文字列の列と異なる長さの文字列の列間の変換  
  
    -   倍精度の Excel 数値列と他の型の数値列の列間の変換  
  
## <a name="excel-source-configuration"></a>Excel ソースの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[Excel ソース エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[Excel ソース エディター] &#40;[接続マネージャー] ページ&#41;](../excel-source-editor-connection-manager-page.md)  
  
-   [[Excel ソース エディター] &#40;[列] ページ&#41;](../excel-source-editor-columns-page.md)  
  
-   [[Excel ソース エディター] &#40;[エラー出力] ページ&#41;](../excel-source-editor-error-output-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるすべてのプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [Excel のカスタム プロパティ](excel-custom-properties.md)  
  
 Excel ファイルのグループによるループ処理については、「 [Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する](../control-flow/foreach-loop-container.md)」をご覧ください。  
  
## <a name="related-tasks"></a>Related Tasks  

-   [SQL Server Integration Services (SSIS) を使用して、Excel からデータをインポートする、または Excel にデータをエクスポートする](../load-data-to-from-excel-with-ssis.md)

-   [クエリ パラメーターをデータ フロー コンポーネントの変数にマップする](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する](../control-flow/foreach-loop-container.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   hrvoje.piasevoli.com のブログ「 [Importing data from 64-bit Excel in SSIS](https://go.microsoft.com/fwlink/?LinkId=217673)」(SSIS での 64 ビット バージョンの Excel からのデータ インポート)  
  
-   ブログ エントリ「 [Integration Services における Excel、3 の第 1 部。接続とコンポーネント](https://go.microsoft.com/fwlink/?LinkId=217674)、dougbert.com  
  
-   ブログ エントリ「 [Integration Services における Excel、3 の第 2 部。テーブルとデータ型](https://go.microsoft.com/fwlink/?LinkId=217675)、dougbert.com します。  
  
-   ブログ エントリ「 [Integration Services における Excel、3 の第 3 部。問題と代替策](https://go.microsoft.com/fwlink/?LinkId=217676)、dougbert.com します。  
  
-   ブログ エントリ「[接続を Excel (XLSX) (SSIS) で](https://microsoft-ssis.blogspot.com/2014/02/connecting-to-excel-xlsx-in-ssis.html)します。  
  
  
