---
title: bcp ユーティリティを使用した一括データのインポートとエクスポート (SQL Server) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 06/14/2017
ms.openlocfilehash: 7075bf87ed64686750bc4a267af431268987ff35
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708209"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>bcp ユーティリティを使用した一括データのインポートとエクスポート (SQL Server)

このトピックでは、 [bcp ユーティリティ](../../tools/bcp-utility.md) を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内の SELECT ステートメントで指定できる任意の場所 (パーティション ビューを含む) からデータをエクスポートする方法について説明します。  
  
 bcp ユーティリティ (Bcp.exe) は、一括コピー プログラム (BCP) API を使用するコマンド ライン ツールです。 bcp ユーティリティは次のタスクを実行します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルからデータ ファイルへのデータの一括エクスポート  
  
-   クエリからのデータの一括エクスポート  
  
-   データ ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルへのデータの一括インポート  
  
-   フォーマット ファイルの生成  
  
 bcp ユーティリティには、 **bcp** コマンドを使用してアクセスします。 **bcp** コマンドを使用してデータを一括インポートするには、テーブルのスキーマとテーブル列のデータ型を理解しておく必要があります (既存のフォーマット ファイルを使用する場合を除く)。  
  
 bcp ユーティリティでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルのデータを他のプログラムで使用できるようにデータ ファイルにエクスポートできます。 このユーティリティでは、別のデータベース管理システム (DBMS) など、別のプログラムのデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルにインポートすることもできます。 データは、まずエクスポート元プログラムからデータ ファイルにエクスポートされ、その後に別の操作として、データ ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルにコピーされます。  
  
 **bcp** コマンドには、データ ファイルのデータ型やその他の情報を指定するためのスイッチがあります。 これらのスイッチを指定しなかった場合は、データ ファイルに含まれているデータ フィールドの型などのフォーマット情報を要求されます。 その後、対話型の応答内容を含んだフォーマット ファイルを作成するかどうかをたずねるメッセージが表示されます。 一括インポート操作や一括エクスポート操作を後で行う場合は、フォーマット ファイルを使用すると便利です。 フォーマット ファイルは、同等のデータ ファイルに対して **bcp** コマンドを後で実行するときに指定できます。 詳細については、「[bcp を使用した互換性のためのデータ形式の指定 &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  bcp ユーティリティは ODBC 一括コピーを使用して書き込まれます。  
  
 **bcp** コマンドの構文の説明については、「 [bcp Utility](../../tools/bcp-utility.md)」を参照してください。  
  
## <a name="examples"></a>使用例

 **bcp** の例については、次のトピックを参照してください。  
  
-   [bcp ユーティリティ](../../tools/bcp-utility.md)  
  
-   [フォーマット ファイルの作成 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [XML ドキュメントの一括インポートと一括エクスポートの例 &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [データの一括インポート時の ID 値の保持 &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  

## <a name="see-also"></a>関連項目

[INSERT &#40;&#41;transact-sql](/sql/t-sql/statements/insert-transact-sql)
[SELECT 句&#40;&#41;transact-sql](/sql/t-sql/queries/select-clause-transact-sql)
[bcp Utility](../../tools/bcp-utility.md)   
[データ&#40;&#41;SQL Server の一括インポートの準備](prepare-to-bulk-import-data-sql-server.md)
[BULK INSERT &#40;transact-sql&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)
[データ&#40;の一括インポートとエクスポート SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)1[OPENROWSET &#40;Transact-sql&#41;](/sql/t-sql/functions/openrowset-transact-sql)5[フォーマットファイル&#40;を作成&#41; SQL Server](create-a-format-file-sql-server.md)