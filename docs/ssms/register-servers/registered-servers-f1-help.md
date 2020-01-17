---
title: '[登録済みサーバー] の F1 ヘルプ | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], Help
- Registered Servers [SQL Server], help
- SQL Server Management Studio Help [SQL Server], registered servers
ms.assetid: 59f76b28-ba78-4a1a-b5d5-8b581f30114d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cf08f76b0df0b3624aa1450b2463599b31fb85fa
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266142"
---
# <a name="registered-servers-f1-help"></a>[登録済みサーバー] の F1 ヘルプ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  ここでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の [登録済みサーバー] コンポーネントの F1 ヘルプについて説明します。 さまざまなオプションについて説明します。
  
 登録済みサーバーの詳細および登録済みサーバーの処理方法へのリンクについては、「 [登録済みサーバー](../../tools/sql-server-management-studio/register-servers.md) 」をご覧ください。 
 

 クリックすると、[登録済みサーバー] の設定を保存します。 
 
 ## <a name="reporting-services-new-or-edit-server-registration-general-tab"></a>Reporting Services の [新規サーバーの登録] または [サーバー登録プロパティの編集] ([全般] タブ) 
  このタブを使用すると、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]のインスタンスを登録するときのオプションを指定できます。  
  
 このページにアクセスするには、[登録済みサーバー] で、 **[登録済みサーバー]** ツール バーの **[Reporting Services]** をクリックし、登録済みサーバー グループ ( **[Reporting Services]** など) を右クリックして、 **[新規作成]** をポイントし、 **[サーバーの登録]** をクリックします。  
  
### <a name="options"></a>および  
 **サーバーの種類**  
 [登録済みサーバー] を使用してサーバーを登録する場合、 **[サーバーの種類]** ボックスは読み取り専用になり、 **[登録済みサーバー]** ペインに表示されているサーバーの種類と一致する値が表示されます。 別の種類のサーバーを登録するには、 **[登録済みサーバー]** ツール バーで目的のサーバーをクリックした後で、新しいサーバーの登録を開始します。  
  
 **サーバー名**  
 接続先のレポート サーバー インスタンスを指定します。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]では、インスタンス名を使用してレポート サーバーにアクセスできます。 インストールする各 SQL Server インスタンスに対して、1 つのレポート サーバー インスタンスを使用できます。 既定のインスタンスを使用する場合は、SQL Server インスタンスの名前を入力します。 名前付きのインスタンスを使用する場合は、レポート サーバーに接続するための名前付きインスタンスを MSSQL$InstanceName の形式で指定します。  
  
 **[認証]**  
 レポート サーバーへの認証は、インターネット インフォメーション サービス (IIS) によって実行されます。 Reporting Services に接続する際に、次のいずれかの認証モードを選択します。  
  
 **Windows 認証モード ([Windows 認証])**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 資格情報を使用して、レポート サーバー インスタンスに接続します。  
  
 **基本認証**  
 Reporting Services をインストールしたときに、基本認証を使用するように構成している場合は、 **基本認証** を使用して接続します。  
  
 **フォーム認証**  
 Reporting Services をインストールしたときに、カスタム認証拡張機能を使用するように構成している場合は、 **フォーム認証** を使用して接続します。  
  
 **[ユーザー名]**  
 接続に使用するログイン名を入力します。 このオプションは、 **[基本認証]** または **[フォーム認証]** を選択した場合にのみ使用できます。  
  
 **Password**  
 ユーザー名に対応するパスワードを入力します。 このオプションは、 **[基本認証]** または **[フォーム認証]** を選択した場合にのみ編集できます。  
  
 **[パスワードを保存する]**  
 入力したパスワードを保存します。 このオプションは、 **[基本認証]** または **[フォーム認証]** をクリックした場合にのみ使用できます。  
  
> **注:** パスワードの保存を止めるには、このチェック ボックスをオフにして **[保存]** をクリックします。  
  
 **[登録済みサーバーの名前]**  
 [登録済みサーバー] に表示する名前です。 この名前は、 **[サーバー名]** ボックスの名前と同じである必要はありません。  
  
 **[登録済みサーバーの説明]**  
 サーバーの説明をオプションで入力します。  
  
 **テスト**  
 クリックすると、 **[サーバー名]** で選択されたサーバーへの接続をテストします。  
  
 
 ## <a name="analysis-services---multidimensional-data-new-or-edit-server-registration-general-tab"></a>Analysis Services - 多次元データの [新規サーバーの登録] または [サーバー登録プロパティの編集] ([全般] タブ)
 
  このタブを使用すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスを登録するときのオプションを指定できます。  
  
 このページにアクセスするには、[登録済みサーバー] で、[登録済みサーバー] ツール バーの **[Analysis Services]** をクリックし、 **Analysis Services**などの登録済みサーバー グループを右クリックして、 **[新規作成]** をポイントし、 **[サーバーの登録]** をクリックします。  
  
### <a name="options"></a>および  
 **サーバーの種類**  
 [登録済みサーバー] を使用してサーバーを登録する場合、 **[サーバーの種類]** ボックスは読み取り専用になり、[登録済みサーバー] ペインに表示されているサーバーの種類と一致する値が表示されます。 別の種類のサーバーを登録するには、 **[登録済みサーバー]** ツール バーで目的のサーバーをクリックした後で、新しいサーバーの登録を開始します。  
  
 **サーバー名**  
 接続するサーバー インスタンスを選択します。 既定では、最後に接続していたサーバー インスタンスが表示されます。  
  
 **[認証]**  
 Windows 認証では、ユーザーが、各自の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 資格情報を使用し、Windows ユーザーまたは Windows グループのメンバーとして接続することができます。  
  
 **User name**  
 このオプションは、このリリースでは使用できません。  
  
 **Password**  
 このオプションは、このリリースでは使用できません。  
  
 **[パスワードを保存する]**  
 このオプションは、このリリースでは使用できません。  
  
 **[登録済みサーバーの名前]**  
 [登録済みサーバー] に表示する名前です。 この名前は、 **[サーバー名]** ボックスの名前と一致する必要はありません。  
  
 **[登録済みサーバーの説明]**  
 サーバーの説明をオプションで入力します。  
  
 **テスト**  
 クリックすると、 **[サーバー名]** で選択されたサーバーへの接続をテストします。 
 
 ## <a name="ssis-new-or-edit-server-registration-general-tab"></a>SSIS の [新規サーバーの登録] または [サーバー登録プロパティの編集] ([全般] タブ) 
 
 このタブを使用すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を登録するときのオプションを指定できます。  
  
 このページにアクセスするには、[登録済みサーバー] で、 **[登録済みサーバー]** ツール バーの **[Integration Services]** をクリックし、登録済みサーバー グループを右クリックして、 **[新規作成]** をポイントし、 **[サーバーの登録]** をクリックします。  
  
### <a name="options"></a>および  
 **サーバーの種類**  
 [登録済みサーバー] でサーバーを登録する場合は、 **[サーバーの種類]** ボックスは読み取り専用になっており、そのサーバーは [登録済みサーバー] に表示されるサーバーの種類に一致します。 別の種類のサーバーを登録するには、新しいサーバーの登録を開始する前に、 **[登録済みサーバー]** , **[データベース エンジン]** , **[分析サーバー]** , **[Reporting Services]** 、 **[SQL Server Compact]** **[Edition]** 、または **[Integration Services]** をクリックします。  
  
 **サーバー名**  
 接続先のサーバーを選択します。 既定では、最後に接続していたサーバーが表示されます。  
  
 **[認証]**  
 Windows 認証モードを使用すると、ユーザーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザー アカウントを使用して接続できます。  
  
 **User name**  
 このオプションは、このリリースでは使用できません。  
  
 **Password**  
 このオプションは、このリリースでは使用できません。  
  
 **[パスワードを保存する]**  
 このオプションは、このリリースでは使用できません。  
  
 **[登録済みサーバーの名前]**  
 **[登録済みサーバー]** に表示する名前です。 この名前は、 **[サーバー名]** ボックスの名前と一致する必要はありません。  
  
 **[登録済みサーバーの説明]**  
 サーバーの説明をオプションで入力します。  
  
 **テスト**  
 クリックすると、 **[サーバー名]** で選択されたサーバーへの接続をテストします。 
  

 
 
  
