---
title: ALTER CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER CREDENTIAL
- ALTER_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], credentials
- credentials [SQL Server], ALTER CREDENTIAL statement
- modifying credentials
- authentication [SQL Server], credentials
- ALTER CREDENTIAL statement
ms.assetid: b08899a6-c09e-4af4-91aa-a978ada79264
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: f6ac23553500fbf3092d9450b6f5a222863dc1dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065921"
---
# <a name="alter-credential-transact-sql"></a>ALTER CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  資格情報のプロパティを変更します。  

> [!IMPORTANT]
> ベスト プラクティスとしての "行うべき" 情報です。タスクを完了するための "行う必要がある" 情報 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>引数  
 *credential_name*  
 変更する資格情報の名前を指定します。  
  
 IDENTITY **='***identity_name***'**  
 サーバーの外部に接続するときに使用するアカウントの名前を指定します。  
  
 SECRET **='***secret***'**  
 送信の認証に必要なシークレットを指定します。 *シークレット* は省略可能です。
  
> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Key Vault と Shared Access Signature の ID のみです。 Windows ユーザー ID はサポートされません。
  
## <a name="remarks"></a>Remarks  
 資格情報が変更されたとき、両方の値 *identity_name* と *シークレット* がリセットされます。 SECRET 引数を省略すると、格納されているシークレットの値は NULL に設定されます。  
  
 シークレットはサービス マスター キーを使用して暗号化されます。 サービス マスター キーが再生成された場合、シークレットは新しいサービス マスター キーを使って再暗号化されます。  
  
 資格情報に関する情報は、**sys.credentials** カタログ ビューで確認できます。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY CREDENTIAL 権限が必要です。 資格情報がシステム資格情報の場合は、CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-password-of-a-credential"></a>A. 資格情報のパスワードを変更する  
 次の例では、`Saddles` という資格情報に格納されているシークレットを変更します。 資格情報には、Windows ログイン `RettigB` とそのパスワードが含まれています。 新しいパスワードは、SECRET 句を使って資格情報に追加されます。  
  
```  
ALTER CREDENTIAL Saddles WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 資格情報からパスワードを削除する  
 次の例では、`Frames` という資格情報からパスワードを削除します。 資格情報には、Windows ログイン `Aboulrus8` とパスワードが含まれています。 SECRET オプションを指定しないので、ステートメントを実行した後、資格情報のパスワードは NULL になります。  
  
```  
ALTER CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [資格情報 &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
