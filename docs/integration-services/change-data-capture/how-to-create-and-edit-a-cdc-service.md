---
title: CDC Service を作成および編集する方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1b3d47a5-dc89-482d-bbc7-fff04f194c43
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9df960fa5018ad8f4368c99a91c5aed3fe0aab15
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294788"
---
# <a name="how-to-create-and-edit-a-cdc-service"></a>CDC Service を作成および編集する方法

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  この手順では、CDC Service 構成コンソールから新しい Oracle CDC Service を作成および編集する方法について説明します。  
  
 この手順を実行する Windows ユーザーには、Oracle CDC サービスが構成されているコンピューター上の管理者権限が必要です。  
  
### <a name="to-create-a-new-cdc-service"></a>新しい CDC サービスを作成するには  
  
1.  **[スタート]** メニューの **[CDC Service Configuration for Oracle]** をクリックします。  
  
2.  左側のペインから [ローカルの CDC Service] を右クリックし、[新しいサービス] をクリックします。  
  
     **[アクション]** ペインから **[新しいサービス]** をクリックすることもできます。  
  
3.  [新しい Oracle CDC Service] ダイアログ ボックスに必要な情報を入力します。 [新しい Oracle CDC Service] ダイアログ ボックスに情報を入力する方法については、「 [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) 」を参照してください。  
  
     [新しい Oracle CDC Service] ダイアログ ボックスで指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが、サービスの実行時に Oracle CDC Service によって使用されます。 このログインは、public 固定サーバー ロールのメンバーであることだけが必要です。その他の権限は必要ありません。 新しい Oracle CDC のインスタンスが追加されると、そのログインには、関連付けられている **CDC データベースへの** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクセスが与えられます。  
  
4.  必要な情報の入力が完了したら、 **[OK]** をクリックします。  
  
     Oracle CDC Windows Service の定義を作成するには、プログラムに、関連付けられている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内の MSXDBCDC データベースに対する更新アクセスが必要です。 **[OK]** をクリックすると、MSXDBCDC データベースに対する更新アクセスを持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを入力するためのダイアログ ボックスが表示されます。  
  
     [SQL Server への接続] ダイアログ ボックスに入力するデータについては、「 [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)」を参照してください。  
  
5.  **[OK]** をクリックして、[新しい Oracle CDC Service] ダイアログ ボックスを閉じます。  
  
### <a name="to-edit-a-cdc-service"></a>CDC サービスを編集するには  
  
1.  **[スタート]** メニューの **[CDC Service Configuration for Oracle]** をクリックします。  
  
2.  左側のペインから **[ローカルの CDC Service]** をクリックし、編集するローカル サービスを右クリックし、 **[プロパティ]** をクリックします。  
  
     中央のペインで対象のサービスを選択し、 **[アクション]** ペインから **[プロパティ]** をクリックすることもできます。  
  
3.  [CDC Service のプロパティ] ダイアログ ボックスに必要な情報を入力します。 [CDC Service のプロパティ] ダイアログ ボックスに情報を入力する方法については、「 [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) 」を参照してください。  
  
4.  必要な情報の入力が完了したら、 **[OK]** をクリックします。[SQLServer への接続] ダイアログ ボックスが表示されます。  
  
     MSXDBDCDC データベースに対する書き込み権限を持たないログインが新しい Oracle CDC インスタンスの作成を試みると、エラー メッセージが表示されます。 そのダイアログ ボックスで **[OK]** をクリックします。[SQL Server への接続] ダイアログ ボックスが表示されます。 このダイアログ ボックスには、 **db_owner** データベース ロールなど、MSXDBCDC データベースに対する書き込み権限を持つログインの資格情報を入力する必要があります。  
  
     [SQL Server への接続] ダイアログ ボックスに入力するデータについては、「 [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)」を参照してください。  
  
5.  [Oracle への接続] ダイアログ ボックスで **[OK]** をクリックします。 両方のダイアログ ボックスが閉じ、サービスが更新および登録されます。  
  
## <a name="see-also"></a>参照  
 [Attunity の Change Data Capture Designer for Oracle](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md)  
  
  
