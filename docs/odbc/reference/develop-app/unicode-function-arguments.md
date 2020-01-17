---
title: Unicode 関数の引数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 88ce592ebbf5a1b44d55b1b3119ef96e713112bc
ms.sourcegitcommit: 26868c8ac3217176b370d972a26d307598a10328
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74833018"
---
# <a name="unicode-function-arguments"></a>Unicode 関数の引数
ODBC 3.5 (またはそれ以降) のドライバーマネージャーでは、引数に文字列または SQLPOINTER へのポインターを受け取るすべての関数の ANSI バージョンと Unicode バージョンの両方がサポートされています。 Unicode 関数はマクロとしてではなく、関数として実装されます (拡張子は*W*)。 ANSI 関数 (のサフィックスを使用して、または指定しないで呼び出すことができ*ます) は*、現在の ODBC API 関数と同じです。  
  
## <a name="remarks"></a>コメント  
 常にを返すか、文字列または長さの引数を受け取る Unicode 関数は、文字数として渡されます。 サーバーデータの長さの情報を返す関数の場合、表示サイズと有効桁数は文字数で示されます。 長さ (データの転送サイズ) が文字列または文字列以外のデータを参照する場合、長さはオクテット長で記述されます。 たとえば、 **Sqlgetinfow**の長さはバイト数として取得されますが、 **SQLExecDirectW**では文字数が使用されます。  
  
 文字数は、ANSI 関数のバイト数 (オクテット) と、UNICODE 関数の WCHAR の数 (16 ビットワード) を示します。 特に、2バイト文字シーケンス (DBCS) またはマルチバイト文字シーケンス (MBCS) は、複数のバイトで構成できます。 UTF-16 Unicode 文字シーケンスは、複数の WCHARs で構成できます。  
  
 Unicode (W) バージョンと ANSI (A) バージョンの両方をサポートする ODBC API 関数の一覧を次に示します。  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColAttributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQLNativeSQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSetConnectOption**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
|**SQLGetDiagField**||  
  
 次に示すのは、Unicode (W) バージョンと ANSI (A) バージョンの両方をサポートする ODBC インストーラーおよび ODBC 変換関数の一覧です。  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**Sqlインストーラエラー**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**Sqlgetがあるドライバー**|**SQLRemoveDSNFromINI**|  
|**Sqlgetdrivers ドライバー**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]
>  ODBC *3. x*ドライバーマネージャーでは、unicode **#define**を使用した odbc *2.x アプリケーションの*再コンパイルがサポートされているため、非推奨の関数では unicode から ANSI へのマッピングがサポートされています。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Unicode アプリケーション](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode ドライバー](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [ドライバー マネージャーの関数マッピング](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
