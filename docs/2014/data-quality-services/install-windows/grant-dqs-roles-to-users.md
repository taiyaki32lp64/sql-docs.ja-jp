---
title: ユーザーに DQS ロールを付与する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: afb445b5-bdbe-4bfe-844f-344766cdc2b2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6c5c6cf2953de3b23e55cf75b0287750a4abbb86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480567"
---
# <a name="grant-dqs-roles-to-users"></a>ユーザーに DQS ロールを付与する
  このトピックでは、Windows プリンシパルに基づいて SQL ログインを作成し、DQS_MAIN データベースで [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) ロールを付与する方法を説明します。  
  
## <a name="prerequisites"></a>前提条件  
  
-   DQSInstaller.exe ファイルを実行して [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のインストールを完了しておく必要があります。 詳細については、「 [Data Quality Server のインストールを完了するための DQSInstaller.exe の実行](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)」を参照してください。  
  
-   SQL ログインを作成し、DQS ロールを付与するには、Windows ユーザー アカウントが適切な固定サーバー ロール (securityadmin、serveradmin、sysadmin など) のメンバーであることが必要です。  
  
### <a name="to-create-sql-login-and-grant-dqs-roles"></a>SQL ログインを作成し、DQS ロールを付与するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動します。  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、SQL Server インスタンスを展開し、 **[セキュリティ]** を展開します。  
  
3.  **[セキュリティ]** フォルダーを右クリックし、 **[新規作成]** をポイントして、 **[ログイン]** をクリックします。  
  
4.  **[ログイン - 新規作成]** ダイアログ ボックスの **[ログイン名]** ボックスで Windows ユーザーの名前を指定し、認証の種類として **[Windows 認証]** を指定し、 **[検索]** をクリックしてユーザーを検証します。  
  
5.  ユーザーの検証後、左ペインの **[ユーザー マッピング]** ページをクリックします。  
  
6.  右側のウィンドウで、下のチェック ボックスを選択します、**マップ**の列、 **DQS_MAIN**データベースを選び、 **dqs_administrator**、 **dqs_kb_editor ロール。** 、または**dqs_kb_operator**  チェック ボックス、**データベース ロールのメンバーシップ。DQS_MAIN**ウィンドウで、ユーザーのために必要なアクセス レベルによって異なります。 3 つの DQS ロールの詳細については、「 [DQS のセキュリティ](../dqs-security.md)」を参照してください。  
  
7.  **[ログイン - 新規作成]** ダイアログ ボックスで、 **[OK]** をクリックして変更を適用します。  
  
    > [!NOTE]  
    >  **dqs_administrator** ロールをユーザーに付与し、変更を適用してから、ユーザー権限を再びオンにすると、その他の 2 つの DQS ロールのチェック ボックス ( **[dq_kb_editor]** および **[dqs_kb_operator]** ) もオンになります。  
  
## <a name="next-steps"></a>次の手順  
 先ほど SQL ログインを作成し、DQS ロールを付与した Windows ユーザー アカウントを使用して [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] へのログオンを試みます。  
  
## <a name="see-also"></a>参照  
 [Data Quality Services のインストール](install-data-quality-services.md)   
 [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  
