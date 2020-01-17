---
title: 修正プログラムのアンインストール
description: Analytics Platform System の修正プログラムをアンインストールします。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef6929aeb06c9472eb3ff210de016117a9636ded
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399761"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Analytics Platform System の修正プログラムのアンインストール 
次の手順では、以前にインストールした Analytics Platform System 修正プログラムをアンインストールする方法について説明します。  
  
## <a name="before-you-begin"></a>開始する前に  
  
### <a name="prerequisites"></a>前提条件  
これらの手順を実行するには、次のものが必要です。  
  
-   アプライアンスを監視するために管理コンソールにアクセスするためのアクセス許可を持つ分析プラットフォームシステムログイン。  
  
-   <em><appliance_domain></em> **-HST01**ノードにログインするドメイン管理者アカウント。  
  
-   アンインストールする修正プログラムのサポート技術情報の記事番号。  
  
## <a name="HowToUninstallPDW"></a>SQL Server PDW 修正プログラムをアンインストールするには  
  
1.  ファブリックドメイン管理者として<em><appliance_domain></em> **-HST01**ノードにログオンします。  
  
2.  [管理者として実行] オプションを使用して、コマンドプロンプトを開きます。  
  
3.  ディレクトリをに`C:\PDWINST\Patches\<kbarticle>\media`変更*<kbarticle>* します。には、アンインストールする修正プログラムのサポート技術情報の記事番号を指定します。  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  修正プログラムを削除するには、次のコマンドを実行します。  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>参照  
[Microsoft Update &#40;Analytics Platform System&#41;をダウンロードして適用します](download-and-apply-microsoft-updates.md)  
[Microsoft 更新プログラムのアンインストール &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Analytics platform system の修正プログラム &#40;analytics Platform System&#41;を適用します](apply-analytics-platform-system-hotfixes.md)  
[ソフトウェアサービス &#40;Analytics Platform System&#41;](software-servicing.md)  
  
