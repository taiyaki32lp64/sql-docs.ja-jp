---
title: 一括挿入タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.bulkinserttask.f1
- sql13.dts.designer.bulkinserttask.connection.f1
- sql13.dts.designer.bulkinserttask.general.f1
- sql13.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert task
- copying data [Integration Services]
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 00c117a2282216f5f326cbf524f3326af5cc93e1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294327"
---
# <a name="bulk-insert-task"></a>一括挿入タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  一括挿入タスクは、大量のデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルまたはビューにコピーするための効率的な方法です。 たとえば、会社で 100 万行の製品リストをメインフレーム システムに格納し、電子商取引システムで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して Web ページを構成しているとします。 また、メインフレームにあるマスター製品リストを使用して、夜間に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の製品テーブルを更新する必要があるものとします。 このテーブルを更新するには、製品リストをタブ区切り形式で保存し、一括挿入タスクを使用してデータを直接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルにコピーします。  
  
 高速なデータ コピーを確実に行うため、コピー元ファイルからテーブルまたはビューへのデータ移動時に、データ変換を行うことはできません。  
  
## <a name="usage-considerations"></a>使用に関する注意点  
 一括挿入タスクを使用する前に、次の点を考慮してください。  
  
-   一括挿入タスクで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたはビューに転送できるのは、テキスト ファイルのデータのみです。 一括挿入タスクを使用して他のデータベース管理システム (DBMS) からデータを転送するには、データをコピー元からテキスト ファイルにエクスポートし、そのテキスト ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたはビューにインポートする必要があります。  
  
-   コピー先は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブルまたはビューである必要があります。 コピー先のテーブルまたはビューに既にデータがある場合、一括挿入タスクが実行されると新しいデータが既存のデータに追加されます。 データを置換する場合は、一括挿入タスクを実行する前に、DELETE または TRUNCATE ステートメントを実行する SQL 実行タスクを実行します。 詳細については、「 [SQL 実行タスク](../../integration-services/control-flow/execute-sql-task.md)」を参照してください。  
  
-   一括挿入タスク オブジェクトではフォーマット ファイルを使用できます。 **bcp** ユーティリティを使用して作成したフォーマット ファイルを使用する場合、一括挿入タスクでフォーマット ファイルのパスを指定できます。 一括挿入タスクでは、XML および XML 以外のフォーマット ファイルの両方がサポートされます。 フォーマット ファイルの使用方法の詳細は、「[データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。  
  
-   一括挿入タスクが含まれるパッケージを実行できるのは、固定サーバー ロール sysadmin のメンバーのみです。  
  
## <a name="bulk-insert-task-with-transactions"></a>トランザクションでの一括挿入タスク  
 バッチ サイズが設定されていないときは、一括コピー操作全体が 1 つのトランザクションとして処理されます。 バッチ サイズが **0** の場合は、データが 1 つのバッチに挿入されます。 バッチ サイズが設定されているときは、各バッチはバッチの実行終了時にコミットされるトランザクションを示します。  
  
 一括挿入タスクがトランザクションに関連付けられている場合、その動作は、パッケージ トランザクションに結合されているかどうかによって異なります。 一括挿入タスクがパッケージ トランザクションに結合する場合、エラーのない各バッチは次のバッチが実行されるまで 1 つの単位としてコミットされます。 一括挿入タスクがパッケージ トランザクションに結合する場合、タスクの実行終了時にエラーのないバッチはそのままトランザクション内に残ります。 これらのバッチは、パッケージのコミットまたはロールバック操作の対象となります。  
  
 一括挿入タスクに失敗した場合、正しく読み込まれたバッチは自動的にロールバックされません。同様に、一括挿入タスクが成功した場合でも、これらのバッチは自動的にコミットされません。 コミットとロールバックの各操作は、パッケージおよびワークフローのプロパティ設定で指定されている場合に限り発生します。  
  
## <a name="source-and-destination"></a>コピー元とコピー先  
 コピー元のテキスト ファイルの場所を指定するときは、次の点を考慮してください。  
  
-   サーバーには、コピー元ファイルおよびコピー先データベースの両方にアクセスする権限が必要です。  
  
-   一括挿入タスクはサーバーで実行されます。 したがって、タスクが使用するすべてのフォーマット ファイルは、そのサーバー上に存在する必要があります。  
  
-   一括挿入タスクが読み込むコピー元ファイルの場所は、データ挿入先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースと同じサーバー上でも、リモート サーバー上でもかまいません。 コピー元ファイルがリモート サーバー上にある場合、汎用名前付け規則 (UNC) を使用して、ファイル名をパスで指定する必要があります。  
  
## <a name="performance-optimization"></a>パフォーマンスの最適化  
 パフォーマンスを最適化するには、次のことを考慮してください。  
  
-   テキスト ファイルがデータの挿入先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースと同じコンピューター上にある場合、データがネットワーク経由で転送されないため、コピー操作の実行速度がいっそう速くなります。  
  
-   一括挿入タスクでは、エラーが発生した行はログに記録されません。 この情報を取得する必要がある場合は、データ フロー コンポーネントのエラー出力を使用すれば、エラーが発生した行を例外ファイルにキャプチャできます。  
  
## <a name="custom-log-entries-available-on-the-bulk-insert-task"></a>一括挿入タスクで使用できるカスタム ログ エントリ  
 次の表は、一括挿入タスクのカスタム ログ エントリの一覧です。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**BulkInsertTaskBegin**|一括挿入が開始されたことを示します。|  
|**BulkInsertTaskEnd**|一括挿入が終了したことを示します。|  
|**BulkInsertTaskInfos**|タスクに関する説明情報を提供します。|  
  
## <a name="bulk-insert-task-configuration"></a>一括挿入タスクの構成  
 一括挿入タスクは、次の方法で構成できます。  
  
-   コピー先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース、およびデータを挿入するテーブルまたはビューに接続する OLE DB 接続マネージャーを指定します。 一括挿入タスクでは、コピー先データベースに対して OLE DB 接続のみをサポートします。  
  
-   ファイルまたはフラット ファイル接続マネージャーを指定して、コピー元ファイルにアクセスします。 一括挿入タスクは、コピー元ファイルの場所にのみ接続マネージャーを使用します。 接続マネージャー エディターでその他のオプションを選択しても、一括挿入タスクでは無視されます。  
  
-   フォーマット ファイルを使用するか、またはコピー元データの列区切り記号と行区切り記号を定義して、一括挿入タスクで使用するフォーマットを定義します。 フォーマット ファイルを使用する場合は、フォーマット ファイルにアクセスするファイル接続マネージャーを指定します。  
  
-   タスクでデータを挿入する場合、挿入先のテーブルまたはビューで実行するアクションを指定します。 オプションとして、CHECK 制約の有効化、ID 挿入の許可、NULL の保持、トリガーの起動、またはテーブルのロックを選択できます。  
  
-   挿入するデータのバッチに関する情報を設定します。たとえば、バッチ サイズ、挿入するファイルの先頭行と最終行、行の挿入を停止せずにタスクを実行できる挿入エラーの最大数、並べ替えの対象となる列の名前などです。  
  
 一括挿入タスクでフラット ファイル接続マネージャーを使用してコピー元ファイルにアクセスする場合、タスクはフラット ファイル接続マネージャーで指定されたフォーマットを使用しません。 その代わり、フォーマット ファイルに指定されたフォーマットか、またはタスクの RowDelimiter プロパティおよび ColumnDelimiter プロパティの値が一括挿入タスクで使用されます。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="programmatic-configuration-of-the-bulk-insert-task"></a>プログラムによる一括挿入タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   support.microsoft.com の技術記事「 [UAC 対応システムで "データを挿入するための SSIS 一括挿入を準備できません" というエラーが発生することがある](https://go.microsoft.com/fwlink/?LinkId=233693)」  
  
-   msdn.microsoft.com の技術記事: [Integration Services のパフォーマンス チューニング技法](https://go.microsoft.com/fwlink/?LinkId=233700)  
  
-   simple-talk.com の技術記事: [SQL Server Integration Services を使用してデータの一括読み込みを行う](https://go.microsoft.com/fwlink/?LinkId=233701)  
  
## <a name="bulk-insert-task-editor-connection-page"></a>[一括挿入タスク エディター] ([接続] ページ)
  **[一括挿入タスク エディター]** ダイアログ ボックスの **[接続]** ページを使用すると、一括挿入操作の挿入元と挿入先、および使用するフォーマットを指定できます。  
  
 一括挿入操作の詳細については、「[Bulk Insert Task](../../integration-services/control-flow/bulk-insert-task.md)」(一括挿入タスク) と「[データのインポートまたはエクスポート用のフォーマット ファイル (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[接続]**  
 OLE DB 接続マネージャーを一覧から選択するか、[\<**新しい接続...** >] をクリックして新しい接続を作成します。  
  
 **関連トピック:** [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
 **[DestinationTable]**  
 挿入先のテーブルまたはビューの名前を入力するか、テーブルまたはビューを一覧から選択します。  
  
 **Format**  
 一括挿入のフォーマットの挿入元を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[ファイルを使用]**|フォーマット指定が格納されているファイルを選択します。 このオプションを選択すると、動的オプションの **[FormatFile]** が表示されます。|  
|**[指定]**|フォーマットを指定します。 このオプションを選択すると、動的オプションの **[RowDelimiter]** および **[ColumnDelimiter]** が表示されます。|  
  
 **[最近使ったファイル]**  
 ファイル接続マネージャーまたはフラット ファイル接続マネージャーを一覧から選択するか、[\<**新しい接続...** >] をクリックして新しい接続を作成します。  
  
 このファイルの場所は、このタスクの接続マネージャーに指定されている SQL Server データベース エンジンを基準とする相対パスです。 SQL Server データベース エンジンは、サーバーのローカル ハード ドライブ、共有、または SQL Server にマップされたドライブでこのテキスト ファイルにアクセスできる必要があります。 SSIS ランタイムはこのファイルにアクセスしません。  
  
 フラット ファイル接続マネージャーを使用してソース ファイルにアクセスした場合、フラット ファイル接続マネージャーに指定されたフォーマットは一括挿入タスクで使用されません。 その代わり、フォーマット ファイルに指定されたフォーマットか、またはタスクの RowDelimiter プロパティおよび ColumnDelimiter プロパティの値が一括挿入タスクで使用されます。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md) 
  
 **[テーブルの更新]**  
 データベースおよびビューの一覧を更新します。  
  
### <a name="format-dynamic-options"></a>[Format] の動的オプション  
  
#### <a name="format--use-file"></a>[Format] = [ファイルを使用]  
 **[FormatFile]**  
 フォーマット ファイルのパスを入力します。または、参照ボタン **[...]** をクリックし、フォーマット ファイルを指定します。  
  
#### <a name="format--specify"></a>[Format] = [指定]  
 **[RowDelimiter]**  
 ソース ファイルの行区切り記号を指定します。 既定値は **{CR}{LF}** です。  
  
 **[ColumnDelimiter]**  
 ソース ファイルの列区切り記号を指定します。 既定値は **[タブ]** です。  
  
## <a name="bulk-insert-task-editor-general-page"></a>[一括挿入タスク エディター] ([全般] ページ)
  **[一括挿入タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用して、一括挿入タスクの名前と説明を指定します。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 一括挿入タスクに一意の名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 一括挿入タスクの説明を入力します。  
 
## <a name="bulk-insert-task-editor-options-page"></a>[一括挿入タスク エディター] ([オプション] ページ)
  **[一括挿入タスク エディター]** ダイアログ ボックスの **[オプション]** ページを使用すると、一括挿入操作のプロパティを設定できます。 一括挿入タスクにより、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルまたはビューに大量のデータがコピーされます。  
  
 一括挿入タスクについては、「[一括挿入タスク](../../integration-services/control-flow/bulk-insert-task.md)」および「[「BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **CodePage**  
 データ ファイル内のデータのコード ページを指定します。  
  
 **[DataFileType]**  
 読み込み操作で使用するデータ型の値を指定します。  
  
 **BatchSize**  
 バッチ内の行数を指定します。 既定では、データ ファイル全体です。 **[BatchSize]** を 0 に設定すると、データは単一のバッチに読み込まれます。  
  
 **[LastRow]**  
 コピーする最後の行を指定します。  
  
 **[FirstRow]**  
 コピーを開始する最初の行を指定します。  
  
 **[一括挿入タスク エディター]**  
 |項目|定義|  
|----------|----------------|  
|**CHECK 制約**|テーブルおよび列に対する制約をチェックします。|  
|**[NULL を保持する]**|空の列に任意の既定値を挿入する代わりに、一括挿入操作中に NULL 値を保持します。|  
|**[ID 挿入を許可する]**|ID 列に既存の値を挿入します。|  
|**[テーブル ロック]**|一括挿入中にテーブルをロックします。|  
|**[トリガーを起動する]**|テーブル上のすべての挿入トリガー、更新トリガー、および削除トリガーを起動します。|  
  
 **SortedData**  
 一括挿入ステートメントに ORDER BY 句を指定します。 指定する列名は、挿入先テーブル内の有効な列でなければなりません。 既定値は **false**です。 これは、データが ORDER BY 句によって並べ替えられないことを意味します。  
  
 **[MaxErrors]**  
 一括挿入操作が取り消されるまでに発生が許可される最大エラー数を指定します。 0 の値は、許可されるエラー数が無制限であることを示します。  
  
> [!NOTE]  
>  一括読み込み操作でインポートできない行は、1 つのエラーとしてカウントされます。  
  
