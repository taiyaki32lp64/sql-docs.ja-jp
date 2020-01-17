---
title: 起動 Configuration Manager
description: Analytics Platform System appliance の Configuration Manager ツールを起動する手順。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 421265abcf3731ed48ff34a6b199ba5cd3c6af5c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401054"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>Analytics Platform System の Configuration Manager を起動する
このトピックでは、Analytics Platform System appliance の**Configuration Manager**を起動する手順について説明します。  
  
## <a name="before-you-begin"></a>開始する前に  
  
### <a name="prerequisites"></a>前提条件  
Analytics Platform System**Configuration Manager**は、アプライアンスドメイン管理者のみが実行できます。 このツールを実行するには、アプライアンスドメイン管理者のパスワードが必要です。 追加の APS 管理者を作成するには、「aps[ドメイン管理者 &#40;aps&#41;を作成](create-an-aps-domain-administrator-aps.md)する」を参照してください。  
  
## <a name="Accessing"></a>Configuration Manager ツールを起動する  
Configuration Manager を実行するには、リモートデスクトップを使用して PDW コントロールノード (**_PDW_region_CTL01**) ノードに接続し、 _appliance_domain_**\Administrator**としてログインします。 **Configuration Manager**プログラムを起動する場合は、[**管理者として実行**] オプションを使用して、管理者の資格情報が使用されていることを確認します。  
  
#### <a name="to-launch-from-a-browser-window"></a>ブラウザーウィンドウから起動するには  
  
1.  ブラウザーを開き、ディレクトリ`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`に移動します。  
  
2.  [`dwconfig.exe`] を右クリックし、**[管理者として実行]** をクリックします。  
  
#### <a name="to-launch-from-a-command-prompt"></a>コマンドプロンプトから起動するには  
  
1.  デスクトップで [**スタート**] メニューを開き、[**プログラム**]、[**アクセサリ**] の順にクリックし、[**コマンドプロンプト**] を右クリックして、[**管理者として実行**] をクリックします。  
  
2.  コマンドプロンプトで、次のコマンドを入力してディレクトリ`cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`を変更します。  
  
3.  コマンドプロンプトで、「」 `dwconfig.exe`と入力します。  
  
**Configuration Manager**が開始されると、左側のウィンドウに使用可能なすべての機能が表示されます。 このセクションの残りの部分では、ツールで使用できる各アクションを実行する方法について説明します。  
  
**Configuration Manager**を閉じて終了するには、画面の右下隅にある [**終了**] をクリックします。  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>参照  
[管理コンソール &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-the-admin-console.md)  
  
