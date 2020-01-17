---
title: リモートテーブルのコピー
description: リモートテーブルのコピー機能を使用して、非アプライアンスサーバー上の SMP SQL Server データベースにテーブルをコピーするように並列データウェアハウスを構成する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6c9a0a29b543eb287c7e233d6b1ea77bb2a0d45c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401262"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>リモートテーブルコピー用に並列データウェアハウスを構成する
リモートテーブルのコピー機能を使用して、非アプライアンスサーバー上の SMP SQL Server データベースにテーブルをコピーする SQL Server PDW を構成する方法について説明します。  
  
このトピックでは、リモートテーブルのコピーを構成するための構成手順の1つについて説明します。 すべての構成手順の一覧については、「[リモートテーブルのコピー](remote-table-copy.md)」を参照してください。  
  
## <a name="before-you-begin"></a>開始する前に  
リモートテーブルのコピーを使用するように SQL Server PDW を構成するには、次のことを行う必要があります。  
  
-   Analytics Platform システム管理者アカウントに、 <strong> *appliance_domain*の AD01</strong>ノードと<strong> *appliance_domain*</strong>ノードに直接ログインできるようにします。  
  
-   移行先サーバーのホスト名または IP 名を確認します。  
  
## <a name="HowToPDW"></a>リモートテーブルのコピー用に SQL Server PDW を構成する: DNS でホスト名を更新する  
リモートテーブルのコピーに使用される**CREATE REMOTE table**ステートメントでは、SMP Windows システムの ip アドレスまたは ip 名を使用して、移行先サーバーを指定します。 IP 名を使用するには、DNS サーバーに名前解決を成功させるためのエントリを追加する必要があります。  
  
次の手順では、DNS サーバーを更新する方法を説明します。  
  
1.  アクティブな AD ノード (通常は<strong> *appliance_domain*-AD01</strong>) にログオンします。  
  
2.  DNS マネージャーを開きます。 これは、[**スタート**] メニューの [**管理ツール**] にあります。  
  
3.  DNS マネージャーを使用して、IP 名を追加します。  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[DNS フォワーダーを使用してアプライアンス以外の DNS 名を解決する](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
