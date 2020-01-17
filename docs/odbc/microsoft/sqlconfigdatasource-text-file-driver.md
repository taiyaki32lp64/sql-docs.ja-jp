---
title: SQLConfigDataSource (テキスト ファイル ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46bb00fb01ed3fee8098420794af089f2d8b981e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054085"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (テキスト ファイル ドライバー)
> [!NOTE]  
>  このトピックでは、テキスト ファイル ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 **SQLConfigDataSource**関数を追加するには、次の変更、またはデータ ソースの削除が動的に、次のキーワードを使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|文字セット|OEM または ANSI テキスト ドライバー。|  
|COLNAMEHEADER|テキストのドライバーの場合は、データの最初のレコードが列名を指定するかどうかを示します。 TRUE または FALSE のいずれか。|  
|DEFAULTDIR|ディレクトリ パスの指定。|  
|DESCRIPTION|データ ソース内のデータの説明。<br /><br /> これは、と同じオプション設定**説明**設定 ダイアログ ボックスをオンにします。|  
|DRIVER|ドライバー DLL パスの指定。|  
|DRIVERID|ドライバーの整数の ID。 27 (テキスト)|  
|拡張機能|データ ソース上のテキスト ファイルのファイル名拡張子の一覧を表示します。<br /><br /> これは、と同じオプション設定**拡張機能の一覧**設定 ダイアログ ボックスをオンにします。|  
|FIL|テキスト ファイルの種類|  
|ファイルの種類|テキストのドライバー (テキスト) のファイルの種類。|  
|FORMAT|テキスト ドライバー、FIXEDLENGTH、または指定できます TABDELIMITED、CSVDELIMITED (コンマ) を DELIMITED() (によって、かっこで指定された特殊文字)。 特殊文字 1 文字であり、文字、10 進または 16 進数の形式であることができます。|  
|MAXSCANROWS|既存のデータに基づく列のデータ型を設定するときにスキャンする行の数。<br /><br /> テキスト ドライバーの場合を入力できます数値 1 から 32767 まで; をスキャンする行の数ただし、この値は、25 は既定は常にします。 (上限外の数値はエラーを返します。)<br /><br /> これは、と同じオプション設定**スキャンする行**設定 ダイアログ ボックスをオンにします。|  
|READONLY|読み取り専用ファイルを作成する場合は TRUE読み取り専用ファイルを作成する場合は FALSE。<br /><br /> これは、と同じオプション設定**読み取り専用**セットアップ ダイアログ ボックス。|
