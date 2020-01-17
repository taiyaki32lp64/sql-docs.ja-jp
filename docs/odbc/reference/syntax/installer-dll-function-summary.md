---
title: インストーラー DLL 関数の概要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6d2a865764a3d802a7e5a5341226d7d1aa855f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095680"
---
# <a name="installer-dll-function-summary"></a>インストーラー DLL 関数の概要
次の表では、インストーラー DLL 内の関数について説明します。 構文とセマンティクスの各関数の詳細については、次を参照してください。 [Installer DLL API リファレンス](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)します。  
  
|タスク|関数名|用途|  
|----------|-------------------|-------------|  
|ODBC のインストール|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|ドライバー固有のセットアップ DLL を読み込みます。|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|インストールされたドライバーの一覧を返します。|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|システム情報には、ドライバーを追加します。|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|ドライバー マネージャーのターゲット ディレクトリを返します。|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|インストーラーの関数のエラーまたは状態情報を返します。|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|システム情報に翻訳者を追加します。|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|エラーを報告するドライバーまたはトランスレーター セットアップ ライブラリを使用できます。|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|システム情報からドライバーを削除します。|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|システム情報から ODBC コア コンポーネントを削除します。|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|システム情報から、変換プログラムを削除します。|  
|データ ソースの構成|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|ドライバー固有のセットアップ DLL を呼び出します。|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|データ ソースを追加する ダイアログ ボックスが表示されます。|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|DSN の値を一覧表示した Odbc.ini エントリが、システム情報の場所を示す構成モードを取得します。|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|値は、システム情報を書き込みます。|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|トランスレーターを選択するダイアログ ボックスが表示されます。|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|データ ソースとドライバーを構成するダイアログ ボックスが表示されます。|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|ファイル Dsn から情報を読み取ります。|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|既定のデータ ソースを削除します。|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|データ ソースを削除します。|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|DSN の値を一覧表示した Odbc.ini エントリが、システム情報の場所を示す構成モードを設定します。|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|長さとデータ ソース名の有効性を確認します。|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|データ ソースを追加します。|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|ファイル Dsn に情報を書き込みます。|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|システム情報の値を取得します。|
