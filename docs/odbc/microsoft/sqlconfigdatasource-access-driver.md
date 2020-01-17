---
title: SQLConfigDataSource (Access ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85b515ed4c30d68e62a49e1044c4ddf6f5cc5ab1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985235"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Access ドライバー)
> [!NOTE]  
>  このトピックでは、Access ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 **SQLConfigDataSource**関数を追加するには、次の変更、またはデータ ソースの削除が動的に、次のキーワードを使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|シーケンスは、フィールドが並べ替えられます。<br /><br /> これは、と同じオプション設定**照合シーケンス**設定 ダイアログ ボックスをオンにします。|  
|COMPACT_DB|データベース ファイルに対してデータ圧縮を実行します。 次の形式があります。COMPACT_DB = < path_name >< optionaL_sort_order >\<省略可能な暗号化キーワード >。<br /><br /> COMPACT_DB キーワードを使用して、DSN キーワードを使用して同じステートメント内で、このドライバーは、DSN キーワードを無視します。 したがって、データベースを最適化して、DSN を指定することは、2 段階のプロセスです。|  
|CREATE_DB|データベース ファイルを作成します。 次の形式があります。CREATE_DB = < path_name >\<optional_sort 順序 >< optional_ENCRYPT キーワード > パス名が Microsoft Access データベースへの完全パス。 エラーが、パス名が既存のデータベースを指定する場合に返されます。 並べ替え順序は、Microsoft へのアクセスのセットアップ ダイアログ ボックスで、作成 ボタンが押されたときに表示される新しいデータベース ダイアログ ボックスをセットとしてになります。 並べ替え順序が指定されていない場合は、[全般] が使用されます。<br /><br /> CREATE_DB キーワードを使用して、DSN キーワードを使用して同じステートメント内で、このドライバーは、DSN キーワードを無視します。 したがって、データベースを作成し、DSN を指定することは、2 段階のプロセスです。を作成する Microsoft Access データベースのパス名には、1 つ以上のスペースが含まれている場合の、CREATE_DB キーワードを使用する場合、パス名全体囲む必要があります、二重引用符で次の例に示すように。<br /><br /> "C:\PROGRAM files \common FILES files \ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (引用符は必要に応じて)|  
|CREATE_SYSDB|システム データベース ファイルを作成します。 次の形式があります。CREATE_SYSDB =\<パス名 >\<並べ替え順序では省略可能 > パス名は、Microsoft Access データベースへの完全パスです。 エラーが、パス名が既存のデータベースを指定する場合に返されます。 並べ替え順序をセットのようになります、**新しいデータベース** ダイアログ ボックスが表示されるときに、**作成**のボタンがクリックされた、 **ODBC Microsoft アクセスのセットアップ** ダイアログ ボックス。 並べ替え順序が指定されていない場合は、[全般] が使用されます。|  
|CREATE_V2DB|Microsoft Access の 2.0 と互換性があるデータベース ファイルを作成します。 次の形式があります。CREATE_V2DB =\<パス名 >\<並べ替え順序では省略可能 > パス名は、Microsoft Access データベースへの完全パスです。 エラーが、パス名が既存のデータベースを指定する場合に返されます。 並べ替え順序は、Microsoft へのアクセスのセットアップ ダイアログ ボックスで、作成 ボタンが押されたときに表示される新しいデータベース ダイアログ ボックスをセットとしてになります。 並べ替え順序が指定されていない場合は、[全般] が使用されます。<br /><br /> CREATE_V2DB キーワードを使用して、DSN キーワードを使用して同じステートメント内で、このドライバーは、DSN キーワードを無視します。 したがって、データベースを作成し、DSN を指定することは、2 段階のプロセスです。<br /><br /> を作成する Microsoft Access データベースのパス名には、1 つ以上のスペースが含まれている場合の、CREATE_V2DB キーワードを使用する場合、パス名全体囲む必要があります、二重引用符で次の例に示すように。<br /><br /> "C:\PROGRAM files \common FILES files \ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (引用符は必要に応じて)|  
|DBQ|データベース ファイルの名前。<br /><br /> これは、と同じオプション設定**データベース**設定 ダイアログ ボックスをオンにします。|  
|DEFAULTDIR|データベース ファイルへのパスの指定。|  
|DESCRIPTION|データ ソース内のデータの説明。<br /><br /> これは、と同じオプション設定**説明**設定 ダイアログ ボックスをオンにします。|  
|DRIVER|ドライバー DLL パスの指定。|  
|DRIVERID|ドライバーの整数の ID。  25 (Microsoft Access)|  
|FIL|ファイルの種類の Microsoft Access の MS Access|  
|IMPLICITCOMMITSYNC|Microsoft Access ドライバーが内部または暗黙的なコミットを非同期的に実行されるかどうかを判断します。 この値は"Yes"は、Microsoft Access ドライバーが完了する内部/暗黙のトランザクションでコミットを待つことを意味する最初に設定されます。<br /><br /> このオプションの値は、結果を慎重に検討することがなく変更しないでください。 オプションの詳細については、次を参照してください。、 *Microsoft Jet データベース エンジン プログラマー ガイド*します。<br /><br /> これは、と同じオプション設定**ImplicitCommitSync**設定 ダイアログ ボックスをオンにします。|  
|MAXBUFFERSIZE|内部バッファーのキロバイト単位でディスクとデータの転送を Microsoft Access で使用されるサイズ。 既定のバッファー サイズは、2048 の KB (2048 として表示されますです)。 256 で割り切れる任意の整数値を使用できます。 これは、と同じオプション設定**バッファー サイズ**設定 ダイアログ ボックスをオンにします。|  
|MAXSCANROWS|既存のデータに基づく列のデータ型を設定するときにスキャンする行の数。<br /><br /> スキャンする行の 1 から 16 の数値を入力できます。 値の既定値は 8 です。0 に設定されている場合は、すべての行がスキャンされます。 (上限外の数値はエラーを返します。)<br /><br /> これは、と同じオプション設定**スキャンする行**設定 ダイアログ ボックスをオンにします。|  
|PAGETIMEOUT|削除される前に、(使用しない) 場合、ページがバッファーに残っている、ミリ秒単位で時間の期間を指定します。 既定では (0.5 秒) の 2 つ目の 5-10 分です。 このオプションは、ODBC ドライバーを使用するすべてのデータ ソースに適用されることに注意してください。<br /><br /> これは、と同じオプション設定**ページのタイムアウト**設定 ダイアログ ボックスをオンにします。|  
|PWD|パスワード。|  
|READONLY|読み取り専用ファイルを作成する場合は TRUE読み取り専用ファイルを作成する場合は FALSE。<br /><br /> これは、と同じオプション設定**読み取り専用**セットアップ ダイアログ ボックス。|  
|REPAIR_DB|コミット処理中に発生する障害によって損傷しているデータベースを修復します。<br /><br /> REPAIR_DB キーワードを使用して、DSN キーワードを使用して同じステートメント内で、このドライバーは、DSN キーワードを無視します。 したがって、データベースを修復して、DSN を指定することは、2 段階のプロセスです。|  
|SYSTEMDB|Microsoft Access ドライバーの場合、システム データベース ファイルにパスを指定します。<br /><br /> これは、と同じオプション設定**システム データベース**設定 ダイアログ ボックスをオンにします。|  
|スレッド|使用するエンジンのバック グラウンド スレッドの数。 この値は、既定値は、3 が、変更することができます。<br /><br /> これは、と同じオプション設定**スレッド**設定 ダイアログ ボックスをオンにします。|  
|UID|Microsoft Access ドライバーの場合は、ユーザー ID の名前は、ログインに使用します。|  
|USERCOMMITSYNC|Microsoft Access ドライバーがユーザー定義のトランザクションを非同期的に実行されるかどうかを判断します。 この値は"Yes"は、Microsoft Access ドライバーが完了するユーザー定義のトランザクションでコミットを待つことを意味する最初に設定されます。<br /><br /> このオプションの値は、結果を慎重に検討することがなく変更しないでください。 オプションの詳細については、次を参照してください。、 *Microsoft Jet データベース エンジン プログラマー ガイド*します。<br /><br /> これは、と同じオプション設定**UserCommitSync**設定 ダイアログ ボックスをオンにします。|
