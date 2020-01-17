---
title: アプライアンスのネットワーク構成
description: Analytics Platform System (APS) アプライアンスは、IHV の工場フロアから、すべてのサーバーと適用可能なデバイスの IP アドレスの修正セットを使用して構築および構成されています。 アプライアンスの配送時には、特定の顧客のデータセンター要件に合わせて、外部 (イーサネット) IP アドレスを再構成する必要があります。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: af892cbb43b42953732bda59d371e3e22855413b
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401412"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Analytics Platform System のアプライアンスネットワーク構成
Analytics Platform System (APS) アプライアンスは、IHV の工場フロアから、すべてのサーバーと適用可能なデバイスの IP アドレスの修正セットを使用して構築および構成されています。 アプライアンスの配送時には、特定の顧客のデータセンター要件に合わせて、外部 (イーサネット) IP アドレスを再構成する必要があります。  
  
> [!NOTE]  
> PDW V1 では、各コントロールラックノードへの外部接続を提供するために、8個の外部 (*顧客向け*) アドレスが必要でした。 PDW 2012 (V2) は、IP アドレス経由でアプライアンスのすべてのコンポーネントを外部に公開することで、ネットワーク通信を強化しました。 この方法では、コストを削減し、柔軟性を高め、データの移動、データの読み込み、Hadoop の統合を強化する、より堅牢な設計を実現します。 必要な IP アドレスの数は、アプライアンス内のノード数によって異なります。 この大きな IP アドレスブロックに対応するには、ユーザーが PDW 用に別のサブネットを設定する必要があります。 このサブネット内には、最大5つの PDW ラックのコンポーネントに対応するのに十分な IP アドレス空間 (最大250のアドレス) があります。  
  
[**ネットワークの構成**] ページでは、分析プラットフォームシステムアプライアンス上のノードに対して外部に接続されているネットワーク設定を表示できます。 このページは読み取り専用です。  
  
![DWConfig アプライアンス ネットワーク](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>アプライアンスのネットワーク構成を更新するには  
**AplianceInfo**ファイルを編集してからセットアップを実行して、ファブリックドメインおよびワークロードドメインの IP アドレスを変更します。 これはオフライン操作です。 PDW のリージョンは、IP アドレスの変更中に自動的に停止されます。  
  
> [!NOTE]  
> ドメイン名はセットアップ中に指定され、文字で始まる最大6文字の英数字で指定します。 頻繁な名前付けシステムでは、F で始まるファブリックドメインが作成されます。これは、P から始まる PDW ワークロードドメインです。この形式はヘルプファイルのトピック全体で想定されていますが、必須ではありません。 <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Analytics Platform System の IP アドレスを変更するには  
  
1.  **リモートデスクトップ**アプリケーションを使用して、ワークロードドメイン管理者アカウントを使用して**HST01**に接続します。  
  
2.  HST01 ノードで、 **c:\pdwinst\media\AplianceInfo.xml**にあるアプライアンスの情報ファイルを開きます。  
  
    > [!NOTE]  
    > ファイルが存在しない場合は、新しいファイルを作成する必要があります。  
  
3.  必要に応じてイーサネット IP 値を更新し、ファイルを保存します。  
  
4.  コマンドプロンプトウィンドウで、次のセットアップコマンドを実行して、PDW リージョンの IP アドレスを更新します。これは、P/F/H ドメイン名と管理者パスワードを使用して行います。  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>製造元参照  
Dell アプライアンスの詳細については、以下を参照してください。  
  
-   PowerConnect スイッチの手順[Dell PowerConnect 6200 Series SYSTEM CLI リファレンスガイド](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC [Integrated Dell Remote Access Controller 7 (iDRAC7) バージョン1.30.30 ユーザーガイド](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU の**Dell 従量制ラック pdu**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>参照  
[Configuration Manager &#40;Analytics Platform System&#41;を起動します。](launch-the-configuration-manager.md)  
  
