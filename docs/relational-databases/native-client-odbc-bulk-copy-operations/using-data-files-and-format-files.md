---
title: データファイルとフォーマットファイルの使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- ODBC, functions
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [SQL Server Native Client]
- ODBC, bulk copy operations
- bulk copy [ODBC], data files
ms.assetid: c01b7155-3f0a-473d-90b7-87a97bc56ca5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e7cf91baeb6771f0abb52fb5b8f4c4dc2bddafe0
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785282"
---
# <a name="using-data-files-and-format-files"></a>データ ファイルとフォーマット ファイルの使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  最も単純な一括コピー プログラムでは次の操作を実行します。  
  
1.  [Bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)を呼び出して、テーブルまたはビューからデータファイルへの一括コピー (BCP_OUT の設定) を指定します。  
  
2.  [Bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)を呼び出して、一括コピー操作を実行します。  
  
 データ ファイルはネイティブ モードで作成されるので、テーブルやビューのすべての列から取得したデータは、データベースと同じ形式でデータ ファイルに格納されます。 その後、同様の手順を使用して、このデータ ファイルをサーバーに一括コピーできます。ただし、DB_OUT ではなく DB_IN を設定します。 この操作は、コピー元のテーブルとコピー先のテーブルの構造が厳密に同じ場合にのみ機能します。 結果のデータファイルは、 **/n** (ネイティブモード) スイッチを使用して**bcp**ユーティリティに入力することもできます。  
  
 テーブルやビューから直接取得するのではなく、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの結果セットを一括コピー出力するには、次の操作を実行します。  
  
1.  **Bcp_init**を呼び出して一括コピーを指定しますが、テーブル名には NULL を指定します。  
  
2.  *EOption*を BCPHINTS に設定し、transact-sql ステートメントを含む sqltchar 文字列へのポインターを*ivalue*に設定して[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)を呼び出します。  
  
3.  **Bcp_exec**を呼び出して、一括コピー操作を実行します。  

 結果セットを生成するステートメントであればどのような [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントも使用できます。 作成されるデータ ファイルには [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの最初の結果セットが格納されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで複数の結果セットが生成される場合、一括コピーでは、最初の結果セットよりも後にある結果セットは無視されます。  
  
 列のデータがテーブルとは異なる形式で格納されるデータファイルを作成するには、 [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)を呼び出して、変更する列の数を指定した後、形式を変更する各列に対して[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)を呼び出します。 これは、 **bcp_init**を呼び出した後、 **bcp_exec**を呼び出す前に行います。 **bcp_colfmt**は、列のデータをデータファイルに格納する形式を指定します。 これは、一括コピー時に使用できます。**Bcp_colfmt**を使用して、行ターミネータと列ターミネータを設定することもできます。 たとえば、データにタブ文字が含まれていない場合は**bcp_colfmt**を使用してタブ区切りファイルを作成し、各列のターミネータとしてタブ文字を設定できます。  
  
 **Bcp_colfmt**を一括コピーして使用する場合、 **bcp_colfmt**を最後に呼び出した後[bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)を呼び出すことによって作成したデータファイルを記述するフォーマットファイルを簡単に作成できます。  
  
 フォーマットファイルで記述されたデータファイルからを一括コピーする場合は、 **bcp_init**の後、 **bcp_exec**する前に[bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)を呼び出してフォーマットファイルを読み取ります。  
  
 **Bcp_control**関数は、データファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に一括コピーするときに、いくつかのオプションを制御します。 **bcp_control**は、終了前のエラーの最大数、一括コピーを開始するファイル内の行、停止する行、バッチサイズなどのオプションを設定します。  
  
## <a name="see-also"></a>参照  
 [一括コピー操作&#40;の実行 (ODBC)&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
