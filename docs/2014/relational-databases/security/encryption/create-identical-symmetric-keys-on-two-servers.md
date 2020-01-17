---
title: 2 台のサーバーでの同じ対称キーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- symmetric keys [SQL Server], creating
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 1ff075880833be8179697cb4047babee67cfe61e
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957230"
---
# <a name="create-identical-symmetric-keys-on-two-servers"></a>2 台のサーバーでの同じ対称キーの作成
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] を使用して [!INCLUDE[tsql](../../../includes/tsql-md.md)]で 2 台のサーバーに同じ対称キーを作成する方法について説明します。 暗号化テキストの暗号化を解除するには、暗号化に使用したキーが必要です。 1 つのデータベースで暗号化と暗号化解除の両方が行われる場合、データベースに格納されているキーを、権限に応じて暗号化と暗号化解除の両方に使用できます。 一方、暗号化と暗号化解除が別々のデータベースまたは別々のサーバーで行われる場合、一方のデータベースに格納されているキーを他方のデータベースで使用することはできません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [保護](#Security)  
  
-   [Transact-sql を使用して2つの異なるサーバーに同一の対称キーを作成するには](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Restrictions"></a>制限事項と制約事項  
  
-   対称キーを作成するときには、証明書、パスワード、対称キー、非対称キー、PROVIDER のうち少なくとも 1 つを使用して対称キーを暗号化する必要があります。 キーには種類ごとの暗号化を複数指定できます。 つまり、1 つの対称キーを、複数の証明書、パスワード、対称キー、および非対称キーを使用して同時に暗号化できます。  
  
-   データベースのマスター キーの公開キーではなく、パスワードを使用して対称キーを暗号化する場合は、TRIPLE DES 暗号化アルゴリズムが使用されます。 このため、AES など、強力な暗号化アルゴリズムで作成されたキーでも、キー自身はそれより弱いアルゴリズムで保護されます。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 データベースに対する ALTER ANY SYMMETRIC KEY 権限が必要です。 AUTHORIZATION を指定する場合は、データベース ユーザーに対する IMPERSONATE 権限、またはアプリケーション ロールに対する ALTER 権限が必要です。 証明書または非対称キーを使用して暗号化する場合は、証明書または非対称キーに対する VIEW DEFINITION 権限が必要です。 対称キーを所有できるのは、Windows ログイン、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン、およびアプリケーション ロールだけです。 グループとロールは対称キーを所有できません。  
  
##  <a name="TsqlProcedure"></a>Transact-sql の使用  
  
#### <a name="to-create-identical-symmetric-keys-on-two-different-servers"></a>2 台のサーバーに同じ対称キーを作成するには  
  
1.  
  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  
  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の CREATE MASTER KEY、CREATE CERTIFICATE、および CREATE SYMMETRIC KEY ステートメントを実行して、キーを作成します。  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'My p@55w0Rd';  
    GO  
    CREATE CERTIFICATE [cert_keyProtection] WITH SUBJECT = 'Key Protection';  
    GO  
    CREATE SYMMETRIC KEY [key_DataShare] WITH  
        KEY_SOURCE = 'My key generation bits. This is a shared secret!',  
        ALGORITHM = AES_256,   
        IDENTITY_VALUE = 'Key Identity generation bits. Also a shared secret'  
        ENCRYPTION BY CERTIFICATE [cert_keyProtection];  
    GO  
    ```  
  
4.  別のサーバー インスタンスに接続し、別のクエリ ウィンドウを開き、前述の SQL ステートメントを実行して、そのサーバーに同じキーを作成します。  
  
5.  最初のサーバーで次の OPEN SYMMETRIC KEY ステートメントと SELECT ステートメントを実行して、キーをテストします。  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6.  他方のサーバーで、上の SELECT ステートメントの結果を次のコードの `@blob` 値として貼り付け、次のコードを実行して、このキーで暗号化テキストの暗号化を解除できることを確認します。  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7.  両方のサーバーで対称キーを終了します。  
  
    ```  
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  
  
 詳細については、次のトピックを参照してください。  
  
-   [CREATE MASTER KEY &#40;Transact-sql&#41;](/sql/t-sql/statements/create-master-key-transact-sql)  
  
-   [Transact-sql&#41;&#40;証明書の作成](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-sql&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)  
  
-   [ENCRYPTBYKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [DECRYPTBYKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/decryptbykey-transact-sql)  
  
-   [オープン対称キー &#40;Transact-sql&#41;](/sql/t-sql/statements/open-symmetric-key-transact-sql)  
  
  
