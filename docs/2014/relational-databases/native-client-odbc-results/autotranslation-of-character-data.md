---
title: 文字データの自動変換 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5182ab1a72caac4181e50df2199f3e0457d3aaac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200211"
---
# <a name="autotranslation-of-character-data"></a>文字データの自動変換
  ANSI などの文字データ文字の SQL_C_CHAR で宣言された変数またはデータに格納されている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用して、 **char**、 **varchar**、または**テキスト**データ型のことができます文字の制限の数のみを表します。 1 文字ごとに 1 バイトを使用して保存される文字データでは、256 文字しか表現できません。 SQL_C_CHAR 変数に格納される値は、クライアント コンピューターの ANSI コード ページ (ACP) を使用して解釈されます。 使用して格納されている値**char**、 **varchar**、または**テキスト**サーバー上のデータ型は、サーバーの ACP を使用して評価されます。  
  
 サーバーとクライアントの両方に同じの ACP があるかどうかは、SQL_C_CHAR に格納された値を解釈するときに問題があるない**char**、 **varchar**、または**テキスト**オブジェクト。 サーバーとクライアントが別の Acp かどうかは、クライアントの SQL_C_CHAR データで使用されている場合、サーバー上の別の文字として解釈可能性があります**char**、 **varchar**、または**テキスト**列、変数、またはパラメーター。 たとえば、0xa5 という値を格納している文字のバイトは、文字として解釈される?? コードを使用してコンピューター上のページ 437 とは、円 (聞き取り不能) をコード ページ 1252 を実行しているコンピューターにアクセスするように解釈されます。  
  
 Unicode データは、1 文字あたり 2 バイトを使用して格納されます。 Unicode の仕様は、すべての拡張文字を網羅しています。したがって、すべての Unicode 文字は、すべてのコンピューターで同じ文字に解釈されます。  
  
 AutoTranslate 機能、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは異なるコード ページが、クライアントとサーバー間の文字のデータ移動の問題を最小化しようとしています。 接続文字列の AutoTranslate を設定できます[SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md)の構成文字列[SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)、またはデータ ソースを構成するときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBCドライバーは ODBC アドミニストレーターを使用します。  
  
 クライアントの SQL_C_CHAR 変数との間で移動するデータの変換は行われません AutoTranslate の設定を"no"にすると、および**char**、 **varchar**、または**テキスト**列、変数、またはのパラメーターを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。 この場合、データに拡張文字が含まれていて、クライアント コンピューターとサーバー コンピューターのコード ページが異なっていると、ビット パターンはクライアントとサーバーでは異なって解釈される可能性があります。 クライアントとサーバーが同じコード ページを使用している場合は、データは同じ文字に解釈されます。  
  
 AutoTranslate が"yes"に設定されている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、Unicode を使用して、クライアントの SQL_C_CHAR 変数との間で移動するデータを変換しますおよび**char**、 **varchar**、または**テキスト**列、変数、またはパラメーターで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
-   クライアントの SQL_C_CHAR 変数からデータを送信するときに、 **char**、 **varchar**、または**テキスト**列、変数、またはパラメーターで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース, ODBCドライバーは、サーバーの acp に基づいて文字に Unicode からし、クライアントの acp に基づいて Unicode を SQL_C_CHAR から最初に変換します。  
  
-   データを送信するときに、 **char**、 **varchar**、または**テキスト**列、変数、またはパラメーターで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントのSQL_C_CHAR変数にデータベース[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC ドライバーは、まず、クライアントの ACP を使用して SQL_C_CHAR に Unicode からし、サーバーの acp に基づいて unicode 文字から変換します。  
  
 すべてのこれらの変換行われるため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーをクライアントでサーバーの acp に基づいて実行すると、クライアント コンピューターにインストールされているコード ページのいずれかが指定する必要があります。  
  
 Unicode を使用して文字を変換することで、両方のコード ページに存在しているすべての文字を適切に変換できます。 ただし、一方のコード ページにあっても、他方のコード ページにない文字の場合は、変換先のコード ページでは表現できません。 たとえば、コード ページ 1252 では、コード ページ 437 しませんに登録商標記号 (?) があります。  
  
 AutoTranslate の設定は、次の変換には影響しません。  
  
-   文字の SQL_C_CHAR クライアント変数と Unicode の間のデータ移動**nchar**、 **nvarchar**、または**ntext**列、変数、またはパラメーターで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
-   Unicode の SQL_C_WCHAR クライアント変数と文字の間のデータ移動**char**、 **varchar**、または**テキスト**列、変数、またはパラメーターで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
 文字から Unicode にデータが移動される場合、データは必ず変換されます。  
  
## <a name="see-also"></a>参照  
 [結果の処理&#40;ODBC&#41;](processing-results-odbc.md)   
 [照合順序と Unicode のサポート](../collations/collation-and-unicode-support.md)  
  
  
