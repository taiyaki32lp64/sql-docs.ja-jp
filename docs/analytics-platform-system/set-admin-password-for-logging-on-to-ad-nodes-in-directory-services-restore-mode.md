---
title: Active Directory パスワードの設定
description: Analytics Platform System (APS) のディレクトリサービス復元モードで Active Directory ノード管理者のログオンパスワードを設定します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbbf42106602a25b03072a9c9abfb04f04d3c49
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400331"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>ディレクトリサービス復元モード (DSRM) で AD ノードにログオンするための管理者パスワードを設定する-Analytics Platform System
ディレクトリサービス復元モード (DSRM) は、Active Directory Domain Services (AD DS) を修復または回復するためのブートモードです。 AD DS が失敗した後、または AD DS を復元する必要があるときに、アプライアンスの AD ノードにログオンするために使用されます。 DSRM のパスワードは、ハードウェアベンダーサイトでのアプライアンスのセットアップ中に初期化されており、アプライアンス管理者が変更する必要があります。 Analytics Platform System は2つの AD DS (ドメインコントローラー) を備えています。** _appliance_domain_-AD01**および** _appliance_domain_-AD02**。 各アプライアンス AD ノードについて、次の手順に従って DSRM パスワードを変更します。  
  
## <a name="HowToDSRM"></a>管理者パスワードをリセットするには  
  
1.  アプライアンスの AD ノード<strong> _appliance_domain_AD_xx_</strong>仮想マシンでコマンドプロンプトウィンドウを開きます。  
  
2.  コマンド プロンプトで「 `ntdsutil`」と入力します。  
  
3.  **Ntdsutil**プロンプトで、「」 `set dsrm password`と入力します。  
  
4.  [**管理者パスワードのリセット:** ] プロンプト`reset password on server null`で、「」と入力します。  
  
5.  プロンプトで、新しいパスワードを入力します。  
  
6.  各アプライアンス AD バーチャルマシンについて、上記の手順 1-5 を繰り返します。  
  
    > [!WARNING]  
    > Analytics Platform System では、ドメイン管理者またはローカル管理者のパスワードのドル記号 ($) はサポートされていません。 ドル記号を含むパスワードが検証され、使用できるようになりますが、アップグレードとメンテナンスのアクティビティをブロックできます。  
  
> [!NOTE]  
> 特定の AD 仮想マシンで Active Directory Domain Services または仮想マシンが破損した場合は、影響を受けた AD 仮想マシンの交換**evm**を実行することをお勧めします。 CSS に問い合わせてください。  
  
## <a name="see-also"></a>参照  
[&#40;Analytics Platform System&#41;のパスワードリセット](password-reset.md)  
  
