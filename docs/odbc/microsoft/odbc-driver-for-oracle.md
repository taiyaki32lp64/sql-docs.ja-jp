---
title: ODBC Driver for Oracle |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fc15968501fed6b94a7ccddb984cbdf76bcbcb0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915802"
---
# <a name="odbc-driver-for-oracle"></a>ODBC Driver for Oracle
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 Microsoft® ODBC Driver for Oracle ODBC に準拠したアプリケーションを Oracle データベースに接続することができます。 ODBC Driver for Oracle で説明されているオープン データベース コネクティビティ (ODBC) 仕様に準拠している、 *ODBC プログラマ リファレンス*します。 PL/SQL パッケージ、DTC XA/統合、およびインターネット インフォメーション サービス (IIS) 内から Oracle アクセスへアクセスを許可します。  
  
 Oracle RDBMS とは、ワークステーションとミニコンピューターのさまざまなオペレーティング システムで実行されるマルチ ユーザーのリレーショナル データベース管理システムです。 Microsoft Windows を実行している IBM 互換コンピューターは、ネットワーク経由での Oracle データベース サーバーと通信できます。 サポートされているネットワークには、Microsoft LAN Manager、NetWare、VINES、DECnet、および TCP/IP をサポートするネットワークが含まれます。  
  
 ODBC Driver for Oracle では、ODBC インターフェイスを通じて、Oracle データベース内のデータにアクセスするアプリケーションができるようにします。 ドライバーがローカルの Oracle データベースにアクセスできる、または SQL 経由のネットワークと通信できる * Net します。 次の図では、このアプリケーションとドライバーのアーキテクチャについて説明します。  
  
 ![Oracle 用 ODBC ドライバー&#47;ドライバーのアーキテクチャ](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 ODBC Driver for Oracle は、API への準拠レベル 1 および SQL への準拠レベルのコアに準拠します。 API への準拠レベル 2 で、ほとんどのコアと拡張の SQL の適合性レベルで文法の一部の関数もサポートしています。 ドライバーは ODBC 2.5 に準拠し、32 ビット システムをサポートします。 Oracle 7.3 x が完全にはサポートされていますOracle8 には、サポートが制限されています。 Oracle の新しいリレーショナル オブジェクト モデルはサポートや ODBC Driver for Oracle は任意の Unicode データ型、Blob、Clob、およびなどの新しい Oracle8 データ型をサポートしません。 サポートされているデータの種類の詳細については、次を参照してください。 [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)このガイドでします。  
  
 Oracle のデータにアクセスするには、次のコンポーネントが必要です。  
  
-   ODBC Driver for Oracle  
  
-   Oracle の RDBMS データベース  
  
-   Oracle クライアント ソフトウェア  
  
 また、次のリモート接続します。  
  
-   ドライバーとデータベースを実行しているコンピューターを接続するネットワーク。 ネットワークは、SQL をサポートする必要があります * Net 接続します。  
  
## <a name="component-documentation"></a>コンポーネントのドキュメント  
 このガイドを設定して、Microsoft ODBC Driver for Oracle を構成して、プログラムによる機能の追加に関する詳細情報が含まれています。 技術的な参考資料も含まれています。  
  
 特定の Oracle 製品の動作については、Oracle 製品に付属するマニュアルを参照してください。  
  
 設定するか、Microsoft ODBC Driver for Oracle、ODBC データ ソース アドミニストレーターを使用して構成する方法については、次を参照してください。、 [ODBC データ ソース アドミニストレーター](../../odbc/admin/odbc-data-source-administrator.md)ドキュメント。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ODBC Driver for Oracle ユーザー ガイド](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [ODBC Driver for Oracle プログラマー向けリファレンス](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
