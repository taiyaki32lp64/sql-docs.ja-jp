---
title: 32 ビット ドライバーで 16 ビット アプリケーションを使用して |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4be5d2cacaeca7cf53caa330a126284370ec80f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088195"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>32 ビット ドライバーで 16 ビット アプリケーションを使用
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 代わりに 32 ビットまたは 64 ビットのドライバー マネージャーを使用します。  
  
 32 ビット ドライバーがスレッドを作成する Win32 API 関数を明示的に呼び出していない限り、Windows ベース システムで 32 ビット ドライバーで 16 ビット アプリケーションを実行できます。 Windows (WOW) サブシステム上の Windows では、16 ビット モードでアプリケーションを実行し、16 ビット オペレーティング システムの呼び出しを解決します。 ODBC 32 ビット ドライバーをアプリケーションから Dll 解決 16 ビットの呼び出しをサンキングします。 16 ビット アプリケーションは、Windows API を使用し、32 ビット ドライバーは、Win32 API を使用します。  
  
## <a name="architecture"></a>Architecture  
 次の図は、方法は、16 ビット アプリケーションと 32 ビット ドライバーの通信。 16 ビットのドライバー マネージャーと、32 ビット ドライバーの間は、汎用 ODBC 呼び出しを 32 ビットの 16 ビット ODBC 呼び出しを変換する Dll をサンクのです。  
  
 ![どの 16&#45;32 ビット アプリと通信&#45;ビット ドライバー](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  16 ビット アプリケーションは、32 ビット ドライバーを使用した対話、いつでも、32 ビット ドライバー マネージャーは常に「2.0」ODBC のバージョンと、ドライバーでサポートされるを返します。  
  
## <a name="administration"></a>管理  
 ODBC データ ソース アドミニストレーターを使用して、32 ビット ドライバーのデータ ソースを管理できます。 Microsoft® Windows® 2000 を実行しているコンピューター上の ODBC アドミニストレーターを開くには、Windows コントロール パネルを開き、ダブルクリック**管理ツール**、し、ダブルクリック**データ ソース (ODBC)** します。 Microsoft Windows の以前のバージョンを実行するコンピューターで、アイコンの名前は**32 ビット ODBC**または単に**ODBC**します。  
  
 次の図は、16 ビット アプリケーションが 32 ビット ドライバーのセットアップ DLL を呼び出す方法を示します。 16 ビット インストーラー DLL と 32 ビット ドライバーのセットアップ DLL は、32 ビット インストーラー DLL の呼び出しに 16 ビットのインストーラー DLL の呼び出しに変換する汎用サンク DLL です。  
  
 ![方法を 16&#45;ビット アプリの呼び出しを 32&#45;ビット ドライバーのセットアップ DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 Windows (16 ビットから 32 ビットのサンク) で Windows、という名前の Ds32gt.dll は、32 ビットの設定を使用して渡される 16 ビットの引数値型に変換します。 追加のサンク DLL DLL バックアップを 16 ビット。  
  
## <a name="components"></a>コンポーネント  
 MDAC 2.8 SP1 SDK の ODBC コンポーネントには、32 ビット ドライバーで 16 ビット アプリケーションを実行するために、次のファイルが含まれています。 これらのコンポーネントがディレクトリに \Redist します。  
  
|ファイル名|説明|  
|---------------|-----------------|  
|Odbc16gt.dll|16 ビット ODBC の汎用サンク DLL|  
|Odbc32gt.dll|32 ビット ODBC の汎用サンク DLL|  
|Odbccp32.dll|32 ビット インストーラー DLL|  
|Odbcad32.exe|32 ビット管理者プログラム|  
|Odbcinst.hlp|インストーラーのヘルプ ファイル|  
|Ds16gt.dll|DLL をサンクがジェネリックの 16 ビットのドライバーのセットアップ|  
|Ctl3d32.dll|32 ビットのウィンドウの 3 次元スタイル ライブラリ|  
  
 さらに、ODBC 3.51 の一部ではない、16 ビット ODBC 2.10 ドライバー マネージャーと共に以下のファイルは必要があり、16 ビット アプリケーションをインストールする必要があります。  
  
|ファイル名|説明|  
|---------------|-----------------|  
|Odbc.dll|16 ビットのドライバー マネージャー|  
|Odbcinst.dll|16 ビット インストーラー DLL|  
|Odbcadm.exe|16 ビット odbc データ ソース アドミニストレーター|
