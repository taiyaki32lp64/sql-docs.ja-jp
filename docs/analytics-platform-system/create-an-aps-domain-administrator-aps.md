---
title: ドメイン管理者の作成
description: 一部の操作では、分析プラットフォームのシステムドメイン管理者特権が必要です。 ここでは、追加のアプライアンスドメイン管理者を作成する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1a0d50e485f0e8f48de11b2e5a3c27c9f9be047e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401229"
---
# <a name="create-an-aps-domain-administrator"></a>APS ドメイン管理者の作成
一部の操作では、分析プラットフォームのシステムドメイン管理者特権が必要です。 ここでは、追加のアプライアンスドメイン管理者を作成する方法について説明します。  
  
## <a name="create-a-domain-administrator"></a>ドメイン管理者の作成  
すべての aps ノードを構成するための十分なアクセス許可を与えるには`dwconfig.exe`、 **aps Configuration Manager** () を実行するユーザーが**domain Admins**グループのメンバーである必要があります。 APS サービスを開始および停止するには、ユーザーが**PdwControlNodeAccess**グループのメンバーである必要があります。  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Domain Admins グループにユーザーを追加するには  
  
1.  既存のアプライアンスドメイン管理者アカウントを使用して、アクティブな AD ノード **(_アプライアンス\_ドメイン_-AD01**または** _\_アプライアンスのドメイン_-AD02**) にログインします。  
  
2.  [スタート] メニューの **[ファイル名を指定して実行]** をクリックします。 [**名前**] ボックスに「 **dsa.msc**」と入力します。 [**OK**] をクリックすると、  
  
3.  **Active Directory ユーザーとコンピューター** ] プログラムで、[**ユーザー**] を右クリックし、[**新規作成**] をポイントして [**ユーザー**] をクリックします。  
  
4.  [**新しいオブジェクト-ユーザー** ] ダイアログボックスで、新しいユーザーの説明を入力し、[**次へ**] をクリックします。  
  
    [パスワード] ダイアログボックスを完了し、[**次へ**] をクリックします。  
  
    > [!WARNING]  
    > SQL Server PDW では、ドメイン管理者またはローカル管理者のパスワードのドル記号 ($) はサポートされていません。 ドル記号を含むパスワードは有効であり、使用できますが、アップグレードとメンテナンスのアクティビティをブロックすることができます。  
  
    新しいユーザーの説明を確認し、[**完了**] をクリックします。  
  
5.  ユーザーの一覧で、新しいユーザーをダブルクリックして、[ユーザーのプロパティ] ダイアログボックスを開きます。  
  
6.  
  **[所属するグループ]** タブの **[追加]** をクリックします。  
  
    「Domain Admins」と入力し**ます。PdwControlNodeAccess**をクリックし、[**名前の確認**] をクリックします。 [**OK**] をクリックすると、  
  
    これにより、新しいユーザーが**Domain Admins**グループと**PdwControlNodeAccess**グループに追加されます。 [**OK**] をクリックすると、  
  
## <a name="see-also"></a>参照  
[Configuration Manager &#40;Analytics Platform System&#41;を起動します。](launch-the-configuration-manager.md)  
  
