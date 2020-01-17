---
title: SQLRemoveDriverManager 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriverManager
helpviewer_keywords:
- SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5cd31a45ed891a8dc95f4f23981d4b626a6095b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024542"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0:Windows XP Service Pack 2、Windows Server 2003 Service Pack 1 では、以降のオペレーティング システムでは、非推奨とされます。  
  
 **概要**  
 **SQLRemoveDriverManager**システム情報の Odbcinst.ini のエントリから ODBC コア コンポーネントに関する情報を削除または変更します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *pdwUsageCount*  
 [出力]使用率カウント ドライバー マネージャーのこの関数が呼び出された後です。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。 エントリが存在しない場合、システムの情報でこの関数が呼び出されたときに、関数は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLRemoveDriverManager** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|コンポーネントがレジストリに見つかりません|インストーラーは、レジストリに存在しないか、レジストリで見つかりませんでした、ドライバー マネージャーの情報を削除できませんでした。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|インクリメントまたはコンポーネントの使用率カウントは減少できませんでした。|ドライバー マネージャーの使用率カウントをデクリメントするインストーラーが失敗しました。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLRemoveDriverManager**補完、 **SQLInstallDriverManager**関数、およびコンポーネントの使用状況のカウント システム情報に更新します。 この関数は、セットアップ アプリケーションからのみ呼び出す必要があります。  
  
 **SQLRemoveDriverManager**コア コンポーネントの使用率カウントは 1 減ります。 コンポーネントの使用率カウントは 0 には、エントリのシステム情報は削除されます。 コア コンポーネントのエントリは、システムについては、"ODBC Core"というタイトルの下に、次の場所には。  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  アプリケーション削除しないでください物理的にドライバー マネージャーのファイル コンポーネントの使用率カウントとファイルの使用率カウントに達すると 0 です。  
  
 **SQLRemoveDriverManager**すべてのファイルを実際に削除されません。 呼び出し元のプログラムはファイルを削除する担当し、ファイルの使用状況の維持をカウントします。 ドライバー マネージャーのファイルは、should not、ただし、これらのファイルは、ファイルの使用率カウントはインクリメントされませんが、他のアプリケーションで使用できるため、両方のコンポーネントの使用率カウントとファイルの使用率カウントを 0 に到達したときに削除されます。  
  
 **SQLRemoveDriverManager**がアンインストール プロセスの一部として呼び出されます。 全体として ODBC コア コンポーネント (をドライバー マネージャー、カーソル ライブラリ、インストーラー、言語ライブラリ、管理者、サンクのファイルおよびなどを含む) はアンインストールされます。 次のファイルは削除**SQLRemoveDriverManager**がアンインストール プロセスの一部として呼び出されます。  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32 します。DLL|  
|ODBCCR32 します。DLL|ODBC16GT します。DLL|  
|ODBCCU32 します。DLL|ODBC32GT します。DLL|  
|ODBCINT します。DLL|DS16GT します。DLL|  
|ODBCTRAC します。DLL|DS32GT します。DLL|  
|MSVCRT40 します。DLL|ODBCAD32 します。実行可能ファイル|  
|ODBCCP32 します。CPL||  
  
 **SQLRemoveDriverManager**アップグレード プロセスの一部としても呼ばれます。 アプリケーションは、アップグレードを実行する必要があることと、ドライバーが既にインストールを検出した場合、ドライバーを削除して再インストールする必要があります。  
  
 **SQLRemoveDriverManager**最初のコンポーネントの使用率カウントをデクリメントを呼び出す必要があります。 **SQLInstallDriverEx**し、コンポーネントの使用率カウントをインクリメントする呼び出す必要があります。 アプリケーションのセットアップ プログラムは、古いコア コンポーネント ファイルを新しいファイルに置き換える必要があります。 ファイル使用状況カウントが、同じままになります、および古いバージョンのコア コンポーネント ファイルを使用する他のアプリケーションがより新しいバージョンのファイルを使用するようになりました。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ドライバー マネージャーのインストール|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
