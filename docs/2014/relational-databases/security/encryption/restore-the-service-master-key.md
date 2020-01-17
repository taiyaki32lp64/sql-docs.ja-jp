---
title: サービス マスター キーの復元 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], importing
- service master key [SQL Server], restoring
ms.assetid: 14bdbbbe-d384-4692-b670-4243d2466fe1
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 21abdf4e5781f179c8168ff02aa611bd7dffd39f
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957175"
---
# <a name="restore-the-service-master-key"></a>サービス マスター キーの復元
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] を使用して [!INCLUDE[tsql](../../../includes/tsql-md.md)]でサービス マスター キーを復元する方法について説明します。  
  
> [!WARNING]  
>  サービス マスター キーの復元が必要になることはほとんどありません。 サービス マスター キーを復元する必要が生じた場合は、十分注意して作業を行ってください。 詳細については、「 [Back Up the Service Master Key](service-master-key.md)」をご覧ください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [保護](#Security)  
  
-   [Transact-sql を使用してサービスマスターキーを復元するには](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Restrictions"></a>制限事項と制約事項  
  
-   サービス マスター キーを復元するとき、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、現在のサービス マスター キーで暗号化されているすべてのキーとシークレットの暗号化が解除され、次にそれらがバックアップ ファイルから読み込まれたサービス マスター キーで暗号化されます。  
  
-   暗号化解除が 1 つでも失敗した場合、復元は失敗します。 FORCE オプションを使用するとエラーを無視できますが、暗号化を解除できないデータが失われる可能性があります。  
  
-   暗号化階層の再生成操作はリソースを大量に消費するため、 リソース要求が少ないときに実行するように考慮してください。  
  
> [!CAUTION]  
>  サービス マスター キーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 暗号化階層のルートになります。 サービス マスター キーでは、直接または間接的に、そのツリー内の他のすべてのキーが保護されます。 強制復元で、依存関係のあるキーの暗号化を解除できなかった場合、そのキーで保護されているデータは失われます。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 サーバーに対する CONTROL SERVER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a>Transact-sql の使用  
  
#### <a name="to-restore-the-service-master-key"></a>サービス マスター キーを復元するには  
  
1.  バックアップしたサービス マスター キーのコピーを、物理バックアップ メディアまたはローカル ファイル システム上のディレクトリから取得します。  
  
2.  
  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
3.  
  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
4.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Restores the service master key from a backup file.  
    RESTORE SERVICE MASTER KEY   
        FROM FILE = 'c:\temp_backups\keys\service_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    >  キーのファイル パスとキーのパスワード (存在する場合) は、実際は上に示したものと異なります。 両方がサーバーとキーのセットアップで固有であることをご確認ください。  
  
  
