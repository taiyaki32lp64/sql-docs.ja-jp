---
title: RDS を使用してでの ODBC 接続プーリング |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling in RDS [ADO]
ms.assetid: e8b912c1-da5b-4e85-a000-1e6648a94237
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2ffcc64cb9d0e45d371e927cd1c15be51cd917c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921937"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>RDS での ODBC 接続プールの使用
ODBC データ ソースを使用している場合は、クライアントの負荷の処理を高パフォーマンスを実現するために、接続オプションでは、インターネット インフォメーション サービス (IIS) のプールを使用できます。 接続プールは、頻繁に使用される接続の開いている状態を維持する接続は、リソース マネージャーです。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 接続プールを有効にするのには、インターネット インフォメーション サービスのマニュアルを参照してください。  
  
 有効にすると接続プール可能性があります Web サーバーに適用他の制限事項、Microsoft インターネット インフォメーション サービスのドキュメントで説明したように注意してください。  
  
 確実に、接続プールは安定して追加のパフォーマンスが向上、TCP/IP ソケット ネットワーク ライブラリを使用する Microsoft SQL Server を構成する必要があります。  
  
 これを行うには、する必要があります。  
  
-   TCP/IP ソケットを使用する SQL Server コンピューターを構成します。  
  
-   TCP/IP ソケットを使用する Web サーバーを構成します。  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>TCP/IP ソケットを使用する SQL Server コンピューターを構成します。  
 SQL Server コンピューターには、データ ソースとの対話は、TCP/IP ソケットのネットワーク ライブラリを使用するため、SQL Server セットアップ プログラムを実行します。  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>SQL Server コンピューターの TCP/IP ソケット ネットワーク ライブラリを指定するには  
  
### <a name="in-microsoft-sql-server-65"></a>Microsoft SQL server 6.5。  
  
1.  スタート メニューからのプログラム、Microsoft SQL Server 6.5、 をポイントおよび SQL の設定 をクリックします。  
  
2.  続行を 2 回クリックします。  
  
3.  Microsoft SQL Server でのオプション ダイアログ ボックスは、ネットワーク サポートの変更を選択し、し、続行 をクリックします。  
  
4.  TCP/IP ソケットのチェック ボックスが選択されているかどうかを確認し、[ok] をクリックします。  
  
5.  これを完了すると、続行 をクリックし、セットアップを終了します。  
  
### <a name="in-microsoft-sql-server-70"></a>Microsoft SQL server 7.0。  
  
1.  スタート メニューからのプログラム、Microsoft SQL Server 7.0、 をポイントおよびサーバー ネットワーク ユーティリティ をクリックします。  
  
2.  ダイアログ ボックスの [全般] タブで [追加] をクリックします。  
  
3.  ネットワーク ライブラリ構成の追加 ダイアログ ボックスで、TCP/IP をクリックします。  
  
4.  ポート番号とプロキシ アドレス ボックスでは、ネットワーク管理者によって提供されるポート番号とプロキシ アドレスを入力します。  
  
5.  終了するには、[ok] をクリックし、セットアップを終了します。  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>TCP/IP ソケットを使用する Web サーバーを構成します。  
 TCP/IP ソケットを使用する Web サーバーを構成するための 2 つのオプションがあります。 すべての SQL Server は、Web サーバーからアクセスするかどうかに依存するはまたは特定の SQL Server のみが Web サーバーからアクセスします。  
  
 すべての SQL Server に Web サーバーからアクセスをする場合は、Web サーバー コンピューターで SQL Server クライアントの構成ユーティリティを実行する必要があります。 次の手順では、TCP/IP ソケット ネットワーク ライブラリを使用してこの IIS Web サーバーから行われるすべての SQL Server 接続の既定のネットワーク ライブラリを変更します。  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>Web サーバー (すべての SQL Server) を構成するには  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL server 6.5。  
  
1.  スタート メニューからのプログラム、Microsoft SQL Server 6.5、 をポイントおよび SQL クライアント設定ユーティリティ をクリックします。  
  
2.  ネットワーク ライブラリ タブをクリックします。  
  
3.  ネットワークの既定のボックスで、TCP/IP ソケットを選択します。  
  
4.  変更を保存し、ユーティリティを終了する元に戻す をクリックします。  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL server 7.0。  
  
1.  スタート メニューからのプログラム、Microsoft SQL Server 7.0、 をポイントおよびクライアント ネットワーク ユーティリティ をクリックします。  
  
2.  [全般] タブをクリックします。  
  
3.  既定のネットワーク ライブラリ ボックスでは、TCP/IP をクリックします。  
  
4.  変更を保存し、ユーティリティを終了するには、[ok] をクリックします。  
  
 特定の SQL Server に Web サーバーからアクセスした場合は、Web サーバー コンピューターで SQL Server クライアントの構成ユーティリティを実行する必要があります。 特定の SQL Server 接続のネットワーク ライブラリを変更するには、次のように Web サーバー コンピューターで SQL Server クライアント ソフトウェアを構成します。  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>Web サーバー (特定の SQL Server) を構成するには  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL server 6.5。  
  
1.  スタート メニューからのプログラム、Microsoft SQL Server 6.5、 をポイントおよび SQL クライアント設定ユーティリティ をクリックします。  
  
2.  詳細設定 タブをクリックします。  
  
3.  サーバーのボックスで、TCP/IP ソケットを使用して接続先のサーバーの名前を入力します。  
  
4.  DLL の名前 ボックスでは、TCP/IP ソケットを選択します。  
  
5.  [追加/変更] をクリックします。 このサーバーを指すすべてのデータ ソースでは TCP/IP ソケットが使用されます。  
  
6.  クリックしてください。  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL server 7.0。  
  
1.  スタート メニューからのプログラム、Microsoft SQL Server 7.0、 をポイントおよびクライアント設定ユーティリティ をクリックします。  
  
2.  [全般] タブをクリックします。  
  
3.  [追加] をクリックします。  
  
4.  サーバーの別名 ボックスで、サーバーの別名を入力します。 ネットワーク ライブラリ ボックスで、[TCP/IP] をクリックします。 コンピューター名 ボックスで、クライアントの TCP/IP ソケットをリッスンしているコンピューターのコンピューター名を入力します。 ポート番号 ボックスでは、SQL Server がリッスンするポートを入力します。  
  
5.  [Ok] をクリックして、ユーティリティを終了し、もう一度 [ok] です。  
  
## <a name="see-also"></a>関連項目  
 [RDS の基礎](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















