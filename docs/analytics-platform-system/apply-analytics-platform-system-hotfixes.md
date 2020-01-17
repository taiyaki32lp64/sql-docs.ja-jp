---
title: Analytics Platform System の修正プログラムの適用
description: この記事では、Analytics Platform システムソフトウェアに修正プログラムを適用する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd62413ec8542aba9f3973d0e8483cb9c5c9128a
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401371"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Analytics Platform System の修正プログラムの適用
この記事では、Analytics Platform システムソフトウェアに修正プログラムを適用する方法について説明します。  
  
## <a name="before-you-begin"></a>開始する前に  
  
> [!WARNING]  
> アプライアンスまたはアプライアンスのコンポーネントがダウンしているか、またはフェールオーバーされた状態である場合は、Analytics Platform System の修正プログラムを適用しないようにしてください。 その場合は、サポートにお問い合わせください。  
  
> [!WARNING]  
> アプライアンスの使用中は、Analytics Platform System の修正プログラムを適用しないでください。 修正プログラムを適用すると、アプライアンスノードが再起動される可能性があります。 アプライアンスが使用されていない場合は、メンテナンス期間中に修正プログラムを適用する必要があります。  
  
### <a name="prerequisites"></a>前提条件  
これらの手順を実行するには、次のものが必要です。  
  
-   アプライアンスの状態を監視するために管理コンソールにアクセスするためのアクセス許可を持つ Analytics Platform システムログイン。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   _<domain_name>_ **-HST01**ノードに接続するためのファブリックドメイン管理者アカウントの情報。  
  
## <a name="HowToInstallPDW"></a>Analytics Platform System 修正プログラムを適用するには  
Microsoft の更新プログラムとは異なり、Analytics プラットフォームシステムソフトウェアの修正プログラムは WSUS では処理されません。 これらのユーザーには、ワークフローが異なり、修正プログラムパッケージを実行してインストールされます。  
  
1.  **アプライアンスの状態インジケーターを確認します。**  
  
    1.  管理コンソールを開き、[アプライアンスの状態] ページに移動します。 詳細については、「[管理コンソールを使用したアプライアンスの監視 &#40;Analytics Platform System](monitor-the-appliance-by-using-the-admin-console.md) 」を参照してください&#41;  
  
    2.  次の手順に進む前に、すべての赤または黄色のインジケーターを解決する必要があります。 これには次のようないくつかの例外があります。  
  
        -   ディスクエラーが発生した場合は、管理コンソールの [アラート] ページを使用して、各サーバーまたは SAN アレイ内に1つ以上のディスク障害が発生していないことを確認します。 各サーバーまたは SAN アレイ内に1つ以上のディスク障害が発生していない場合は、次の手順に進み、ディスク障害を修正することができます。 できるだけ早くディスクエラーを修正するには、Microsoft サポートにお問い合わせください。  
  
        -   C:\ にない、重大でない (黄色の) ディスクボリュームエラーがある場合ディスクボリュームのエラーを解決する前に、次の手順に進むことができます。  
  
2.  **Analytics Platform System 修正プログラムをインストールする**  
  
    1.  ドメイン管理者として <*appliance_domain*>-HST01 ノードにログインします。  
  
    2.  [**管理者として実行**] オプションを使用して、コマンドプロンプトを開きます。  
  
    3.  次のコマンドを実行し*<HotfixPackageName>* ます。を修正プログラムの実行可能パッケージの名前に置き換え、他のプレースホルダー項目 *<  >* を適切な情報に置き換えます。  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  修正プログラムパッケージに記載されている手順に従います。  
  
## <a name="see-also"></a>参照  
[Microsoft Update &#40;Analytics Platform System&#41;をダウンロードして適用します](download-and-apply-microsoft-updates.md)  
[Microsoft 更新プログラムのアンインストール &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Analytics platform system の修正プログラム &#40;Analytics Platform System&#41;をアンインストールする](uninstall-analytics-platform-system-hotfixes.md)  
[ソフトウェアサービス &#40;Analytics Platform System&#41;](software-servicing.md)  
  
