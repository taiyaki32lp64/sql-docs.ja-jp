---
title: サブスクリプションの種類 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d936c1a1086f13d43bc38758f86a0ab80f757f7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63249381"
---
# <a name="subscription-type"></a>サブスクリプションの種類
  マージ レプリケーションでは、サーバーとクライアントという 2 つのサブスクリプションの種類がオファーされます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンでは、これらはグローバルとローカルと呼ばれていました。 サブスクライバーはサーバー サブスクリプションによって次の操作を実行できます。  
  
-   他のサブスクライバーにデータを再パブリッシュする。  
  
-   代わりの同期パートナーを提供する。  
  
-   設定された優先度に応じて競合を解決する。  
  
 ほとんどのサブスクライバーは、この機能を必要とせず、クライアント サブスクリプションを使用できます。 クライアント サブスクリプションは競合の検出と解決ができますが、サブスクライバーには優先度が割り当てられていません。変更によって競合が発生した場合は、変更をパブリッシャーに最初に送信したサブスクライバーが優先されます。  
  
> [!NOTE]  
>  サブスクリプションの種類は、作成後に変更することはできません。  
  
## <a name="options"></a>および  
 **[サブスクリプションのプロパティ]**  
 **[サブスクリプションの種類]** 列のドロップダウン リスト ボックスで、各サブスクライバーに対して、 **[クライアント]** または **[サーバー]** を選択します。 サブスクライバーでサーバー サブスクリプションを使用する場合は、 **[競合解決の優先度]** 列に 0 ～ 99.99 の範囲の数値を入力します。数字が大きいほどサブスクライバーに対する優先度が高くなります。  
  
## <a name="see-also"></a>参照  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [ssSDSFull](create-a-push-subscription.md)   
 [パブリケーションのサブスクライブ](subscribe-to-publications.md)  
  
  
