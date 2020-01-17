---
title: ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: d4fc71583bf972b2def20d78a69001f00d14966d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065829"
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  データベース スコープ資格情報のプロパティを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>引数  
 *credential_name*  
 変更対象のデータベース スコープ資格情報の名前を指定します。  
  
 IDENTITY **='***identity_name***'**  
 サーバーの外部に接続するときに使用するアカウントの名前を指定します。 Azure Blob Storage からファイルをインポートするには、ID 名が `SHARED ACCESS SIGNATURE` である必要があります。  Shared Access Signature の詳細については、「[Shared Access Signatures (SAS) の使用](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)」をご覧ください。  
    
  
 SECRET **='***secret***'**  
 送信の認証に必要なシークレットを指定します。 "*シークレット*" は、Azure BLOB ストレージからファイルをインポートするために必要です。 "*シークレット*" は、他の目的では省略可能な場合があります。   
> [!WARNING]
>  SAS キー値は '?' (疑問符) で始まることがあります。 SAS キーを使用する場合は、先頭の '?' を削除する必要があります。 そうしないと、作業がブロックされる可能性があります。    
  
## <a name="remarks"></a>Remarks  
 データベース スコープの資格情報が変更されたとき、*identity_name* の値と "*シークレット*" の値は両方ともリセットされます。 SECRET 引数を省略すると、格納されているシークレットの値は NULL に設定されます。  
  
 シークレットはサービス マスター キーを使用して暗号化されます。 サービス マスター キーが再生成された場合、シークレットは新しいサービス マスター キーを使って再暗号化されます。  
  
 データベース スコープの資格情報に関する情報は、[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) カタログ ビューで確認できます。  
  
## <a name="permissions"></a>アクセス許可  
 資格情報に対する `ALTER` 権限が必須です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. データベース スコープ資格情報のパスワードを変更する  
 次の例では、`Saddles` というデータベース スコープの資格情報に格納されているシークレットを変更します。 データベース スコープの資格情報には、Windows ログインが含まれています。`RettigB` とそのパスワードです。 新しいパスワードには、SECRET 句を使用して、データベース スコープの資格情報が追加されます。  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 資格情報からパスワードを削除する  
 次の例では、`Frames` というデータベース スコープ資格情報からパスワードを削除します。 データベース スコープの資格情報には、Windows ログインが含まれています。`Aboulrus8` とパスワードです。 ステートメントを実行すると、SECRET オプションが指定されていないので、データベース スコープ資格情報のパスワードは NULL になります。  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [資格情報 &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [データベース スコープの資格情報の作成 (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [データベース スコープの資格情報の削除 (Transact-SQL)](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
