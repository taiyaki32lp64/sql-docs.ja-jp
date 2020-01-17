---
title: マージ レプリケーションの Web 同期 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication synchronization [SQL Server replication]
- Internet [SQL Server replication], synchronization
- synchronization [SQL Server replication], Web Synchronization
- Web publishing [SQL Server replication], synchronization
- Web synchronization, about
- Web synchronization
ms.assetid: 84785aba-b2c1-4821-9e9d-a363c73dcb37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a3dfc7b81bf6f6a3ef0b9b74a2d1a78f3e3e1db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200110"
---
# <a name="web-synchronization-for-merge-replication"></a>マージ レプリケーションの Web 同期
  マージ レプリケーションの Web 同期を利用すると、HTTPS プロトコルを使用したデータのレプリケートが可能になり、以下のようなシナリオで役立ちます。  
  
-   モバイル ユーザーからのデータをインターネット上で同期します。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース間で、企業のファイアウォールを経由してデータを同期します。  
  
 たとえば、移動中の営業担当者は Web 同期を使用することができます。 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]の営業担当者は、担当地域内の多数の店舗や納入業者を回ります。 長い移動の際にはホテルに滞在するため、一日の終わりに販売データをアップロードしたり、製品の更新をダウンロードするための便利な方法が必要になります。  
  
 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] の IT 部門は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で各ポータブル コンピューターを構成し、マージ レプリケーションで Web 同期を使用できるようにしました。 各ポータブル コンピューターのマージ エージェントでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] インターネット インフォメーション サービス (IIS) を実行しているコンピューターにインストールされたレプリケーション コンポーネントを指すインターネットの URL を保持しています。 これらのコンポーネントにより、パブリッシャーとサブスクライバーが同期されます。 これで各担当者は、リモート ダイアルアップ接続を行わなくても、任意のインターネット接続経由で必要なデータのアップロードやダウンロードが行えるようになります。 インターネット接続では SSL (Secure Sockets Layer) を使用するため、仮想プライベート ネットワーク (VPN) は必要ありません。  
  
 Web 同期に必要なコンポーネントを構成する方法については、「[Configure Web Synchronization (Web 同期の構成)](configure-web-synchronization.md)」、「[Configure IIS for Web Synchronization (Web 同期用の IIS の構成)](configure-iis-for-web-synchronization.md)」、「[Configure IIS 7 for Web Synchronization (Web 同期用の IIS 7 の構成)](configure-iis-7-for-web-synchronization.md)」をご覧ください。  
  
> [!NOTE]  
>  Web 同期は、ポータブル コンピューター、ハンドヘルド デバイスなどのクライアントでデータを同期することを目的に設計されています。 Web 同期は、サーバー間のアプリケーションでの大量のデータ同期には適していません。  
  
## <a name="overview-of-how-web-synchronization-works"></a>Web 同期の動作の概要  
 Web 同期を使用すると、サブスクライバーでの更新はパッケージ化され、HTTPS プロトコルを使用して XML メッセージとして IIS を実行しているコンピューターに送信されます。 次に IIS を実行しているコンピューターは、バイナリ形式でパブリッシャーにコマンドを送信します (通常は TCP/IP を使用します)。 パブリッシャーでの更新は、IIS を実行しているコンピューターに送信され、XML メッセージとしてパッケージ化されてサブスクライバーに配信されます。  
  
 次の図は、マージ レプリケーションの Web 同期に関係するコンポーネントを示しています。  
  
 ![Web 同期コンポーネントとデータ フロー](media/web-sync01.gif "Web 同期コンポーネントとデータ フロー")  
  
 Web 同期は、プル サブスクリプションだけのオプションなので、サブスクライバー上では必ずマージ エージェントが動作します。 標準のマージ エージェント、マージ エージェントの ActiveX コントロール、またはレプリケーション管理オブジェクト (RMO) によって同期機能を提供するアプリケーションのいずれかを使用できます。 IIS を実行しているコンピューターの場所を指定するには、マージ エージェントの **-InternetUrl** パラメーターを使用します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション リスナー (Replisapi.dll) は、IIS を実行しているコンピューター上で構成され、パブリッシャーとサブスクライバーからサーバーに送信されたメッセージを処理します。 トポロジの各ノードは、マージ レプリケーション競合回避モジュール (Replrec.dll) を使用して XML データ ストリームを処理します。  
  
 Web 同期に参加するすべてのコンピューターに、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降が必要です。  
  
### <a name="synchronization-process"></a>同期プロセス  
 同期中の手順は次のとおりです。  
  
1.  マージ エージェントがサブスクライバーで開始されます。 このエージェントでは、次のことを行います。  
  
    1.  サブスクリプション データベースに SQL 接続を行います。  
  
    2.  データベースからすべての変更を抽出します。  
  
    3.  IIS を実行しているコンピューターに HTTPS 要求を行います。  
  
    4.  データの変更を XML メッセージとしてアップロードします。  
  
2.  IIS を実行しているコンピューター上でホストされる、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション リスナーおよびマージ レプリケーション競合回避モジュールでは、次のことを行います。  
  
    1.  HTTPS 要求に応答します。  
  
    2.  パブリケーション データベースに SQL 接続を行います。  
  
    3.  アップロードされた変更をパブリケーション データベースに適用します。  
  
    4.  サブスクライバー用にダウンロードされた変更を抽出します。  
  
    5.  HTTPS 応答をマージ エージェントに返送します。  
  
3.  その後、サブスクライバーのマージ エージェントは HTTPS 応答を受け取り、サブスクリプション データベースに変更のダウンロードを適用します。  
  
## <a name="see-also"></a>参照  
 [Configure Web Synchronization](configure-web-synchronization.md)   
 [Topologies for Web Synchronization](topologies-for-web-synchronization.md)  
  
  
