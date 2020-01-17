---
title: SQL Server 変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlserverdest.f1
- sql13.dts.designer.sqlserverdestadapter.connection.f1
- sql13.dts.designer.sqlserverdestadapter.mappings.f1
- sql13.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: a0227cd8-6944-4547-87e8-7b2507e26442
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 481cac0715f00c7d29a92b77101c4a09a28056a6
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298047"
---
# <a name="sql-server-destination"></a>SQL Server 変換先

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SQL Server 変換先はローカルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続し、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたはビューに一括で読み込みます。 SQL Server 変換先は、リモート サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにアクセスするパッケージでは使用できません。 代わりに、このパッケージでは OLE DB 変換先を使用する必要があります。 詳細については、「 [OLE DB 変換先](../../integration-services/data-flow/ole-db-destination.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 SQL Server 変換先が含まれたパッケージを実行するユーザーには、"グローバル オブジェクトの作成" 権限が許可されている必要があります。 **[管理ツール]** のローカル セキュリティ ポリシー ツールを使用することにより、この権限をユーザーに許可できます。 SQL Server 変換先を使用するパッケージの実行時にエラー メッセージが表示された場合は、パッケージを実行しているアカウントに "グローバル オブジェクトの作成" 権限が許可されていることを確認してください。  
  
## <a name="bulk-inserts"></a>一括挿入  
 SQL Server 変換先を使用してリモートの SQL Server データベースにデータを一括読み込みしようとすると、次のようなエラー メッセージが表示されることがあります。"OLE DB レコードを使用できます。 ソース:"Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client" Hresult: 0x80040E14 説明: "SSIS ファイル マッピング オブジェクト 'Global\DTSQLIMPORT' を開けなかったので、一括読み込みできませんでした。 オペレーティング システム エラー コード 2 (指定されたファイルが見つかりません)。 Windows セキュリティ経由でローカル サーバーにアクセスしていることを確認してください。""  
  
 SQL Server 変換先で行われるのは、一括挿入タスクで行われるものと同じ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への高速なデータ挿入です。ただし、パッケージで SQL Server 変換先を使用することによって、データが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に読み込まれる前に変換を列データに適用できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にデータを読み込む場合は、OLE DB 変換先ではなく SQL Server 変換先を使用することをお勧めします。  
  
### <a name="bulk-insert-options"></a>一括挿入オプション  
 SQL Server 変換先で高速読み込みデータ アクセス モードを使用する場合、次の高速読み込みオプションを指定できます。  
  
-   インポートしたデータ ファイルの ID 値を保持します。または、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって割り当てられた一意の値を使用します。  
  
-   一括読み込み操作中に、NULL 値を保持します。  
  
-   一括インポート操作中に、インポート先のテーブルまたはビュー上の制約を確認します。  
  
-   一括読み込み操作中に、テーブルレベルのロックを取得します。  
  
-   一括読み込み操作中に、変換先のテーブル上で定義されている挿入トリガーを実行します。  
  
-   一括挿入操作中に読み込む、入力の最初の行番号を指定します。  
  
-   一括挿入操作中に読み込む、入力の最後の行番号を指定します。  
  
-   一括読み込み操作が取り消されるまでに許可されるエラーの最大数を指定します。 インポートできない各行は、エラーとしてカウントされます。  
  
-   並べ替えられたデータが含まれる入力内の列を指定します。  
  
 一括読み込みオプションの詳細については、「[BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)」を参照してください。  
  
#### <a name="performance-improvements"></a>パフォーマンスの強化  
 一括挿入、および一括挿入操作中のテーブル データへのアクセスのパフォーマンスを向上するには、既定のオプションを次のように変更する必要があります。  
  
-   一括インポート操作中に、インポート先のテーブルまたはビュー上の制約を確認しません。  
  
-   一括読み込み操作中に、変換先のテーブル上で定義されている挿入トリガーを実行しません。  
  
-   ロックをテーブルに適用しません。 これにより、一括挿入操作中、他のユーザーおよびアプリケーションはテーブルを引き続き使用できます。  
  
## <a name="configuration-of-the-sql-server-destination"></a>SQL Server 変換先の構成  
 SQL Server 変換先は、次の方法で構成できます。  
  
-   データの一括読み込み先となるテーブルまたはビューを指定します。  
  
-   CHECK 制約を実行するかどうかなどのオプションを指定することにより、一括読み込み操作をカスタマイズします。  
  
-   同じバッチ内ですべての行をコミットするか、バッチとしてコミットする行の最大数を設定するかのいずれかを指定します。  
  
-   一括読み込み操作のタイムアウトを指定します。  
  
 この変換先は、OLE DB 接続マネージャーを使用してデータ ソースに接続します。OLE DB 接続マネージャーでは、使用する OLE DB プロバイダーを指定します。 詳細については、「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトでは、OLE DB 接続マネージャーを作成できるデータ ソース オブジェクトも用意されます。 これにより、SQL Server 変換先でデータ ソースとデータ ソース ビューが使用できるようになります。  
  
 SQL Server 変換先は 1 つの入力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [SQL Server 変換先のカスタム プロパティ](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [SQL Server 変換先を使用してデータの一括読み込みを行う](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [SQL Server 変換先を使用してデータの一括読み込みを行う](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   support.microsoft.com の技術記事「 [UAC 対応システムで "データを挿入するための SSIS 一括挿入を準備できません" というエラーが発生することがある](https://go.microsoft.com/fwlink/?LinkId=199482)」  
  
-   msdn.microsoft.com の技術記事: [Integration Services のパフォーマンス チューニング技法](https://go.microsoft.com/fwlink/?LinkId=233700)  
  
-   simple-talk.com の技術記事: [SQL Server Integration Services を使用してデータの一括読み込みを行う](https://go.microsoft.com/fwlink/?LinkId=233701)  
  
## <a name="sql-destination-editor-connection-manager-page"></a>[SQL 変換先エディター] ([接続マネージャー] ページ)
  **[SQL 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、データ ソース情報を指定したり、結果をプレビューしたりできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先エディターは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブルまたはビューにデータを読み込みます。  
  
### <a name="options"></a>オプション  
 **[キャッシュなし]**  
 一覧から既存の接続を選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 **[テーブルまたはビューを使用する]**  
 既存のテーブルまたはビューを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して新しいテーブルを作成します。  
  
> [!NOTE]  
>  **[新規作成]** をクリックすると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
 **プレビュー**  
 **[クエリ結果のプレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
## <a name="sql-destination-editor-mappings-page"></a>[SQL 変換先エディター] ([マッピング] ページ)
  **[SQL 変換先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用すると、入力列を変換先列にマップできます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる入力列を変換先列にマップします。  
  
 **使用できる変換先列**  
 使用できる変換先列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる変換先列を入力列にマップします。  
  
 **入力列**  
 上の表で選択された入力列が表示されます。 **[使用できる入力列]** ボックスの一覧を使用して、マッピングを変更できます。  
  
 **変換先列**  
 マップされているかどうかに関係なく、使用できる変換先列を表示します。  
  
## <a name="sql-destination-editor-advanced-page"></a>[SQL 変換先エディター] ([詳細設定] ページ)
  **[SQL 変換先エディター]** ダイアログ ボックスの **[詳細設定]** ページを使用すると、詳細な一括挿入オプションを指定できます。  
  
### <a name="options"></a>オプション  
 **[ID を保持する]**  
 タスクが値を ID 列に挿入するかどうかを指定します。 このプロパティの既定値は **False**です。  
  
 **[NULL を保持する]**  
 タスクが NULL 値を保持するかどうかを指定します。 このプロパティの既定値は **False**です。  
  
 **[テーブル ロック]**  
 データが読み込まれるときにテーブルをロックするかどうかを指定します。 このプロパティの既定値は **True**です。  
  
 **CHECK 制約**  
 タスクが制約をチェックするかどうかを指定します。 このプロパティの既定値は **True**です。  
  
 **[トリガーを起動する]**  
 テーブルにおける一括挿入でトリガーを起動するかどうかを指定します。 このプロパティの既定値は **False**です。  
  
 **[先頭行]**  
 先頭行が挿入されるように指定します。 このプロパティの既定値は、 **-1**です。これは、値が割り当てられていないことを示します。  
  
> [!NOTE]  
>  このプロパティに値を割り当てない場合、 **[SQL 変換先エディター]** のテキスト ボックスをクリアします。 **[プロパティ]** ウィンドウ、 **[詳細エディター]** 、およびオブジェクト モデルでは、-1 を使用します。  
  
 **[最終行]**  
 最終行が挿入されるように指定します。 このプロパティの既定値は、 **-1**です。これは、値が割り当てられていないことを示します。  
  
> [!NOTE]  
>  このプロパティに値を割り当てない場合、 **[SQL 変換先エディター]** のテキスト ボックスをクリアします。 **[プロパティ]** ウィンドウ、 **[詳細エディター]** 、およびオブジェクト モデルでは、-1 を使用します。  
  
 **[エラーの最大数]**  
 一括挿入を停止する前に許容するエラー数を指定します。 このプロパティの既定値は、 **-1**です。これは、値が割り当てられていないことを示します。  
  
> [!NOTE]  
>  このプロパティに値を割り当てない場合、 **[SQL 変換先エディター]** のテキスト ボックスをクリアします。 **[プロパティ]** ウィンドウ、 **[詳細エディター]** 、およびオブジェクト モデルでは、-1 を使用します。  
  
 **Timeout**  
 タイムアウトで一括挿入が停止されるまでの待機時間を秒数で指定します。  
  
 **[列の順序]**  
 キー列の名前を入力します。 各列は、昇順または降順で並べ替えることができます。 複数のキー列を使用する場合は、リストをコンマで区切ります。  
  
## <a name="see-also"></a>参照  
 [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
  
