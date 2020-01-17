---
title: ALTER ENDPOINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER ENDPOINT
- ALTER_ENDPOINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ENDPOINT statement
- modifying endpoints
- endpoints [SQL Server], modifying
ms.assetid: 70f35566-30cf-47c6-8394-dfe5d71629d3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0b07cc17344e27d82155ceaae8e55494deb0bd57
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065668"
---
# <a name="alter-endpoint-transact-sql"></a>ALTER ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  既存のエンドポイントを、次の方法で変更できるようにします。  
  
-   新しいメソッドを既存のエンドポイントに追加する。  
  
-   既存のメソッドを変更するか、またはエンドポイントから削除する。  
  
-   エンドポイントのプロパティを変更する。  
  
> [!NOTE]  
>  このトピックでは、ALTER ENDPOINT に固有の構文および引数について説明します。 CREATE ENDPOINT と ALTER ENDPOINT の両方に共通する引数の説明については、「[CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)」を参照してください。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] からは、ネイティブ XML Web サービス (SOAP/HTTP エンドポイント) は削除されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER ENDPOINT endPointName [ AUTHORIZATION login ]  
[ STATE = { STARTED | STOPPED | DISABLED } ]  
[ AS { TCP } ( <protocol_specific_items> ) ]  
[ FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING } (  
   <language_specific_items>  
        ) ]  
  
<AS TCP_protocol_specific_arguments> ::=  
AS TCP (  
  LISTENER_PORT = listenerPort  
  [ [ , ] LISTENER_IP = ALL | ( 4-part-ip ) | ( "ip_address_v6" ) ]  
)  
<FOR SERVICE_BROKER_language_specific_arguments> ::=  
FOR SERVICE_BROKER (  
   [ AUTHENTICATION = {   
      WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]  
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
   ]  
  
  [ , MESSAGE_FORWARDING = {ENABLED | DISABLED} ]  
  [ , MESSAGE_FORWARD_SIZE = forwardSize  
)  
  
<FOR DATABASE_MIRRORING_language_specific_arguments> ::=  
FOR DATABASE_MIRRORING (  
   [ AUTHENTICATION = {   
      WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]  
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
    ]   
   [ , ] ROLE = { WITNESS | PARTNER | ALL }  
)  
  
```  
  
## <a name="arguments"></a>引数  
  
> [!NOTE]  
>  次の引数は、ALTER ENDPOINT に固有の引数です。 その他の引数の説明については、「[CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)」を参照してください。  
  
 **AS** { **TCP** }  
 **ALTER ENDPOINT** ではトランスポート プロトコルを変更できません。  
  
 **AUTHORIZATION** *login*  
 **ALTER ENDPOINT** では **AUTHORIZATION** オプションを使用できません。 エンドポイントの作成時にのみ所有者を割り当てることができます。  
  
 **FOR** { **TSQL** | **SERVICE_BROKER** | **DATABASE_MIRRORING** }  
 **ALTER ENDPOINT** ではペイロードの種類を変更できません。  
  
## <a name="remarks"></a>Remarks  
 ALTER ENDPOINT を使用する場合、更新するパラメーターのみを指定します。 既存のエンドポイントのすべてのプロパティは、明示的に変更しない限り変更されません。  
  
 ENDPOINT DDL ステートメントは、ユーザー トランザクション内部では実行できません。  
  
 エンドポイントに対して使用する暗号化アルゴリズムの選択については、「[暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)」を参照してください。  
  
> [!NOTE]  
>  RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のバージョンでは、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を暗号化解除できます。  
>   
>  RC4 は比較的弱いアルゴリズムで、AES は比較的強いアルゴリズムです。 しかし、AES は RC4 に比べて非常に処理が遅くなります。 速度よりもセキュリティを優先する場合は、AES を使用することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 固定サーバー ロール **sysadmin** のメンバーであるか、そのエンドポイントの所有者であるか、または ALTER ANY ENDPOINT 権限が許可されている必要があります。  
  
 既存のエンドポイントの所有権を変更するには、ALTER AUTHORIZATION ステートメントを使用する必要があります。 詳細については、「[ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)」を参照してください。  
  
 詳細については、「 [GRANT (エンドポイントの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DROP ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
