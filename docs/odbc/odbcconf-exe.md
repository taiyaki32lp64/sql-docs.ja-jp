---
title: ODBCCONF.EXE |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b70622ea038b61883ce7a5307a558a5667139fb1
ms.sourcegitcommit: a26cb217adfbbfb3636dff43fb19a46462e2e994
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74491964"
---
# <a name="odbcconfexe"></a>ODBCCONF.EXCEL.EXE
ODBCCONF は、ODBC ドライバーとデータソース名を構成できるコマンドラインツールです。  
  
> [!NOTE]  
>  ODBCCONF は、今後のバージョンの Windows Data Access コンポーネントでは削除される予定です。 この機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 PowerShell コマンドを使用して、ドライバーとデータソースを管理できます。 これらの PowerShell コマンドの詳細については、「 [Windows Data Access Components のコマンドレット](/powershell/module/wdac)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>引数  
 *オプション*  
 0個以上のスイッチオプション。 使用できるスイッチの一覧については、このトピックで後述する「解説」を参照してください。  
  
 *処置*  
 実行する1つのアクション。 使用可能なオプションの一覧については、「解説」を参照してください。  
  
## <a name="remarks"></a>コメント  
 次のスイッチを使用できます。  
  
|スイッチ|説明|  
|------------|-----------------|  
|/A {*action*}|アクションを指定してください。<br /><br /> 1つのアクションのみが指定されている場合、/a は省略可能です。|  
|/?|ODBCCONF の使用状況を表示します。EXCEL.EXE.|  
|スイッチ|アクションが失敗した場合、処理は続行されます。|  
|/E|処理が完了したら、/F で指定された応答ファイルを消去します。|  
|/F|などの応答ファイルを使用し`odbcconf /F my.rsp`ます。<br /><br /> .rsp は次のようになります。`REGSVR c:\my.dll`<br /><br /> /A は、応答ファイルでは使用されません。|  
|/H|使用状況 (ヘルプ) を表示します。 このスイッチは/? と同じです。|  
|/L [*モード*]*ファイル名*|プログラム出力をファイルに送信するには、次の3つのモードのいずれかを実行します: normal (n)、verbose (v)、debug (d)。 デバッグモードでは、odbcconf によって読み込まれる Dll が記録されます。<br /><br /> モードを指定せずに/L を指定すると、ログファイルは空になります。<br /><br /> たとえば、 **/lv .log**を使用します。|  
|/R|操作は再起動後に実行されます。|  
|/S|サイレント モード。 エラーメッセージを表示しません。|  
  
 次の操作を実行できます。  
  
|操作|説明|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name * * ドライバー固有の構成パラメーター*|適切なドライバーセットアップ DLL を読み込み、 **configdriver**関数を呼び出します。<br /><br /> [Sqlconfigdriver 関数](../odbc/reference/syntax/sqlconfigdriver-function.md)と同じです。<br /><br /> 例:<br /><br /> /A {CONFIGDRIVER "ドライバー名" "CPTimeout = 60"}<br /><br /> /A {CONFIGDRIVER "ドライバー名" "DriverODBCVer = 03.80"}|  
|CONFIGDSN *driver_name* DSN =*name* &#124;*属性*|システムデータソースを追加または変更します。<br /><br /> [Sqlconfigdatasource 関数](../odbc/reference/syntax/sqlconfigdatasource-function.md)と同じです。<br /><br /> 例:<br /><br /> /A {CONFIGDSN "SQL Server" "DSN = name &#124; Server = srv"}|  
|CONFIGSYSDSN *driver_name* DSN =*name* &#124;*属性*|システムデータソースを追加または変更します。<br /><br /> [Sqlconfigdatasource 関数](../odbc/reference/syntax/sqlconfigdatasource-function.md)と同じです。<br /><br /> 例:<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN = name &#124; Server = srv"}|  
|INSTALLDRIVER|[Sqlinstalldriverex 関数](../odbc/reference/syntax/sqlinstalldriverex-function.md)と同じです。<br /><br /> INSTALLDRIVER に渡されるキーワードと値のペアの構文の詳細については、「 [Driver Specification サブキー](../odbc/reference/install/driver-specification-subkeys.md)」を参照してください。<br /><br /> 例:<br /><br /> /A {INSTALLDRIVER "your Driver &#124; Driver = c:\. dll &#124; Setup &#124; = APILevel = 2 &#124; ConnectFunctions = YYY &#124; DriverODBCVer = 03.50 &#124; FileUsage = 0 &#124; SQLLevel = 1"}。|  
|INSTALLTRANSLATOR *translator の構成 * * ドライバーのパス*|翻訳者に関する情報を HKEY_LOCAL_MACHINE に追加し**ます。INI\ODBC トランスレーター**レジストリキー。<br /><br /> [SQLInstallTranslatorEx 関数](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)と同じです。<br /><br /> INSTALLDRIVER に渡されるキーワードと値のペアの構文の詳細については、「 [Translator Specification サブキー](../odbc/reference/install/translator-specification-subkeys.md)」を参照してください。<br /><br /> 例:<br /><br /> /A {INSTALLTRANSLATOR "My Translator &#124; Translator = c:\my.dll &#124; Setup = c:\my.dll"}|  
|REGSVR *dll*|DLL を登録します。<br /><br /> Regsvr32 と同じです。<br /><br /> 例:<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|を HKEY_LOCAL_MACHINE します。INI\ODBC File DSN\DefaultDSNDir が存在しない場合、SETFILEDSNDIR アクションによってそのファイルが作成され、HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir に \ODBC\Data Sources と共に付加された値が割り当てられます。<br /><br /> HKEY_LOCAL_MACHINE の値 (\)。INI\ODBC File DSN\DefaultDSNDir ファイルベースのデータソースを作成するときに、ODBC データソースアドミニストレーターによって使用される既定の場所を指定します。<br /><br /> 例:<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>参照  
 [Microsoft Open Database Connectivity (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
