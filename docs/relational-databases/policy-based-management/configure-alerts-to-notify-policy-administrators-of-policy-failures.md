---
title: 管理者にポリシー エラーを通知する警告の構成
description: SQL Server のポリシー評価でエラーが出たとき、ポリシー管理者に通知する警告を構成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1562a1799e442292d61857d4598da69b4c11c70f
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557819"
---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>ポリシー管理者にポリシー エラーを通知する警告の構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
-   実行するアクションに電子メール メッセージの送信が含まれる場合は、メール アカウントを構成する必要があります。 データベース メールを使用することをお勧めします。 データベース メールをセットアップする方法の詳細については、「 [データベース メール アカウントの作成](../../relational-databases/database-mail/create-a-database-mail-account.md)」を参照してください。  
  
  
