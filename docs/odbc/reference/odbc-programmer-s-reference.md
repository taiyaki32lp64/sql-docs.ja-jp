---
title: ODBC プログラマ&#39;リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd729956ee7bb1fccf7a8fceb7a435042df4df7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111191"
---
# <a name="odbc-programmer39s-reference"></a>ODBC プログラマ&#39;リファレンス
*ODBC プログラマ リファレンス*次のセクションが含まれています。  
  
-   [ODBC 3.8 の新](../../odbc/reference/what-s-new-in-odbc-3-8.md)Windows 8 SDK に追加された新しい ODBC の機能を一覧表示されます。  
  
-   [ODBC プログラムのサンプル](../../odbc/reference/sample-odbc-program.md)ODBC のサンプル プログラムを表示します。  
  
-   [ODBC の概要](../../odbc/reference/introduction-to-odbc.md)構造化照会言語と、ODBC と ODBC インターフェイスの概要についての簡単な歴史を提供します。  
  
-   [アプリケーションの開発](../../odbc/reference/develop-app/developing-applications.md)ODBC インターフェイスとそれを実装するドライバーを使用するアプリケーションの開発に関する情報を格納します。  
  
-   [ODBC ソフトウェアのインストールと構成](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md)のインストールとセットアップ DLL 関数の参照に関する情報を提供します。  
  
-   [ODBC ドライバーの開発](../../odbc/reference/develop-driver/developing-an-odbc-driver.md)ドライバーの記述に関する情報が含まれています。  
  
-   [API リファレンス](../../odbc/reference/syntax/odbc-reference.md)構文とすべての ODBC 関数のセマンティック情報が含まれています。  
  
-   [ODBC の付録](../../odbc/reference/appendixes/odbc-appendixes.md)技術的な詳細を含み、ODBC エラー コード、データ型、および SQL 文法のテーブルを参照します。  
  
## <a name="working-with-the-odbc-documentation"></a>ODBC のドキュメントの操作  
 ODBC インターフェイスは、C プログラミング言語で使用するために設計されています。 ODBC インターフェイスの使用では、3 つの領域に します。SQL ステートメント、ODBC 関数呼び出し、C プログラミングします。 このドキュメントには、次の前提としています。  
  
-   C のプログラミング言語の知識。  
  
-   一般的な DBMS の知識と SQL に精通します。  
  
 次の表記規則が使用されます。  
  
|Format|使用目的|  
|------------|--------------|  
|選択 * から|大文字の文字は、SQL ステートメント、マクロ名、およびオペレーティング システム コマンド レベルで使用される用語を示します。|  
|`RETCODE SQLFetch(hdbc)`|固定幅フォントは、コマンドラインのサンプルとプログラム コードに使用されます。|  
|*argument*|斜体の単語は、プログラムの引数については、ユーザーまたはアプリケーションを提供する必要があります強調を word ことを示します。|  
|**SQLEndTran**|太字では、構文を正確に示すように、関数名を含む入力する必要があることを示します。|  
|&#124;|垂直バーは、構文の行で相互に排他的な 2 つの選択肢を分離します。|  
|[...]|省略記号は、する引数は複数回繰り返すことを示します。|  
|. と呼ばれています。 .|3 つのドットの列では、前のコード行の継続を示します。|  
  
## <a name="about-the-code-examples"></a>コード例について  
 このガイドのコード例は、あくまで説明のために設計されています。 ODBC の原則を示すために主に書き込まれるため、効率性も確保されているわかりやすくするため。 さらに、コードのセクション全体は、わかりやすくするため除外された場合があります。 非 ODBC 関数 (これらの関数が名前が"SQL"で始まらない) およびほとんどのエラー処理の定義が含まれます。  
  
 ANSI 文字列と同じデータベース スキーマの先頭に表示されているすべてのコード例を使用して[カタログ関数](../../odbc/reference/develop-app/catalog-functions.md)します。  
  
## <a name="recommended-reading"></a>推奨トピック  
 SQL の詳細については、次の標準を使用できます。  
  
-   データベースの整合性機能強化、ANSI、1989 ANSI X3.135 1989 と SQL の言語。  
  
-   データベース表現言語 - SQL:ANSI X3H2 および ISO/IEC JTC1/SC21 WG3 9075:1992 (SQL 92)。  
  
-   グループを開く、データ管理:構造化照会言語 (SQL) バージョン 2 (Open Group、1996)。  
  
 多くの書籍を標準とベンダー固有の SQL ガイドだけでなく、SQL をについて説明しますなど。  
  
-   C. J.、Darwen、Hugh での日付:*SQL Standard のガイド*(Addison-wesley、1993)。  
  
-   Emerson、Sandra L.、Darnovsky、Marcy、および Bowman、Judith S.:*実際的な SQL Handbook* (Addison-wesley、1989)。  
  
-   Groff、James R. と Weinberg、Paul N.:*SQL を使用して*(Osborne Mcgraw-hill、1990)。  
  
-   グルーバー、Martin:*SQL を理解する*(Sybex、1990)。  
  
-   回線のモジュラー ジャック L. および林さんの j. Hursch:*SQL、構造化照会言語*(タブ書籍、1988)。  
  
-   Melton、Jim、および Simon、Alan R.:*新しい SQL をについて理解します。完全なガイド*(Morgan Kaufmann 発行元、1993)。  
  
-   Fabian Pascal:*SQL とリレーショナルの基礎*(M & T Books、1990)。  
  
-   Trimble、J. Harvey、Jr. および Chappell、David:*SQL の概要*(Wiley、1989)。  
  
-   Van der Lan、Rick F.:*SQL の概要*(Addison-wesley、1988)。  
  
-   Vang、Soren:*SQL とリレーショナル データベース*(Microtrend 書籍、1990)。  
  
-   Viescas、John:*SQL へのクイック リファレンス ガイド*(Microsoft Corp.、1989)。  
  
 トランザクション処理の詳細については、次を参照してください。  
  
-   グレーの場合、j. n. 最も、Andreas:*トランザクションの処理:概念と手法*(Morgan Kaufmann 発行元、1993)。  
  
-   Hackathorn、Richard D.:*エンタープライズ データベース接続*(Wiley & Sons、1993)。  
  
 コールレベル インターフェイスの詳細については、次の標準を使用できます。  
  
-   Open Group、*データ管理。SQL 呼び出しレベルのインターフェイス (CLI)、C451* (Open Group、1995)。  
  
-   ISO/IEC 9075-3:1995、コールレベル インターフェイス (SQL/CLI)。  
  
 ODBC の詳細については、本の数はなどです。  
  
-   Geiger、Kyle:*ODBC の内部*(Microsoft Press®、1995)。  
  
-   Gryphon、Robert、Charpentier、Luc、Oelschlager、Jon、Shoemaker、Andrew、Jim、クロスと Lilley、Albert W.:*ODBC 2 を使用して*(キュー、1994)。  
  
-   Johnston、Tom および Osborne、マークを付けます。*ODBC の開発者ガイド*(Howard W. Sams & 会社、1994)。  
  
-   北、Ken:*Windows のマルチ DBMS プログラミング:C++、Visual Basic、ODBC、OLE 2 およびツールを使用して、プロジェクトの DBMS* (John Wiley & Sons, inc., 1995)。  
  
-   Stegman、Michael O.、Signore、Robert、および Creamer、John:*ODBC ソリューション、Open Database Connectivity で分散環境*(Mcgraw-hill 刊、1995)。  
  
-   ウェルチ、Keith:*ODBC 2 を使用して*(キュー、1994)。  
  
-   Whiting、請求書:*Teach Yourself 21 日間に ODBC* (Howard W. Sams & 会社、1994)。
