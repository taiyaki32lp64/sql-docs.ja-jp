---
title: TCP/IP のプロパティ ([IP アドレス] タブ) |Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], listening on
- listening [SQL Server], on ports
ms.assetid: 4c17ed45-9da7-4bec-bce6-970109fe7365
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 927f732d4f04c43b5e2973a82509e4da7970a448
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023811"
---
# <a name="tcpip-properties-ip-addresses-tab"></a>[TCP/IP のプロパティ]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  **[TCP/IP のプロパティ]** ダイアログ ボックス ([IP アドレス] タブ) では、TCP/IP プロトコルの特定の IP アドレスに関するオプションを構成します。 **[TCP 動的ポート]** と **[TCP ポート]** だけは、 **[IP All]** を選択することですべてのアドレスを一度に構成できます。  
  
 SQL Server を再起動すると変更が有効になります。 SQL Server Browser サービスの開始と停止の詳細については、「[SQL Server Browser サービスの開始および停止](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)」をご覧ください。  
  
## <a name="static-vs-dynamic-ports"></a>静的ポートと動的ポート  
 SQL Server の既定のインスタンスは、着信接続をポート 1433 でリッスンします。 このポートは、セキュリティ上の理由またはクライアント アプリケーションの要件に応じて変更することができます。 既定では、名前付きインスタンス (SQL Server Express を含む) は動的ポートでリッスンするように構成されています。 静的ポートを構成するには、 **[TCP 動的ポート]** を空白にし、 **[TCP ポート]** に使用可能なポート番号を指定します。 ファイアウォールでポートを開く方法の詳細については、オンライン ブックの「SQL Server のアクセスを許可するための Windows ファイアウォールの構成」を参照してください。  
  
## <a name="dynamic-ports"></a>動的ポート  
 SQL Server のインスタンスが動的ポートでリッスンするように構成されている場合、インスタンスは起動時にオペレーティング システムを調べて使用できるポートを検出し、そのポートに対するエンドポイントを開きます。 着信接続は、そのポート番号を指定して接続する必要があります。 SQL Server を起動するたびにポート番号が変わる可能性があるので、SQL Server には、ポートを監視して、着信接続をそのインスタンスの現在のポートにダイレクトする SQL Server Browser サービスが用意されています。 ファイアウォール経由で SQL Server に接続する場合に動的ポートを使用すると、SQL Server の再起動時にポート番号が変わる可能性があるので、そのたびにファイアウォールの設定を変更しなければなりません。 ファイアウォールによる接続の問題を回避するには、静的ポートを使用するように SQL Server を構成します。  
  
## <a name="options"></a>オプション  
 **Active**  
 コンピューターでその IP アドレスがアクティブかどうかを示します。 **[IPAll]** では指定できません。  
  
 **有効**  
 **[TCP/IP のプロパティ] ダイアログ ボックス ([プロトコル] タブ)** で **[すべて受信待ち]** プロパティを **[いいえ]** に設定している場合、このプロパティは SQL Server がそのポートでリッスンしているかどうかを示します。 **[TCP/IP のプロパティ] ダイアログ ボックス ([プロトコル] タブ)** で **[すべて受信待ち]** プロパティを **[はい]** に設定している場合、このプロパティは無視されます。 **[IPAll]** では指定できません。  
  
 **[IP アドレス]**  
 この接続が使用している IP 接続を表示または変更します。 コンピューターが使用している IP アドレスと、IP ループバック アドレス 127.0.0.1 が一覧表示されます。 **[IPAll]** では指定できません。 IP アドレスは、IPv4 形式または IPv6 形式で指定できます。  
  
 **[TCP 動的ポート]**  
 動的ポートが有効になっていない場合は空白です。 動的ポートを使用するには、0 に設定します。  
  
 **[IPAll]** には、使用する動的ポートのポート番号が表示されます。  
  
 **[TCP ポート]**  
 SQL Server がリッスンするポートを表示または変更します。 既定では、SQL Server の既定のインスタンスはポート 1433 でリッスンします。  
  
 データベース エンジンは、同じ IP アドレスで複数のポートをリッスンできます。複数のポートを指定するには、「1433,1500,1501」のようにコンマで区切って入力します。 このフィールドには最大 2,047 文字まで入力できます。  
  
 1 つの IP アドレスを複数のポートでリッスンするように構成する場合は、 **[TCP/IP のプロパティ]** ダイアログ ボックスの **[プロトコル]** タブで **[すべて受信待ち]** パラメーターも **[いいえ]** に設定する必要があります。 詳細については、SQL Server オンライン ブックの「複数の TCP ポートでリッスンするようにデータベース エンジンを構成する方法」を参照してください。  
  
## <a name="adding-or-removing-ip-addresses"></a>IP アドレスの追加または削除  
 SQL Server 構成マネージャーでは、SQL Server のインストール時に使用可能になった IP アドレスが表示されます。 使用可能な IP アドレスは、ネットワーク カードが追加または削除された場合、動的に割り当てられた IP アドレスが期限切れになった場合、ネットワーク構造が再構成された場合、あるいはコンピューターの物理的な場所が変わった場合 (ラップトップ コンピューターが別の建物でネットワークに接続するときなど) に、変わることがあります。 IP アドレスを変更するには、 **[IP アドレス]** ボックスを編集し、SQL Server を再起動します。  
  
## <a name="additional-topics-in-books-online"></a>オンライン ブックの追加トピック  
 「 **特定の TCP ポートで受信待ちするようにサーバーを構成する方法 (SQL Server 構成マネージャー)** 」や「 **複数の TCP ポートでリッスンするデータベース エンジンの構成**」などのトピックを MSDN で参照してください。  
  
## <a name="see-also"></a>参照  
 [ネットワーク プロトコルの選択](https://msdn.microsoft.com/library/ms187892(v=sql.120).aspx)   
 [TCP/IP を使用した有効な接続文字列の作成](creating-a-valid-connection-string-using-tcp-ip.md)   
 [SQL Server Browser サービス](sql-server-browser-service.md)  
  
  
