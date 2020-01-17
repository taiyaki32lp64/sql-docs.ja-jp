---
title: 参照変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptrans.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47b04c547700eda94d4c4f19b4a1211f8cdbf694
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900256"
---
# <a name="lookup-transformation"></a>参照変換
  参照変換は、入力列のデータを参照データセットの列と結合することにより参照を実行します。 参照を使用すると、共通の列の値に基づいている関連テーブル内の追加情報にアクセスできます。  
  
 参照データセットは、キャッシュ ファイル、既存のテーブル、既存のビュー、新しいテーブル、または SQL クエリの結果のいずれかになります。 参照変換では、OLE DB 接続マネージャーまたはキャッシュ接続マネージャーを使用して、参照データセットに接続します。 詳細については、「 [OLE DB 接続マネージャー](../../connection-manager/ole-db-connection-manager.md) 」および「 [キャッシュ接続マネージャー](../../connection-manager/cache-connection-manager.md)」をご覧ください。  
  
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
  
-   参照データセット内に一致するエントリがない場合、結合は行われません。 既定では、参照変換で一致するエントリがない行は、エラーとして扱われます。 ただし、それらの行を不一致出力にリダイレクトするように参照変換を構成することもできます。 詳細については、「[[参照変換エディター] &#40;[全般] ページ&#41;](../../lookup-transformation-editor-general-page.md)」および「[[参照変換エディター] &#40;[エラー出力] ページ&#41;](../../lookup-transformation-editor-error-output-page.md)」をご覧ください。  
  
-   参照テーブル内の複数のエントリが一致する場合、参照クエリから最初に返されたエントリのみが返されます。 複数のエントリが一致する場合、すべての参照データセットをキャッシュに読み込むように参照変換が構成されているときだけ、エラーまたは警告が生成されます。 この場合、参照変換によってデータセットがキャッシュに読み込まれたときに複数の一致エントリが検出されると、警告が生成されます。  
  
 複合結合の場合、変換入力の複数の列を参照データセットの列に結合できます。 この変換では、DT_R4、DT_R8、DT_TEXT、DT_NTEXT、または DT_IMAGE データ型以外のすべてのデータ型の列を結合できます。 詳細については、「 [Integration Services Data Types](../integration-services-data-types.md)」を参照してください。  
  
 通常、参照データセットの値が、変換出力に追加されます。 たとえば、参照変換により、入力列の値を使用してテーブルから製品名を抽出し、製品名を変換出力に追加できます。 参照テーブルの値によって列の値を置換したり、値を新しい列に追加できます。  
  
 参照変換が実行する参照では、大文字と小文字は区別されます。 データ内の大文字/小文字の相違が原因で参照が失敗するのを回避するために、最初に文字マップ変換を使用して、データを大文字または小文字に変換します。 次に、参照テーブルを生成する SQL ステートメント内で UPPER 関数または LOWER 関数を使用します。 詳細については、「[Character Map Transformation](character-map-transformation.md)」(文字マップ変換)、「[UPPER &#40;Transact-SQL&#41;](/sql/t-sql/functions/upper-transact-sql)」、および「[LOWER &#40;Transact-SQL&#41;](/sql/t-sql/functions/lower-transact-sql)」をご覧ください。  
  
 参照変換の入力と出力を次に示します。  
  
-   入力。  
  
-   一致出力。 一致出力は、参照データセット内の 1 つ以上のエントリと一致した変換入力内の行を処理します。  
  
-   不一致出力。 不一致出力は、参照データセット内の 1 つ以上のエントリと一致しない入力内の行を処理します。 一致エントリがない行をエラーとして扱うように参照変換を構成している場合、これらの行はエラー出力にリダイレクトされます。 それ以外の場合、これらの行は不一致出力にリダイレクトされます。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)] の参照変換の出力は 1 つだけでした。 作成された参照変換を実行する方法の詳細についての[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]を参照してください[参照変換のアップグレード](../../../sql-server/install/upgrade-lookup-transformations.md)します。  
  
-   エラー出力。  
  
## <a name="caching-the-reference-dataset"></a>参照データセットのキャッシュ  
 インメモリ キャッシュは、参照データセットを格納し、データのインデックスを作成するハッシュ テーブルを格納します。 キャッシュは、パッケージの実行が完了するまでメモリ内に保持されます。 キャッシュはキャッシュ ファイル (.caw) に永続化できます。  
  
 キャッシュをファイルに永続化すると、システムによるキャッシュの読み込みが高速化されます。 これにより、参照変換とパッケージのパフォーマンスが向上します。 キャッシュ ファイルを使用する場合は、データベース内にあるデータの最新の状態が反映されていないデータを操作していることに注意してください。  
  
 キャッシュをファイルに永続化する他の利点を次に示します。  
  
-   ***複数のパッケージ間でキャッシュ ファイルを共有できます。詳細については、「***  [キャッシュ接続マネージャーの変換を使用してフル キャッシュ モードの参照変換を実装する](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  ***」をご覧ください。***  
  
-   キャッシュ ファイルをパッケージと一緒に配置できます。 ***これにより、このデータを複数のコンピューター上で使用できます。*** 詳細については、「 [参照変換用のキャッシュを作成および配置する](create-and-deploy-a-cache-for-the-lookup-transformation.md)」をご覧ください。  
  
-   RAW ファイル ソースを使用してキャッシュ ファイルからデータを読み取ることができます。 次に他のデータ フロー コンポーネントを使用してデータを変換または移動できます。 詳細については、「 [RAW ファイル ソース](../raw-file-source.md)」をご覧ください。  
  
    > [!NOTE]  
    >  キャッシュ接続マネージャーは、RAW ファイル変換先を使用して作成または変更されたキャッシュ ファイルをサポートしていません。  
  
-   ファイル システム タスクを使用して、キャッシュ ファイルに対して処理を実行したり属性を設定したりできます。 詳細については、「 [ファイル システム タスク](../../control-flow/file-system-task.md)」をご覧ください。  
  
 キャッシュのオプションを次に示します。  
  
-   参照データセットは、テーブル、ビュー、または SQL クエリを使用して生成され、参照変換が実行される前にキャッシュに読み込まれます。 OLE DB 接続マネージャーを使用して、データセットにアクセスします。  
  
     このキャッシュ オプションは、 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]の参照変換に用意されているフル キャッシュ オプションと互換性があります。  
  
-   参照データセットは、データ フロー内の接続されているデータ ソースまたはキャッシュ ファイルから生成され、参照変換の実行前にキャッシュに読み込まれます。 キャッシュ接続マネージャー (および必要に応じてキャッシュ変換) を使用して、データセットにアクセスします。 詳細については、「 [キャッシュ接続マネージャー](../../connection-manager/cache-connection-manager.md) 」および「 [キャッシュ変換](cache-transform.md)」をご覧ください。  
  
-   参照データセットは、参照変換の実行時に、テーブル、ビュー、または SQL クエリを使用して生成されます。 参照データセットに一致するエントリがある行、およびデータセットに一致するエントリがない行がキャッシュに読み込まれます。  
  
     キャッシュのメモリ サイズを超えると、使用頻度の最も低い行が、参照変換によって自動的にキャッシュから削除されます。  
  
     このキャッシュ オプションは、 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]の参照変換に用意されている部分キャッシュ オプションと互換性があります。  
  
-   参照データセットは、参照変換の実行時に、テーブル、ビュー、または SQL クエリを使用して生成されます。 データはキャッシュされません。  
  
     このキャッシュ オプションは、 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]の参照変換に用意されているキャッシュなしオプションと互換性があります。  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、文字列の比較方法が異なります。 実行前に参照データセットをキャッシュに読み込むように参照変換が構成されている場合、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] によりキャッシュ内で参照比較が行われます。 それ以外の場合、参照操作でパラメーター化 SQL ステートメントが使用され、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により参照比較が行われます。 つまり、キャッシュの種類に応じて、参照変換が、同じ参照テーブルから異なる数の一致結果を返す可能性があります。  
  
## <a name="related-tasks"></a>Related Tasks  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。 詳細については、以下のトピックをご覧ください。  
  
-   [キャッシュなしモードまたは部分キャッシュ モードの参照を実装する](implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [キャッシュ接続マネージャーの変換を使用してフル キャッシュ モードの参照変換を実装する](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [OLE DB 接続マネージャーを使用してフル キャッシュ モードの参照変換を実装する](../../connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   MSDN ライブラリのビデオ「[フル キャッシュ モードで参照変換を実装する方法](https://go.microsoft.com/fwlink/?LinkId=131031)」 (msdn.microsoft.com)  
  
-   blogs.msdn.com のブログ「 [参照変換のキャッシュ モードを使用する際の推奨事項](https://go.microsoft.com/fwlink/?LinkId=146623)」  
  
-   blogs.msdn.com のブログ記事「[参照パターン: 大文字と小文字を区別しない](https://go.microsoft.com/fwlink/?LinkId=157782)」  
  
-   msftisprodsamples.codeplex.com のサンプル「 [参照変換](https://go.microsoft.com/fwlink/?LinkId=267528)」  
  
     [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 製品サンプルとサンプル データベースのインストールの詳細については、「 [SQL Server Integration Services 製品サンプル](https://go.microsoft.com/fwlink/?LinkId=267527)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [あいまい参照変換](fuzzy-lookup-transformation.md)   
 [用語参照変換](term-lookup-transformation.md)   
 [データ フロー](../data-flow.md)   
 [Integration Services の変換](integration-services-transformations.md)  
  
  
