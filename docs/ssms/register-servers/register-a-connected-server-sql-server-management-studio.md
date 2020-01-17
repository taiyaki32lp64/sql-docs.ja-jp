---
title: 接続済みのサーバーの登録 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], register connected servers
- connected server registrations [SQL Server]
ms.assetid: 77deb5f5-0f80-484f-8b8b-29afa67ec18f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 24751639dcd0484bb31f1783ca936dddd3e9240c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68256303"
---
# <a name="register-a-connected-server-sql-server-management-studio"></a>接続済みのサーバーの登録 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) を使用して、接続されたサーバーを登録する方法について説明します。 サーバーを登録することによって、頻繁にアクセスするサーバーの接続情報を保存しておくことができます。 サーバーの登録は、接続する前か、またはオブジェクト エクスプローラーから接続するときに実行できます。  メニューから **[表示]** \\ **[登録済みサーバー]** に移動して、SSMS で登録済みサーバーを表示することができます。
  
 **このトピックの内容**  
  
-   **サーバーを登録する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-register-a-connected-server"></a>接続済みのサーバーを登録するには  
  
オブジェクト エクスプローラーで、接続済みのサーバーを右クリックし、 **[登録]** をクリックします。
  
**サーバー名**  
このフィールドには、既定で接続先のサーバー名が設定されます。  必要に応じて、サーバー名を入力することも、ドロップ ダウン リストからいずれかを選択することもできます。

**[認証]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続する際には、2 つの認証モードのいずれかを選択します。 

-    **[Windows 認証]**  
Windows 認証モードを使用すると、ユーザーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザー アカウントを使用して接続できます。 

-    **SQL Server 認証 (SQL Server Authentication)**    
指定されたログイン名とパスワードを使用して、信頼関係の低い接続から接続した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで認証を行います。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログイン アカウントが設定されていない場合、認証は失敗し、エラー メッセージが返されます。

     > [!IMPORTANT]  
     > [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] 詳細については、「 [認証モードの選択](../../relational-databases/security/choose-an-authentication-mode.md)」を参照してください。  

     -    **User name**  
接続に使用されている、現在のユーザー名を表示します。 この読み取り専用オプションは、Windows 認証を使用した接続が指定されている場合にのみ使用できます。 **[ユーザー名]** を変更するには、別のユーザーとしてコンピューターにログインします。 

     -    **Login**  
接続に使用するログインを入力します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合にのみ使用できます。  

     -    **パスワード**  
ログインのパスワードを入力します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合にのみ編集できます。 

     -    **[パスワードを保存する]**  
入力したパスワードを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で暗号化して保存する場合に選択します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合にのみ表示されます。  

          > [!NOTE]  
          > パスワードの保存を止めるには、このチェック ボックスをオフにして **[保存]** をクリックします。  

**[登録済みサーバーの名前]**  
[登録済みサーバー] に表示する名前です。 この名前は、 **[サーバー名]** ボックスの名前と一致する必要はありません。  
  
**[登録済みサーバーの説明]**  
サーバーの説明をオプションで入力します。  
  
**テスト**  
クリックすると、 **[サーバー名]** で選択されたサーバーへの接続をテストします。  
  
**[保存]**  
クリックすると、登録済みサーバーの設定を保存します。 

## <a name="see-also"></a>参照  
[新しい登録済みサーバーの作成 (SQL Server Management Studio)](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)
  
  
