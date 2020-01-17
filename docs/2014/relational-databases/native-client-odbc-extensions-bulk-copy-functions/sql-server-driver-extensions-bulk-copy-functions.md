---
title: 一括コピー関数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2888f34c1e4c4103845d07e569a0dbabeb2e4caa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225542"
---
# <a name="bulk-copy-functions"></a>一括コピー関数
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 専用の一括コピー API 拡張機能を使用すると、クライアント アプリケーションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルへのデータ行の追加や、テーブルからのデータ行の抽出をすばやく行うことができます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を使用している場合は、SQLNCLI11.LIB と SQLNCLI.H 内にある一括コピー関数 (BCP) を参照できます。  
  
 アプリケーションで BCP API 関数呼び出しを使用する場合は、アプリケーションで使用するドライバー (.dll) に付属するライブラリ (.lib) とアプリケーションをリンクする必要があります。 BCP アプリケーションを複数のドライバー ライブラリとリンクしないでください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [bcp_batch](bcp-batch.md)  
  
-   [bcp_bind](bcp-bind.md)  
  
-   [bcp_colfmt](bcp-colfmt.md)  
  
-   [bcp_collen](bcp-collen.md)  
  
-   [bcp_colptr](bcp-colptr.md)  
  
-   [bcp_columns](bcp-columns.md)  
  
-   [bcp_control](bcp-control.md)  
  
-   [bcp_done](bcp-done.md)  
  
-   [bcp_exec](bcp-exec.md)  
  
-   [bcp_getcolfmt](bcp-getcolfmt.md)  
  
-   [bcp_gettypename](bcp-gettypename.md)  
  
-   [bcp_init](bcp-init.md)  
  
-   [bcp_moretext](bcp-moretext.md)  
  
-   [bcp_readfmt](bcp-readfmt.md)  
  
-   [bcp_sendrow](bcp-sendrow.md)  
  
-   [bcp_setbulkmode](bcp-setbulkmode.md)  
  
-   [bcp_setcolfmt](bcp-setcolfmt.md)  
  
-   [bcp_writefmt](bcp-writefmt.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server ドライバーの拡張機能](../../database-engine/dev-guide/sql-server-driver-extensions.md)   
 [一括コピー操作を実行する&#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
