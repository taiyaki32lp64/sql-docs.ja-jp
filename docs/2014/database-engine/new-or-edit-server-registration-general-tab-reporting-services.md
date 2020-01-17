---
title: 新しいサーバーの登録 ([全般] タブ) (Reporting Services) を編集または |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerserver.general.reportserver.f1
ms.assetid: 5f899a8e-52ef-46b5-b7a9-f200ccd9f724
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0e6d6d3ad57726c42556c9ecc2662edce102e57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62844278"
---
# <a name="new-or-edit-server-registration-general-tab-reporting-services"></a>[新規サーバーの登録] または [サーバー登録プロパティの編集] ([全般] タブ) (Reporting Services)
  このタブを使用すると、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]のインスタンスを登録するときのオプションを指定できます。  
  
 このページにアクセスするには、[登録済みサーバー] で、 **[登録済みサーバー]** ツール バーの **[Reporting Services]** をクリックし、登録済みサーバー グループ ( **[Reporting Services]** など) を右クリックして、 **[新規作成]** をポイントし、 **[サーバーの登録]** をクリックします。  
  
## <a name="options"></a>および  
 **サーバーの種類**  
 [登録済みサーバー] を使用してサーバーを登録する場合、 **[サーバーの種類]** ボックスは読み取り専用になり、 **[登録済みサーバー]** ペインに表示されているサーバーの種類と一致する値が表示されます。 別の種類のサーバーを登録するには、 **[登録済みサーバー]** ツール バーで目的のサーバーをクリックした後で、新しいサーバーの登録を開始します。  
  
 **サーバー名**  
 接続先のレポート サーバー インスタンスを指定します。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]では、インスタンス名を使用してレポート サーバーにアクセスできます。 インストールする各 SQL Server インスタンスに対して、1 つのレポート サーバー インスタンスを使用できます。 既定のインスタンスを使用する場合は、SQL Server インスタンスの名前を入力します。 名前付きのインスタンスを使用する場合は、レポート サーバーに接続するための名前付きインスタンスを MSSQL$InstanceName の形式で指定します。  
  
 **[認証]**  
 レポート サーバーへの認証は、インターネット インフォメーション サービス (IIS) によって実行されます。 Reporting Services に接続する際に、次のいずれかの認証モードを選択します。  
  
 **Windows 認証モード ([Windows 認証])**  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 資格情報を使用して、レポート サーバー インスタンスに接続します。  
  
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
  
> [!NOTE]  
>  パスワードの保存を止めるには、このチェック ボックスをオフにして **[保存]** をクリックします。  
  
 **[登録済みサーバーの名前]**  
 [登録済みサーバー] に表示する名前です。 この名前は、 **[サーバー名]** ボックスの名前と同じである必要はありません。  
  
 **[登録済みサーバーの説明]**  
 サーバーの説明をオプションで入力します。  
  
 **テスト**  
 クリックすると、 **[サーバー名]** で選択されたサーバーへの接続をテストします。  
  
 **[保存]**  
 クリックすると、登録済みサーバーの設定を保存します。  
  
  
