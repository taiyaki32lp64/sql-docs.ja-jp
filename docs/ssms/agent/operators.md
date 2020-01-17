---
title: オペレーター | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- operators (users) [Database Engine]
- fail-safe operator [SQL Server]
- aliases [SQL Server], operators
- SQL Server Agent alerts, operators
- contact information [SQL Server Agent]
- net send [SQL Server]
- e-mail [SQL Server], SQL Server Agent operators
- pager notifications [SQL Server Agent]
- mail [SQL Server], SQL Server Agent operators
- operators (users) [Database Engine], defining
- jobs [SQL Server Agent], operators
- alerts [SQL Server], operators
ms.assetid: 38e8488f-2669-4cea-b9c3-5f394a663678
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c4059bda6f761171292f2977f7d8e6a3f6896451
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260082"
---
# <a name="operators"></a>オペレーター
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

オペレーターとは、ジョブの完了時や警告の発生時に電子通知を受け取ることのできる人またはグループの別名です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスでは、オペレーターを経由した管理者の通知がサポートされています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの通知機能および監視機能はオペレーターが有効にします。  
  
## <a name="operator-attributes-and-concepts"></a>オペレーターの属性と概念  
オペレーターの主な属性は次のとおりです。  
  
-   オペレーター名  
  
-   連絡先情報  
  
### <a name="naming-an-operator"></a>オペレーターの名前付け  
すべてのオペレーターに名前を付ける必要があります。 オペレーター名は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意である必要があります。使用できる文字数は最大 **128** 文字です。  
  
### <a name="contact-information"></a>連絡先情報  
オペレーターの連絡先情報では、オペレーターに通知する方法を定義します。 オペレーターへの通知には、電子メール、ポケットベル、または **net send** コマンドを使用できます。  
  
> [!IMPORTANT]
> [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の今後のバージョンでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントからポケットベル オプションと **net send** オプションが削除される予定です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。  
  
-   **電子メールによる通知**  
  
    電子メールによる通知では、電子メール メッセージがオペレーターに送信されます。 電子メールによる通知を使用するには、オペレーターの電子メール アドレスを指定します。  
  
-   **ポケットベルによる通知**  
  
    ポケットベル機能は、電子メールによって実装されます。 ポケットベルによる通知を使用するには、オペレーターがポケットベルのメッセージを受信する電子メール アドレスを指定します。 ポケットベルによる通知を設定するには、受信メールを処理してポケットベル メッセージに変換するソフトウェアをメール サーバーにインストールする必要があります。 このソフトウェアは、次のいずれかの方法を使用します。  
  
    -   ポケットベル プロバイダーのサイトにあるリモート メール サーバーにメールを転送します。  
  
        必要なソフトウェアは、一般にローカル メール システムの一部として使用できますが、ポケットベル プロバイダーがこのサービスを提供している必要があります。 詳細については、ポケットベルのマニュアルを参照してください。  
  
    -   インターネット経由でポケットベル プロバイダーのサイトにある電子メール サーバーに電子メールをルーティングします。  
  
        これは第 1 の方法の変形です。  
  
    -   接続されているモデムを使用して、着信電子メールを処理し、ポケットベルにダイヤルします。  
  
        このソフトウェアは、ポケットベル サービスのプロバイダーがライセンスを持っています。 このソフトウェアは、ポケットベルの番号として電子メール アドレス情報の全部または一部を解釈するか、変換テーブルで電子メールの名前をポケットベル番号と照合することによって、定期的に受信トレイを処理する電子メール クライアントとして動作します。  
  
        すべてのオペレーターが同じポケットベル プロバイダーを利用している場合は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、ポケットベル電子メール間システムが要求する特別な電子メール書式を指定できます。 この特別な書式は、プレフィックスまたはサフィックスの形式で、電子メールの次の行に含めることができます。  
  
        **Subject:**  
  
        **Cc**:  
  
        **To**:  
  
    > [!NOTE]  
    > 容量の小さい英数字のポケットベル システムを使用している場合は、エラーのテキストをポケットベルの通知から除外することで、送信されるテキストを短縮できます。 容量の小さい英数字のポケットベル システムには、1 ページあたりのバイト数が 64 バイトに制限されているものなどがあります。  
  
-   **net sendnotification**  
  
    この方法では、 **net send** コマンドを使用して、オペレーターにメッセージを送信します。 **net send**では、ネットワーク メッセージの受信者 (コンピューターまたはユーザー) を指定します。  
  
    > [!NOTE]  
    > **net send** コマンドでは、Microsoft Windows Messenger を使用します。 警告を正しく送信するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターと、オペレーターが使用しているコンピューターの両方で、このサービスを実行する必要があります。  
  
## <a name="alerting-and-fail-safe-operators"></a>警告通知先オペレーターと緊急時のオペレーター  
警告に応答して通知を受けるオペレーターを選択できます。 警告のスケジュールを設定して、オペレーターへの通知を順番に割り当てることも可能です。 たとえば、月曜日、水曜日、金曜日に発生した警告は管理者 A に通知し、火曜日、木曜日、土曜日に発生した警告は管理者 B に通知することができます。  
  
緊急時のオペレーターは、指定されているオペレーターに対するすべてのポケットベルによる通知が失敗した後で警告の通知を受けます。 たとえば、ポケットベルによる通知のために 3 人のオペレーターを定義し、そのいずれのオペレーターにもポケットベルで通知できなかった場合、緊急時のオペレーターが通知を受けます。  
  
緊急時のオペレーターは、次の場合に通知を受けます。  
  
-   警告を管理するオペレーターにポケットベルで通知できなかった場合  
  
    プライマリ オペレーターに通知できなかった理由には、ポケットベル アドレスが誤っているか、オペレーターが非番であるなどがあります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが **msdb** データベースのシステム テーブルにアクセスできない場合  
  
    **sysnotifications** システム テーブルは、警告に関してオペレーターが担う責任を指定します。  
  
緊急時のオペレーターは、安全のための機能です。 緊急時の職務を他のオペレーターに割り当て直すか、または緊急時の割り当てを削除しなければ、緊急時の職務に割り当てられたオペレーターを削除することはできません。  
  
## <a name="notifying-an-operator"></a>オペレーターへの通知  
オペレーターに通知するには、次のうち 1 つまたは複数をセットアップする必要があります。  
  
-   データベース メール機能を使用して電子メールを送信するには、SMTP をサポートしている電子メール サーバーにアクセスできる必要があります。  
  
-   ポケットベル通知機能を使用する場合は、サードパーティによるポケットベルとメール間のソフトウェアとハードウェアが必要です。  
  
-   **net send**を使用するには、指定のコンピューターにオペレーターがログオンしており、そのコンピューターで Windows Messenger からのメッセージの受信が許可されている必要があります。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**タスク**|**トピック**|  
|オペレーターの作成に関連するタスク|[オペレーターの作成](../../ssms/agent/create-an-operator.md)<br /><br />[Designate a Fail-Safe Operator](../../ssms/agent/designate-a-fail-safe-operator.md)|  
|警告の割り当てに関連するタスク|[オペレーターへの警告の割り当て](../../ssms/agent/assign-alerts-to-an-operator.md)<br /><br />[警告への応答の定義 (SQL Server Management Studio)](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)<br /><br />[sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)<br /><br />[オペレーターへの警告の割り当て](../../ssms/agent/assign-alerts-to-an-operator.md)|  
  
## <a name="see-also"></a>参照  
[データベース メール](../../relational-databases/database-mail/database-mail.md)  
  
