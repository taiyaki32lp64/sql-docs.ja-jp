---
title: Sybase (SybaseToSQL) への接続 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6cb2f4196737cceec2f60684de1b7409f5e383a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083392"
---
# <a name="connect-to-sybase-sybasetosql"></a>Sybase への接続 (SybaseToSQL)
使用して、 **Sybase への接続**を移行する Sybase Adaptive Server Enterprise (ASE) のインスタンスに接続する ダイアログ ボックス。  
  
このダイアログ ボックスにアクセスする、**ファイル**メニューの  **Sybase への接続**します。 以前接続した場合、コマンドは**Sybase への再接続**します。  
  
## <a name="options"></a>および  
**Provider**  
Sybase サーバーへの接続用のコンピューターにインストールされているプロバイダーのいずれかを選択します。  
  
**モード**  
いずれかの標準的なまたは高度な接続モードを選択します。 標準モードでは、入力またはサーバー名、ポート、ユーザー名、およびパスワードの値を選択します。 高度なモードでは、接続文字列を指定します。  
  
**サーバー名**  
入力するか、またはアダプティブ サーバーの IP アドレスを選択します。 既定のサーバー名は、コンピューター名と同じです。 これは、標準モードのオプションです。  
  
**[サーバー ポート]**  
ASE への接続を既定以外のポートを使用している場合は、ポート番号を入力します。 既定のポート番号は、5000 です。 これは、標準モードのオプションです。  
  
**ユーザー名**  
ASE への接続に使用されるユーザー名を入力します。 これは、標準モードのオプションです。  
  
**Password**  
ユーザー名に対応するパスワードを入力します。 これは、標準モードのオプションです。  
  
**[接続文字列]**  
ASE に、接続の完全な接続文字列を入力します。  
  
接続文字列は、パラメーターの名前と値のペアで構成されます。 パラメーターの名前は、使用中のプロバイダーによって異なります。  
  
**さまざまなプロバイダーの接続パラメーターは次のとおりです。**  
  
1.  接続パラメーターを**OLE DB プロバイダー**  
  
    |設定|Sybase 12.5 パラメーター|Sybase 15 パラメーター|  
    |-----------|-------------------------|-----------------------|  
    |サーバー名|[サーバー名]|Server|  
    |Port|サーバーのポート アドレス|Port|  
    |[ユーザー名]|[ユーザー ID]|[ユーザー ID]|  
    |Password|パスワード|Password|  
    |プロバイダー|プロバイダー|プロバイダー|  
  
    Sybase ASE の 12.5 の接続文字列の例のとおりです。  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Sybase ASE 15 では、接続文字列の例のとおりです。  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  接続パラメーターを**ODBC プロバイダー**  
  
    |設定|Sybase 12.5/15 パラメーター|  
    |-----------|-----------------------------|  
    |ドライバー名|ドライバー●どらいば○|  
    |[サーバー名]|Server|  
    |[ユーザー名]|uid|  
    |Password|pwd|  
    |[ポート番号]|Port|  
  
    Sybase ASE 12.5 または 15 では、接続文字列の例のとおりです。  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  接続パラメーターを**ADO.NET プロバイダー**  
  
    |設定|Sybase 12.5/15 パラメーター|  
    |-----------|-----------------------------|  
    |[サーバー名]|Server|  
    |[ユーザー名]|uid|  
    |Password|pwd|  
    |[ポート番号]|Port|  
  
    ADO.NET プロバイダーの接続文字列の例は、次のようです。  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
詳細については、ASE のドキュメントを参照してください。  
  
これは、高度なモードのオプションです。  
  
