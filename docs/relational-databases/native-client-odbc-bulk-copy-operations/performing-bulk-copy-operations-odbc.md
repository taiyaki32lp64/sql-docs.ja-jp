---
title: 一括コピー操作の実行 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC]
- ODBC, bulk copy operations
- minimally logged operations [SQL Server Native Client]
- bulk copy [ODBC], about bulk copy
ms.assetid: 5c793405-487c-4f52-88b8-0091d529afb3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e58c355c437d325e2a0db228f8ed4af83956fecf
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785042"
---
# <a name="performing-bulk-copy-operations-odbc"></a>一括コピー操作の実行 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 標準では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の一括コピー操作が直接サポートされません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 以降のインスタンスに接続するときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の一括コピー操作を実行する DB-Library 関数がサポートされます。 このドライバー固有の拡張機能では、一括コピー関数を使用する既存の DB-Library アプリケーションを簡単にアップグレードできる手段が用意されています。 次のファイルには、一括コピー専用のサポートが含まれています。  
  
-   sqlncli.h  
  
     一括コピー関数の関数プロトタイプと定数定義が含まれています。 一括コピー操作を実行する ODBC アプリケーションでは、sqlncli.h をインクルードする必要があります。このファイルは、コンパイル時にアプリケーションのインクルード パスに存在している必要があります。  
  
-   sqlncli11.lib  
  
     リンカーのライブラリ パスに存在し、リンクされるファイルとして指定する必要があります。 sqlncli11.lib は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーに付属しています。  
  
-   sqlncli11.dll  
  
     実行時に存在する必要があります。 sqlncli11.dll は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーに付属しています。  
  
> [!NOTE]  
>  ODBC **Sqlbulkoperations**関数には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の一括コピー関数とのリレーションシップはありません。 アプリケーションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固有の一括コピー関数を使用して、一括コピー操作を実行する必要があります。  
  
## <a name="minimally-logging-bulk-copies"></a>一括コピーの最小ログ記録  
 完全復旧モデルでは、一括読み込みで実行されたすべての行挿入操作が、トランザクション ログに完全に記録されます。 ただし大量のデータを読み込むと、トランザクション ログがすぐにいっぱいになる可能性があります。 特定の条件下では、最小ログ記録が可能になります。 最小ログ記録を行うことで、一括読み込み操作によってログ領域がいっぱいになる可能性が少なくなります。また、これは完全なログ記録よりも効率的です。  
  
 最小ログ記録の使用の詳細については、「[一括インポートで最小ログ記録を行うための前提条件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降で bcp.exe を使用すると、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] より前のバージョンでは発生しなかった状況でエラーが発生することがあります。 これは、新しいバージョンでは bcp.exe でデータ型が暗黙的に変換されなくなったためです。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] より前のバージョンでは、対象テーブルのデータ型が money データ型の場合、bcp.exe で数値データが money データ型に変換されました。 ただし、その際には、余分なフィールドは単純に切り捨てられていました。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降では、ファイルと対象テーブルのデータ型が一致しない場合、変換先のテーブルに合わせるために切り捨てが必要なデータがあると、bcp によってエラーが発生します。 このエラーを解決するには、対象のデータ型に合わせてデータを修正します。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] より前のリリースの bcp.exe を使用することもできます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [データ ファイルとフォーマット ファイルの使用](../../relational-databases/native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
-   [プログラム変数からの一括コピー](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-from-program-variables.md)  
  
-   [一括コピー バッチ サイズの管理](../../relational-databases/native-client-odbc-bulk-copy-operations/managing-bulk-copy-batch-sizes.md)  
  
-   [テキスト データと画像データの一括コピー](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-text-and-image-data.md)  
  
-   [DB-Library から ODBC への一括コピーの変換](../../relational-databases/native-client-odbc-bulk-copy-operations/converting-from-db-library-to-odbc-bulk-copy.md)  
  
## <a name="see-also"></a>参照  
 [ &#40;ODBC&#41; ](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  の SQL Server Native Client  
 [データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
