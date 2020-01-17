---
title: ポリシー管理者にポリシー エラーを通知する警告の構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 57eb4f021a25fa2fa559fa7ff21d12bb621cc53a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126911"
---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>ポリシー管理者にポリシー エラーを通知する警告の構成
  ポリシー ベースの管理ポリシーが 3 つの自動評価モードのいずれかで実行された場合にポリシー違反が発生すると、メッセージがイベント ログに書き込まれます。 このメッセージがイベント ログに書き込まれたときに通知を受けるには、メッセージを検出してアクションを実行する警告を作成します。 警告は、次の表に示すようにメッセージを検出します。  
  
|実行モード|メッセージ番号|  
|--------------------|--------------------|  
|変更中 - 禁止<br /><br /> (自動の場合)|34050|  
|変更中 - 禁止<br /><br /> (要求時に実行する場合)|34051|  
|スケジュールで実行|34052|  
|変更中|34053|  
  
 ポリシー ベースの管理のエラー メッセージに対処するように警告を設定するには、次のトピックを参照してください。  
  
-   [オペレーターの作成](../../ssms/agent/create-an-operator.md)  
  
-   [エラー番号を使用して警告を作成する](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [オペレーターへの警告の割り当て](../../ssms/agent/assign-alerts-to-an-operator.md)  
  
## <a name="permissions"></a>アクセス許可  
 要求時に評価されるポリシーは、ユーザーのセキュリティ コンテキストで実行されます。 エラー ログに書き込むには、ALTER TRACE 権限を持っているか、固定サーバー ロール sysadmin のメンバーである必要があります。 権限が不十分なユーザーがポリシーを評価した場合、イベント ログへの書き込みは行われず、警告は発生しません。  
  
 自動実行モードは、sysadmin ロールのメンバーとして実行されます。 これにより、エラー ログへの書き込みと警告の生成が可能になります。  
  
## <a name="additional-considerations-about-alerts"></a>警告に関するその他の注意点  
 警告に関するその他の注意点を次に示します。  
  
-   警告は、有効になっているポリシーに対してのみ発生します。 **[要求時]** ポリシーは有効にできないので、要求時に実行されるポリシーに対して警告は発生しません。  
  
-   実行するアクションに電子メール メッセージの送信が含まれる場合は、メール アカウントを構成する必要があります。 データベース メールを使用することをお勧めします。 データベース メールをセットアップする方法の詳細については、「 [データベース メール アカウントの作成](../database-mail/create-a-database-mail-account.md)」を参照してください。  
  
  
