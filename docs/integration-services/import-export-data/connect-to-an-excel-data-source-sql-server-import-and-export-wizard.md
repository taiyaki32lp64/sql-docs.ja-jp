---
title: Excel データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 82e21333bdd0f4be27f19ee19f43fd5f0abab309
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285574"
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Excel データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


この記事では、SQL Server インポートおよびエクスポート ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページから **Microsoft Excel** データ ソースに接続する方法を説明します。

Microsoft Excel ブックへの接続例を次のスクリーン ショットに示します。

![Excel 接続](../../integration-services/import-export-data/media/excel-connection.png) 

Excel ファイルに接続するために追加のファイルのダウンロードとインストールが必要になる場合もあります。 詳細については、「[Excel に接続するために必要なファイルを取得する](../load-data-to-from-excel-with-ssis.md#files-you-need)」を参照してください。

> [!IMPORTANT]
> Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題については、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。

## <a name="options-to-specify"></a>指定するオプション

> [!NOTE]
> このデータ プロバイダーの接続オプションは、Excel が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

**[Excel ファイル パス]**  
 Excel ファイルのパスとファイル名を指定します。 例:
-   ローカル コンピューター上の上のファイルの場合、**C:\\MyData.xlsx** です。
-   ネットワーク共有上のファイルの場合、 **\\\\Sales\\Database\\Northwind.xlsx** です。

または、 **[参照]** をクリックします。  
  
 **[参照]**  
 **[ファイルを開く]** ダイアログ ボックスを使用して、ワークシートを検索します。  

> [!NOTE]
> パスワードで保護された Excel ファイルはウィザードで開くことができません。

 **[Excel バージョン]**  
変換元または変換先のブックで使用される Excel のバージョンを選択します。

**[先頭行に列名を含める]**  
データの最初の行に列名が含まれるかどうかを指定します。
-   データに列名が含まれていないのにこのオプションを有効にすると、ウィザードではソース データの最初の行が列名として扱われます。
-   データに列名が含まれているのにこのオプションを無効にすると、ウィザードでは列名の行がデータの最初の行として扱われます。

データに列名を付けない場合、ウィザードでは列見出しとして F1、F2 などが使用されます。

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>データ ソースのリストに Excel が表示されない
データ ソースのリストに Excel が表示されない場合は、64 ビットのウィザードを実行していないか確認してください。 Excel と Access のプロバイダーは、通常 32 ビットで、64 ビットのウィザードでは表示されません。 代わりに 32 ビットのウィザードを実行します。

> [!NOTE]
> 64 ビット バージョンの SQL Server インポートおよびエクスポート ウィザードを使用するには、SQL Server をインストールする必要があります。 SQL Server Data Tools (SSDT) および SQL Server Management Studio (SSMS) は 32 ビット アプリケーションであり、32 ビット バージョンのウィザードを含む、32 ビット ファイルのみがインストールされます。

## <a name="see-also"></a>参照
[SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む](../load-data-to-from-excel-with-ssis.md)  
[データ ソースの選択](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[変換先の選択](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

