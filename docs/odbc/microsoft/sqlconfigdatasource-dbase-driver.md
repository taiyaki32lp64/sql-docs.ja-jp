---
title: SQLConfigDataSource (dBASE ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 569a83110d7d5a3cd25eed8f68753d13793f8b10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054099"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE ドライバー)
> [!NOTE]  
>  このトピックでは、dBASE ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 **SQLConfigDataSource**関数を追加するには、次の変更、またはデータ ソースの削除が動的に、次のキーワードを使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|シーケンスは、フィールドが並べ替えられます。<br /><br /> シーケンスを指定できます。ASCII (既定値) または国際します。<br /><br /> これは、と同じオプション設定**照合シーケンス**設定 ダイアログ ボックスをオンにします。|  
|DEFAULTDIR|ディレクトリ パスの指定。|  
|DELETED|DBASE ドライバーの場合は、削除済みとしてマークされている行の取得やに配置されているかどうかを指定します。 場合 1 の場合、削除された行に設定するには表示されません。0 の場合、削除された行に設定する場合、同じ行の削除されていないよう扱われます。<br /><br /> これは、と同じオプション設定**削除された行を表示する**セットアップ ダイアログ ボックス。|  
|DESCRIPTION|データ ソース内のデータの説明。<br /><br /> これは、と同じオプション設定**説明**設定 ダイアログ ボックスをオンにします。|  
|DRIVER|ドライバー DLL パスの指定。|  
|DRIVERID|ドライバーの整数の ID。<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|ファイル dBase III、IV、dBase ファイルまたは dBase 5 を入力します。|  
|PAGETIMEOUT|削除される前に、(使用しない) 場合、ページがバッファーに残っている 2 番目の部分の 1/10 の期間を指定します。 既定値は 600 秒 (60 秒) の部分の 1/10。 このオプションは、ODBC ドライバーを使用するすべてのデータ ソースに適用されることに注意してください。<br /><br /> これは、と同じオプション設定**ページのタイムアウト**設定 ダイアログ ボックスをオンにします。|  
|READONLY|読み取り専用ファイルを作成する場合は TRUE読み取り専用ファイルを作成する場合は FALSE。<br /><br /> これは、と同じオプション設定**読み取り専用**セットアップ ダイアログ ボックス。|  
|STATISTICS|DBASE ドライバーの場合は、テーブル サイズの統計情報を近似するかどうかを判断します。 このオプションは、ODBC ドライバーを使用するすべてのデータ ソースに適用されることに注意してください。<br /><br /> これは、と同じオプション設定**行カウントの概数**設定 ダイアログ ボックスをオンにします。|  
|スレッド|使用するエンジンのバック グラウンド スレッドの数。 この値は 3 であるため、変更することはできません。<br /><br /> これは、と同じオプション設定**スレッド**設定 ダイアログ ボックスをオンにします。|
