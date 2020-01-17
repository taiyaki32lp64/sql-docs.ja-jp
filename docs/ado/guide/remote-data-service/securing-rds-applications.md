---
title: RDS アプリケーションのセキュリティ保護 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d91b8f41c344d45bfde646d24819e73c0cd8f283
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922224"
---
# <a name="securing-rds-applications"></a>RDS アプリケーションの保護
このトピックでは、rds. のセキュリティ情報を提供します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer のセキュリティに関する問題  
 新しいセキュリティが強化された Microsoft Internet Explorer に追加、ADO および RDS オブジェクトは、「安全」モード環境でのみ実行に制限されます。 これは、異なるゾーン、セキュリティ レベル、動作の制限、安全でない操作は、これらの問題を認識し、セキュリティ設定をカスタマイズすることが必要です。  
  
## <a name="security-and-your-web-server"></a>セキュリティと Web サーバー  
 使用する場合、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Internet の Web サーバー上のオブジェクト、これは、潜在的なセキュリティ リスクことに注意してください。 有効なデータ ソース名 (DSN)、ユーザー ID、およびパスワード情報を取得する外部ユーザーは、そのデータ ソースにクエリを送信するページを作成できます。 登録解除して削除する 1 つのオプションは、データ ソースへのアクセスをさらに制限された場合は、 **RDSServer.DataFactory**オブジェクト (msadcf.dll) とハード コードされたクエリの代わりにカスタム ビジネス オブジェクトを使用します。  
  
 RDSServer.DataFactory オブジェクトを使用するセキュリティへの影響の詳細については、Microsoft Security Web サイトのマイクロソフト セキュリティ情報の MS99 025 を参照してください。  
  
## <a name="client-impersonation-and-security"></a>クライアントの偽装とセキュリティ  
 場合、**パスワード認証**(Windows NT 4.0) の Windows NT チャレンジ/レスポンス認証または統合 Windows 認証 (Windows 2000 の場合)、IIS Web サーバーのプロパティを設定し、ビジネス オブジェクトは、クライアントのセキュリティ コンテキストで呼び出されます。 これは、HTTP 経由のクライアントの偽装を許可する RDS 1.5 の新機能です。 このモードで作業するとき、Web サーバー (IIS) へのログオンには匿名ではありませんが、ユーザー ID とクライアント コンピューターが実行されているパスワードを使用します。 ODBC Dsn は、信頼関係接続を使用する設定は、し、SQL Server などのデータベースへのアクセスは、クライアントのセキュリティ コンテキストでします。 これは、データベースが、IIS と同じコンピューターにある場合にのみ機能が、クライアントの資格情報は、まだ別のコンピューターに持ち越すことはできません。  
  
 たとえば、クライアント、John Doe, userid ="JohnD"とパスワード =「シークレット」は、クライアント コンピューターにログオンします。 アクセスする必要があるブラウザー ベースのアプリケーションを実行した、 **RDSServer.DataFactory**オブジェクトを作成する、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)"MyServer"のコンピューターで SQL クエリを実行して IIS を実行します。 MyServer、Windows NT Server 4.0 を実行するシステムが Windows NT チャレンジ/レスポンス認証を使用するよう設定されて、その ODBC DSN に「を使用して、信頼された接続」選択すると、され、サーバーにも、SQL Server データ ソースが含まれています。 Web サーバーで要求が受信されると、ユーザー ID とパスワードをクライアントを要求します。 そのため、要求が MyServer としてログオン"JohnD"から「シークレット」IUSER_MyServer (これは、匿名のパスワード認証が既定では) ではなく/。 同様に、"JohnD"の SQL Server にログオンするときに/「シークレット」を使用します。  
  
 その結果、IIS の Windows NT チャレンジ/レスポンス認証モードにより、HTML ページをユーザーがデータベースにログオンするために必要なユーザーの ID とパスワードの情報について明示的に要求されることがなく作成できます。 IIS 基本認証が使用されている場合、これにも必要です。  
  
## <a name="password-authentication"></a>パスワード認証  
 RDS は、次の 3 つのパスワード認証モードのいずれかで実行されている IIS Web サーバーと通信できます。Anonymous、Basic、または NT チャレンジ/レスポンス認証 (Windows 2000 では統合 Windows 認証と呼ばれます)。 これらの設定は、Web サーバーがクライアント コンピューターにある NT の Web サーバー上の明示的なアクセス特権を必要とするなど、アクセスを制御する方法を定義します。


