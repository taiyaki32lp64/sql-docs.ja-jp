---
title: SQL Server 変更データベースの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraIns
ms.assetid: 4f79c24a-e99a-4a06-8637-51eeec406259
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f53fe9d295fdd5cd34c6391332af12b9f6788668
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294764"
---
# <a name="create-the-sql-server-change-database"></a>SQL Server 変更データベースの作成

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  新しいインスタンス ウィザードを起動すると、[CDC データベースの作成] ページが表示されます。 [CDC データベースの作成] ページを使用して、新しい CDC インスタンスに関する情報を提供し、新しい変更データベースを作成します。  
  
 作成した新しい CDC データベースは、SQL Server CDC に対して有効になります。このように有効にするには、ログインが `sysadmin` 固定サーバー ロールのメンバーである必要があります。  
  
 Oracle CDC インスタンスの作成ウィザードを開始したユーザーが `sysadmin` 固定サーバー ロールのメンバーではない場合、[SQL Server への接続] ダイアログ ボックスが表示され、SQL Server CDC に対してデータベースを有効にするタスクを実行するために sysadmin ロールのメンバーの資格情報を入力するよう求められます。 CDC データベースが作成されると、 `sysadmin` ログインは破棄され、Oracle デザイナー コンソールが入力されたときに使用された元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインで作業が再開されます。  
  
> [!IMPORTANT]  
>  SQL Server CDC に対してデータベースを有効にするタスク以外のタスクでは、新しいインスタンス ウィザードの実行に使用された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに、 `dbcreator` 固定サーバー ロールと、MSXDBCDC データベースに対する UPDATE 権限が含まれている必要があります。  
  
 [SQL Server への接続] ダイアログ ボックスへのデータの入力については、「 [SQL Server Connection for Instance Creation](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **[Oracle CDC インスタンス]**  
 作成する CDC インスタンスに関する次の情報を入力します。  
  
-   **[名前]** :新しいサービスの名前を入力します。 この名前は、新しい変更データベースの名前にもなります。  
  
-   **説明**:新しいインスタンスを識別するのに役立つ説明を入力します。 これは省略可能です。  
  
 **[SQL Server 変更データベース]**  
 このセクションは、データベースの作成に使用されます。  
  
1.  **[データベースの変更]** : 新しい変更データベースの名前です。 データベースの名前は、インスタンスに指定した名前と同じです。 この読み取り専用フィールドには、データベースへの完全なパスが表示されます。  
  
2.  **[データベースの作成]** : データベースを作成するには、 **[データベースの作成]** をクリックします。  
  
     データベースを作成するには、ログインに `sysasmin` サーバー ロールが必要です。 詳細については、上記のセキュリティに関する注意を参照してください。  
  
     データベースを作成したら、 **[次へ]** をクリックして「 [Connect to an Oracle Source Database](../../integration-services/change-data-capture/connect-to-an-oracle-source-database.md)」に進みます。  
  
## <a name="see-also"></a>参照  
 [SQL Server 変更データベース インスタンスを作成する方法](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Oracle CDC Service](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
  
