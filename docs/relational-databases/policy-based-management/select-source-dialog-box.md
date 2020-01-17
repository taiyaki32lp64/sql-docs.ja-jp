---
title: '[ソースの選択] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.selectsource.f1
ms.assetid: d664c2e5-dd0c-4da8-b27d-aa4ee4fc0ffd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dc505c0fe87a298ba4a9015f467119c1b7d6d3f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021724"
---
# <a name="select-source-dialog-box"></a>[ソースの選択] ダイアログ ボックス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このダイアログ ボックスを使用すると、実行するポリシーのソースを選択できます。 ポリシーを含む 1 つ以上の XML ファイルを選択するには、 **[ファイル]** を選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス上にあるポリシーを実行するには、 **[サーバー]** を選択します。  
  
 このダイアログ ボックスは、複数の方法で開くことができます。  
  
 **このダイアログ ボックスを開くには**  
  
-   [登録済みサーバー] で、 **[ローカル サーバー グループ]** を右クリックするか、 **[ローカル サーバー グループ]** または **[中央管理サーバー]** の下にあるサーバーを右クリックして、 **[ポリシーの評価]** をクリックします。 **[ポリシーの評価]** ダイアログ ボックスの **[ポリシーの選択]** ページで、参照ボタン ( **[...]** ) をクリックします。  
  
-   オブジェクト エクスプローラーで、 **[管理]** 、 **[ポリシー管理]** の順に展開し、 **[ポリシー]** を右クリックして **[ポリシーのインポート]** をクリックします。 **[インポート]** ダイアログ ボックスで、参照ボタン ( **[...]** ) をクリックします。  
  
-   オブジェクト エクスプローラーで、サーバー、データベース、またはデータベース オブジェクトを右クリックし、 **[ポリシー]** 、 **[評価]** の順にクリックします。 **[ポリシーの評価]** ダイアログ ボックスの **[ポリシーの選択]** ページで、参照ボタン ( **[...]** ) をクリックします。  
  
## <a name="options"></a>オプション  
 **[ファイル]**  
 ポリシーを含む 1 つ以上の XML ファイルを選択します。  
  
 **[サーバー]**  
 実行するポリシーを含むサーバーを選択できるようにします。  
  
 **サーバーの種類**  
 ポリシーを含んでいるのは [!INCLUDE[ssDE](../../includes/ssde-md.md)] サーバーだけです。 このボックスは読み取り専用です。  
  
 **サーバー名**  
 接続するサーバー インスタンスを選択します。 既定では、最後に接続していたサーバー インスタンスが表示されます。  
  
 **[認証]**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続する際には、2 つの認証モードのいずれかを選択します。  
  
 **Windows 認証モード ([Windows 認証])**  
 Windows 認証モードを使用すると、ユーザーは Windows ユーザー アカウントを使用して接続できます。  
  
 **SQL Server 認証 (SQL Server Authentication)**  
 指定されたログイン名とパスワードを使用して、信頼関係の低い接続から接続した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで認証を行います。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログイン アカウントが設定されていない場合、認証は失敗し、エラー メッセージが返されます。  
  
> [!IMPORTANT]  
>  可能な場合は、Windows 認証を使用します。  
  
 **User name**  
 接続に使用するユーザー名を入力します。 このオプションは、Windows 認証を使用した接続を選択した場合にのみ使用できます。  
  
 **Login**  
 接続に使用するログインを入力します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合にのみ使用できます。  
  
 **パスワード**  
 ログインのパスワードを入力します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合にのみ編集できます。  
  
## <a name="see-also"></a>参照  
 [[ポリシー管理] ノード &#40;オブジェクト エクスプローラー&#41;](../../relational-databases/policy-based-management/policy-management-node-object-explorer.md)   
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
