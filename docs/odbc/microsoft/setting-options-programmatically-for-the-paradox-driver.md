---
title: Paradox ドライバーのプログラムでオプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 658d03469e2733b0c25513a4d4a89c6ab88b9852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063513"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Paradox ドライバーのプログラムでオプションの設定

|OPTION|説明|メソッド|  
|------------|-----------------|------------|  
|ディレクトリ|対象となるディレクトリを設定します。|このオプションを動的に設定するには、使用、 **DEFAULTDIR**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|  
|照合順序|シーケンスは、フィールドが並べ替えられます。<br /><br /> シーケンスは、ASCII (既定)、国際化、スウェーデン語、フィンランド語、またはノルウェー語、デンマーク語。|このオプションを動的に設定するには、使用、 **COLLATINGSEQUENCE**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|  
|説明|データ ソース内のデータの説明 (オプション)たとえば、"日付、給与履歴、およびすべての従業員の現在のレビュー。 hire"という|このオプションを動的に設定するには、使用、**説明**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|  
|[Exclusive]|場合、**排他**ボックスがオンの場合、データベースの排他モードで開くし、一度に 1 つだけのユーザーによってアクセスできます。 排他モードで実行する場合、パフォーマンスが向上します。|このオプションを動的に設定するには、使用、**排他**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|  
|Net のスタイル|Paradox データにアクセスするときに使用するネットワーク アクセスのスタイル: いずれか"3*x*"Paradox 3。 *。x*または"4 *。x*"paradox 4 *。x*または 5 *。x*します。 3"に設定することができます。*x*"または"4 *。x*"のバージョンが 4 である場合 *。x*または 5 *。x*バージョンが Paradox 3 の場合は *。x*、スタイルである必要があります"3 *。x*"。|このオプションを動的に設定するには、使用、**不正**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|  
|ページのタイムアウト|削除される前に、(使用しない) 場合、ページがバッファーに残っている 2 番目の部分の 1/10 の期間を指定します。 既定値は 600 秒 (60 秒) の部分の 1/10。 このオプションは、ODBC ドライバーを使用するすべてのデータ ソースに適用されます。<br /><br /> ページのタイムアウトは、固有の遅延のため、0 をすることはできません。 ページのタイムアウトは、その値を下回るページのタイムアウト オプションが設定されている場合でも、本質的な遅延よりも小さくできません。|このオプションを動的に設定するには、使用、 **PAGETIMEOUT**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|  
|[読み取り専用]|読み取り専用データベースを指定します。|このオプションを動的に設定するには、使用、 **READONLY**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|  
|ディレクトリを選択します|アクセスするファイルを含むディレクトリを選択するダイアログ ボックスが表示されます。<br /><br /> ときに、最もよく使用されているファイル ディレクトリを指定してデータのソース ディレクトリを定義するが配置されています。 ODBC ドライバーは、このディレクトリを既定のディレクトリとして使用します。 頻繁に使用される場合は、その他のファイルをこのディレクトリにコピーします。 または、ディレクトリの名前を持つ SELECT ステートメント内のファイル名を修飾することができます。<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 使用して、新しい既定のディレクトリを指定することも、 **SQLSetConnectOption**関数 SQL_CURRENT_QUALIFIER オプションを使用します。|このオプションを動的に設定するには、使用、 **DEFAULTDIR**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|  
|ネットワーク ディレクトリを選択します。|Pdoxusrs.net ファイルが含まれているために、ロックの paradox を含むディレクトリの完全なパス (Paradox 4 *。x*) または Paradox.net ファイル (Paradox 5 *。x*)。 ディレクトリがこれらのファイルのいずれかにもない場合、Paradox ドライバーを作成します。 これらのファイルについては、Paradox ドキュメントを参照してください。<br /><br /> ネットワーク ディレクトリを選択するで Paradox ユーザー名を入力する必要があります、**ユーザー名**テキスト ボックス。 クリックして**ネットワーク ディレクトリの選択**ネットワーク ディレクトリを選択します。|このオプションを動的に設定するには、使用、 **PARADOXNETPATH**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|  
|[ユーザー名]|Paradox のユーザー名。 これは、ロックが発生した場合に、Paradox ファイルの他のユーザーに表示される名前です。|このオプションを動的に設定するには、使用、 **PARADOXUSERNAME**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)します。|
