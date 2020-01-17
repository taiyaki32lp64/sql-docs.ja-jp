---
title: 接続文字列の形式と属性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a007f4c7c92bf4254e4d36638cf2d92ba0764be5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082019"
---
# <a name="connection-string-format-and-attributes"></a>接続文字列の形式と属性
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 ダイアログ ボックスを使用する代わりに、一部のアプリケーションはデータ ソース接続情報を指定する接続文字列を必要があります。 接続文字列は、ドライバーがデータ ソースに接続する方法を指定する属性の数値で構成されます。 属性は、特定のドライバーが、適切なデータ ソース接続を行うには理解する必要がある情報を識別します。 さまざまな属性のセットがあり、各ドライバーが、接続文字列の形式は常に同じです。 接続文字列では、次の形式があります。  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Microsoft ODBC Driver for Oracle を使用すると、ドライバーの最初のバージョンの接続文字列の形式をサポートしている`CONNECTSTRING`の代わりに =`SERVER=`します。  
  
 指定する必要があります Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうか、`Trusted_Connection=yes`接続文字列でユーザー ID とパスワードの情報の代わりにします。  
  
 データ ソースを指定する必要があります、UID、PWD、サーバー (または CONNECTSTRING) を指定しない場合は名前とドライバーの属性。 ただし、その他のすべての属性は省略可能です。 関連する DSN タブで指定されている場合は、属性を指定しないと、その属性の既定値、 **ODBC データ ソース アドミニストレーター**  ダイアログ ボックス。 属性の値は大文字小文字を区別することはあります。  
  
 接続文字列の属性は次のとおりです。  
  
|属性|説明|既定値|  
|---------------|-----------------|-------------------|  
|DSN|データ ソース名の一覧の ドライバー タブで、 **ODBC データ ソース アドミニストレーター**  ダイアログ ボックス。|""|  
|PWD|アクセスする Oracle サーバーのパスワード。 このドライバーは、Oracle は、パスワードの配置の制限をサポートします。|""|  
|SERVER|アクセスする Oracle サーバーへの接続文字列。|""|  
|UID|Oracle サーバーのユーザー名。 システムに応じて、この属性は省略可能なできない可能性があります - は、特定のデータベースとテーブルが必要ですがこの属性セキュリティ上の理由。<br /><br /> 「/」を使用して Oracle の使用のシステムの認証を操作します。|""|  
|BUFFERSIZE|列をフェッチするときに使用される最適なバッファー サイズ。<br /><br /> Oracle サーバーから 1 つのフェッチがこのサイズのバッファーを入力するための十分な行を返されるようにをフェッチしています。 ドライバーが最適化されます。 大きな値は、大量のデータをフェッチする場合は、パフォーマンスを向上する傾向があります。|65535|  
|SYNONYMCOLUMNS|この値が true の場合 (1)、SQLColumn () API の呼び出しは、列情報を返します。 それ以外の場合、SQLColumn () は、テーブルおよびビューの列のみを返します。 ODBC Driver for Oracle は、この値が設定されていないときに、高速アクセスを提供します。|1|  
|REMARKS|この値が true の場合 (1)、ドライバーは、「解説」列を返します、 [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)結果セット。 ODBC Driver for Oracle は、この値が設定されていないときに、高速アクセスを提供します。|0|  
|StdDayOfWeek|DAYOFWEEK スカラー ODBC 標準を適用します。 既定ではこれが有効ですが、ローカライズされたバージョンが必要なユーザーは、Oracle の値をそのまま使用する動作を変更できます。|1|  
|GuessTheColDef|ドライバーが 0 以外の値を返すかどうかを指定します、 *cbColDef*の引数**SQLDescribeCol**します。 場所がない Oracle 定義のスケールでは、計算など、数値列にのみ適用される列とせず、有効桁数または小数点数として定義されている列。 A **SQLDescribeCol** Oracle にその情報が提供されない場合に、有効桁数の返します 130 を呼び出します。|0|  
  
 たとえば、MyOracleServerOracle Server と Oracle のユーザー MyUserID を使用して MyDataSource データ ソースに接続する接続文字列は次のようになります。  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 オペレーティング システムの認証と MyOtherOracleServerOracle サーバーを使用して MyOtherDataSource データ ソースに接続する接続文字列は次のようになります。  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
