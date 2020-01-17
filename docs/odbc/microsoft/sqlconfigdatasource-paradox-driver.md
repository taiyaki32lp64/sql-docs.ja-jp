---
title: SQLConfigDataSource (Paradox ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 33cc778d921b90a460dab6bda352fd7627d2cf7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054073"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Paradox ドライバー)
> [!NOTE]  
>  このトピックでは、Paradox ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 **SQLConfigDataSource**関数を追加するには、次の変更、またはデータ ソースの削除が動的に、次のキーワードを使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|シーケンスは、フィールドが並べ替えられます。<br /><br /> Paradox ドライバーを使用する場合、シーケンスが ASCII (既定値) を指定できます、国際化、スウェーデン語、フィンランド語、またはノルウェー語、デンマーク語。<br /><br /> これは、と同じオプション設定**照合シーケンス**設定 ダイアログ ボックスをオンにします。|  
|DBQ|データベース ファイルの名前。<br /><br /> これは、と同じオプション設定**データベース**設定 ダイアログ ボックスをオンにします。|  
|DEFAULTDIR|ディレクトリ パスの指定。|  
|DESCRIPTION|データ ソース内のデータの説明。<br /><br /> これは、と同じオプション設定**説明**設定 ダイアログ ボックスをオンにします。|  
|DRIVER|ドライバー DLL パスの指定。|  
|DRIVERID|ドライバーの整数の ID。<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (paradox 4.x)<br /><br /> 538 (paradox 5.x)|  
|排他的|データベースが (一度に 1 つだけのユーザーによってアクセス)、排他モードで開くか、共有モード (一度に 1 つ以上のユーザーによってアクセス) かどうか決定します。 (排他モード) を true または false (共有モード) を指定できます。<br /><br /> これは、と同じオプション設定**排他**設定 ダイアログ ボックスをオンにします。|  
|FIL|ファイルの種類 Paradox 3.x、Paradox 4.x、または Paradox 5.x|  
|ファイルの種類|テキストのドライバー (テキスト) のファイルの種類。|  
|PAGETIMEOUT|削除される前に、(使用しない) 場合、ページがバッファーに残っている 2 番目の部分の 1/10 の期間を指定します。 既定値は 600 秒 (60 秒) の部分の 1/10。 このオプションは、ODBC ドライバーを使用するすべてのデータ ソースに適用されることに注意してください。<br /><br /> これは、と同じオプション設定**ページのタイムアウト**設定 ダイアログ ボックスをオンにします。|  
|PARADOXNETPATH|PDOXUSRS.net ファイルが含まれているために、ロックの paradox を含むディレクトリの完全なパス (Paradox 4 *。x*) または PARADOX.net ファイル (Paradox 5 *。x*)。 ディレクトリがこれらのファイルのいずれかにもない場合、Paradox ドライバーを作成します。 これらのファイルについては、Paradox ドキュメントを参照してください。<br /><br /> ネットワーク ディレクトリを選択する前に、Paradox のユーザー名を入力する必要があります。<br /><br /> これは、と同じオプション設定**ネットワーク ディレクトリの選択**セットアップ ダイアログ ボックス。|  
|不正|ネットワーク アクセス Paradox データにアクセスするときに使用するスタイルを Paradox ドライバーの場合: Paradox 3 のいずれか"3.x"。*x*または"4.x"Paradox 4 for *。x*または 5 *。x*します。 バージョンが Paradox 4 の場合は、"3.x"または"4.x"に設定できます。*x*または 5 *。x*バージョンが Paradox 3 の場合は *。x*スタイルが"3.x"にする必要があります。<br /><br /> これは、と同じオプション設定**Net スタイル**セットアップ ダイアログ ボックス。|  
|PARADOXUSERNAME|Paradox ドライバーの場合 Paradox のユーザー名。<br /><br /> これは、と同じオプション設定**ユーザー名**設定 ダイアログ ボックスをオンにします。|  
|PWD|パスワード。<br /><br /> これはオプションのキーワードであり、ドライバーによって、ファイルに書き込むことはありません。 呼び出しで使用される**SQLDriverConnect** Paradox のパスワードで保護されたファイルに対して。 テーブルが開かれるたびに、使用するパスワードが有効になります。 接続文字列にパスワードが渡されない場合、そのテーブルのパスワードは確立されません。 テーブルには、異なるパスワードがある、同じのセッションでは、複数開くことができません。 また、テーブルを結合することができます。|  
|READONLY|読み取り専用ファイルを作成する場合は TRUE読み取り専用ファイルを作成する場合は FALSE。<br /><br /> これは、と同じオプション設定**読み取り専用**セットアップ ダイアログ ボックス。|  
|スレッド|使用するエンジンのバック グラウンド スレッドの数。 この値は 3 であるため、変更することはできません。<br /><br /> これは、と同じオプション設定**スレッド**設定 ダイアログ ボックスをオンにします。|
