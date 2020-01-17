---
title: 暗号化キーの構成と管理 (SSRS 構成マネージャー) | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- private keys [Reporting Services]
- cryptography [Reporting Services]
- symmetric keys [Reporting Services]
- encryption [Reporting Services]
- public keys [Reporting Services]
ms.assetid: 58e61636-88a2-4338-ae5f-3dd210aee887
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1d45ec74ab78ad9b201f7829af00d417215e3ac1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651749"
---
# <a name="ssrs-encryption-keys---manage-encryption-keys"></a>SSRS 暗号化キー - 暗号化キーの管理
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、暗号化キーを使用して、レポート サーバー データベースに格納されている資格情報および接続情報をセキュリティで保護します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の暗号化では、公開キー、秘密キー、対称キーを組み合わせて機密データの保護に使用します。 対称キーは、レポート サーバーをインストールまたは構成するとき、レポート サーバーの初期化中に作成されます。レポート サーバーはこの対称キーを使用して、レポート サーバーに保存される機密データを暗号化します。 公開キーと秘密キーはオペレーティング システムによって作成され、これらのキーを使用して対称キーが保護されます。 公開キーと秘密キーのペアは、レポート サーバー データベースに機密データを格納するレポート サーバー インスタンスごとに作成されます。  
  
 暗号化キーを管理するには、対称キーのバックアップ コピーを作成するほか、キーの復元、削除、変更のタイミングと方法を知る必要があります。 レポート サーバーのインストールを移行する場合、またはスケールアウト配置を構成する場合は、対称キーを新しいインストールに適用できるように、対称キーのバックアップ コピーが必要です。  
  
> [!IMPORTANT]  
>  セキュリティを高めるために、Reporting Services の暗号化キーは定期的に変更することをお勧めします。 キーを変更する推奨されるタイミングは、Reporting Services のメジャー バージョンのアップグレードの直後です。 アップグレード後であれば、アップグレード サイクル以外での Reporting Services の暗号化キーの変更に伴う他のサービスの中断を最小限に抑えることができます。  
  
 対称キーを管理する場合、Reporting Services 構成ツールまたは **rskeymgmt** ユーティリティを使用できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に含まれるツールは、対称キーのみの管理に使用します (公開キーと秘密キーはオペレーティング システムによって管理されます)。 Reporting Services 構成ツールと **rskeymgmt** ユーティリティはどちらも、以下のタスクをサポートします。  
  
-   レポート サーバーを復旧させるため、または計画的な移行の一環として使用できるように、対称キーのコピーをバックアップします。  
  
-   以前保存した対称キーをレポート サーバー データベースに復元し、新しいレポート サーバー インスタンスによって暗号化されたわけではない既存のデータにアクセスできるようにします。  
  
-   暗号化されたデータにアクセスできなくなった場合は、レポート サーバー データベース内の暗号化されたデータを削除します。  
  
-   対称キーに障害が起きた場合は、その対称キーを再作成し、データを再暗号化します。 セキュリティを重視する場合は、対称キーを定期的 (たとえば、数か月ごと) に再作成して、キーを解読しようとするサイバー攻撃からレポート サーバー データベースを保護する必要があります。  
  
-   複数のレポート サーバーが 1 つのレポート サーバー データベースとそのデータベースの暗号化を解除する対称キーの両方を共有する場合、スケールアウト配置のレポート サーバーでレポート サーバーのインスタンスを追加、または削除します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
 暗号化キーの作成方法について説明します。  
  
 [Reporting Services の暗号化キーのバックアップと復元](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
 暗号化キーをバックアップおよび復元し、レポート サーバーを復旧または移行する方法について説明します。  
  
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
 レポート サーバーでの暗号化について説明します。  
  
 [暗号化キーの削除と再作成 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)  
 対称キーを新しいバージョンに置き換える方法、および対称キーを検証できない場合にやり直す方法について説明します。  
  
 [スケールアウト配置に関する暗号化キーの追加と削除 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)  
 暗号化キーを追加および削除し、どのレポート サーバーをスケールアウト配置の一部に含めるのかを管理する方法について説明します。  
  
## <a name="see-also"></a>参照  
[Reporting Services Configuration Manager (ネイティブ モード)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)
