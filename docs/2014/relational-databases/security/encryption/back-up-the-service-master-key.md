---
title: サービス マスター キーのバックアップ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], exporting
ms.assetid: f60b917c-6408-48be-b911-f93b05796904
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: c6e67b2eacfd428bc296596699ff65939789d1e8
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957276"
---
# <a name="back-up-the-service-master-key"></a>サービス マスター キーのバックアップ
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用してサービス マスター キーをバックアップする方法について説明します。 サービス マスター キーは、暗号化階層のルートになります。 サービス マスター キーは、バックアップして安全な別の場所に保存してください。 このバックアップの作成は、サーバー管理操作の最初の段階で実行します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [保護](#Security)  
  
-   [サービスマスターキーをバックアップするには](#Procedure)  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Restrictions"></a>制限事項と制約事項  
  
-   マスター キーは開かれている必要があります。したがって、バックアップ前に暗号化を解除する必要があります。 サービス マスター キーで暗号化されている場合は、マスター キーを明示的に開く必要はありません。ただし、マスター キーがパスワードのみで暗号化されている場合は、明示的に開く必要があります。  
  
-   マスター キーは作成後すぐにバックアップし、安全な別の場所に保存することをお勧めします。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 データベースに対する CONTROL 権限が必要です。  
  
##  <a name="Procedure"></a>Transact-sql の使用  
  
#### <a name="to-back-up-the-service-master-key"></a>サービス マスター キーをバックアップするには  
  
1.  
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、バックアップするサービス マスター キーが格納されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続します。  
  
2.  バックアップ メディアでサービス マスター キーの暗号化に使用するパスワードを指定します。 このパスワードに対しては、複雑性がチェックされます。 詳細については、「 [Password Policy](../password-policy.md)」をご参照ください。  
  
3.  バックアップしたキーのコピーを保存するためにリムーバブル バックアップ メディアを用意します。  
  
4.  キーのバックアップを作成する NTFS ディレクトリを指定します。 このディレクトリは、次の手順で指定するファイルの作成先となります。 このディレクトリは、制限の厳しいアクセス制御リスト (ACL) で保護する必要があります。  
  
5.  
  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
6.  
  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
7.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Creates a backup of the "AdventureWorks2012" master key.  
    -- Because this master key is not encrypted by the service master key, a password must be specified when it is opened.  
    USE AdventureWorks2012;  
    GO  
    BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_ key'   
        ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    >  キーのファイル パスとキーのパスワード (存在する場合) は、実際は上に示したものと異なります。 両方がサーバーとキーのセットアップで固有であることを確認してください。  
  
8.  ファイルをバックアップ メディアにコピーして、コピーしたファイルを確認します。  
  
9. バックアップを安全な場所に保存します。  
  
 詳細については、「[OPEN MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-master-key-transact-sql)」と「[BACKUP MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql)」を参照してください。  
  
  
