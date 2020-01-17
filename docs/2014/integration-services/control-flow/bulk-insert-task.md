---
title: 一括挿入タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.f1
helpviewer_keywords:
- Bulk Insert task
- copying data [Integration Services]
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9b5da9ff28dc658f870033a02fe88b14ea442c51
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832874"
---
# <a name="bulk-insert-task"></a>一括挿入タスク
  一括挿入タスクは、大量のデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルまたはビューにコピーするための効率的な方法です。 たとえば、会社で 100 万行の製品リストをメインフレーム システムに格納し、電子商取引システムで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して Web ページを構成しているとします。 また、メインフレームにあるマスター製品リストを使用して、夜間に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の製品テーブルを更新する必要があるものとします。 このテーブルを更新するには、製品リストをタブ区切り形式で保存し、一括挿入タスクを使用してデータを直接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルにコピーします。  
  
 高速なデータ コピーを確実に行うため、コピー元ファイルからテーブルまたはビューへのデータ移動時に、データ変換を行うことはできません。  
  
## <a name="usage-considerations"></a>使用に関する注意点  
 一括挿入タスクを使用する前に、次の点を考慮してください。  
  
-   一括挿入タスクで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたはビューに転送できるのは、テキスト ファイルのデータのみです。 一括挿入タスクを使用して他のデータベース管理システム (DBMS) からデータを転送するには、データをコピー元からテキスト ファイルにエクスポートし、そのテキスト ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたはビューにインポートする必要があります。  
  
-   コピー先は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブルまたはビューである必要があります。 コピー先のテーブルまたはビューに既にデータがある場合、一括挿入タスクが実行されると新しいデータが既存のデータに追加されます。 データを置換する場合は、一括挿入タスクを実行する前に、DELETE または TRUNCATE ステートメントを実行する SQL 実行タスクを実行します。 詳細については、「 [SQL 実行タスク](execute-sql-task.md)」を参照してください。  
  
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
 次の表は、一括挿入タスクのカスタム ログ エントリの一覧です。 詳細については、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」を参照してください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`BulkInsertTaskBegin`|一括挿入が開始されたことを示します。|  
|`BulkInsertTaskEnd`|一括挿入が終了したことを示します。|  
|`BulkInsertTaskInfos`|タスクに関する説明情報を提供します。|  
  
## <a name="bulk-insert-task-configuration"></a>一括挿入タスクの構成  
 一括挿入タスクは、次の方法で構成できます。  
  
-   コピー先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース、およびデータを挿入するテーブルまたはビューに接続する OLE DB 接続マネージャーを指定します。 一括挿入タスクでは、コピー先データベースに対して OLE DB 接続のみをサポートします。  
  
-   ファイルまたはフラット ファイル接続マネージャーを指定して、コピー元ファイルにアクセスします。 一括挿入タスクは、コピー元ファイルの場所にのみ接続マネージャーを使用します。 接続マネージャー エディターでその他のオプションを選択しても、一括挿入タスクでは無視されます。  
  
-   フォーマット ファイルを使用するか、またはコピー元データの列区切り記号と行区切り記号を定義して、一括挿入タスクで使用するフォーマットを定義します。 フォーマット ファイルを使用する場合は、フォーマット ファイルにアクセスするファイル接続マネージャーを指定します。  
  
-   タスクでデータを挿入する場合、挿入先のテーブルまたはビューで実行するアクションを指定します。 オプションとして、CHECK 制約の有効化、ID 挿入の許可、NULL の保持、トリガーの起動、またはテーブルのロックを選択できます。  
  
-   挿入するデータのバッチに関する情報を設定します。たとえば、バッチ サイズ、挿入するファイルの先頭行と最終行、行の挿入を停止せずにタスクを実行できる挿入エラーの最大数、並べ替えの対象となる列の名前などです。  
  
 一括挿入タスクでフラット ファイル接続マネージャーを使用してコピー元ファイルにアクセスする場合、タスクはフラット ファイル接続マネージャーで指定されたフォーマットを使用しません。 その代わり、フォーマット ファイルに指定されたフォーマットか、またはタスクの RowDelimiter プロパティおよび ColumnDelimiter プロパティの値が一括挿入タスクで使用されます。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [一括挿入タスク エディター &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [一括挿入タスク エディター &#40;[接続] ページ&#41;](../bulk-insert-task-editor-connection-page.md)  
  
-   [一括挿入タスク エディター &#40;[オプション] ページ&#41;](../bulk-insert-task-editor-options-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="programmatic-configuration-of-the-bulk-insert-task"></a>プログラムによる一括挿入タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   support.microsoft.com の技術記事「 [UAC 対応システムで "データを挿入するための SSIS 一括挿入を準備できません" というエラーが発生することがある](https://go.microsoft.com/fwlink/?LinkId=233693)」  
  
-   msdn.microsoft.com の技術記事: [Integration Services のパフォーマンス チューニング技法](https://go.microsoft.com/fwlink/?LinkId=233700)  
  
-   simple-talk.com の技術記事: [SQL Server Integration Services を使用してデータの一括読み込みを行う](https://go.microsoft.com/fwlink/?LinkId=233701)  
  
  
