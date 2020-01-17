---
title: データベース エンジン アクセスのファイル システム アクセス許可の構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- file system permissions
- service account [SQL Server], file system permissions
- permissions [SQL Server], file system
ms.assetid: 78bba43c-4edb-4216-84ac-d6246ae5546d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a42a4a17a1eee9222318e2b508b28d190361d85e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012782"
---
# <a name="configure-file-system-permissions-for-database-engine-access"></a>データベース エンジン アクセスのファイル システム権限の構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]にデータベース ファイルの格納場所へのファイル システム アクセス権を付与する方法について説明します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスには、データベース ファイルが格納されているファイル フォルダーにアクセスするための Windows ファイル システム権限が必要です。 既定の場所への権限は、セットアップ中に構成されます。 別の場所にデータベース ファイルを配置した場合は、次の手順に従って、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] にその場所へのフル コントロール権限を付与する必要がある場合があります。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、権限は各サービスのサービスごとの SID に割り当てられます。 このシステムはサービスの分離と多層防御を提供するのに役立ちます。 サービスごとの SID はサービス名から取得され、各サービスに固有です。 トピック「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 」にはサービスごとの SID についての記載があり、「 **Windows の特権および権限**」で名前が指定されています。 サービスごとの SID に対して、ファイルの場所へのアクセス権を割り当てる必要があります。  
  
## <a name="to-grant-file-system-permission-to-the-per-service-sid"></a>サービスごとの SID にファイル システム権限を付与するには  
  
1.  エクスプローラーを使用して、データベース ファイルが格納されているファイル システムの場所に移動します。 ファイル システム フォルダーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[セキュリティ]** タブで **[編集]** をクリックし、 **[追加]** をクリックします。  
  
3.  **[ユーザー、コンピューター、サービス アカウント、またはグループの選択]** ダイアログ ボックスで、場所の一覧の上部にある **[場所]** をクリックし、コンピューター名を選択して、 **[OK]** をクリックします。  
  
4.  **[選択するオブジェクト名を入力してください]** ボックスに、オンライン ブックのトピック「 [**Windows サービス アカウントと権限の構成**](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」に記載されているサービスごとの SID の名前を入力します。 ( [!INCLUDE[ssDE](../../includes/ssde-md.md)] のサービスごとの SID の名前の場合、既定のインスタンスには **NT SERVICE\MSSQLSERVER** 、指定のインスタンスには **NT SERVICE\MSSQL$InstanceName** を使用します。)  
  
5.  **[名前の確認]** をクリックして、このエントリを検証します。 (検証に失敗した場合、名前が見つからないと示されることがあります。 **[OK]** をクリックすると、 **[複数の名前が見つかりました]** ダイアログ ボックスが表示されます。 ここで、サービスごとの SID の名前として **MSSQLSERVER** または **NT SERVICE\MSSQL$InstanceName**を選択し、 **[OK]** をクリックします。  **[OK]** を再度クリックして、 **[権限]** ダイアログ ボックスに戻ります。)   
6.  **[グループまたはユーザー名]** ボックスで、サービスごとの SID を選択します。 **[\<名前> のアクセス許可]** ボックスで、 **[フル コントロール]** の **[許可]** チェック ボックスをオンにします。  
  
7. **[適用]** をクリックし、 **[OK]** を 2 回クリックして終了します。  
  
## <a name="see-also"></a>参照  
 [データベース エンジン サービスの管理](../../database-engine/configure-windows/manage-the-database-engine-services.md)   
 [システム データベースの移動](../../relational-databases/databases/move-system-databases.md)   
 [ユーザー データベースの移動](../../relational-databases/databases/move-user-databases.md)  
  
  
