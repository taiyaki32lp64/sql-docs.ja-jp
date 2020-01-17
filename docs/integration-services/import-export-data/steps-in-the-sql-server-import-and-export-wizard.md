---
title: SQL Server インポートおよびエクスポート ウィザードの手順 | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0a6fb370c80af6221812b88d3694a230dc206f7b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296204"
---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザードの手順

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このトピックでは、SQL Server インポートおよびエクスポート ウィザードを使用して、データをインポートおよびエクスポートする一連の手順について説明します。 また、ウィザードで表示される各ページやダイアログ ボックスを説明するドキュメントの個々のページへのリンクも含まれます。

このトピックでは、ウィザードの**手順**についてのみ説明します。 他のものをお探しの場合は、「[関連タスクとコンテンツ](#related)」を参照してください。

## <a name="steps-for-importing-and-exporting-data"></a>データのインポートとエクスポートの手順  
 次の表に、データのインポートとエクスポートを行うための手順と、ウィザードの該当ページを示します。 ウィザードで選択したオプションに応じて表示されるページは異なるため、通常はすべてのページが表示されることはありません。  

一般的なセッションで見られる画面をいくつか簡単にご覧いただくため、この単純なエンド ツー エンドの例を 1 つのページ示した「[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)」をご覧ください。

|手順|ウィザード ページ|  
|----------|------------------|  
|**ようこそ**<br />このページでいかなる操作も必要はありません。|[SQL Server インポートおよびエクスポート ウィザードへようこそ](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|データの変換元**を選択します**。|[データ ソースの選択](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|データの**変換先を選択します**。|[変換先の選択](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**変換先を構成します**。 (省略可能な手順)<br /><br /> - 新しい変換先データベースを作成します。<br />- データをテキスト ファイルにコピーする場合は、追加設定を構成します。|[データベースの作成](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[フラット ファイルの変換先の構成](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**何をコピーするかを指定します。**|[テーブルのコピーまたはクエリの指定](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[コピー元のテーブルおよびビューを選択](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[基になるクエリの指定](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**コピー操作を構成します**。 (省略可能な手順)<br /><br /> - 新しい変換先テーブルを作成します。<br />- ユーザーが選択した変換元と変換先の間のデータ型マッピングの方法を、ウィザードが認識しない場合の操作を決定します。<br />- 変換元と変換先の間の列マッピングを見直します。<br />- 変換元と変換先の間のデータ型変換に関する問題を処理します。<br />- コピーされるデータを見直します。|[テーブル作成 SQL ステートメント](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[変換の確認を伴わない型変換](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[列マッピング](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[データ型マッピングの確認](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[[列変換の詳細] ダイアログ ボックス](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[[データのプレビュー] ダイアログ ボックス](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**データをコピーします。**<br /><br /> 必要に応じて、設定を SQL Server Integration Services (SSIS) パッケージとして保存します。|[パッケージの保存および実行](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[SSIS パッケージの保存](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[ウィザードの完了](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[操作の実行](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> ウィザードのページまたはダイアログ ボックスで F1 キーをタップすると、現在のページの文書が表示されます。

## <a name="related"></a> 関連タスクとコンテンツ  
その他の基本的なタスクは次のとおりです。
-   **ウィザードのしくみの簡単な例を参照してください。**

    -   **スクリーン ショットを参照する場合。** この単純なエンド ツー エンドの例を 1 つのページ示した「[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)」をご覧ください。

    -   **ビデオを視聴する場合。** ウィザードを実行し、わかりやすく簡単な手順でデータを Excel にエクスポートする方法を説明した YouTube の 4 分間のビデオ「[SQL Server インポートおよびエクスポート ウィザードを使用して Excel にエクスポートする](https://go.microsoft.com/fwlink/?linkid=829049)」 をご覧ください。

-   **ウィザードのしくみについては、以下を参照してください。**

    -   **ウィザードのしくみについては、以下を参照してください。** ウィザードの概要をお探しの場合は、「 [SQL Server でサポートされるインポートとエクスポートのデータ ソース](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)」を参照してください。

    -   **データ ソースおよび変換先に接続する方法を学習する。** データへの接続方法についての情報を探している場合は、「[SQL Server インポートおよびエクスポート ウィザードを使用してデータ ソースに接続する](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)」の一覧から目的のページを選んでください。 いくつかの一般的に使用されるデータ ソースごとに個別のドキュメントのページがあります。 

-   **ウィザードを起動します。** ウィザードを実行する準備が整い、開始方法について知りたい場合は、「[SQL Server インポートおよびエクスポート ウィザードを起動する](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)」を参照してください。

-     **ウィザードを取得します。** ウィザードを実行する必要はあるが、コンピューターに [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールしていない場合は、SQL Server Data Tools (SSDT) をインストールすることで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードをインストールできます。 詳細については、「 [SQL Server Data Tools (SSDT) のダウンロード](https://msdn.microsoft.com/library/mt204009.aspx)」を参照してください。


