---
title: 高可用性を実現するための SQL Server Integration Services (SSIS) Scale Out のサポート | Microsoft Docs
description: この記事では、高可用性を実現するために SSIS Scale Out を構成する方法について説明します
ms.custom: performance
ms.date: 05/23/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 36f4dce1559df59a61ee25d26b76d0ddd4dda3c1
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028749"
---
# <a name="scale-out-support-for-high-availability"></a>高可用性を実現するための Scale Out のサポート

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SSIS Scale Out では、複数の Scale Out Worker を使用してパッケージを実行することで、Scale Out Worker 側の高可用性が提供されます。

Scale Out Master 側の高可用性は、[Always On for SSIS Catalog](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) と Windows フェールオーバー クラスターにより実現されます。 このソリューションでは、Scale Out Master の複数のインスタンスは、Windows フェールオーバー クラスターでホストされています。 プライマリ ノードの Scale Out Master サービスまたは SSISDB がダウンすると、セカンダリ ノードのサービスまたは SSISDB が引き続きユーザーの要求を受け入れて、Scale Out Worker と通信します。

また、SQL Server フェールオーバー クラスター インスタンスを使用して Scale Out Master 側の高可用性を達成することもできます。 「[SQL Server フェールオーバー クラスター インスタンスを介した高可用性の Scale Out のサポート](scale-out-failover-cluster-instance.md)」を参照してください。

SSIS カタログに Always On を使用して Scale Out Master 側の高可用性を設定するには、次の手順を実行します。

## <a name="1-prerequisites"></a>1.Prerequisites
Windows フェールオーバー クラスターを設定します。 手順については、ブログ投稿の「[Windows Server 2012 のフェールオーバー クラスター機能とツールのインストール](https://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx)」 を参照してください。 すべてのクラスター ノードに機能とツールをインストールします。

## <a name="2-install-scale-out-master-on-the-primary-node"></a>2.プライマリ ノードに Scale Out Master をインストールする
Scale Out Master のプライマリ ノードに SQL Server データベース エンジン サービス、Integration Services、Scale Out Master をインストールします。 

インストール中に、次の操作を行います。

### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 ドメイン アカウントに Scale Out Master サービスを実行するアカウントを設定する
このアカウントは、後で Windows フェールオーバー クラスター内のセカンダリ ノード上の SSISDB にアクセスできる必要があります。 Scale Out Master サービスと SSISDB は個別にフェールオーバーできるため、フェールオーバー後は同じノード上にない場合があります。

![HA サーバーの構成](media/ha-server-config.PNG)

### <a name="22-include-the-dns-host-name-for-the-scale-out-master-service-in-the-cns-of-the-scale-out-master-certificate"></a>2.2 Scale Out Master サービスの DNS ホスト名を Scale Out Master 証明書の CN に含める

このホスト名は Scale Out Master エンドポイントであり、フェールオーバー クラスター内にクラスター化された汎用サービスとして作成されます (手順 7 を参照してください)。   (サーバー名ではなく、DNS ホスト名を指定してください。)

![HA マスターの構成](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-the-secondary-node"></a>3.セカンダリ ノードに Scale Out Master をインストールする
Scale Out Master のセカンダリ ノードに SQL Server データベース エンジン サービス、Integration Services、Scale Out Master をインストールします。 

プライマリ ノードで使用したものと同じ Scale Out Master 証明書を使用します。 プライマリ ノードで、Scale Out Master SSL 証明書を秘密キーと共にエクスポートし、セカンダリ ノード上のローカル コンピューターのルート証明書ストアにインストールします。 セカンダリ ノードに Scale Out Master をインストールするときに、この証明書を選択します。

![HA マスターの構成 2](media/ha-master-config2.PNG)

> [!NOTE]
> 他のセカンダリ ノードで Scale Out Master のこれらの操作を繰り返すことで、複数の Scale Out Master のバックアップを設定できます。

## <a name="4-set-up-and-configure-ssisdb-support-for-always-on"></a>4.Always On の SSISDB サポートを設定および構成する

「[Always On for SSIS Catalog (SSISDB)](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)」に記載されている Always On の SSISDB サポートを設定および構成する手順に従います。

さらに、SSISDB を追加する可用性グループに対して可用性グループ リスナーを作成する必要があります。 「[可用性グループ リスナーの作成または構成](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)」を参照してください。

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5.Scale Out Master サービス構成ファイルを更新する
プライマリ ノードとセカンダリ ノードで Scale Out Master サービス構成ファイル `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config` を更新します。 **SqlServerName** を *[Availability Group Listener DNS name],[Port]* に更新します。

## <a name="6-enable-package-execution-logging"></a>6.パッケージ実行のログ記録を有効にする

SSISDB でのログ記録は、ログイン **##MS_SSISLogDBWorkerAgentLogin##** (パスワードは自動生成されます) によって行われます。 SSISDB のすべてのレプリカのログ記録を機能させるには、次の操作を行います。

### <a name="61-change-the-password-of-ms_ssislogdbworkeragentlogin-on-the-primary-sql-server"></a>6.1 プライマリ SQL Server で **##MS_SSISLogDBWorkerAgentLogin##** のパスワードを変更する

### <a name="62-add-the-login-to-the-secondary-sql-server"></a>6.2 ログインをセカンダリ SQL Server に追加する

### <a name="63-update-the-connection-string-used-for-logging"></a>6.3 ログで使用する接続文字列を更新する
以下のパラメーター値を使用して、ストアド プロシージャ `[catalog].[update_logdb_info]` を呼び出します。

-   `@server_name = '[Availability Group Listener DNS name],[Port]'`

-   `@connection_string = 'Data Source=[Availability Group Listener DNS name],[Port];Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=[Password]];'`

## <a name="7-configure-the-scale-out-master-service-role-of-the-windows-server-failover-cluster"></a>7. Windows Server フェールオーバー クラスターの Scale Out Master サービス ロールを構成する

1.  フェールオーバー クラスター マネージャーで、Scale Out のクラスターに接続します。クラスターを選択します。 メニューで **[アクション]** を選択してから、 **[役割の構成]** を選択します。

2.  **[高可用性ウィザード]** ダイアログ ボックスの **[役割の選択]** ページで、 **[汎用サービス]** を選択します。 **[サービスの選択]** ページで、[SQL Server Integration Services Scale Out Master 14.0] を選択します。

3.  **[クライアント アクセス ポイント]** ページで、Scale Out Master サービスの DNS ホスト名を入力します。

    ![HA ウィザード 1](media/ha-wizard1.PNG)

4.  ウィザードを終了します。

Azure の仮想マシンでは、この構成手順の他に追加の手順が必要です。 これらの概念および手順の詳しい説明については、この記事の範囲対象外です。

1.  Azure ドメインを設定する必要があります。 Windows Server フェールオーバー クラスタリングでは、クラスター内のすべてのコンピューターが同じドメインのメンバーである必要があります。 詳細については、「[Azure Portal を使用して Azure Active Directory Domain Services を有効にする](https://docs.microsoft.com/azure/active-directory-domain-services/create-instance)」を参照してください。

2. Azure ロード バランサーを設定する必要があります。 これは可用性グループ リスナーの要件です。 詳細については、「[チュートリアル:Azure portal の Basic ロードバランサーを使用して内部トラフィックの負荷を分散する](https://docs.microsoft.com/azure/load-balancer/tutorial-load-balancer-basic-internal-portal)」を参照してください。

## <a name="8-update-the-scale-out-master-address-in-ssisdb"></a>8.SSISDB で Scale Out Master アドレスを更新する

プライマリ SQL Server で、パラメーター値 `@MasterAddress = N'https://[Scale Out Master service DNS host name]:[Master Port]'` を使用して、ストアド プロシージャ `[catalog].[update_master_address]` を実行します。 

## <a name="9-add-the-scale-out-workers"></a>9.Scale Out Worker を追加する

これで、[Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md) を使用して、Scale Out Worker を追加できます。 接続ページで「`[SQL Server Availability Group Listener DNS name],[Port]`」と入力します。

## <a name="upgrade-scale-out-in-high-availability-environment"></a>高可用性環境で Scale Out をアップグレードする
高可用性環境で Scale Out をアップグレードするには、[Always On for SSIS Catalog のアップグレード手順](../catalog/ssis-catalog.md#Upgrade)に従い、各コンピューター上の Scale Out Master と Scale Out Worker をアップグレードし、上記の手順 7 の Windows Server フェールオーバー クラスター ロールを新しいバージョンの Scale Out Master サービスを使用して再作成します。

## <a name="next-steps"></a>次の手順
詳細については、次の記事をご覧ください。
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)
