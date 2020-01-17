---
title: 暗号化された列のデータをレプリケートする (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], replicating data
- encryption [SQL Server replication]
- publishing [SQL Server replication], encrypted columns
ms.assetid: d1f8f586-e5a3-4a71-9391-11198d42bfa3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97fd1ef113ec76a00394da298f1def188168a37d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62955845"
---
# <a name="replicate-data-in-encrypted-columns-sql-server-management-studio"></a>暗号化された列のデータをレプリケートする (SQL Server Management Studio)
  レプリケーションでは、暗号化された列データをパブリッシュできます。 このデータの暗号化を解除してサブスクライバーで使用するには、パブリッシャーでのデータの暗号化に使用されたキーがサブスクライバーにも存在する必要があります。 レプリケーションでは、暗号化キーを送信する安全なメカニズムは提供されません。 このため、暗号化キーはサブスクライバーで手動で再作成する必要があります。 このトピックでは、パブリッシャーで列を暗号化し、暗号化キーをサブスクライバーで使用できるようにする方法について説明します。  
  
 基本的な手順は次のとおりです。  
  
1.  パブリッシャーで対称キーを作成します。  
  
2.  その対称キーを使用して列データを暗号化します。  
  
3.  暗号化された列を含むテーブルをパブリッシュします。  
  
4.  パブリケーションにサブスクライブします。  
  
5.  サブスクリプションを初期化します。  
  
6.  手順 1 と同じ値を ALGORITHM、KEY_SOURCE、IDENTITY_VALUE に使用して、サブスクライバーで対称キーを再作成します。  
  
7.  暗号化された列データにアクセスします。  
  
> [!NOTE]  
>  列データを暗号化するには、対称キーを使用する必要があります。 対称キー自体は、パブリッシャーとサブスクライバーで、それぞれ異なる手段で保護できます。  
  
### <a name="to-create-and-replicate-encrypted-column-data"></a>暗号化された列データを作成およびレプリケートするには  
  
1.  パブリッシャーで、 [CREATE SYMMETRIC KEY](/sql/t-sql/statements/create-symmetric-key-transact-sql)を実行します。  
  
    > [!IMPORTANT]  
    >  KEY_SOURCE の値は、対象キーの再作成およびデータの暗号化解除に使用できる重要なデータです。 KEY_SOURCE は、常に安全に格納および送信する必要があります。  
  
2.  [OPEN SYMMETRIC KEY](/sql/t-sql/statements/open-symmetric-key-transact-sql) を実行して新しいキーを開きます。  
  
3.  [EncryptByKey](/sql/t-sql/functions/encryptbykey-transact-sql) 関数を使用して、パブリッシャーで列データを暗号化します。  
  
4.  [CLOSE SYMMETRIC KEY](/sql/t-sql/statements/close-symmetric-key-transact-sql) を実行してキーを閉じます。  
  
5.  暗号化された列を含むテーブルをパブリッシュします。 詳細については、「 [Create a Publication](../publish/create-a-publication.md)」を参照してください。  
  
6.  パブリケーションにサブスクライブします。 詳細については、「[プル サブスクリプションの作成](../create-a-pull-subscription.md)」または「[プッシュ サブスクリプションの作成](../create-a-push-subscription.md)」を参照してください。  
  
7.  サブスクリプションを初期化します。 詳しくは、「 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
8.  手順 1 と同じ値を ALGORITHM、KEY_SOURCE、および IDENTITY_VALUE に使用して、サブスクライバーで [CREATE SYMMETRIC KEY](/sql/t-sql/statements/create-symmetric-key-transact-sql) を実行します。 ENCRYPTION BY には別の値を指定することもできます。  
  
    > [!IMPORTANT]  
    >  KEY_SOURCE の値は、対象キーの再作成およびデータの暗号化解除に使用できる重要なデータです。 KEY_SOURCE は、常に安全に格納および送信する必要があります。  
  
9. [OPEN SYMMETRIC KEY](/sql/t-sql/statements/open-symmetric-key-transact-sql) を実行して新しいキーを開きます。  
  
10. [DecryptByKey](/sql/t-sql/functions/decryptbykey-transact-sql) 関数を使用して、サブスクライバーでレプリケートされたデータを暗号解除します。  
  
11. [CLOSE SYMMETRIC KEY](/sql/t-sql/statements/close-symmetric-key-transact-sql) を実行してキーを閉じます。  
  
## <a name="example"></a>例  
 この例では、対称キー、対称キーを保護するために使用される証明書、およびマスター キーを作成しています。 これらのキーは、パブリケーション データベースで作成されます。 これらは、 `SalesOrderHeader` テーブル内の暗号化された列 (EncryptedCreditCardApprovalCode) の作成に使用されます。 この列は、暗号化していない CreditCardApprovalCode 列の代わりに、AdvWorksSalesOrdersMerge パブリケーションでパブリッシュされます。 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
 [!code-sql[HowTo#sp_PublishEncryptedColumn](../../../snippets/tsql/SQL15/replication/howto/tsql/publishencryptedcolumn.sql#sp_publishencryptedcolumn)]  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
## <a name="example"></a>例  
 この例では、最初の例の ALGORITHM、KEY_SOURCE、および IDENTITY_VALUE の場合と同じ値を使用して、サブスクリプション データベース内に同じ対象キーを再作成しています。 この例は、暗号化された列をレプリケートする AdvWorksSalesOrdersMerge パブリケーションへのサブスクリプションが初期化済みであることを前提としています。 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を保存する必要がある場合は、格納時および送信時の不正アクセスからファイルを保護する必要があります。  
  
 [!code-sql[HowTo#sp_SubscriberEncryptedColumn](../../../snippets/tsql/SQL15/replication/howto/tsql/subscriberencryptedcolumn.sql#sp_subscriberencryptedcolumn)]  
  
## <a name="see-also"></a>参照  
 [SQL Server レプリケーションのセキュリティ](view-and-modify-replication-security-settings.md)   
 [2 台のサーバーでの同じ対称キーの作成](../../security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
