---
title: DBASE ドライバーのプログラムでオプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27f675cca5115a8336f2be4b7fa96c091aee1b62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063561"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>dBASE ドライバーのプログラムでオプションの設定

|OPTION|説明|メソッド|  
|------------|-----------------|------------|  
|おおよその行数|テーブル サイズの統計情報を近似するかどうかを判断します。 このオプションは、ODBC ドライバーを使用するすべてのデータ ソースに適用されます。|このオプションを動的に設定するには、使用、**統計**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|  
|照合順序|シーケンスは、フィールドが並べ替えられます。<br /><br /> シーケンスを指定できます。ASCII (既定値) または国際します。|このオプションを動的に設定するには、使用、 **COLLATINGSEQUENCE**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|  
|Data Source Name|給与または担当者など、データ ソースを識別する名前。|このオプションを動的に設定するには、使用、 **DSN**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|  
|[データベース]|Microsoft Access データ ソースは、選択するか、データベースを作成することがなく設定できます。 セットアップ時にデータベースが指定されていない場合は、データ ソースに接続するときにデータベース ファイルを選択するユーザーが求められます。|このオプションを動的に設定するには、使用、 **DBQ**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|  
|説明|データ ソース内のデータの説明 (オプション)たとえば、"日付、給与履歴、およびすべての従業員の現在のレビュー。 hire"という|このオプションを動的に設定するには、使用、**説明**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|  
|[Exclusive]|場合、**排他**ボックスがオンの場合、データベースの排他モードで開くし、一度に 1 つだけのユーザーによってアクセスできます。 排他モードでの実行時のパフォーマンスが向上します。|このオプションを動的に設定するには、使用、**排他**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|  
|ページのタイムアウト|部分ページ (使用しない) 場合は、削除される前に、バッファーに残っている 1 秒の 1/10 の期間を指定します。 既定値は 600 秒 (60 秒) の部分の 1/10。 このオプションは、ODBC ドライバーを使用するすべてのデータ ソースに適用されます。<br /><br /> ページのタイムアウトは、固有の遅延のため、0 をすることはできません。 ページのタイムアウトは、その値を下回るページのタイムアウト オプションが設定されている場合でも、本質的な遅延よりも小さくできません。|このオプションを動的に設定するには、使用、 **PAGETIMEOUT**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|  
|[読み取り専用]|読み取り専用データベースを指定します。|このオプションを動的に設定するには、使用、 **READONLY**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|  
|ディレクトリを選択します|アクセスするファイルを含むディレクトリを選択するダイアログ ボックスが表示されます。<br /><br /> データのソース ディレクトリを定義するときに、最もよく使用されるファイルが配置されているディレクトリを指定します。 ODBC ドライバーは、このディレクトリを既定のディレクトリとして使用します。 頻繁に使用される場合は、その他のファイルをこのディレクトリにコピーします。 または、ディレクトリの名前を持つ SELECT ステートメント内のファイル名を修飾することができます。<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 使用して、新しい既定のディレクトリを指定することも、 **SQLSetConnectOption**関数 SQL_CURRENT_QUALIFIER オプションを使用します。|このオプションを動的に設定するには、使用、 **DEFAULTDIR**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|  
|削除された行を表示します。|削除済みとしてマークされている行の取得やに配置されているかどうかを指定します。 オフの場合、削除された行は表示されません。削除された行が扱われる選択した場合、削除されていない行と同じです。 既定値はオフです。|このオプションを動的に設定するには、使用、 **DELETED**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)します。|
