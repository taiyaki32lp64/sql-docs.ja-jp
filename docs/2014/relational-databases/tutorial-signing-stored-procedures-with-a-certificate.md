---
title: チュートリアル:証明書を使用したストアド プロシージャの署名 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- signing stored procedures tutorial [SQL Server]
ms.assetid: a4b0f23b-bdc8-425f-b0b9-e0621894f47e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: daf80492cd6a0d8040d1497e71600c798e7ef96c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62524095"
---
# <a name="tutorial-signing-stored-procedures-with-a-certificate"></a>チュートリアル:証明書を使用したストアド プロシージャへの署名
  このチュートリアルでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]で生成された証明書を使用してストアド プロシージャに署名する方法について説明します。  
  
> [!NOTE]  
>  このチュートリアルのコードを実行するには、混合モードのセキュリティが構成されていることと、 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースがインストールされていることが条件となります。 シナリオ  
  
 証明書を使用したストアド プロシージャへの署名は、ストアド プロシージャに権限を設定する一方、ユーザーにはこのような権限を明示的に与えないでおこうとする場合に便利です。 この動作は EXECUTE AS ステートメントを使用するなどの方法でも実現できますが、証明書を使用すると、トレースによってプロシージャの最初の呼び出し元を見つけることができ、 高いレベルの監査を行うことができます。特に、セキュリティやデータ定義言語 (DDL) の操作に対しては有効です。  
  
 master データベースに証明書を作成し、サーバーレベルの権限を付与するか、任意のユーザー データベースに証明書を作成し、データベースレベルの権限を付与することができます。 このシナリオでは、ベース テーブルに対する権限を持たないユーザーが [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースにアクセスする必要があることを想定し、また、オブジェクト アクセスの記録を監査します。 ここでは所有権を継承する方法を使用するのではなく、サーバーおよびデータベース ユーザー アカウントを 1 つとデータベース ユーザー アカウントを 1 つ作成し、前者のアカウントにはベース オブジェクトに対する権限を与えず、後者にはテーブルとストアド プロシージャに対する権限を与えます。 ストアド プロシージャと 2 番目のデータベース ユーザー アカウントは両方とも、証明書によりセキュリティ保護されます。 2 番目のデータベース アカウントではすべてのオブジェクトにアクセスでき、ストアド プロシージャへのアクセス許可を最初のデータベース ユーザー アカウントに与えることができます。  
  
 このシナリオでは、最初にデータベース証明書、ストアド プロシージャ、ユーザーを 1 つずつ作成し、次にプロセスをテストします。手順は次のとおりです。  
  
1.  環境を構成する。  
  
2.  証明書を作成する。  
  
3.  ストアド プロシージャを作成し、証明書を使用して署名する。  
  
4.  証明書を使用して証明書アカウントを作成する。  
  
5.  証明書アカウントにデータベース権限を与える。  
  
6.  アクセス コンテキストを表示する。  
  
7.  環境をリセットする。  
  
 以下で、この例の各コード ブロックについて説明します。 完全なサンプル コードをコピーするには、このチュートリアルの最後の「 [完全なサンプル コード](#CompleteExample) 」を参照してください。  
  
## <a name="1-configure-the-environment"></a>1.環境を構成する  
 この例の初期コンテキストを設定するには、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] で新しいクエリを開き、次のコードを実行して [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースを開きます。 このコードにより、データベース コンテキストが `AdventureWorks2012` に変更され、新しいサーバー ログインとデータベース ユーザー アカウント (`TestCreditRatingUser`) が作成されます。ログインにはパスワードが設定されます。  
  
```  
USE AdventureWorks2012;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
```  
  
 CREATE USER ステートメントの詳細については、[「CREATE USER (Transact-SQL)」](/sql/t-sql/statements/create-user-transact-sql) を参照してください。 CREATE LOGIN ステートメントの詳細については、[「CREATE LOGIN (Transact-SQL)」](/sql/t-sql/statements/create-login-transact-sql) を参照してください。  
  
## <a name="2-create-a-certificate"></a>2.証明書を作成する  
 コンテキストの master データベース、またはユーザー データベース、あるいはその両方を使用して、サーバー内に証明書を作成できます。 証明書をセキュリティ保護するには複数のオプションがあります。 証明書の詳細については、[「CREATE CERTIFICATE (Transact-SQL)」](/sql/t-sql/statements/create-certificate-transact-sql) を参照してください。  
  
 次のコードを実行し、データベース証明書をパスワードの保護付きで作成します。  
  
```  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2014';  
GO  
```  
  
## <a name="3-create-and-sign-a-stored-procedure-using-the-certificate"></a>3.ストアド プロシージャを作成し、証明書を使用して署名する  
 次のコードを実行し、`Vendor` データベース スキーマ内の `Purchasing` テーブルからデータを選択するストアド プロシージャを作成して、信用格付け 1 の会社にアクセスを限定します。 ストアド プロシージャの最初のセクションに、ストアド プロシージャを実行するユーザー アカウントのコンテキストが表示されていますが、これは概念を説明するためだけのものです。 要件を満たすために必要なものではありません。  
  
```  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Show who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1  
END  
GO  
```  
  
 次のコードを実行し、データベース証明書を使用してストアド プロシージャに署名します。このときパスワードも使用します。  
  
```  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
```  
  
 ストアド プロシージャの詳細については、[「ストアド プロシージャ (データベース エンジン)」](stored-procedures/stored-procedures-database-engine.md) を参照してください。  
  
 ストアド プロシージャへの署名の詳細については、[「ADD SIGNATURE (Transact-SQL)」](/sql/t-sql/statements/add-signature-transact-sql) を参照してください。  
  
## <a name="4-create-a-certificate-account-using-the-certificate"></a>4.証明書を使用して証明書アカウントを作成する  
 次のコードを実行し、証明書からデータベース ユーザー (`TestCreditRatingcertificateAccount`) を作成します。 このアカウントにサーバー ログインは与えません。最終的には、このアカウントによって基になるテーブルに対するアクセスが制御されます。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="5-grant-the-certificate-account-database-rights"></a>5.証明書アカウントにデータベース権限を与える  
 次のコードを実行し、ベース テーブルとストアド プロシージャに `TestCreditRatingcertificateAccount` 権限を与えます。  
  
```  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
```  
  
 オブジェクトに対する権限付与の詳細については、[「GRANT (Transact-SQL)」](/sql/t-sql/statements/grant-transact-sql) を参照してください。  
  
## <a name="6-display-the-access-context"></a>6.アクセス コンテキストを表示する  
 ストアド プロシージャへのアクセスに関連する権限を表示するには、次のコードを実行して、ストアド プロシージャの実行権限を `TestCreditRatingUser` ユーザーに与えます。  
  
```  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
```  
  
 その後、次のコードを実行し、サーバーに使用した dbo ログインでストアド プロシージャを実行して、 ユーザー コンテキスト情報の出力を確認します。 この出力では、dbo アカウントはグループ メンバーシップを介してではなく、自身の権限を持つコンテキストとして表示されます。  
  
```  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
 次のコードを実行し、 `EXECUTE AS` ステートメントにより `TestCreditRatingUser` アカウントとなってストアド プロシージャを実行します。 今度は、ユーザー コンテキストが USER MAPPED TO CERTIFICATE コンテキストに設定されていることを確認できます。  
  
```  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
 これは、ストアド プロシージャへの署名により監査が可能になったことを示しています。  
  
> [!NOTE]  
>  データベース内でコンテキストを切り替えるには、EXECUTE AS を使用します。  
  
## <a name="7-reset-the-environment"></a>7.環境をリセットする  
 次のコードを実行して、`REVERT` ステートメントにより現在のアカウントのコンテキストを dbo に戻し、環境をリセットします。  
  
```  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
 REVERT ステートメントの詳細については、「[REVERT (Transact-SQL)](/sql/t-sql/statements/revert-transact-sql)」 を参照してください。  
  
##  <a name="CompleteExample"></a> 完全な例  
 次に、完全なサンプル コードを示します。  
  
```  
/* Step 1 - Open the AdventureWorks2012 database */  
USE AdventureWorks2012;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
  
/* Step 2 - Create a certificate in the AdventureWorks2012 database */  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2014';  
GO  
  
/* Step 3 - Create a stored procedure and  
sign it using the certificate */  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Shows who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token;     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1;  
END  
GO  
  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
  
/* Step 4 - Create a database user for the certificate.   
This user has the ownership chain associated with it. */  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
  
/* Step 5 - Grant the user database rights */  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE  
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
  
/* Step 6 - Test, using the EXECUTE AS statement */  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
  
-- Run the procedure as the dbo user, notice the output for the type  
EXEC TestCreditRatingSP;  
GO  
  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXEC TestCreditRatingSP;  
GO  
  
/* Step 7 - Clean up the example */  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
