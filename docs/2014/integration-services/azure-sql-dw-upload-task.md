---
title: Azure SQL DW アップロード タスク | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPDWUPTASK.F1
- SQL11.DTS.DESIGNER.AFPDWUPTASK.F1
ms.assetid: 112cf764-f85a-4c1a-b732-d299d717c0d4
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3c310ee1d60648ac4b1eb299a0fd291adb86aea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061290"
---
# <a name="azure-sql-dw-upload-task"></a>Azure SQL DW アップロード タスク
**Azure SQL DW アップロード タスク** を利用すると、SSIS パッケージで、Azure SQL Data Warehouse (DW) のテーブルにローカル データをアップロードできます。 現在サポートされているソース データ ファイル形式は、UTF8 エンコーディングの区切り記号付きテキストです。 アップロード プロセスでは、効率的な PolyBase 手法に従います。 具体的には、データは最初に Azure Blob Storage にアップロードされ、それから Azure SQL DW にアップロードされます。 そのため、このタスクを利用するには Azure Blob Storage アカウントが必要になります。

**Azure SQL DW アップロード タスク**を追加するには、SSIS ツールボックスからデザイナー キャンバスにドラッグ アンド ドロップし、ダブルクリックまたは右クリックして **[編集]** をクリックし、タスク エディター ダイアログ ボックスを表示します。

**[全般]** ページで、次のプロパティを構成します。

フィールド|説明
-----|-----------
LocalDirectory|アップロードするデータ ファイルを含むローカル ディレクトリを指定します。
Recursively|サブディレクトリを再帰的に検索するかどうかを指定します。
FileName|特定の名前のパターンを持つファイルを選択する名前フィルターを指定します。 例: MySheet\*.xsl\* の場合、MySheet001.xsl や MySheetABC.xslx などのファイルが含まれます。
[RowDelimiter]|各行の終わりに印を付ける文字を指定します。
[列区切り記号]|各列の終わりに印を付ける 1 つ以上の文字を指定します。 例: &#124; (パイプ)、\t (タブ)、' (単一引用符)、" (二重引用符)、および 0x5c (バック スラッシュ)。
IsFirstRowHeader|各データ ファイルの最初の行に実際のデータの代わりに列名を含めるかどうかを指定します。
AzureStorageConnection|Azure Storage 接続マネージャーを指定します。
BlobContainer|ローカル データをアップロードし、PolyBase 経由で Azure DW にリレーする BLOB コンテナーの名前を指定します。 コンテナーが存在しない場合、新規作成されます。
BlobDirectory|ローカル データをアップロードし、PolyBase 経由で Azure DW にリレーする BLOB ディレクトリ (仮想階層構造) を指定します。
RetainFiles|Azure Storage にアップロードしたファイルを保持するかどうかを指定します。
CompressionType|Azure Storage にファイルをアップロードするときに使用する圧縮形式を指定します。 ローカル ソースは影響を受けません。
CompressionLevel|圧縮形式に使用する圧縮レベルを指定します。
AzureDwConnection|Azure SQL DW の ADO.NET 接続マネージャーを指定します。
TableName|アップロード先のテーブルの名前を指定します。 既存のテーブル名を選択するか、 **[\<新しいテーブル...>]** を選択して新規作成します。
TableDistribution|新しいテーブルの配布方法を指定します。 **TableName**に新しいテーブル名が指定されている場合に適用されます。
HashColumnName|ハッシュ テーブル配分に使用される列を指定します。 **TableDistribution** に **HASH**が指定されている場合に適用されます。

新しいテーブルと既存のテーブルにいずれにアップロードするかに基づき、異なる **[マッピング]** ページが表示されます。 前者の場合、マッピングするアップロード元の列とそれに対応する、作成予定のアップロード先のテーブルの名前を構成します。 後者の場合、アップロード元の列とアップロード先の列の間のマッピング関係を構成します。

**[列]** ページで、マッピング元ごとのデータ型プロパティを構成します。

**[T-SQL]** ページには、Azure Blob Storage から Azure SQL DW にデータを読み込むための T-SQL が表示されます。 T-SQL は別のページの構成から自動生成され、タスク実行の一部として実行されます。 生成された T-SQL を特定のニーズに合わせて手動で編集することもできます。 **[編集]** ボタンをクリックしてください。 **[リセット]** ボタンをクリックすれば、自動的に生成されたものに後で戻すことができます。
