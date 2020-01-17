---
title: サービス マスター キーのバックアップ | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], exporting
ms.assetid: f60b917c-6408-48be-b911-f93b05796904
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 1fa730e1143516df2fe5f14c04afcbb9292ac67f
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957486"
---
# <a name="back-up-the-service-master-key"></a>サービス マスター キーのバックアップ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  この記事では、[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用してサービス マスター キーをバックアップする方法について説明します。 サービス マスター キーは、暗号化階層のルートになります。 サービス マスター キーは、バックアップして安全な別の場所に保存してください。 このバックアップの作成は、サーバー管理操作の最初の段階で実行します。  

## <a name="before-you-begin"></a>はじめに  
  
### <a name="limitations-and-restrictions"></a>制限事項と制約事項  

- マスター キーは開かれている必要があります。したがって、バックアップ前に暗号化を解除する必要があります。 サービス マスター キーで暗号化されている場合は、マスター キーを明示的に開く必要はありません。ただし、マスター キーがパスワードのみで暗号化されている場合は、明示的に開く必要があります。  
  
- マスター キーは作成後すぐにバックアップし、安全な別の場所に保存することをお勧めします。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可
データベースに対する CONTROL 権限が必要です。  
  
## <a name="using-transact-sql"></a>Transact-SQL の使用  
  
### <a name="to-back-up-the-service-master-key"></a>サービス マスター キーをバックアップするには
  
1. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、バックアップするサービス マスター キーが格納されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続します。  
  
2. バックアップ メディアでサービス マスター キーの暗号化に使用するパスワードを指定します。 このパスワードに対しては、複雑性がチェックされます。 詳細については、「 [Password Policy](../../../relational-databases/security/password-policy.md)」をご参照ください。  
  
3. バックアップしたキーのコピーを保存するためにリムーバブル バックアップ メディアを用意します。  
  
4. キーのバックアップを作成する NTFS ディレクトリを指定します。 このディレクトリは、次の手順で指定するファイルの作成先となります。 このディレクトリは、制限の厳しいアクセス制御リスト (ACL) で保護する必要があります。  
  
5. **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
6. [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
7. 次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql
    -- Creates a backup of the service master key.
    USE master;
    GO
    BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_ key'
        ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';
    GO
    ```  
  
    > [!NOTE]  
    > キーのファイル パスとキーのパスワード (存在する場合) は、実際は上に示したものと異なります。 両方がサーバーとキーのセットアップで固有であることを確認してください。
  
8. ファイルをバックアップ メディアにコピーして、コピーしたファイルを確認します。  
  
9. バックアップを安全な場所に保存します。  

 詳細については、「[OPEN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-master-key-transact-sql.md)」と「[BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-master-key-transact-sql.md)」を参照してください。  
