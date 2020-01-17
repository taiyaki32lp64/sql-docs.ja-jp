---
title: 32 ビット ドライバーで 32 ビット アプリケーションを使用して |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b4d14cc65b31a0641149ace931efe46c914ad1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088165"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>32 ビット ドライバーで 32 ビット アプリケーションを使用
32 ビット ドライバーでは、32 ビット アプリケーションを実行できます。 32 ビット アプリケーションと 32 ビット ドライバーは、Win32® API を使用します。  
  
## <a name="architecture"></a>Architecture  
 次の図は、方法は、32 ビット アプリケーションと 32 ビット ドライバーの通信。 アプリケーションでは、32 ビット ドライバーを呼び出し、32 ビット ドライバー マネージャーを呼び出します。  
  
 ![どの 32&#45;32 ビット アプリと通信&#45;ビット ドライバー](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Windows Nt または windows 2000 の 32 ビットのサンク インストーラー DLL を使わないでください。 32 ビット インストーラー DLL と同じファイル名がありますが、別の DLL になります。  
  
## <a name="administration"></a>管理  
 ODBC データ ソース アドミニストレーターを使用して、32 ビット ドライバーのデータ ソースを管理できます。 Windows 2000 を実行しているコンピューター上の ODBC アドミニストレーターを開くには、Windows コントロール パネルを開き、ダブルクリック**管理ツール**、し、ダブルクリック**データ ソース (ODBC)** します。 Microsoft Windows の以前のバージョンを実行するコンピューターで、アイコンの名前は**32 ビット ODBC**または単に**ODBC**します。  
  
## <a name="components"></a>コンポーネント  
 ODBC コンポーネントには、32 ビット ドライバーで 32 ビット アプリケーションを実行するために、次のファイルが含まれています。 これらのコンポーネントがディレクトリに \Redist します。  
  
|ファイル名|説明|  
|---------------|-----------------|  
|Odbc32.dll|32 ビット ドライバー マネージャー|  
|Odbccp32.dll|32 ビット インストーラー DLL|  
|Odbcad32.exe|32 ビット odbc データ ソース アドミニストレーター|  
|Odbcinst.hlp|インストーラーのヘルプ ファイル|  
|Msvcrt40.dll|C ランタイム ライブラリ|
