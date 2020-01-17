---
title: テーブルのコピーまたはクエリの指定 (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 524e878933652699bef6e31da42d3a784b54df7c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892644"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>[テーブルのコピーまたはクエリの指定] \(SQL Server インポートおよびエクスポート ウィザード)
  使用して、**指定のテーブルのコピーまたはクエリ**ページ データをコピーする方法を指定します。 グラフィカル インターフェイスを使用して、コピーする既存データベースを選択したり、Transact-SQL を使用してさらに複雑なクエリを作成したりできます。  
  
 このウィザードの詳細については、次を参照してください。 [SQL Server インポートおよびエクスポート ウィザード](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)します。 ウィザードを正常に実行するために必要なアクセス許可と同様に、ウィザードを開始するためのオプションについては、次を参照してください。 [、SQL Server インポートおよびエクスポート ウィザードを実行](start-the-sql-server-import-and-export-wizard.md)します。  
  
 SQL Server インポートおよびエクスポート ウィザードの目的は、変換元から変換先にデータをコピーすることです。 また、このウィザードでは、変換先データベースと変換先テーブルも作成できます。 ただし、複数のデータベースやテーブルまたは他の種類のデータベース オブジェクトをコピーする必要がある場合は、データベース コピー ウィザードを使用してください。 詳細については、「 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)」を参照してください。  
  
## <a name="options"></a>および  
 **1 つ以上のテーブルまたはビューからデータをコピーする**  
 使用して、指定したコピー先または変換先に選択したソース テーブルとビューからフィールドをコピー、**選択元のテーブルおよびビュー**  ダイアログ ボックス。 レコードのフィルター選択や並べ替えを実行せず、コピー元のすべてのデータをコピーする場合に、このオプションを使用します。  
  
 使用すると、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 、データ ソースに接続するデータ プロバイダー、 **1 つまたは複数のテーブルまたはビューからデータをコピー**オプションを利用できない可能性があります。 このオプションは、ProviderDescriptors.xml ファイルに ProviderDescription セクションがあるプロバイダーでのみ使用できます。 各 ProviderDescription セクションには、対応するプロバイダーからメタデータを取得するのに必要な情報が含まれています。 既定では、ProviderDescriptors.xml ファイルには、次のプロバイダーの ProviderDescription セクションのみが含まれています。  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 させる、 **1 つまたは複数のテーブルまたはビューからデータをコピー**オプション、その他のプロバイダーは、サード パーティは、ProviderDescriptors.xml ファイルに独自の ProviderDescriptor セクションを追加することができます。 既定では、このファイルは\<*ドライブ*>: \Program Files\Microsoft SQL Server\100\DTS\ProviderDescriptors します。 ProviderDescriptor セクションの要件については、ProviderDescriptors.xsd スキーマ ファイルを参照してください。既定では、このファイルは、ProviderDescriptors.xml ファイルと同じフォルダーに格納されています。  
  
 **転送するデータを指定するためのクエリを記述する**  
 使用して行を取得する SQL ステートメントを作成、**ソース クエリの指定** ダイアログ ボックス。 コピー操作中にコピー元データを変更したり、制限したりする場合に、このオプションを使用します。 選択条件に一致する行のみをコピーできます。  
  
  
