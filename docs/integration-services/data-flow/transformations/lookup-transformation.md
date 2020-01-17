---
title: 参照変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.lookuptrans.f1
- sql13.dts.designer.lookuptransformation.general.f1
- sql13.dts.designer.lookuptransformation.referencetable.f1
- sql13.dts.designer.lookuptransformation.columns.f1
- sql13.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d4c44f8920fc3a8060dcff6112eb41055f1584d2
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291258"
---
# <a name="lookup-transformation"></a>参照変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  参照変換は、入力列のデータを参照データセットの列と結合することにより参照を実行します。 参照を使用すると、共通の列の値に基づいている関連テーブル内の追加情報にアクセスできます。  
  
 参照データセットは、キャッシュ ファイル、既存のテーブル、既存のビュー、新しいテーブル、または SQL クエリの結果のいずれかになります。 参照変換では、OLE DB 接続マネージャーまたはキャッシュ接続マネージャーを使用して、参照データセットに接続します。 詳細については、「 [OLE DB 接続マネージャー](../../../integration-services/connection-manager/ole-db-connection-manager.md) 」および「 [キャッシュ接続マネージャー](../../../integration-services/data-flow/transformations/cache-connection-manager.md)」をご覧ください。  
  
 参照変換は、次の方法で構成できます。  
  
-   使用する接続マネージャーを選択します。 データベースに接続する場合は、OLE DB 接続マネージャーを選択します。 キャッシュ ファイルに接続する場合は、キャッシュ接続マネージャーを選択します。  
  
-   参照データセットを含むテーブルまたはビューを指定します。  
  
-   SQL ステートメントを指定して、参照データセットを生成します。  
  
-   入力と参照データセット間の結合を指定します。  
  
-   参照データセットの列を参照変換の出力に追加します。  
  
-   キャッシュ オプションを構成します。  
  
 参照変換では、OLE DB 接続マネージャー用に次のデータベース プロバイダーをサポートしています。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle  
  
-   DB2  
  
 参照変換は、変換入力の値と参照データセットの値の間で等結合を実行しようとします。 等結合の場合、変換入力の各行は、参照データセットの少なくとも 1 行と一致する必要があります。等結合を行うことができない場合、参照変換で次のいずれかの処理が実行されます。  
  
-   参照データセット内に一致するエントリがない場合、結合は行われません。 既定では、参照変換で一致するエントリがない行は、エラーとして扱われます。 ただし、それらの行を不一致出力にリダイレクトするように参照変換を構成することもできます。  
  
-   参照テーブル内の複数のエントリが一致する場合、参照クエリから最初に返されたエントリのみが返されます。 複数のエントリが一致する場合、すべての参照データセットをキャッシュに読み込むように参照変換が構成されているときだけ、エラーまたは警告が生成されます。 この場合、参照変換によってデータセットがキャッシュに読み込まれたときに複数の一致エントリが検出されると、警告が生成されます。  
  
 複合結合の場合、変換入力の複数の列を参照データセットの列に結合できます。 この変換では、DT_R4、DT_R8、DT_TEXT、DT_NTEXT、または DT_IMAGE データ型以外のすべてのデータ型の列を結合できます。 詳細については、「 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 通常、参照データセットの値が、変換出力に追加されます。 たとえば、参照変換により、入力列の値を使用してテーブルから製品名を抽出し、製品名を変換出力に追加できます。 参照テーブルの値によって列の値を置換したり、値を新しい列に追加できます。  
  
 参照変換が実行する参照では、大文字と小文字は区別されます。 データ内の大文字/小文字の相違が原因で参照が失敗するのを回避するために、最初に文字マップ変換を使用して、データを大文字または小文字に変換します。 次に、参照テーブルを生成する SQL ステートメント内で UPPER 関数または LOWER 関数を使用します。 詳細については、「[Character Map Transformation](../../../integration-services/data-flow/transformations/character-map-transformation.md)」(文字マップ変換)、「[UPPER &#40;Transact-SQL&#41;](../../../t-sql/functions/upper-transact-sql.md)」、および「[LOWER &#40;Transact-SQL&#41;](../../../t-sql/functions/lower-transact-sql.md)」をご覧ください。  
  
 参照変換の入力と出力を次に示します。  
  
-   入力。  
  
-   一致出力。 一致出力は、参照データセット内の 1 つ以上のエントリと一致した変換入力内の行を処理します。  
  
-   不一致出力。 不一致出力は、参照データセット内の 1 つ以上のエントリと一致しない入力内の行を処理します。 一致エントリがない行をエラーとして扱うように参照変換を構成している場合、これらの行はエラー出力にリダイレクトされます。 それ以外の場合、これらの行は不一致出力にリダイレクトされます。  
  
-   エラー出力。  
  
## <a name="caching-the-reference-dataset"></a>参照データセットのキャッシュ  
 インメモリ キャッシュは、参照データセットを格納し、データのインデックスを作成するハッシュ テーブルを格納します。 キャッシュは、パッケージの実行が完了するまでメモリ内に保持されます。 キャッシュはキャッシュ ファイル (.caw) に永続化できます。  
  
 キャッシュをファイルに永続化すると、システムによるキャッシュの読み込みが高速化されます。 これにより、参照変換とパッケージのパフォーマンスが向上します。 キャッシュ ファイルを使用する場合は、データベース内にあるデータの最新の状態が反映されていないデータを操作していることに注意してください。  
  
 キャッシュをファイルに永続化する他の利点を次に示します。  
  
-   ***複数のパッケージ間でキャッシュ ファイルを共有できます。詳細については、「***  [キャッシュ接続マネージャーの変換を使用してフル キャッシュ モードの参照変換を実装する](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  ***」をご覧ください。***  
  
-   キャッシュ ファイルをパッケージと一緒に配置できます。 ***これにより、このデータを複数のコンピューター上で使用できます。*** 詳細については、「 [参照変換用のキャッシュを作成および配置する](../../../integration-services/data-flow/transformations/create-and-deploy-a-cache-for-the-lookup-transformation.md)」をご覧ください。  
  
-   RAW ファイル ソースを使用してキャッシュ ファイルからデータを読み取ることができます。 次に他のデータ フロー コンポーネントを使用してデータを変換または移動できます。 詳細については、「 [RAW ファイル ソース](../../../integration-services/data-flow/raw-file-source.md)」をご覧ください。  
  
    > [!NOTE]  
    >  キャッシュ接続マネージャーは、RAW ファイル変換先を使用して作成または変更されたキャッシュ ファイルをサポートしていません。  
  
-   ファイル システム タスクを使用して、キャッシュ ファイルに対して処理を実行したり属性を設定したりできます。 詳細については、「 [ファイル システム タスク](../../../integration-services/control-flow/file-system-task.md)」をご覧ください。  
  
 キャッシュのオプションを次に示します。  
  
-   参照データセットは、テーブル、ビュー、または SQL クエリを使用して生成され、参照変換が実行される前にキャッシュに読み込まれます。 OLE DB 接続マネージャーを使用して、データセットにアクセスします。  
  
     このキャッシュ オプションは、 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]の参照変換に用意されているフル キャッシュ オプションと互換性があります。  
  
-   参照データセットは、データ フロー内の接続されているデータ ソースまたはキャッシュ ファイルから生成され、参照変換の実行前にキャッシュに読み込まれます。 キャッシュ接続マネージャー (および必要に応じてキャッシュ変換) を使用して、データセットにアクセスします。 詳細については、「 [キャッシュ接続マネージャー](../../../integration-services/data-flow/transformations/cache-connection-manager.md) 」および「 [キャッシュ変換](../../../integration-services/data-flow/transformations/cache-transform.md)」をご覧ください。  
  
-   参照データセットは、参照変換の実行時に、テーブル、ビュー、または SQL クエリを使用して生成されます。 参照データセットに一致するエントリがある行、およびデータセットに一致するエントリがない行がキャッシュに読み込まれます。  
  
     キャッシュのメモリ サイズを超えると、使用頻度の最も低い行が、参照変換によって自動的にキャッシュから削除されます。  
  
     このキャッシュ オプションは、 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]の参照変換に用意されている部分キャッシュ オプションと互換性があります。  
  
-   参照データセットは、参照変換の実行時に、テーブル、ビュー、または SQL クエリを使用して生成されます。 データはキャッシュされません。  
  
     このキャッシュ オプションは、 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]の参照変換に用意されているキャッシュなしオプションと互換性があります。  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、文字列の比較方法が異なります。 実行前に参照データセットをキャッシュに読み込むように参照変換が構成されている場合、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] によりキャッシュ内で参照比較が行われます。 それ以外の場合、参照操作でパラメーター化 SQL ステートメントが使用され、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により参照比較が行われます。 つまり、キャッシュの種類に応じて、参照変換が、同じ参照テーブルから異なる数の一致結果を返す可能性があります。  
  
## <a name="related-tasks"></a>Related Tasks  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。 詳細については、以下のトピックをご覧ください。  
  
-   [キャッシュなしモードまたは部分キャッシュ モードの参照を実装する](../../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [キャッシュ接続マネージャーの変換を使用してフル キャッシュ モードの参照変換を実装する](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [OLE DB 接続マネージャーを使用してフル キャッシュ モードの参照変換を実装する](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   MSDN ライブラリのビデオ「[フル キャッシュ モードで参照変換を実装する方法](https://go.microsoft.com/fwlink/?LinkId=131031)」 (msdn.microsoft.com)  
  
-   blogs.msdn.com のブログ「 [参照変換のキャッシュ モードを使用する際の推奨事項](https://go.microsoft.com/fwlink/?LinkId=146623)」  
  
-   blogs.msdn.com のブログ記事「[参照パターン: 大文字と小文字を区別しない](https://go.microsoft.com/fwlink/?LinkId=157782)」  
  
-   msftisprodsamples.codeplex.com のサンプル「 [参照変換](https://go.microsoft.com/fwlink/?LinkId=267528)」  
  
     [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 製品サンプルとサンプル データベースのインストールの詳細については、「 [SQL Server Integration Services 製品サンプル](https://go.microsoft.com/fwlink/?LinkId=267527)」をご覧ください。  
  
## <a name="lookup-transformation-editor-general-page"></a>[参照変換エディター] ([全般] ページ)
  [参照変換エディター] ダイアログ ボックスの **[全般]** ページを使用して、キャッシュ モードや接続の種類を選択し、一致するエントリがない行の処理方法を指定します。  
  
### <a name="options"></a>オプション  
 **[フル キャッシュ]**  
 参照変換を実行する前に、参照データセットを生成してキャッシュに読み込みます。  
  
 **[部分キャッシュ]**  
 参照変換の実行中に、参照データセットを生成します。 参照データセットに一致するエントリがある行、およびデータセットに一致するエントリがない行をキャッシュに読み込みます。  
  
 **[キャッシュなし]**  
 参照変換の実行中に、参照データセットを生成します。 キャッシュにデータは読み込まれません。  
  
 **キャッシュ接続マネージャー**  
 キャッシュ接続マネージャーを使用するように参照変換を構成します。 このオプションを選択できるのは、[フル キャッシュ] オプションを選択した場合だけです。  
  
 **[キャッシュなし]**  
 OLE DB 接続マネージャーを使用するように参照変換を構成します。  
  
 **[エントリが一致しない行の処理方法を指定する]**  
 参照データセット内で少なくとも 1 つのエントリが一致しない行を処理するためのオプションを選択します。  
  
 **[一致なしの出力に行をリダイレクトする]** を選択した場合は、行が一致なしの出力にリダイレクトされ、エラーとして処理されなくなります。 **[参照変換エディター]** ダイアログ ボックスの **[エラー出力]** ページの **[エラー]** オプションは使用できません。  
  
 **[エントリが一致しない行の処理方法を指定する]** ボックスの一覧で他のオプションを選択した場合は、行がエラーとして処理されます。 **[エラー出力]** ページの **[エラー]** オプションを使用できます。  
  
### <a name="external-resources"></a>外部リソース  
 blogs.msdn.com のブログ「 [キャッシュ モードの参照](https://go.microsoft.com/fwlink/?LinkId=219518) 」  
  
## <a name="lookup-transformation-editor-connection-page"></a>[参照変換エディター] ([接続] ページ)
  **[参照変換エディター]** ダイアログ ボックスの **[接続]** ページを使用して、接続マネージャーを選択します。 OLE DB 接続マネージャーを選択する場合は、参照データセットを生成するためのクエリ、テーブル、またはビューも選択します。  
  
### <a name="options"></a>オプション  
 **[参照変換エディター]** ダイアログ ボックスの [全般] ページで **[フル キャッシュ]** および **[キャッシュ接続マネージャー]** を選択すると、次のオプションを使用できます。  
  
 **[フル キャッシュ]**  
 既存のキャッシュ接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 新しい接続を作成するには、 **[キャッシュ接続マネージャー エディター]** ダイアログ ボックスを使用します。  
  
 **[参照変換エディター]** ダイアログ ボックスの [全般] ページで **[フル キャッシュ]** 、 **[部分キャッシュ]** 、 **[キャッシュなし]** 、および **[OLE DB 接続マネージャー]** を選択すると、次のオプションを使用できます。  
  
 **[キャッシュなし]**  
 一覧から既存の OLE DB 接続マネージャーを選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 **[テーブルまたはビューを使用する]**  
 既存のテーブルまたはビューを一覧から選択するか、 **[新規作成]** をクリックして新しいテーブルを作成します。  
  
> [!NOTE]  
>  **[参照変換エディター]** の **[詳細設定]** ページで SQL ステートメントを指定する場合、ここで選択したテーブル名はその SQL ステートメントでオーバーライドおよび置換されます。 詳細については、「 [[参照変換エディター] &#40;[詳細設定] ページ&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md)」を参照してください。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して新しいテーブルを作成します。  
  
 **[SQL クエリの結果を使用する]**  
 既存のクエリの参照、新しいクエリの構築、クエリ構文のチェック、およびクエリ結果のプレビューを行うには、このオプションを選択します。  
  
 **[クエリの作成]**  
 **[クエリ ビルダー]** を使用して、実行する Transact-SQL ステートメントを作成します。これは、データを参照することによってクエリを作成するグラフィカルなツールです。  
  
 **[参照]**  
 ファイルとして保存されている既存のクエリを参照します。  
  
 **[クエリの解析]**  
 クエリ構文をチェックします。  
  
 **プレビュー**  
 **[クエリ結果のプレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 結果は 200 行まで表示されます。  
  
### <a name="external-resources"></a>外部リソース  
 blogs.msdn.com のブログ「 [キャッシュ モードの参照](https://go.microsoft.com/fwlink/?LinkId=219518) 」  
  
## <a name="lookup-transformation-editor-columns-page"></a>[参照変換エディター] ([列] ページ)
  **[参照変換エディター]** ダイアログ ボックスの **[列]** ページを使用すると、元のテーブルと参照テーブルの間に結合を指定したり、参照テーブルから参照列を選択したりできます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 入力列とは、データ フロー内の接続されているソースからの列です。 入力列と参照列のデータ型は一致している必要があります。  
  
 ドラッグ アンド ドロップ操作により、使用できる入力列を参照列にマップします。  
  
 キーボードを使用して、 **[使用できる入力列]** テーブル内の列を強調表示し、アプリケーション キーを押して、 **[マッピングの編集]** をクリックすることで、入力列を参照列にマップすることもできます。  
  
 **使用できる参照列**  
 参照列の一覧を表示します。 参照列とは、入力列に一致する値の参照先の参照テーブルにある列です。  
  
 ドラッグ アンド ドロップ操作により、使用できる参照列を入力列にマップします。  
  
 チェック ボックスを使用して、参照操作を実行する参照テーブル内の参照列を選択します。  
  
 キーボードを使用して、 **[使用できる参照列]** テーブル内の列を強調表示し、アプリケーション キーを押して、 **[マッピングの編集]** をクリックすることで、参照列を入力列にマップすることもできます。  
  
 **参照列**  
 選択した参照列を表示します。 選択内容は、 **[使用できる参照列]** テーブルのチェック ボックスの状態に反映されます。  
  
 **[参照操作]**  
 一覧から、参照列で実行する参照操作を選択します。  
  
 **[出力の別名]**  
 各参照列の出力の別名を入力します。 既定では参照列の名前が使用されますが、一意なわかりやすい名前を自由に付けることができます。  
  
## <a name="lookup-transformation-editor-advanced-page"></a>[参照変換エディター] ([詳細設定] ページ)
  **[参照変換エディター]** ダイアログ ボックスの **[詳細設定]** ページを使用して、部分キャッシュを構成し、参照変換用 SQL ステートメントを変更します。  
  
### <a name="options"></a>オプション  
 **[キャッシュ サイズ (32 ビット)]**  
 32 ビット コンピューター用のキャッシュ サイズを MB 単位で調整します。 既定値は 5 MB です。  
  
 **[キャッシュ サイズ (64 ビット)]**  
 64 ビット コンピューター用のキャッシュ サイズを MB 単位で調整します。 既定値は 5 MB です。  
  
 **[エントリが一致しない行のキャッシュを有効にする]**  
 一致するエントリが参照データセットにない行をキャッシュします。  
  
 **[キャッシュからの割り当て]**  
 一致するエントリが参照データセットにない行に対して割り当てるキャッシュの割合を指定します。  
  
 **[SQL ステートメントを変更する]**  
 参照データセットを生成するために使用される SQL ステートメントを変更します。  
  
> [!NOTE]  
>  このページで指定するオプションの SQL ステートメントは、 **[参照変換エディター]** の **[接続]** ページで指定したテーブル名をオーバーライドおよび置換します。 詳細については、「 [[参照変換エディター] &#40;[接続] ページ&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)」を参照してください。  
  
 **[パラメーターの設定]**  
 **[クエリ パラメーターの設定]** ダイアログ ボックスを使用して、入力列をパラメーターにマップします。  
  
### <a name="external-resources"></a>外部リソース  
 blogs.msdn.com のブログ「 [キャッシュ モードの参照](https://go.microsoft.com/fwlink/?LinkId=219518) 」  
  
## <a name="see-also"></a>参照  
 [あいまい参照変換](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [用語参照変換](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)   
 [データ フロー](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
