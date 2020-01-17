---
title: Oracle ソース | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4444236d19c9d7c67aba5a36ba079e1dfa9189b0
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542206"
---
# <a name="oracle-source"></a>Oracle ソース

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Oracle ソースでは、以下のモードで Oracle Database からデータが抽出されます。

- テーブルまたはビュー。

- SQL ステートメントの結果。

ソースでは、Oracle 接続マネージャーを使用して Oracle ソースに接続します。 詳細については、「[Oracle 接続マネージャー](oracle-connection-manager.md)」をご覧ください。

## <a name="error-output"></a>エラー出力

エラー出力には、次の列が含まれています。  

- **エラー コード**: 現在のエラーのエラーの種類を表す数値。 エラー コードは、以下から送信される可能性があります。
    - Oracle サーバー。 Oracle データベースのドキュメントに記載されている詳細なエラーの説明をご覧ください。
    - SSIS ランタイム。 SSIS エラー コードの一覧については、「SSIS のエラー コードおよびメッセージ リファレンス」を参照してください。
- **エラー列**: 変換エラーの原因となっているソースの列の番号。

- **エラー データ列**:エラーの原因となっているデータ。

Oracle ソースでは、読み込みおよび抽出プロセス中に発生したエラーがエラー出力に返されます。 詳細については、「[Oracle ソース エディター ([エラー出力] ページ)](#oracle-source-editor-error-output-page)」をご覧ください。

## <a name="troubleshooting-the-oracle-source"></a>Oracle ソースのトラブルシューティング

Oracle ソースによって Oracle データ ソースに対して行われる ODBC 呼び出しをログに記録して、データのエクスポートに関するトラブルシューティングを行うことができます。 Oracle ソースによって Oracle データ ソースに対して行われる ODBC 呼び出しをログに記録するには、ODBC ドライバー マネージャーによるトレースを有効にします。 詳細については、「 *ODBC で ODBC トレースを生成する方法 (データ ソース管理者向け)* 」の Microsoft のドキュメントを参照してください。

## <a name="oracle-source-custom-properties"></a>ODBC ソースのカスタム プロパティ

Oracle ソースのカスタム プロパティは次のとおりです。 すべてのプロパティは読み取り/書き込み可能です。

|プロパティ名|データ型|[説明]|
|:-|:-|:-|
|AccessMode|Integer (列挙)|データベースへのアクセスに使用するモード。 指定できる値は、 **[テーブル名]** と **[SQL コマンド]** です。 既定値は **[テーブル名]** です。|
|BatchSize|整数|一括読み込みのバッチのサイズ。 これは、配列として抽出されるレコード数です。 <br>このプロパティは、**詳細エディター**によってのみ設定されます|
|DefaultCodePage|整数|データ ソースにコード ページ情報がない場合に使用されるコード ページ。 <br>このプロパティは、**詳細エディター**によってのみ設定されます。|
|PreFetchCount|整数|プリフェッチされた行の数。 <br>このプロパティは、**詳細エディター**によってのみ設定されます。|
|SqlCommand|String|AccessMode が SQL コマンドに設定されている場合に実行される SQL コマンド。|
|TableName|String|AccessMode がテーブル名に設定されている場合に使用されるデータを含んだテーブルの名前。|

## <a name="configuring-the-oracle-source"></a>Oracle ソースの構成

Oracle ソースは、プログラムによって、または SSIS デザイナーを使用して構成できます。

Oracle ソース エディターを次の図に示します。 これには、[接続マネージャー] ページ、[列] ページ、および [エラー出力] ページが含まれています。

詳細については、次のいずれかのセクションを参照してください。

- [Oracle ソース エディター ([接続マネージャー] ページ)](#oracle-source-editor-connection-manager-page)
- [Oracle ソース エディター ([列] ページ)](#oracle-source-editor-columns-page)
- [Oracle ソース エディター ([エラー出力] ページ)](#oracle-source-editor-error-output-page)

![](media/oracle-source.png)

**[詳細エディター] ダイアログ ボックス**には、プログラムによって設定できるプロパティが表示されます。

**[詳細エディター]** ダイアログ ボックスを開くには、次の操作を実行します。

- Integration Services プロジェクトの **[データ フロー]** 画面で、Oracle ソースを右クリックし、 **[詳細エディターの表示]** をクリックします。

**[詳細エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、「[ODBC ソースのカスタム プロパティ](#oracle-source-custom-properties)」をご覧ください。

## <a name="oracle-source-editor-connection-manager-page"></a>Oracle ソース エディター ([接続マネージャー] ページ)

**[接続マネージャー]** ページの **[Oracle ソース エディター]** ダイアログ ボックスでは、データベースからのソース、テーブル、またはビューとして Oracle Database が選択されます。

**[Oracle ソース エディター] の [接続マネージャー] ページを開くには**

- SQL Server Data Tools で、Oracle ソースを含む SQL Server Integration Services (SSIS) パッケージを開きます。

- [データ フロー] タブで、Oracle ソースをダブルクリックします。
### <a name="options"></a>オプション

**Connection manager**

既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい Oracle 接続マネージャーを作成します。

**[新規作成]**

**[新規作成]** をクリックします。 新しい接続マネージャーを作成できる **[Oracle 接続マネージャー エディター]** ダイアログ ボックスが開きます。

**データ アクセス モード**

入力元のデータを選択する方法を選択します。 次の表に示すオプションがあります。

|オプション|[説明]|
|:-|:-|
|[テーブルまたはビュー]|Oracle データ ソースのテーブルまたはビューからデータを取得します。 このオプションを選択した場合、使用できるテーブルまたはビューを **[テーブル名またはビュー名]** の一覧から選択します。|
|[SQL コマンド]|SQL クエリを使用して、Oracle データ ソースからデータを取得します。 このオプションを選択した場合は、以下のいずれかの方法でクエリを入力します。 <br>**[SQL コマンド テキスト]** フィールドに SQL クエリのテキストを入力します。 <br>**[参照]** をクリックして、テキスト ファイルから SQL クエリを読み込みます。 <br>**[クエリの解析]** をクリックして、クエリ テキストの構文を検証します。|

**プレビュー**

**[プレビュー]** をクリックすると、選択したテーブルまたはビューから抽出されたデータを先頭から最大で 200 行表示できます。

## <a name="oracle-source-editor-columns-page"></a>Oracle ソース エディター ([列] ページ)

**[列]** ページでは、出力列をそれぞれの外部 (ソース) 列にマップするために **[Oracle ソース エディター]** ダイアログ ボックスが使われます。

**[Oracle ソース エディター] の [列] ページを開くには**

- SQL Server Data Tools で、Oracle ソースを含む SQL Server Integration Services (SSIS) パッケージを開きます。

- [データ フロー] タブで、Oracle ソースをダブルクリックします。

- [Oracle ソース エディター] で、[列] をクリックします。

### <a name="options"></a>オプション

**使用できる外部列**

使用できる外部列の一覧です。これらを選択し、選択した順序で **[外部列]** の一覧に追加できます。 このテーブルを使って列の追加または削除を行うことはできません。

**[すべて選択]** チェック ボックスをオンにすると、すべての列が選択されます。

**外部列**

選択した外部 (ソース) 列が順序どおりに一覧表示されます。
順序を変更するには、まず [使用できる外部列] の一覧をクリアしてから、別の順序で列を選択します。

**出力列**

選択された外部 (ソース) 列の名前が既定の出力名になります。 ただし、任意の一意の名前を入力できます。
> [!NOTE]
>
>サポートされていないデータ型の列があった場合は、そのデータ型がサポートされていないことを示す警告が表示され、関連する列が列のマッピングから削除されます。

## <a name="oracle-source-editor-error-output-page"></a>Oracle ソース エディター ([エラー出力] ページ)

**[Oracle ソース エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択できます。

**[Oracle ソース エディター] の [エラー出力] ページを開くには**

- SQL Server Data Tools で、Oracle ソースを含む SQL Server Integration Services (SSIS) パッケージを開きます。

- [データ フロー] タブで、Oracle ソースをダブルクリックします。

- [Oracle ソース エディター] で、[エラー出力] をクリックします。

### <a name="options"></a>オプション

**エラー動作**

Oracle ソースでフローでのエラーを処理する方法を選択します (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる)。
**関連セクション**:[データのエラー処理](https://docs.microsoft.com/sql/integration-services/data-flow/error-handling-in-data?view=sql-server-2017)

**切り捨て**

Oracle ソースでフローの切り捨てを処理する方法を選択します (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる)。

## <a name="next-steps"></a>次のステップ

- [Oracle 変換先](oracle-destination.md)を構成する。
- ご質問がある場合は、[技術者コミュニティ](https://aka.ms/AA5u35j)を参照してください。
