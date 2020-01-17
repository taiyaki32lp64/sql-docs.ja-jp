---
title: Web サーバー情報 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5f5c2385b4c58447db008544124ae9048566958
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199945"
---
# <a name="web-server-information"></a>Web サーバー情報
  Web サーバー情報は、マージ レプリケーションの Web 同期オプションを使用する場合に必要です。 Web 同期の構成の詳細については、「[Configure Web Synchronization (Web 同期の構成)](configure-web-synchronization.md)」をご覧ください。  
  
## <a name="options"></a>および  
 **[Web サーバー アドレス]**  
 **[パブリケーションのプロパティ]** ダイアログ ボックスの **[FTP スナップショットとインターネット]** ページで Web サーバー アドレスを指定している場合は、そのアドレスがこのテキスト ボックスに既定として表示されます。 既定値を受け入れるか、このサブスクリプションを同期する [!INCLUDE[msCoName](../../includes/msconame-md.md)] インターネット インフォメーション サービス (IIS) の完全修飾 Web サーバー アドレスを入力します。  
  
 **[各サブスクライバーが Web サーバーに接続する方法を指定します。]**  
 Web サーバーへの接続に使用される認証の種類を指定します。 IIS サーバーへの接続用の [基本認証] を SSL (Secure Sockets Layer) と組み合わせて使用することをお勧めします。 [基本認証] を選択した場合は、サブスクライバーから IIS サーバーへの接続に使用されるログインとパスワードを入力してください。  
  
## <a name="see-also"></a>関連項目  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [プル サブスクリプションのプロパティの表示または変更](view-and-modify-pull-subscription-properties.md)   
 [SQL Server 以外のサブスクライバー](non-sql/non-sql-server-subscribers.md)   
 [パブリケーションのサブスクライブ](subscribe-to-publications.md)   
 [マージ レプリケーションの Web 同期](web-synchronization-for-merge-replication.md)  
  
  
