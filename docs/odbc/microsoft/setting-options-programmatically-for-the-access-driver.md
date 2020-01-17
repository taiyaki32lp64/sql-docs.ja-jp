---
title: プログラムで Access ドライバーのオプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 688716e9b7ba89500a4d2e8a579da42972e43d0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063552"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>プログラムで Access ドライバーのオプションの設定

|OPTION|説明|メソッド|  
|------------|-----------------|------------|  
|バッファー サイズ|内部バッファーのキロバイト単位でディスクとデータの転送を Microsoft Access で使用されるサイズ。 既定のバッファー サイズは、2048 の KB (2048 として表示されますです)。 256 で割り切れる任意の整数値を入力することができます。|このオプションを動的に設定する呼び出しで MAXBUFFERSIZE キーワードを使用して、 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|  
|Data Source Name|給与または担当者など、データ ソースを識別する名前。|このオプションを動的に設定するには、使用、 **DSN**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|  
|[データベース]|Microsoft Access データ ソースは、選択するか、データベースを作成することがなく設定できます。 セットアップ時にデータベースが指定されていない場合、ユーザーは、データ ソースに接続するときに、データベース ファイルを選択を求めます。|このオプションを動的に設定するには、使用、 **DBQ**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|  
|説明|データ ソース内のデータの説明 (オプション)たとえば、"日付、給与履歴、およびすべての従業員の現在のレビュー。 hire"という|このオプションを動的に設定するには、使用、**説明**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|  
|[Exclusive]|場合、**排他**ボックスがオンの場合、データベースの排他モードで開くし、一度に 1 つだけのユーザーによってアクセスできます。 排他モードで実行する場合、パフォーマンスが向上します。|このオプションを動的に設定するには、使用、**排他**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|  
|ImplicitCommitSync|トランザクションの外部で行われた変更がデータベースに書き込まれる方法を決定します。 この値は"Yes"は、Microsoft Access ドライバーが完了する内部/暗黙のトランザクションでコミットを待つことを意味する最初に設定されます。|このオプションが記載されて、**高度なオプションの設定**Microsoft Access ドライバーのダイアログ ボックス。|  
|ページのタイムアウト|削除される前に、(使用しない) 場合、ページがバッファーに残っている、ミリ秒単位で時間の期間を指定します。 Microsoft Access ドライバーを既定値は 500 ミリ秒 (0.5 秒) です。 このオプションは、ODBC ドライバーを使用するすべてのデータ ソースに適用されます。<br /><br /> ページのタイムアウトは、固有の遅延のため、0 をすることはできません。 ページのタイムアウトは、その値を下回るページのタイムアウト オプションが設定されている場合でも、本質的な遅延よりも小さくできません。|このオプションを動的に設定するには、使用、 **PAGETIMEOUT**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|  
|[読み取り専用]|読み取り専用データベースを指定します。|このオプションを動的に設定するには、使用、 **READONLY**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|  
|システム データベース|アクセスする Microsoft Access データベースで使用する Microsoft Access のシステム データベースの完全パス。<br /><br /> をクリックして、**システム データベース** ボタンを使用するシステム データベースを選択します。 Microsoft Access の ODBC ドライバーでは、ユーザー名とパスワードが求められます。 既定の名前は管理者と管理者ユーザーの Microsoft Access での既定のパスワードが空の文字列。<br /><br /> Microsoft Access データベースのセキュリティを向上させるのに管理者ユーザーを置き換えるし、管理者ユーザーを削除する新しいユーザーを作成または管理者のユーザーがアクセスを持っているオブジェクトを変更します。|このオプションを動的に設定するには、使用、 **SYSTEMDB**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|  
|スレッド数|使用するエンジンのバック グラウンド スレッドの数。 Microsoft Access ドライバーの場合は、この値は、既定値は、3 が、変更することができます。 ユーザーは、大量のデータベース内のアクティビティがある場合は、スレッドの数を増やす可能性があります。<br /><br /> このオプションが記載されて、**高度なオプションの設定**Microsoft Access ドライバーのダイアログ ボックス。|このオプションを動的に設定するには、使用、**スレッド**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|  
|UserCommitSync|Microsoft Access ドライバーが明示的なユーザー定義のトランザクションを非同期的に実行されるかどうかを判断します。 この値は"Yes"は、Microsoft Access ドライバーが完了するユーザー定義のトランザクションでコミットを待つことを意味する最初に設定されます。<br /><br /> このオプションを False に設定すると、マルチ ユーザー環境で予期しない結果をことができます。|このオプションを動的に設定するには、使用、 **USERCOMMITSYNC**への呼び出しでキーワード[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)します。|
