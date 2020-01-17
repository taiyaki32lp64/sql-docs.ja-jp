---
title: データの一括インポートと一括エクスポート (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- bulk importing [SQL Server], about bulk importing
- data [SQL Server], bulk export and import
- transferring data
- importing data, (See also bulk importing [SQL Server])
- copying data [SQL Server]
- bulk exporting [SQL Server]
- importing data, bulk import
- copying data [SQL Server], bulk export and import
- exporting data,(See also bulk exporting [SQL Server])
- bulk exporting [SQL Server], about bulk exporting
- bulk importing [SQL Server]
- importing data
ms.assetid: 19049021-c048-44a2-b38d-186d9f9e4a65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e90afe2092623fa1dd356e51af5fff7a19e9a2ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012119"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>データの一括インポートと一括エクスポート (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、*テーブルからのデータの一括エクスポート (* 一括データのエクスポート [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたはパーティション分割されていないビューへの一括データのインポートがサポートされています。 一括インポートと一括エクスポートは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と異種データ ソースとの間で効率的にデータを転送するための重要な機能です。 *一括エクスポート* とは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルから特定のデータ ファイルにデータをコピーすることです。 *一括インポート* は、データ ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルにデータを読み込むことを指します。 たとえば、データを [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel アプリケーションから特定のデータ ファイルにエクスポートした後、そのデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに一括インポートできます。  
  
 **このトピックの内容**  
  
-   [一括インポートと一括エクスポート操作の概要](#Intro)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="Intro"></a> 一括インポートと一括エクスポートの概要  
 このセクションでは、データを一括でインポートおよびエクスポートするために使用できるさまざまな方法を示し、それらを簡単に比較します。 また、フォーマット ファイルについても説明します。  
  
 **このトピックの内容**  
  
-   [一括データ インポートおよびエクスポートする方法](#MethodsForBuliIE)  
  
-   [フォーマット ファイル](#FFs)  
  
###  <a name="MethodsForBuliIE"></a> 一括データ インポートおよびエクスポートする方法  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルからのデータの一括エクスポート、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたはパーティション分割されていないビューへのデータの一括インポートがサポートされています。 使用できる基本的な方法を次に示します。  
  
|方法|説明|データのインポート|データのエクスポート|  
|------------|-----------------|------------------|------------------|  
|[bcp ユーティリティ](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|データの一括エクスポートと一括インポート、およびフォーマット ファイルの生成を行うコマンド ライン ユーティリティ (Bcp.exe)。|[はい]|はい|  
|[BULK INSERT ステートメント](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|データ ファイルのデータをデータベース テーブルまたはパーティション分割されていないビューに直接インポートする [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント。|はい|いいえ|  
|[INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメント](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|INSERT ステートメントでデータを選択するために OPENROWSET(BULK...) 関数を指定することによって、OPENROWSET 一括行セット プロバイダーを使用してデータを [!INCLUDE[tsql](../../includes/tsql-md.md)] テーブルに一括インポートする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメント。|はい|いいえ|  
  
> [!IMPORTANT]  
>  SQL Server の一括インポート操作では、コンマ区切り (CSV) ファイルがサポートされていません。 ただし、場合によっては、SQL Server に対してデータを一括インポートする際、CSV ファイルをデータ ファイルとして使用できます。 CSV ファイルのフィールド ターミネータは必ずしもコンマである必要はありません。 詳細については、「[一括エクスポートまたは一括インポートのデータの準備 &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)」を参照してください。  
  
###  <a name="FFs"></a> フォーマット ファイル  
 **bcp** ユーティリティ、BULK INSERT、および INSERT ...SELECT \* FROM OPENROWSET(BULK...) では、*フォーマット ファイル*という特殊なファイルを使用して、データ ファイル内のフィールドごとにフォーマット情報を格納することができます。 また、フォーマット ファイルには、対応する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに関する情報が含まれる場合もあります。 フォーマット ファイルは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスからデータを一括エクスポートしたり、このインスタンスにデータを一括インポートしたりするのに必要なすべてのフォーマット情報を指定するために使用できます。  
  
 フォーマット ファイルを使用すると、インポートの際にデータ ファイルの形式に従ってデータを解釈したり、エクスポートの際にデータ ファイル内のデータに形式を適用する処理を柔軟に行えるようになります。 これにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または外部アプリケーションの特定の必要性に応じてデータの解釈や再フォーマットを行うことだけを目的としたプログラムを作成する必要がなくなります。 たとえば、コンマ区切り値が必要なアプリケーションに読み込まれるデータを一括インポートする場合、フォーマット ファイルを使用すると、エクスポートされたデータにフィールド ターミネータとしてコンマを挿入できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次の 2 種類のフォーマット ファイルがサポートされます:XML フォーマット ファイルと XML 以外のフォーマット ファイル。  
  
 フォーマット ファイルを生成できるツールは、 **bcp** ユーティリティだけです。 詳細については、「[フォーマット ファイルの作成 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)」をご覧ください。 フォーマット ファイルの使用方法の詳細は、「[データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  一括エクスポート操作または一括インポート操作でフォーマット ファイルが正しく提供されなかった場合に備えて、ユーザーはコマンド ラインで既定の形式をオーバーライドすることもできます。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [インポートおよび bcp ユーティリティを使用した一括データのエクスポート&#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)  
  
-   [BULK INSERT または OPENROWSET を使用して一括データのインポート&#40;一括しています.&#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)  
  
-   [データの一括インポート時の ID 値の保持 &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [一括エクスポートまたは一括インポートのデータの準備 &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **フォーマット ファイルを作成するには**  
  
-   [フォーマット ファイルの作成 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [フォーマット ファイルを使用したデータ フィールドのスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **一括インポートまたは一括エクスポートのデータ形式を使用するには**  
  
-   [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **bcp を使用した互換性のためのデータ形式を指定するには**  
  
1.  [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [bcp を使用したデータ ファイルのプレフィックス長の指定 &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [bcp を使用したファイル ストレージ型の指定 &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>関連項目  
 [一括インポートで最小ログ記録を行うための前提条件](prerequisites-for-minimal-logging-in-bulk-import.md)   
 [データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [XML ドキュメントの一括インポートと一括エクスポートの例 &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [他のサーバーへのデータベースのコピー](../databases/copy-databases-to-other-servers.md)   
 [XML データの一括読み込みの実行 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [一括コピー操作の実行](../native-client/features/performing-bulk-copy-operations.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
