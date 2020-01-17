---
title: 複数のサーバーに対するステートメントの同時実行 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- executing queries against multiple servers
- queries [SQL Server], multiserver
ms.assetid: 197760f3-0a06-43de-8162-69c27d3fbe56
author: markingmyname
ms.author: maghan
ms.openlocfilehash: abf087363c4e4cc17356882322643b6fae0da553
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260580"
---
# <a name="execute-statements-against-multiple-servers-simultaneously"></a>複数のサーバーに対するステートメントの同時実行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]で複数のサーバーに対してクエリを同時に実行する方法について説明します。これを行うには、ローカル サーバー グループ、または 1 つの中央管理サーバーと 1 つ以上のサーバー グループ、およびグループ内の 1 つ以上の登録済みサーバーを作成し、このグループ全体に対してクエリを実行します。 
  
クエリから返された結果は、結合して 1 つの結果ペインに表示するか、別々の結果ペインに表示することができます。 結果セットには、サーバー名を表示する列と、各サーバーに対するクエリで使用されたログインを表示する列を追加できます。 中央管理サーバーおよび従属サーバーは、Windows 認証を使用しないと登録できません。 ローカル サーバー グループ内のサーバーは、Windows 認証または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して登録できます。  
  
> **注:** 次の手順を実行する前に、中央管理サーバーとサーバー グループを作成する必要があります。 詳細については、「[中央管理サーバーとサーバー グループの作成 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)」を参照してください。  

  
##  <a name="Permissions"></a> Permissions  
 中央管理サーバーによって保持される接続は、ユーザーのコンテキスト内で Windows 認証を使用して実行されるため、登録済みサーバーでの有効な権限が変わることがあります。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A のインスタンスでは sysadmin 固定サーバー ロールのメンバーであるユーザーでも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B のインスタンスでは権限が限られていることがあります。  
  
 ## <a name="execute-statements-against-multiple-configuration-targets-simultaneously"></a>複数の構成対象に対してステートメントを同時に実行する  

1.  SQL Server Management Studio では、 **[表示]** メニューで **[登録済みサーバー]** をクリックします。  
  
2.  中央管理サーバーを展開して、サーバー グループを右クリックし、 **[接続]** をポイントして、 **[新しいクエリ]** をクリックします。  
  
3.  クエリ エディターで、次のような [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを入力して実行します。  
  
    ```  
    USE master  
    GO  
    SELECT * FROM sysdatabases;  
    GO  
    ```  
  
     既定では、サーバー グループ内のすべてのサーバーからのクエリ結果が結合されて結果ペインに表示されます。  
  
#### <a name="to-change-the-multiserver-results-options"></a>マルチサーバーの結果オプションを変更するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で、 **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  **[クエリ結果]** 、 **[SQL Server]** の順に展開し、 **[マルチサーバーの結果]** をクリックします。  
  
3.  **[マルチサーバーの結果]** ページで、使用するオプション設定を指定し、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [中央管理サーバーを使用した複数のサーバーの管理](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
