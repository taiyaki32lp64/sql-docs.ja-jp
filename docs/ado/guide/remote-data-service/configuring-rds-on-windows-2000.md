---
title: Windows 2000 での RDS の構成 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6230fb7ffbaa1226bc65d391d988ad064617998
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922896"
---
# <a name="configuring-rds-on-windows-2000"></a>Windows 2000 での RDS の構成
Windows 2000 にアップグレードした後に正常に機能する rds 問題が発生した場合、問題をトラブルシューティングする手順に従います。  
  
1.  World Wide Web 発行サービスの最初を Internet Explorer を使用して https:// サーバーに移動して実行することを確認します。 この方法で Web サーバーにアクセスできない場合は、コマンド プロンプトを開き、"NET 開始 W3SVC"次のコマンドを入力します。  
  
2.  [スタート] メニューには、実行を選択します。 Msdfmap.ini を入力し、メモ帳で msdfmap.ini ファイルを開くには、[ok] をクリックします。 [既定の接続] のセクションを確認し、アクセス パラメーターは、NOACCESS に設定されている場合は読み取り専用に変更します。  
  
3.  RegEdit ユーティリティを使用して、"HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo"に移動し、確認**HandlerRequired** 0 に設定されていると**DefaultHandler**は""(Null 文字列)。  
  
     **注**を停止し、コマンド プロンプトで次のコマンドを入力して、World Wide Web 発行サービスを再起動する必要があります、レジストリのこのセクションを変更する場合。"NET STOP W3SVC"と"NET 開始 W3SVC"。  
  
4.  RegEdit ユーティリティを使用してレジストリ"HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch"に移動し、という名前のキーがあることを確認**RDSServer.Datafactory**します。 それ以外の場合は、作成します。  
  
5.  インターネット サービス マネージャーを使用して、既定の Web サイトを見つけて MSADC 仮想ルートのプロパティを表示します。 ディレクトリのセキュリティ/IP アドレスおよびドメイン名の制限を検査します。 「アクセスが拒否されました」がオンの場合は、"Granted"を選択します。  
  
 場合、サーバーの再起動を行ってください。 変更は、最初の問題を解決するためには表示されません。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。Windows 8 および Windows Server 2012 以降、Windows オペレーティング システムで RDS サーバー コンポーネントは含まれなくします。 RDS を使用するアプリケーションを移行[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="see-also"></a>関連項目  
 [RDS の基礎](../../../ado/guide/remote-data-service/rds-fundamentals.md)


