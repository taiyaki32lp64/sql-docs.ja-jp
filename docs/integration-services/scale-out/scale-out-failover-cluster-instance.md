---
title: SQL Server フェールオーバー クラスター インスタンスを介した高可用性を実現するための SQL Server Integration Services (SSIS) Scale Out のサポート | Microsoft Docs
description: この記事では、SQL Server フェールオーバー クラスター インスタンスを使用して高可用性を実現するための SSIS Scale Out を構成する方法について説明します
ms.custom: performance
ms.date: 04/10/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 5c4d5cc303d297a21b730abc30e10b85c65cc3d2
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811201"
---
# <a name="scale-out-support-for-high-availability-via-sql-server-failover-cluster-instance"></a>SQL Server フェールオーバー クラスター インスタンスを介した高可用性の Scale Out のサポート

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server フェールオーバー クラスター インスタンスを使用して Scale Out Master 側の高可用性を設定するには、次の手順を実行します。

## <a name="1-prerequisites"></a>1.Prerequisites
Windows フェールオーバー クラスターを設定します。 手順については、ブログ投稿の「[Windows Server 2012 のフェールオーバー クラスター機能とツールのインストール](https://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx)」 を参照してください。 すべてのクラスター ノードに機能とツールをインストールします。

## <a name="2-install-sql-server-failover-cluster"></a>2.SQL Server フェールオーバー クラスターをインストールする
SQL Server フェールオーバー クラスターをインストールします。 手順については、「[SQL Server フェールオーバー クラスターのインストール](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)」を参照してください。 インストール時に、[機能の選択] ページで [データベース エンジン サービス] を選択します。 今後の構成のために SQL Server ネットワーク名を記録します。

![SQL ネットワーク名](media/sql-network-name.PNG)

セカンダリ ノードを SQL Server フェールオーバー クラスターに追加します。

## <a name="3-install-scale-out-master-on-the-primary-node"></a>3.プライマリ ノードに Scale Out Master をインストールする
クラスター化されていないインストールの場合、セットアップ ウィザードを使用して、プライマリ ノード上に Integration Services と Scale Out Master をインストールします。 

インストール時に、Scale Out Master 証明書の CN に SQL Server ネットワーク名を含めます。

> [!NOTE]
> SSISDB と Scale Out Master サービスを個別にフェールオーバーする場合、Scale Out Master の構成については、「[2.プライマリ ノードに Scale Out Master をインストールする](scale-out-support-for-high-availability.md#2-install-scale-out-master-on-the-primary-node)」に従います。

## <a name="4-install-scale-out-master-on-the-secondary-node"></a>4.セカンダリ ノードに Scale Out Master をインストールする
「[3.セカンダリ ノードに Scale Out Master をインストールする](scale-out-support-for-high-availability.md#3-install-scale-out-master-on-the-secondary-node)」に従います

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5.Scale Out Master サービス構成ファイルを更新する
プライマリ ノードとセカンダリ ノードで、Scale Out Master サービス構成ファイル \<ドライブ\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config を更新します。 既定のインスタンスの **SqlServerName** を [SQL Server ネットワーク名]//[インスタンス名] または [SQL Server ネットワーク名] に更新します。

## <a name="6-add-scale-out-master-service-to-sql-server-role-in-windows-failover-cluster"></a>6.Windows フェールオーバー クラスターで SQL Server の役割に Scale Out Master サービスを追加する
フェールオーバー クラスター マネージャーで、Scale Out のクラスターに接続します。エクスプローラーで [ロール] を選択し、SQL Server のロールを右クリックし、[リソースの追加]、[汎用サービス] の順に選択します。 

![汎用サービス](media/generic-service.PNG)

新しいリソース ウィザードで、Scale Out Master サービスを選択し、ウィザードを終了します。 

Scale Out Master サービスをオンラインにします。

![オンラインにする](media/bring-online.PNG)

> [!NOTE]
> SSISDB と Scale Out Master サービスを個別にフェールオーバーする場合、「[7.Windows フェールオーバー クラスターの Scale Out Master サービス ロールを構成する](scale-out-support-for-high-availability.md#7-configure-the-scale-out-master-service-role-of-the-windows-server-failover-cluster)」に従います。

## <a name="7-install-scale-out-workers"></a>7.Scale Out Worker をインストールする
worker ノードに Scale Out Worker をインストールします。 インストール時に、マスター エンドポイントに https://[SQL Server ネットワーク名]:[マスター ポート] を指定します。 

> [!NOTE]
> SSISDB と Scale Out Master サービスを個別にフェールオーバーする場合は、SQL Server ネットワーク名の代わりに Scale Out Master サービスの DNS ホスト名を指定します。

## <a name="8-install-scale-out-worker-client-certificate"></a>8.Scale Out Worker クライアント証明書をインストールする
SQL Server フェールオーバー クラスター内のすべてのノードにワーカー証明書をインストールします。 「[Scale Out Worker クライアント証明書をインストールする](walkthrough-set-up-integration-services-scale-out.md#InstallCert)」を参照してください。

> [!NOTE]
> Scale Out Master は SQL Server フェールオーバー クラスターをサポートしていません。 Scale Out Manager を使用して Scale Out Worker を追加する場合は、すべてのマスター ノードにワーカー証明書を手動でインストールする必要があります。

## <a name="next-steps"></a>次の手順
詳細については、次の記事をご覧ください。
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)
