---
title: 32 ビット ドライバーで 16 ビットおよび 32 ビット アプリケーションを使用して |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 941c821d7622b2364ec1cd417dd9b50302540b95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088171"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>32 ビット ドライバーで 16 ビットおよび 32 ビット アプリケーションを使用
> [!IMPORTANT]  
>  16 ビット アプリケーションのサポートは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに 32 ビットまたは 64 ビット アプリケーションを開発します。  
  
 ODBC データ アクセス コンポーネントでは、32 ビット ドライバーで 16 ビットおよび 32 ビット アプリケーションを使用できます。 Microsoft® Windows® 95/98 および Microsoft Windows と Windows 2000 オペレーティング システムでは、次のアプリケーションとドライバーの組み合わせをサポートします。  
  
-   32 ビット ドライバーで 16 ビット アプリケーション  
  
-   32 ビット ドライバーで 32 ビット アプリケーション  
  
 16 ビット ドライバーで 32 ビット アプリケーションを使用することはサポートされていません。  
  
> [!NOTE]  
>  ODBC version 3.0 のリリース以降、Windows NT 4.0 がサポートされています。  
  
 ODBC には、「サンク」ダイナミック リンク ライブラリ (Dll) に 16 ビットのアドレスを 32 ビットのアドレスに変換する、またはその逆は、上記の構成をサポートするために必要な ODBC コンポーネントが含まれています。 セットアップ プログラムは、そのシステムに必要な ODBC コンポーネントのインストールを使用しているオペレーティング システムを決定します。 すべてのシステムで使用される ODBC コンポーネントをインストールすることもできます。  
  
 ほとんどの場合、アプリケーションまたはドライバーから 16 ビットの移植を 32 ビットは、5 つの種類の変更。  
  
-   メッセージの処理コードの変更  
  
-   整数とハンドルは、32 ビットを変更します。  
  
-   Windows アプリケーション プログラミング インターフェイス (Api) への呼び出しでの変更  
  
-   スレッド セーフ ドライバーを変更  
  
-   ODBC コンポーネントへの変更  
  
 アプリケーションまたはドライバー プログラミング観点からは、16 ビットおよび 32 ビットの ODBC コンポーネント間の大きな違いは、別のファイル名があることです。 システムの観点からは、各アプリケーションまたはドライバーの接続のアーキテクチャが異なるとデータ ソースを管理するために使用するツールは異なる。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [32 ビット ドライバーで 16 ビット アプリケーションを使用](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [32 ビット ドライバーで 32 ビット アプリケーションを使用](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
