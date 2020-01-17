---
title: デスクトップ データベース ドライバーのアーキテクチャ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ccd1f14b0cfbcbdbc675a142ebabf11932409832
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071907"
---
# <a name="desktop-database-drivers-architecture"></a>デスクトップ データベース ドライバーのアーキテクチャ
使用には、Microsoft Windows 95 以降、または Windows NT 4.0 と Windows 2000 は、これらのドライバーが設計されています。 Windows 95 以降; のみの 32 ビット アプリケーションがサポートされます。16 ビットおよび 32 ビット アプリケーションは、Windows NT 4.0 および Windows 2000 でサポートされます。  
  
> [!NOTE]  
>  これらのドライバーで使用される ODBC のバージョンについてを参照してください、 *ODBC プログラマ リファレンス*と過去および現在のリリース ノート。 これらのドライバーは、表示される領域以外に準拠している、 *ODBC プログラマ リファレンス*します。  
  
 ODBC のデスクトップ データベース ドライバーには、Microsoft Access、dBASE、Excel、Paradox、およびテキストの 32 ビット ドライバーが含まれます。 いいえ-16 ビットのドライバーが含まれます。 (Microsoft FoxPro 用のドライバーは使用可能な個別に) です。  
  
 Windows 95 以降のアプリケーション/ドライバーのアーキテクチャを示します。  
  
 ![アプリ&#47;ドライバー アーキテクチャ。Windows 95 以降](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Windows 95 で 16 ビット アプリケーションでこれらのドライバーの使用がサポートされていません。  
  
 Windows NT 4.0 や Windows 2000 のアプリケーション/ドライバーのアーキテクチャを示します。  
  
 ![アプリ&#47;ドライバー アーキテクチャ。NT 4.0 および Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 デスクトップ データベース ドライバーは、2 階層のドライバーです。 2 層構成では、ドライバーは、解析、検証、最適化、およびクエリの実行のプロセスを実行しません。 代わりに、Microsoft Jet は、これらのタスクを実行します。 ODBC API 呼び出しを処理し、SQL エンジンとして機能します。 Microsoft Jet は、ドライバーの分離不可能整数部分になります。ドライバーが付属し、ドライバーが存在する場合でも、コンピューター上の他のアプリケーションが使用しなくします。  
  
 デスクトップ データベース ドライバーは、6 つの異なるドライバー - またはより正確に 1 つで構成されているドライバー ファイル (Odbcjt32.dll) を ODBC[ドライバー マネージャー](../../odbc/reference/the-driver-manager.md) 6 つの異なる方法で使用します。 Odbcjt32.dll でドライバーをドライバー マネージャーを使用してデータ ソースのレジストリ エントリで DRIVERID フラグを決定します。 アプリケーションへの呼び出しに含まれる接続文字列でこのフラグを渡します**SQLDriverConnect**します。 既定では、フラグは、Microsoft Access ドライバーの ID です。  
  
 ドライバーのセットアップ ファイルは、セットアップ時に、DRIVERID フラグを変更します。 Microsoft Access ドライバーを除くすべてのドライバーでは、関連付けられたセットアップ DLL があります。 クリックすると**セットアップ**で、 [Microsoft ODBC データ ソース アドミニストレーター](../../odbc/admin/odbc-data-source-administrator.md) ODBC インストーラー DLL (Odbcinst.dll) は、データ ソースのセットアップ DLL を読み込みます。 ODBC インストーラーの関数をエクスポートする DLL のセットアップ**SQLConfigDataSource**します。 ウィンドウ ハンドルが渡された場合**SQLConfigDataSource**、この関数は、セットアップ ウィンドウを表示し、ユーザー インターフェイスから選択したドライバーに従って DRIVERID フラグを変更します。  
  
 NULL ウィンドウのハンドルが渡されるファイルがプログラムによって作成されると、 **SQLConfigDataSource**、関数は、データ ソースを作成、動的にに従って DRIVERID フラグを変更して、 *lpszDriver*関数呼び出しの引数。  
  
 Odbcjt32.dll では、Microsoft Jet API の上に ODBC 関数を実装します。 ODBC および Microsoft Jet の関数間の直接マッピングただしします。 カーソル モデルと SQL のマッピングなど、さまざまな要因は、関数の直接的な相関関係を回避します。  
  
 ODBC ドライバーは、Microsoft Jet エンジンと ODBC ドライバー マネージャーの間存在します。 アプリケーションによって呼び出されたいくつかの ODBC 関数は、ドライバー マネージャーによって処理され、ドライバーに渡されません。 Microsoft Jet をこれらの関数には、ドライバー マネージャーへの直接接続があるないために、呼び出す関数を表示されません。
