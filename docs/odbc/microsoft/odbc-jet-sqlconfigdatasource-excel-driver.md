---
title: ODBC Jet SQLConfigDataSource (Excel ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab33bfdef2b633cd5a7a3e215a3f6522d8d664ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915701"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Excel ドライバー)
> [!NOTE]  
>  このトピックでは、Excel ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 **SQLConfigDataSource**関数を追加するには、次の変更、またはデータ ソースの削除が動的に、次のキーワードを使用します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|DBQ|Microsoft Excel ドライバーの Microsoft Excel 5.0 またはそれ以降のファイルにアクセスするときにブック ファイルの名前。<br /><br /> これは、と同じオプション設定**データベース**設定 ダイアログ ボックスをオンにします。|  
|DEFAULTDIR|ディレクトリ パスの指定。<br /><br /> これは、と同じオプション設定**ディレクトリの選択**または**ブックの選択**設定 ダイアログ ボックスをオンにします。|  
|DESCRIPTION|データ ソース内のデータの説明。<br /><br /> これは、と同じオプション設定**説明**設定 ダイアログ ボックスをオンにします。|  
|DRIVER|ドライバー DLL パスの指定。|  
|DRIVERID|ドライバーの整数の ID。<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0 または 7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|ファイルの種類、たとえば、Excel 3.0、Excel 4.0、Excel 5.0、Excel 7.0、Excel 97、Excel 2000、または Excel 2003。|  
|消えて|かどうか、範囲の最初の行のセルがテーブル (1) の列名を含めるかどうかを示します (0)。|  
|MAXSCANROWS|既存のデータに基づく列のデータ型を設定するときにスキャンする行の数。<br /><br /> スキャンする行の 1 から 16 の数値を入力できます。 値の既定値は 8 です。0 に設定されている場合は、すべての行がスキャンされます。 (上限外の数値はエラーを返します。)<br /><br /> これは、と同じオプション設定**スキャンする行**設定 ダイアログ ボックスをオンにします。|  
|READONLY|読み取り専用ファイルを作成する場合は TRUE読み取り専用ファイルを作成する場合は FALSE。<br /><br /> これは、と同じオプション設定**読み取り専用**セットアップ ダイアログ ボックス。|  
|スレッド|使用するエンジンのバック グラウンド スレッドの数。 Microsoft Access ドライバーの場合は、この値は、既定値は、3 が、変更することができます。 Dbase MicrosoftExceldriver この値は 3 であり、変更することはできません。<br /><br /> これは、と同じオプション設定**スレッド**設定 ダイアログ ボックスをオンにします。|
