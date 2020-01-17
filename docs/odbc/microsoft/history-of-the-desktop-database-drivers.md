---
title: デスクトップ データベース ドライバーの履歴 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d225bac273558b928e3e8fd2f41bd121a723f6ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952369"
---
# <a name="history-of-the-desktop-database-drivers"></a>デスクトップ データベース ドライバーの履歴
次の表では、デスクトップ データベース ドライバーのバージョン履歴を示します。  
  
|バージョン|リリース日|説明|  
|-------------|------------------|-----------------|  
|1.0|8 月 1993 年|PageAhead ソフトウェアによって生成された SIMBA クエリ プロセッサを使用します。 SIMBA は、ODBC 呼び出しと SQL ステートメントを受信するには、Microsoft Jet インストール可能な ISAM 呼び出しにそれらを処理および Microsoft Jet ISAM ディスパッチ レイヤーを読み込み、適切なインストール可能な ISAM ドライバーを呼び出すには、呼び出されます。|  
|2.0|1994 年 12 月|ODBC の機能を大幅に拡張する ODBC 2.0 と共に使用します。 バージョン 2.0 の主な変更は、Microsoft Jet データベース エンジンが SIMBA クエリ プロセッサを置き換えることでした。 Microsoft Jet データベース エンジンで、デスクトップ データベース ドライバーは ISAM ドライバーのインストール可能な Microsoft Jet Microsoft アクセス テクノロジとさらに密接に統合します。 多くの機能強化は次のとおりです。<br /><br /> のスクロール可能なカーソル ネイティブ サポート。<br />の外部結合、更新可能な異種の結合、およびトランザクション ネイティブ サポート。<br />-Microsoft Windows NT のドライバーの 32 ビット バージョン。|  
|3.0|1995 年 10 月|Windows 95 および Windows NT のワークステーションまたはサーバーのサポートを提供します。 このリリースでのみの 32 ビット ドライバーが含まれていたWindows バージョン 3.1 用の 16 ビットのドライバーが削除されました。|  
|3.5|1996 年 10 月|これらのドライバーが 2 バイト文字セット (DBCS)-有効になっており、以前のバージョンよりもより適切なインターネット アプリケーションで使用された、ファイル データ ソース名 (Dsn) の使用に対応します。 Microsoft Access ドライバーは、Windows 95/98 と Windows NT 3.51 以降のオペレーティング システムの Alpha プラットフォーム上で使用するための RISC バージョンでリリースされました。|  
|4.0|1998 年の終わり|Microsoft Jet エンジン Unicode 形式との互換性と以前のバージョンの ANSI 形式のサポートを提供します。|  
  
> [!NOTE]  
>  Version3.5 ドライバーは、ODBC2 を使用する設計されました。*x*します。 ODBC 3.0 での動作も、ODBC 3.0 のすべての機能はサポートされません。 これらのドライバーが ODBC 3.0 を操作する方法についての詳細については、次を参照してください。[旧バージョンとの互換性と標準準拠](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)します。
