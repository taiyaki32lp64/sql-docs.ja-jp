---
title: Foreach ループ エディター (コレクション ページ) |Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.collection.f1
ms.assetid: 95a19dde-61ca-4d9b-aa3d-131fa4264296
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5b9396ab5a25bba979859ac685c4759b8b01c24d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66428798"
---
# <a name="foreach-loop-editor-collection-page"></a>[Foreach ループ エディター] ([コレクション] ページ)
  **[Foreach ループ エディター]** ダイアログ ボックスの **[コレクション]** ページを使用すると、列挙子の型を指定して列挙子を構成できます。  
  
 Foreach ループ コンテナーとその構成方法については、「 [Foreach ループ コンテナー](control-flow/foreach-loop-container.md) 」と「 [Foreach ループ コンテナーを構成する](../../2014/integration-services/configure-a-foreach-loop-container.md)」を参照してください。  
  
## <a name="static-options"></a>静的オプション  
 **列挙子**  
 列挙子の型を一覧から選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|説明|  
|-----------|-----------------|  
|**[Foreach File 列挙子]**|ファイルを列挙します。 この値を選択すると、セクション **[Foreach File 列挙子]** に動的オプションが表示されます。|  
|**[Foreach Item 列挙子]**|アイテム内の値を列挙します。 この値を選択すると、セクション **[Foreach Item 列挙子]** に動的オプションが表示されます。|  
|**[Foreach ADO 列挙子]**|テーブルまたはテーブル内の行を列挙します。 この値を選択すると、セクション **[Foreach ADO 列挙子]** に動的オプションが表示されます。|  
|**[Foreach ADO.NET Schema Rowset 列挙子]**|スキーマを列挙します。 この値を選択すると、セクション **[Foreach ADO.NET Schema Rowset 列挙子]** に動的オプションが表示されます。|  
|**[Foreach From Variable 列挙子]**|変数内の値を列挙します。 この値を選択すると、セクション **[Foreach From Variable 列挙子]** に動的オプションが表示されます。|  
|**[Foreach Nodelist 列挙子]**|XML ドキュメント内のノードを列挙します。 この値を選択すると、セクション **[Foreach NodeList 列挙子]** に動的オプションが表示されます。|  
|**[ForEach SMO 列挙子]**|SMO オブジェクトを列挙します。 この値を選択すると、セクション **[Foreach SMO 列挙子]** に動的オプションが表示されます。|  
|**[Foreach Azure Blob 列挙子]**|指定された BLOB の場所に BLOB ファイルを列挙します。 この値を選択すると、セクション **[Foreach Azure Blob 列挙子]** に動的オプションが表示されます。|  
|**[Foreach ADLS File 列挙子]**|フィルターを使用して ADLS にファイルを列挙します。 この値を選択すると、セクション **[Foreach ADLS File 列挙子]** に動的オプションが表示されます。|
  
 **式**  
 **[式]** をクリックして展開すると、既存のプロパティ式のリストが表示されます。 参照ボタン ( **[...]** ) ボタンをクリックして、列挙子プロパティのプロパティ式を追加するか、既存のプロパティ式を編集して評価します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md)、[プロパティ式エディター](expressions/property-expressions-editor.md)、[式ビルダー](expressions/expression-builder.md)  
  
## <a name="enumerator-dynamic-options"></a>列挙子の動的オプション  
  
### <a name="enumerator--foreach-file-enumerator"></a>[Enumerator] = [Foreach File 列挙子]  
 Foreach File 列挙子を使用して、フォルダー内のファイルを列挙します。 たとえば、Foreach ループに SQL 実行タスクが含まれている場合、Foreach File 列挙子を使用して、SQL 実行タスクが実行する SQL ステートメントが含まれているファイルを列挙できます。 この列挙子は、サブフォルダーが含められるように構成することができます。  
  
 Foreach File 列挙子が列挙するフォルダーとサブフォルダーの内容は、ループの実行中に変化する場合があります。これは、外部プロセスまたはループ内のタスクによって、ループの実行時にファイルの追加、名前変更、または削除が発生するためです。 これは、次のような予期しない状況が発生する可能性を意味しています。  
  
-   ファイルが削除された場合、Foreach ループ内の 1 つのタスクで使用されたものとは異なるファイルのセットが、それ以降のタスクで使用される可能性があります。  
  
-   ファイルの名前が変更され、それらのファイルを置き換えるためのファイルが外部プロセスによって自動的に追加されると、Foreach ループは同じファイル コンテンツに対して 2 回作業を実行することになる可能性があります。  
  
-   ファイルが追加されると、Foreach ループがどのファイルに対して作業を実行したか判断することが困難になる可能性があります。  
  
 **フォルダー**  
 列挙するルート フォルダーのパスを示します。  
  
 **[参照]**  
 ルート フォルダーの場所を参照して指定します。  
  
 **[ファイル]**  
 列挙するファイルを指定します。  
  
> [!NOTE]  
>  ワイルドカード文字 (*) を使用して、コレクションに含めるファイルを指定します。 たとえば、名前に "abc" が含まれているファイルを追加するには、\*abc\* というフィルターを使用します。  
>   
>  ファイル名の拡張子を指定すると、列挙子は、文字が追加された同じ拡張子のファイルも返します (これは、旧バージョンとの互換性のために 8.3 ファイル名も比較する、オペレーティング システムの **dir** コマンドと同じ動作です)。この列挙子の動作は、予期しない結果になる場合があります。 たとえば、Excel 2003 ファイルのみを列挙する場合は「*.xls」と指定しますが、 列挙子は Excel 2007 のファイルも返します。これらのファイルの拡張子が ".xlsx" であるためです。  
>   
>  コレクションに追加するファイルを式で指定するには、 **[コレクション]** ページの **[式]** を展開し、 **[FileSpec]** プロパティを選択して参照ボタン ( […] ) をクリックし、プロパティ式を追加します。 指定したファイルの動的選択の詳細については、次を参照してください。[ファイル マスクの SSIS 動的設定。FileSpec](https://rajsudeep.blogspot.com/2010/09/ssisdynamically-set-file-mask-filespec.html)  
  
 **[完全修飾名]**  
 ファイル名の完全修飾パスを取得する場合に選択します。 [ファイル] オプションにワイルドカード文字が指定されている場合、返された完全修飾パスはフィルターに一致します。  
  
 **[テーブル名のみ]**  
 ファイル名のみを取得する場合に選択します。 [ファイル] オプションにワイルドカード文字が指定されている場合、返されたファイル名はフィルターに一致します。  
  
 **[ファイル名と拡張子]**  
 ファイル名とファイル名拡張子を取得する場合に選択します。 [ファイル] オプションにワイルドカード文字が指定されている場合、返されたファイル名および拡張子はフィルターに一致します。  
  
 **[サブフォルダーをスキャンする]**  
 列挙にサブフォルダーを含める場合に選択します。  
  
### <a name="enumerator--foreach-item-enumerator"></a>[Enumerator] = [Foreach Item 列挙子]  
 Foreach Item 列挙子は、コレクション内のアイテムを列挙するために使用します。 コレクション内のアイテムは、列と列の値を指定して定義します。 行内の各列は個々のアイテムを定義します。 たとえば、プロセス実行タスクで実行される実行可能ファイルとそのタスクで使用される作業ディレクトリを指定するアイテムに 2 つの列を割り当て、1 列は実行可能ファイルの名前、もう 1 列は作業ディレクトリの表示に使用できます。 行数により、ループが繰り返される回数が決まります。 テーブルに 10 行ある場合は、ループが 10 回繰り返されます。  
  
 プロセス実行タスクのプロパティを更新するには、列のインデックスを使用してアイテムの列に変数をマップします。 列挙子のアイテムで定義される最初の列のインデックス値は 0、2 番目の列のインデックス値は 1 になり、それ以降も順番にインデックス値が割り当てられます。 変数の値は、ループが繰り返されるたびに更新されます。 プロセス実行タスクの `Executable` プロパティと `WorkingDirectory` プロパティは、これらの変数を使用するプロパティ式で更新できます。  
  
 **[For Each Item コレクションのアイテムの定義]**  
 テーブル内の各列に値を提供します。  
  
> [!NOTE]  
>  値を行列に入力した後で、新しい行がテーブルに自動的に追加されます。  
  
> [!NOTE]  
>  提供された値が列データ型と互換性がない場合、テキストは赤になります。  
  
 **[列データ型]**  
 アクティブな列のデータ型を一覧表示します。  
  
 **[削除]**  
 アイテムを一覧から削除するには、そのアイテムを選択してから **[削除]** をクリックします。  
  
 **[列]**  
 アイテム内の列のデータ型を構成する場合にクリックします。  
  
 **関連トピック:** [[For Each Item 列] ダイアログ ボックスの UI リファレンス](../../2014/integration-services/for-each-item-columns-dialog-box-ui-reference.md)  
  
### <a name="enumerator--foreach-ado-enumerator"></a>[Enumerator] = [Foreach ADO 列挙子]  
 Foreach ADO 列挙子は、変数に格納されている ADO オブジェクトまたは ADO.NET オブジェクト内の行またはテーブルを列挙するために使用します。 たとえば、変数にデータセットを書き込むスクリプト タスクが Foreach ループに含まれている場合、Foreach ADO 列挙子を使用して、データセット内の行を列挙できます。 変数に ADO.NET データセットが格納されている場合は、複数のテーブル内の行を列挙するか、テーブルを列挙するようにこの列挙子を構成できます。  
  
 **[ADO オブジェクト ソース変数]**  
 ユーザー定義変数を一覧から選択するか、\< **[新しい変数...]** をクリックして新しい変数を作成します。  
  
> [!NOTE]  
>  変数は、Object データ型にする必要があります。それ以外の場合はエラーが発生します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、[変数の追加](../../2014/integration-services/add-variable.md)  
  
 **[最初のテーブル内の行]**  
 最初のテーブルの行のみを列挙する場合に選択します。  
  
 **[すべてのテーブルの行 (ADO.NET のデータセットのみ)]**  
 すべてのテーブルの行を列挙する場合に選択します。 このオプションは、列挙するオブジェクトがすべて同じ ADO.NET データセットのメンバーである場合にのみ使用できます。  
  
 **[すべてのテーブル (ADO.NET のデータセットのみ)]**  
 テーブルのみを列挙する場合に選択します。  
  
### <a name="enumerator--foreach-adonet-schema-rowset-enumerator"></a>[Enumerator] = [Foreach ADO.NET Schema Rowset 列挙子]  
 Foreach ADO.NET Schema Rowset 列挙子は、指定したデータ ソースのスキーマを列挙するために使用します。 たとえば、Foreach ループに SQL 実行タスクが含まれている場合、Foreach ADO.NET Schema Rowset 列挙子を使用して、 **AdventureWorks** データベース内の列や、スキーマ権限を取得するための SQL 実行タスクなど、スキーマを列挙できます。  
  
 **Connection**  
 ADO.NET 接続マネージャーを一覧から選択するか、[\<**新しい接続...** >] をクリックして ADO.NET 接続マネージャーを作成します。  
  
> [!IMPORTANT]  
>  ADO.NET 接続マネージャーでは、OLE DB の .NET プロバイダーを使用する必要があります。 SQL Server に接続する場合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client の使用をお勧めします。このプロバイダーは、 **[接続マネージャー]** ダイアログ ボックスの **[OleDb の .Net プロバイダー]** セクションに一覧表示されます。  
  
 **関連トピック:** [ADO 接続マネージャー](connection-manager/ado-connection-manager.md)、[ADO.NET の接続マネージャーの構成](configure-ado-net-connection-manager.md)  
  
 **[スキーマ]**  
 列挙するスキーマを選択します。  
  
 **[制限の設定]**  
 指定したスキーマに適用する制約を設定します。  
  
 **関連トピック:** [[スキーマの制限] ダイアログ ボックス](../../2014/integration-services/schema-restrictions-dialog-box.md)  
  
### <a name="enumerator--foreach-from-variable-enumerator"></a>[Enumerator] = [Foreach From Variable 列挙子]  
 Foreach From Variable 列挙子は、指定した変数に含まれる列挙可能なオブジェクトを列挙するために使用します。 たとえば、クエリを実行し、その結果を変数に格納する SQL 実行タスクが Foreach ループに含まれている場合、Foreach From Variable 列挙子を使用してクエリの結果を列挙できます。  
  
 **変数**  
 一覧で変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、[変数の追加](../../2014/integration-services/add-variable.md)  
  
### <a name="enumerator--foreach-nodelist-enumerator"></a>[Enumerator] = [Foreach NodeList 列挙子]  
 Foreach Nodelist 列挙子は、XPath 式を XML ファイルに適用した結果として生成された XML ノードのセットを列挙するために使用します。 たとえば、Foreach ループにスクリプト タスクが含まれている場合、Foreach NodeList 列挙子を使用して、XPath 式の条件を満たす値を XML ファイルからスクリプト タスクに渡すことができます。  
  
 XML ファイルに適用される XPath 式は、OuterXPathString プロパティに格納された外部 XPath 操作です。 XPath 列挙型に設定されている場合`ElementCollection`、Foreach NodeList 列挙子は、要素のコレクションに、InnerXPathString プロパティに格納されている、内部 XPath 式を適用できます。  
  
 XML ドキュメントとデータの操作の詳細については、MSDN ライブラリの「[.NET Framework における XML の使用](https://go.microsoft.com/fwlink/?LinkId=56214)」を参照してください。  
  
 **[DocumentSourceType]**  
 XML ドキュメントのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|説明|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 **[DocumentSource]**  
 **[DocumentSourceType]** が **[直接入力]** に設定されている場合は、XML コードを入力するか、 **[ドキュメント ソース エディター]** ダイアログ ボックスで参照ボタン ([...]) をクリックして XML を指定します。  
  
 **[DocumentSourceType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **[DocumentSourceType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、[変数の追加](../../2014/integration-services/add-variable.md)。  
  
 **[EnumerationType]**  
 一覧から列挙型を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|説明|  
|-----------|-----------------|  
|**[Navigator]**|XPathNavigator を使用して列挙します。|  
|**[Node]**|XPath 操作によって返されたノードを列挙します。|  
|**[NodeText]**|XPath 操作によって返されたテキスト ノードを列挙します。|  
|`ElementCollection`|XPath 操作によって返された要素ノードを列挙します。|  
  
 **[OuterXPathStringSourceType]**  
 XPath 文字列のソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|説明|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 `OuterXPathString`  
 **[OuterXPathStringSourceType]** が **[直接入力]** に設定されている場合は、XPath 文字列を指定します。  
  
 **[OuterXPathStringSourceType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **[OuterXPathStringSourceType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、\< **[新しい変数...]** をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、[変数の追加](../../2014/integration-services/add-variable.md)。  
  
 **[InnerElementType]**  
 場合**EnumerationType**に設定されている`ElementCollection`一覧で、内部要素の型を選択します。  
  
 **[InnerXPathStringSourceType]**  
 内部 XPath 文字列のソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|説明|  
|-----------|-----------------|  
|**[直接入力]**|ソースを XML ドキュメントに設定します。|  
|**[ファイル接続]**|XML ドキュメントが含まれているファイルを選択します。|  
|**変数**|ソースを XML ドキュメントが含まれている変数に設定します。|  
  
 `InnerXPathString`  
 **[InnerXPathStringSourceType]** が **[直接入力]** に設定されている場合は、XPath 文字列を指定します。  
  
 **[InnerXPathStringSourceType]** が **[ファイル接続]** に設定されている場合は、ファイル接続マネージャーを選択するか、\< **[新しい接続...]** > をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **[InnerXPathStringSourceType]** が **[変数]** に設定されている場合は、既存の変数を選択するか、\< **[新しい変数...]** をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、[変数の追加](../../2014/integration-services/add-variable.md)。  
  
### <a name="enumerator--foreach-smo-enumerator"></a>[Enumerator] = [Foreach SMO 列挙子]  
 Foreach SMO 列挙子は、SQL Server 管理オブジェクト (SMO) のオブジェクトを列挙するために使用します。 たとえば、Foreach ループに SQL 実行タスクが含まれている場合、Foreach SMO 列挙子を使用して、 **AdventureWorks** データベース内のテーブルを列挙し、各テーブル内の行数をカウントするクエリを実行できます。  
  
 **Connection**  
 既存の ADO.NET 接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 関連トピック:[ADO.NET 接続マネージャー](connection-manager/ado-net-connection-manager.md)、[ADO.NET の接続マネージャーの構成](configure-ado-net-connection-manager.md)  
  
 **[列挙]**  
 列挙する SMO オブジェクトを指定します。  
  
 **[参照]**  
 SMO 列挙を選択します。  
  
 **関連トピック:** [[SMO 列挙の選択] ダイアログ ボックス](../../2014/integration-services/select-smo-enumeration-dialog-box.md)  
  
### <a name="enumerator--foreach-azure-blob-enumerator"></a>列挙子 = Foreach Azure BLOB 列挙子  
 **Azure BLOB 列挙子**を使用すると、SSIS パッケージは指定された BLOB の場所に BLOB ファイルを列挙できるようになります。 列挙された BLOB ファイルの名前は変数に格納され、Foreach ループ コンテナー内のタスクで使用されます。  
  
 **[Azure Storage 接続マネージャー]**  
 既存の Azure ストレージ接続マネージャーを選択するか、Azure ストレージ アカウントを参照する接続マネージャーを新規作成します。  
  
 関連トピック:[Azure Storage 接続マネージャー](connection-manager/azure-storage-connection-manager.md)  
  
 **BLOB コンテナーの名前**  
 列挙する BLOB ファイルを含む BLOB コンテナーの名前を指定します。  
  
 **[BLOB ディレクトリ]**  
 列挙する BLOB ファイルを含む BLOB ディレクトリの名前を指定します。 BLOB ディレクトリは仮想階層構造です。  
  
 **[BLOB 名のフィルター]**  
 特定の名前のパターンを持つファイルを列挙する名前フィルターを指定します。 例: MySheet*.xls\* の場合、MySheet001.xls や MySheetABC.xlsx などのファイルが含まれます。  
  
 **[BLOB 時間範囲フィルター]**  
 時間範囲フィルターを指定します。 **TimeRangeFrom** の後から **TimeRangeTo** の前までに変更されたファイルが列挙されます。  
### <a name="enumerator--foreach-adls-file-enumerator"></a>列挙子 = Foreach ADLS File 列挙子  
**ADLS File 列挙子**フィルターを使用して ADLS にファイルを列挙するために、SSIS パッケージできます。 スラッシュ (`/`) に列挙されたファイルのプレフィックス付きの完全なパスを変数に格納されているし、Foreach ループ コンテナー内のタスクで使用されることができます。
  
**[AzureDataLakeConnection]**  
Azure Data Lake 接続マネージャーを指定するか、ADLS アカウントを参照する新しい接続マネージャーを作成します。   
  
**[AzureDataLakeDirectory]**  
検索する ADLS ディレクトリを指定します。
  
**[FileNamePattern]**  
ファイル名フィルターを指定します。 名前、指定したパターンに一致するファイルのみが列挙されます。 ワイルドカードの `*` と `?` がサポートされています。 
  
**[SearchRecursively]**  
指定されたディレクトリ内で再帰的に検索するかどうかを指定します。  
  
## <a name="external-resources"></a>外部リソース  
  
-   bidn.com のブログ「 [SSIS の For Each ノード一覧の列挙子](https://go.microsoft.com/fwlink/?LinkId=220671)」  
  
-   ブログ エントリ「[ファイル マスクの SSIS 動的設定。FileSpec](https://rajsudeep.blogspot.com/2010/09/ssisdynamically-set-file-mask-filespec.html)します。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Foreach ループ エディター &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)   
 [Foreach ループ エディター&#40;変数マッピング ページ&#41;](../../2014/integration-services/foreach-loop-editor-variable-mappings-page.md)   
 [[式] ページ](expressions/expressions-page.md)   
 [For ループ コンテナー](control-flow/for-loop-container.md)  
  
  
