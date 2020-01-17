---
title: テキスト ファイル ドライバーのプログラムでオプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e1a28e5c7ccf3c701e5f97440cd97ed843ab53dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063503"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>テキスト ファイル ドライバーのプログラムでオプションの設定

|OPTION|説明|メソッド|  
|------------|-----------------|------------|  
|Data Source Name|給与または担当者など、データ ソースを識別する名前。|このオプションを動的に設定するには、使用、 **DSN**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)します。|  
|形式を定義します。|表示、**テキスト形式の定義** ダイアログ ボックス データ ソース ディレクトリ内の個々 のテーブルのスキーマを指定することができます。|このオプションへの呼び出しによって動的に設定することはできません[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)します。|  
|説明|データ ソース内のデータの説明 (オプション)たとえば、"日付、給与履歴、およびすべての従業員の現在のレビュー。 hire"という|このオプションを動的に設定するには、使用、**説明**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)します。|  
|ディレクトリ|対象となるディレクトリを選択します。|このオプションを動的に設定するには、使用、 **DEFAULTDIR**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)します。|  
|拡張機能の一覧|データ ソース上のテキスト ファイルのファイル名拡張子の一覧を表示します。 テキストのドライバーを使用すると、拡張機能を持たない名前で、CREATE TABLE ステートメントが実行されると、拡張子なしのファイルが作成されます。 その他のドライバーは、拡張機能が指定されていない場合、既定の拡張子を持つファイルを作成します。 拡張子が .txt ファイルを作成するには、名前で、拡張機能を含める必要があります。 拡張子のないファイルを表示する、**テキスト形式の定義**ダイアログ ボックスで、"* です"。 拡張機能の一覧に追加する必要があります。|このオプションを動的に設定するには、使用、**拡張**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|[読み取り専用]|読み取り専用データベースを指定します。|このオプションを動的に設定するには、使用、 **READONLY**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)します。|  
|スキャンする行|各列のデータ型を決定するをスキャンする行の数。 検出されたデータの種類の最大数を指定されたデータ型が決定されます。 列のデータ型に一致しないデータが発生した場合、データ型が NULL 値として返されます。<br /><br /> テキスト ドライバーでは、する可能性がありますの番号を入力 1 から 32767 まで; をスキャンする行の数ただし、この値は、25 は既定は常にします。 (上限外の数値はエラーを返します。)|このオプションを動的に設定するには、使用、 **MAXSCANROWS**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)します。|  
|ディレクトリを選択します|アクセスするファイルを含むディレクトリを選択するダイアログ ボックスが表示されます。<br /><br /> ときに、最もよく使用されているファイル ディレクトリを指定してデータのソース ディレクトリを定義するが配置されています。 ODBC ドライバーは、このディレクトリを既定のディレクトリとして使用します。 頻繁に使用される場合は、その他のファイルをこのディレクトリにコピーします。 または、ディレクトリの名前を持つ SELECT ステートメント内のファイル名を修飾することができます。 `SELECT * FROM C:\MYDIR\EMP`<br /><br /> 使用して、新しい既定のディレクトリを指定することも、 **SQLSetConnectOption**関数 SQL_CURRENT_QUALIFIER オプションを使用します。|このオプションを動的に設定するには、使用、 **DEFAULTDIR**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)します。|
