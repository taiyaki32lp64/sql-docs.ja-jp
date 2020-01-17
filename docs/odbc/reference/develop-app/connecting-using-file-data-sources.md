---
title: ファイル データ ソースを使用して接続する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa340c64f6eb92d803d8918bc99ecf112b19f1e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083116"
---
# <a name="connecting-using-file-data-sources"></a>ファイル データ ソースを使用した接続
ファイルのデータ ソースの接続情報は、.dsn ファイルに格納されます。 その結果、接続文字列を 1 人のユーザーによって繰り返し使用または適切なドライバーがインストールされている場合は、複数のユーザーの間で共有します。 ファイルには、ドライバー名 (または共有不能なファイルのデータ ソースの場合、別のデータ ソース名) が含まれています。 必要に応じて、で使用できる接続文字列と**SQLDriverConnect**します。 ドライバー マネージャーへの呼び出しの接続文字列をビルドする**SQLDriverConnect** .dsn ファイル内のキーワードから。  
  
 ファイルのデータ ソースにより、アプリケーションで使用するための接続文字列を構築することがなく接続オプションを指定する**SQLDriverConnect**します。 通常、ファイルのデータ ソースが指定することによって作成は、 **SAVEFILE**キーワードで、ドライバー マネージャーへの呼び出しによって作成された出力の接続文字列を保存すると、 **SQLDriverConnect** .dsn ファイルにします。 接続文字列を呼び出すことで繰り返し使用できること**SQLDriverConnect**で、 **FILEDSN**キーワード。 これにより、接続プロセスを合理化し、接続文字列の永続的なソースを提供します。  
  
 ファイル データ ソースも作成できます呼び出して**SQLCreateDataSource**インストーラー DLL。 情報は、呼び出すことによって、.dsn ファイルに書き込まれることができます**SQLWriteFileDSN**、呼び出して .dsn ファイルから読み取ると**SQLReadFileDSN**; インストーラー DLL もこれらの関数。 インストーラー DLL については、次を参照してください。[データ ソースを構成する](../../../odbc/reference/install/configuring-data-sources.md)します。  
  
 接続情報の使用されるキーワードは、.dsn ファイルの [ODBC] セクションには。 [ODBC] セクションでは共有可能 .dsn ファイルが、最小限の情報は、DRIVER キーワードを示します。  
  
```  
DRIVER = SQL Server  
```  
  
 共有可能 .dsn ファイルは通常、接続文字列としては、次のように含みます。  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 ファイルのデータ ソースが共有可能 .dsn ファイルのみを含む、 **DSN**キーワード。 接続で示されるデータ ソースに必要なドライバー マネージャーは、共有不能なファイルのデータ ソースの情報を送信するとき、 **DSN**キーワード。 共有不能な .dsn ファイルは、次のキーワードが含まれます。  
  
```  
DSN = MyDataSource  
```  
  
 ファイルのデータ ソースを使用する接続文字列は .dsn ファイルで指定したキーワードと接続文字列への呼び出しで指定したキーワードの和集合**SQLDriverConnect**します。 接続文字列キーワードを持つ .dsn ファイル内のキーワードのいずれかが競合する場合、ドライバー マネージャーは、キーワード値を使用する必要がありますを決定します。 詳細については、次を参照してください。 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)します。  
  
## <a name="see-also"></a>参照  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
