---
title: SQL Server ユーティリティからの SQL Server のインスタンスの削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.utility.remove.f1
ms.assetid: ae1d126a-46d2-47bf-b339-17c743df6491
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: df13432a0b5f835690dd6371fd935198d7798b40
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783290"
---
# <a name="remove-an-instance-of-sql-server-from-the-sql-server-utility"></a>SQL Server ユーティリティからの SQL Server のインスタンスの削除
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスを削除するには、次の手順を実行します。 この手順では、UCP リスト ビューから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが削除されるため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのデータ収集が停止します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスはアンインストールされません。  
  
> [!IMPORTANT]  
>  この手順を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを削除する前に、削除するインスタンス上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および SQL Server エージェントのサービスが実行されていることを確認します。  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のユーティリティ エクスプローラーで、 **[マネージド インスタンス]** をクリックします。 ユーティリティ エクスプローラーのコンテンツ ウィンドウで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスのリスト ビューを確認します。  
  
2.  リスト ビューの **[SQL Server インスタンス名]** 列で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティから削除する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを選択します。 削除するインスタンスを右クリックし、 **[マネージ インスタンスの削除...]** をクリックします。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに、管理者特権のある資格情報を指定します。これには、 **[接続...]** をクリックし、 **[サーバーへの接続]** ダイアログ ボックスで情報を確認して、 **[接続]** をクリックします。 **[マネージド インスタンスの削除]** ダイアログ ボックスにログイン情報が表示されます。  
  
4.  操作を実行する場合は **[OK]** をクリックします。 操作を終了する場合は **[キャンセル]** をクリックします。  
  
## <a name="manually-remove-a-managed-instance-of-sql-server-from-a-sql-server-utility"></a>SQL Server ユーティリティから SQL Server のマネージド インスタンスを手動で削除する  
 この手順では、UCP リスト ビューから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが削除され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのデータ収集が停止されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスはアンインストールされません。  
  
 PowerShell を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスを削除するには、 このスクリプトで、次の操作を実行します。  
  
-   サーバー インスタンス名で UCP を取得します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティから削除します。  
  
```powershell
# Get Ucp connection  
$UcpServerInstanceName = "ComputerName\InstanceName";  
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $UcpServerInstanceName;  
$UcpConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($UcpConnection);  
  
# Now remove the ManagedInstance from the SQL Server Utility  
$ServerInstanceName = "ComputerName\InstanceName";  
$Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $ServerInstanceName;  
$InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
$ManagedInstance = $Utility.ManagedInstances[$ServerInstanceName];  
$ManagedInstance.Remove($InstanceConnection);  
```  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を正確に参照することが重要です。 大文字と小文字を区別する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの場合、@@SERVERNAME によって返された文字種を正確に使用して、インスタンス名を指定する必要があります。 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のマネージド インスタンスのインスタンス名を取得するには、マネージド インスタンスで次のクエリを実行します。  
  
```sql
select @@SERVERNAME AS instance_name  
```  
  
 この時点で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスは UCP から完全に削除されます。 このインスタンスは、次に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのデータを更新すると、リスト ビューに表示されなくなります。 この状態は、ユーザーが SSMS ユーザー インターフェイスで、マネージド インスタンスの削除操作を正常に完了した場合と同じです。  
  
## <a name="see-also"></a>参照  
 [ユーティリティ エクスプローラーを使用した SQL Server ユーティリティの管理](use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [SQL Server ユーティリティのトラブルシューティング](../../database-engine/troubleshoot-the-sql-server-utility.md)  
