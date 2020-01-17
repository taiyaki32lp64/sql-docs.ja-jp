---
title: ハードウェアとソフトウェア要件 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c09ddcac1409da08fedeaf946ac7fb9f6ef668e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952442"
---
# <a name="hardware-and-software-requirements-odbc"></a>ハードウェアとソフトウェアの要件 (ODBC)
このトピックでは、ODBC のデスクトップ データベース ドライバーを使用するための要件を一覧表示します。  
  
## <a name="hardware-requirements"></a>ハードウェア要件  
 ODBC のデスクトップ データベース ドライバーを使用するには、が必要です。  
  
-   IBM と互換性のあるパーソナル コンピューターの場合は。  
  
-   6 MB の空きディスク領域とハード ディスク。  
  
-   少なくとも 16 MB のランダム アクセス メモリ (RAM) です。  
  
## <a name="software-requirements"></a>ソフトウェア要件  
 ODBC ドライバーを使用してデータにアクセスするには、次が必要です。  
  
-   ODBC ドライバー。  
  
-   32 ビット ODBC ドライバー マネージャー、3.51 のバージョンまたはそれ以降 (Odbc32.dll) です。  
  
-   Microsoft Windows 95 以降または Windows NT 4.0 または Windows 2000 の場合は。  
  
-   Microsoft ODBC ドライバーを使用してアプリケーションの少なくとも 20 KB のスタック サイズ。  
  
 Microsoft Windows NT 4.0 または Windows 2000 を使用する場合、32 ビット ドライバーはスレッド セーフ ドライバーへのアクセスを制御するグローバル セマフォを使用してのみです。 ドライバーの同時使用が非常に限定された Windows NT でします。 Jet ISAM レイヤーに対するすべてのアクセスは、Microsoft Jet エンジンを使用するすべてのアプリケーションにシングル スレッドになります。  
  
 Windows on Windows (WOW) Microsoft Windows NT 4.0 上で複数の 16 ビット アプリケーションを実行するときに、別のメモリ領域で、アプリケーションを実行する必要があります。 (同じメモリ空間使えません ODBC では、同じプロセスで複数の環境がサポートされていません。)別のメモリ領域で、アプリケーションを実行するアイコンを選択、アプリケーションのプログラム マネージャーで、開く、**ファイル**メニューをクリックします**プロパティ**、 をクリックし、**個別のメモリで実行領域**します。  
  
 Windows 95 で 16 ビット アプリケーションでこれらのドライバーの使用がサポートされていません。  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>ドライバー固有のハードウェアとソフトウェアの要件  
  
-   Access および dBASEdrivers Autoexec.bat や Config.sys ファイルの変更を必要があります。
