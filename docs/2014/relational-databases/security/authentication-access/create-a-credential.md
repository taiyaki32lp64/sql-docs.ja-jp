---
title: 資格情報の作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- credentials [SQL Server], creating
- authentication [SQL Server], credentials
- logins [SQL Server], credentials
ms.assetid: c1e77e91-2a69-40d9-b8b3-97cffc710586
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ab0560e0df37c80a82017e5f076af969931a79e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63012004"
---
# <a name="create-a-credential"></a>資格情報の作成
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、資格情報を作成する方法について説明します。  
  
 資格情報によって、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証ユーザーは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外部の ID を持つことができます。 これは、主に EXTERNAL_ACCESS 権限セットを使用してアセンブリのコードを実行するために使用されます。 また、バックアップを格納するファイルの場所などのドメイン リソースに、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証ユーザーがアクセスする必要がある場合にも、資格情報が使用されます。  
  
 資格情報は、複数の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインに同時にマップできます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインは、一度に 1 つの資格情報にのみマップできます。 資格情報を作成したら、 **[ログインのプロパティ]\([全般] ページ)** を使用してログインを資格情報にマップします。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **資格情報を作成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   ログインにマップされたプロバイダーの資格情報がない場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントにマップされた資格情報が使用されます。  
  
-   それぞれが異なるプロバイダーで使用される資格情報であれば、1 つのログインに複数の資格情報をマップできます。 マップされた資格情報は、各ログインで各プロバイダーにつき 1 つだけ存在する必要があります。 同じ資格情報を他のログインにマップすることはできます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 資格情報の作成や変更には、ALTER ANY CREDENTIAL 権限が必要です。資格情報にログインをマップするには、ALTER ANY LOGIN 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-credential"></a>資格情報を作成するには  
  
1.  オブジェクト エクスプローラーで、 **[セキュリティ]** フォルダーを展開します。  
  
2.  **[資格情報]** フォルダーを右クリックし、 **[新しい資格情報...]** をクリックします。  
  
3.  **[新しい資格情報]** ダイアログ ボックスで、 **[資格情報名]** ボックスに資格情報の名前を入力します。  
  
4.  **[ID]** ボックスに、送信用の接続に使用するアカウントの名前を入力します ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のコンテキストが適用されない場合)。 通常、これは Windows ユーザー アカウントですが、ID を別の種類のアカウントにすることができます。  
  
     または、省略記号 **[...]** をクリックして **[ユーザーまたはグループの選択]** ダイアログ ボックスを開きます。  
  
5.  **[パスワード]** ボックスと **[パスワードの確認入力]** ボックスに、 **[ID]** ボックスに指定したアカウントのパスワードを入力します。 **[ID]** ボックスの値が Windows ユーザー アカウントである場合は、Windows パスワードを入力します。 パスワードが不要である場合は、 **[パスワード]** ボックスを空にできます。  
  
6.  **[暗号化サービス プロバイダーの使用]** をクリックし、拡張キー管理 (EKM) プロバイダーによって確認される資格情報を設定します。 詳細については、「[拡張キー管理 &#40;EKM&#41;](../encryption/extensible-key-management-ekm.md)」を参照してください。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
###  <a name="Credential"></a> 資格情報を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Creates the credential called "AlterEgo.".   
    -- The credential contains the Windows user "Mary5" and a password.  
    CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
        SECRET = '<EnterStrongPasswordHere>';  
    GO  
    ```  
  
 詳細については、「[CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)」を参照してください。  
  
  
