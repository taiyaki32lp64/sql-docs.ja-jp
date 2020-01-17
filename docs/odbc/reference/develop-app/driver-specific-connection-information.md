---
title: ドライバー固有の接続情報 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69f2c98678739a8b7879e152e13546f2bf9b9cc1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046933"
---
# <a name="driver-specific-connection-information"></a>ドライバー固有の接続情報
**SQLConnect**データ ソース名、ユーザー ID、およびパスワードがデータ ソースに接続するための十分なことと、システム上の他のすべての接続情報を格納できることを前提としています。 これは頻繁にできません。 たとえば、ドライバーは、1 人のユーザー ID とパスワード、サーバーおよび別のユーザー ID とパスワードにログオンするため、DBMS にログオンする必要があります。 **SQLConnect**受け取る、1 人のユーザー ID とパスワード、つまり他のユーザー ID とパスワードが場合、システム上のデータ ソース情報を格納する必要があります**SQLConnect**が使用されます。 これは潜在的なセキュリティ違反であり、パスワードは暗号化されていない限り避ける必要があります。  
  
 **SQLDriverConnect**接続文字列のキーワード/値ペアの任意の接続情報の量を定義するドライバーを使用します。 たとえば、ドライバーが必要です、データ ソース名、ユーザー ID とパスワード、サーバー、およびユーザー ID とパスワードの dbms とします。 XYZ Corp のデータ ソースを常に使用するカスタム プログラム可能性がありますの Id とパスワードを求めるし、次のキーワードと値のペアのセットを構築または*接続文字列、* に渡す**SQLDriverConnect**:  
  
> [!NOTE]  
>  指定する必要があります Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうか、`Trusted_Connection=yes`接続文字列でユーザー ID とパスワードの情報の代わりにします。  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** (データ ソース名) のキーワード、データ ソースの名前、 **UID**と**PWD**キーワードは、ユーザー ID と、サーバーのパスワードを指定し、 **UIDDBMS**と**PWDDBMS**キーワードは、DBMS のユーザー ID とパスワードを指定します。 最後のセミコロンが省略可能なことに注意してください。 **SQLDriverConnect**この文字列を解析して; XYZ Corp データ ソース名を使用して、サーバーのアドレスなど、システムから追加の接続情報を取得して、サーバーと DBMS の指定されたユーザー Id とパスワードを使用してにログオンします。  
  
 キーワードと値のペアで**SQLDriverConnect**特定の構文規則に従う必要があります。 キーワードとその値を含めないで、 **:operator[]{}()、;?\*=! @** 文字。 値、 **DSN**キーワードが空白ののみで構成されていることはできませんし、先頭の空白を含めることはできません。 レジストリの文法のためのキーワードおよびデータ ソース名が円記号を含めることはできません (\\) 文字。 スペースは、キーワードと値のペアで、等号は使用できません。  
  
 **FILEDSN**への呼び出しでキーワードを使用できます**SQLDriverConnect**データ ソースの情報を含むファイルの名前を指定する (を参照してください[接続を使用してファイル データ ソース](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)、このセクションで後述)。 **SAVEFILE**への呼び出しによって正常な接続のキーワードと値のペアが行われた .dsn ファイルの名前を指定するキーワードを使用できる**SQLDriverConnect**が保存されます。 ファイル データ ソースの詳細については、次を参照してください。、 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)関数の説明。
