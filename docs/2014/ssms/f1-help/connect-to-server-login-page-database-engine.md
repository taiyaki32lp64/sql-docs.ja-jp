---
title: '[サーバーへの接続] ([ログイン] ページ) (データベース エンジン) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2fe246a1f8baf1ab9f60ab1fa73e21e81c052aa1
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153700"
---
# <a name="connect-to-server-login-page-database-engine"></a>[サーバーへの接続] ([ログイン] ページ) (データベース エンジン)
  このタブを使用すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]に接続するときのオプションを表示または指定できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証で接続するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証モードと Windows 認証モードで構成する必要があります。 認証モードの決定方法と認証モードの変更方法の詳細については、「[サーバーの認証モードの変更](../../database-engine/configure-windows/change-server-authentication-mode.md)」を参照してください。  
  
## <a name="options"></a>および  
 **サーバーの種類**  
 オブジェクト エクスプローラーからサーバーを登録するときに、接続するサーバーの種類 ( [!INCLUDE[ssDE](../../includes/ssde-md.md)]、Analysis Services、Reporting Services、または Integration Services) を選択します。 ダイアログ ボックスのその他の領域には、選択したサーバーの種類に該当するオプションだけが表示されます。 [登録済みサーバー] を使用してサーバーを登録する場合、 **[サーバーの種類]** ボックスは読み取り専用になり、[登録済みサーバー] コンポーネントに表示されているサーバーの種類と一致する値が表示されます。 別の種類のサーバーを登録するには、新しいサーバーの登録を開始する前に、[登録済みサーバー] ツール バーの [ [!INCLUDE[ssDE](../../includes/ssde-md.md)]]、[Analysis Services]、[Reporting Services]、または [Integration Services] を選択します。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] を通じて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンのインスタンスに接続する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用し、 **[サーバーへの接続]** ダイアログ ボックスの **[接続プロパティ]** タブでデータベースを指定する必要があります。 **[暗号化接続]** チェック ボックスがオンになっていることを確認してください。  
  
 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は **master**に接続されます。 ユーザー データベースを指定すると、オブジェクト エクスプローラーにそのデータベースとそのオブジェクトのみが表示されます。 **master**に接続すると、すべてのデータベースを表示できるようになります。 詳細については、「 [Azure SQL Database の概要](/azure/sql-database/sql-database-technical-overview)」を参照してください。  
  
 **サーバー名**  
 接続するサーバー インスタンスを選択します。 既定では、最後に接続していたサーバー インスタンスが表示されます。  
  
 **\[認証]**  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続する際には、2 つの認証モードのいずれかを選択します。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] を通じて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンのインスタンスに接続する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用し、 **[サーバーへの接続]** ダイアログ ボックスの **[接続プロパティ]** タブでデータベースを指定する必要があります。 **[暗号化接続]** チェック ボックスがオンになっていることを確認してください。  
  
 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は **master**に接続されます。 ユーザー データベースを指定すると、オブジェクト エクスプローラーにそのデータベースとそのオブジェクトのみが表示されます。 **master**に接続すると、すべてのデータベースを表示できるようになります。 詳細については、「 [Azure SQL Database の概要](/azure/sql-database/sql-database-technical-overview)」を参照してください。  
  
 **Windows 認証モード ([Windows 認証])**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証モードを使用すると、ユーザーは Windows ユーザー アカウントを使用して接続できます。  
  
 **SQL Server 認証 (SQL Server Authentication)**  
 指定されたログイン名とパスワードを使用して、信頼関係の低い接続から接続した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで認証を行います。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログイン アカウントが設定されていない場合、認証は失敗し、エラー メッセージが返されます。  
  
> [!IMPORTANT]  
>  可能な場合は、Windows 認証を使用します。  
  
 **ユーザー名**  
 接続に使用するユーザー名を入力します。 このオプションは、Windows 認証を使用した接続を選択した場合のみ使用できます。  
  
 **Login**  
 接続に使用するログインを入力します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続が指定されている場合にのみ使用できます。  
  
 **Password**  
 ログインのパスワードを入力します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合のみ編集できます。  
  
 **[パスワードを保存する]**  
 入力したパスワードを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に記憶させるには、このチェック ボックスをオンにします。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合だけ表示されます。  
  
 **Connect**  
 クリックすると、上記で選択したサーバーに接続します。  
  
 **[オプション]**  
 クリックすると、ダイアログ ボックスが切り替わり、パスワードの保存などの追加のサーバー接続オプションが非表示になります。  
  
  
