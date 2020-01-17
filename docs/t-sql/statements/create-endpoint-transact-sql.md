---
title: CREATE ENDPOINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENDPOINT
- CREATE ENDPOINT
- ENDPOINT_TSQL
- CREATE_ENDPOINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HTTP SOAP support [SQL Server]
- CREATE ENDPOINT statement
- Availability Groups [SQL Server], configuring
- endpoints [SQL Server], creating
- SOAP [SQL Server built-in support], endpoints
- SOAP [SQL Server built-in support], sqlbatch
- DATABASE_MIRRORING option
- HTTP protocol option [SQL Server]
- SOAP [SQL Server built-in support], ad hoc
- TCP protocol option [SQL Server]
- SERVICE_BROKER option
- Availability Groups [SQL Server], endpoint
ms.assetid: 6405e7ec-0b5b-4afd-9792-1bfa5a2491f6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0a320b01433ad95f4bd695a3f700b7e7bb9ba653
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902832"
---
# <a name="create-endpoint-transact-sql"></a>CREATE ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  エンドポイントを作成し、クライアント アプリケーションで使用可能なメソッドを含む、プロパティを定義します。 関連する権限については、「[GRANT (エンドポイントの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)」を参照してください。  
  
 CREATE ENDPOINT の構文は、論理的に次の 2 つの部分に分かれます。  
  
-   最初の部分は、AS から始まり FOR 句の前までの部分です。  
  
     この部分では、トランスポート プロトコル (TCP) に固有の情報を指定し、エンドポイントの受信ポート番号、エンドポイント認証方法、およびエンドポイントへのアクセスを制限する IP アドレスのリスト (該当する場合) を設定します。  
  
-   2 番目は FOR 句から始まる部分です。  
  
     この部分では、エンドポイントでサポートされているペイロードを定義します。 ペイロードには、サポートされている [!INCLUDE[tsql](../../includes/tsql-md.md)]、Service Broker、データベース ミラーリングのうちのいずれかを指定できます。 ここでは、言語固有の情報も指定できます。  
  
> **注:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] からは、ネイティブ XML Web サービス (SOAP/HTTP エンドポイント) は削除されました。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE ENDPOINT endPointName [ AUTHORIZATION login ]  
[ STATE = { STARTED | STOPPED | DISABLED } ]  
AS { TCP } (  
   <protocol_specific_arguments>  
        )  
FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING } (  
   <language_specific_arguments>  
        )  
  
<AS TCP_protocol_specific_arguments> ::=  
AS TCP (  
  LISTENER_PORT = listenerPort  
  [ [ , ] LISTENER_IP = ALL | ( xx.xx.xx.xx IPv4 address ) | ( '__:__1' IPv6 address ) ]  
  
)  
  
<FOR SERVICE_BROKER_language_specific_arguments> ::=  
FOR SERVICE_BROKER (  
   [ AUTHENTICATION = {   
            WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ [ , ] ENCRYPTION = { DISABLED | { { SUPPORTED | REQUIRED }   
       [ ALGORITHM { AES | RC4 | AES RC4 | RC4 AES } ] }   
   ]  
   [ [ , ] MESSAGE_FORWARDING = { ENABLED | DISABLED } ]  
   [ [ , ] MESSAGE_FORWARD_SIZE = forward_size ]  
)  
  

<FOR DATABASE_MIRRORING_language_specific_arguments> ::=  
FOR DATABASE_MIRRORING (  
   [ AUTHENTICATION = {   
            WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
   [ [ [ , ] ] ENCRYPTION = { DISABLED | { { SUPPORTED | REQUIRED }   
       [ ALGORITHM { AES | RC4 | AES RC4 | RC4 AES } ] }   
  
    ]   
   [ , ] ROLE = { WITNESS | PARTNER | ALL }  
)  
```  
  
## <a name="arguments"></a>引数  
 *endPointName*  
 作成するエンドポイントに割り当てられた名前です。 エンドポイントを更新または削除する場合に使用します。  
  
 AUTHORIZATION *login*  
 新規に作成されたエンドポイント オブジェクトの所有権が割り当てられる有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Windows ログインを指定します。 AUTHORIZATION を指定しない場合、既定により、呼び出し元が新しく作成されたオブジェクトの所有者となります。  
  
 AUTHORIZATION を指定して所有権を割り当てるには、呼び出し元は指定された *login* に対する IMPERSONATE 権限が必要です。  
  
 所有権を再割り当てする場合は、「[ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)」を参照してください。  
  
 STATE **=** { STARTED | **STOPPED** | DISABLED }  
 エンドポイントの作成時点での状態です。 エンドポイントの作成時点での状態を指定しない場合、既定値は STOPPED です。  
  
 STARTED  
 エンドポイントが開始され、接続をアクティブにリッスンしています。  
  
 DISABLED  
 エンドポイントは無効です。 この状態では、サーバーはポートの要求をリッスンしますが、クライアントにはエラーを返します。  
  
 **STOPPED**  
 エンドポイントは停止しています。 この状態の場合、サーバーはエンドポイントのポートをリッスンしておらず、エンドポイントの使用要求にも応答しません。  
  
 状態を変更する場合は、「[ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)」を参照してください。  
  
 AS { TCP }  
 使用するトランスポート プロトコルを指定します。  
  
 FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING }  
 ペイロードの種類を指定します。  
  
 現時点では、`<language_specific_arguments>` パラメーターに渡す [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語固有の引数はありません。  
  
 **TCP プロトコル オプション**  
  
 以下は、TCP プロトコル オプションにのみ適用されます。  
  
 LISTENER_PORT **=** _listenerPort_  
 Service Broker TCP/IP プロトコルによって接続を受信待ちされるポート番号を指定します。 通常は 4022 が使用されますが、1024 ～ 32767 の範囲であればどの番号でも有効です。  
  
 LISTENER_IP **=** ALL | **(** _4-part-ip_ **)**  |  **(** "*ip_address_v6*" **)**  
 エンドポイントが受信待ちする IP アドレスを指定します。 既定値は ALL です。 したがって、リスナーによって任意の有効な IP アドレスでの接続が許可されます。  
  
 完全修飾ドメイン名の代わりに IP アドレスを使用してデータベース ミラーリングを構成する (`ALTER DATABASE SET PARTNER = partner_IP_address` または `ALTER DATABASE SET WITNESS = witness_IP_address`) 場合は、ミラーリング エンドポイントの作成時に `LISTENER_IP=ALL` の代わりに `LISTENER_IP =IP_address` を指定する必要があります。  
  
 **SERVICE_BROKER オプションと DATABASE_MIRRORING オプション**  
  
 以下の AUTHENTICATION 引数と ENCRYPTION 引数は、SERVICE_BROKER オプションと DATABASE_MIRRORING オプションで共通です。  
  
> [!NOTE]  
>  SERVICE_BROKER 固有のオプションについては、後の「SERVICE_BROKER オプション」を参照してください。 DATABASE_MIRRORING 固有のオプションについては、後の「DATABASE_MIRRORING オプション」を参照してください。  
  
 AUTHENTICATION **=** \<authentication_options> このエンドポイントの接続に対する TCP/IP 認証要件を指定します。 既定値は WINDOWS です。  
  
 サポートされている認証方法は NTLM または Kerberos、あるいはその両方です。  
  
> [!IMPORTANT]  
>  1 つのサーバー インスタンス上のすべてのミラーリング接続で、1 つのデータベース ミラーリング エンドポイントが使用されます。 追加のデータベース ミラーリング エンドポイントを作成しようとしても失敗します。  
  
 **\<authentication_options> ::=**  
  
 **WINDOWS** [ { NTLM | KERBEROS | **NEGOTIATE** } ]  
 エンドポイントを認証するために、Windows 認証プロトコルを使用してエンドポイントを接続することを指定します。 これは既定値です。  
  
 1 つの認証方法 (NTLM または KERBEROS) を指定した場合、その方法が常に認証プロトコルとして使用されます。 既定値の NEGOTIATE を指定すると、エンドポイントは Windows ネゴシエーション プロトコルを使用して NTLM か Kerberos のどちらかを選択します。  
  
 CERTIFICATE *certificate_name*  
 エンドポイントが、認証用の ID を設定するために *certificate_name* で指定された証明書を使用して接続を認証することを指定します。 反対側のエンドポイントは、指定された証明書の秘密キーと一致する公開キー付きの証明書を持っている必要があります。  
  
 WINDOWS [ { NTLM | KERBEROS | **NEGOTIATE** } ] CERTIFICATE *certificate_name*  
 エンドポイントが Windows 認証を使用して接続を試み、それが失敗した場合は指定された証明書を使用することを指定します。  
  
 CERTIFICATE *certificate_name* WINDOWS [ { NTLM | KERBEROS | **NEGOTIATE** } ]  
 エンドポイントが、指定された証明書を使用して接続を試行され、それが失敗した場合は Windows 認証が使用されるよう指定します。  
  
 ENCRYPTION = { DISABLED | SUPPORTED | **REQUIRED** } [ALGORITHM { **AES** | RC4 | AES RC4 | RC4 AES } ]  
 プロセスで暗号化を使用するかどうかを指定します。 既定値は REQUIRED です。  
  
 DISABLED  
 接続を経由して送信されたデータが暗号化されないことを指定します。  
  
 SUPPORTED  
 反対側のエンドポイントで SUPPORTED または REQUIRED が指定されている場合に限り、データを暗号化することを指定します。  
  
 REQUIRED  
 このエンドポイントへの接続で暗号化を使用する必要があることを指定します。 したがって、このエンドポイントに接続するには、別のエンドポイントで ENCRYPTION が SUPPORTED または REQUIRED に設定されている必要があります。  
  
 必要に応じて、エンドポイントで使用される暗号化の形式を、ALGORITHM 引数を使用して次のように指定できます。  
  
 **AES**  
 エンドポイントで AES アルゴリズムを使用する必要があることを指定します。 これは [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降の既定値です。  
  
 RC4  
 エンドポイントで RC4 アルゴリズムを使用する必要があることを指定します。 これは [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] までの既定値です。  
  
> [!NOTE]  
>  RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のバージョンでは、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を暗号化解除できます。  
  
 AES RC4  
 2 つのエンドポイントが、AES アルゴリズムを優先するこのエンドポイントと暗号化アルゴリズムについてネゴシエートすることを指定します。  
  
 RC4 AES  
 2 つのエンドポイントで暗号化アルゴリズムをネゴシエートし、このエンドポイントでは RC4 アルゴリズムを優先することを示します。  
  
> [!NOTE]  
>  RC4 アルゴリズムは非推奨とされます。 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] AES を使用することをお勧めします。  
  
 両方のエンドポイントで両方のアルゴリズムを異なる順序で指定した場合、接続を受け入れた方のエンドポイントが優先されます。  
  
 **SERVICE_BROKER オプション**  
  
 以下の引数は SERVICE_BROKER オプションに固有のものです。  
  
 MESSAGE_FORWARDING **=** { ENABLED | **DISABLED** }  
 このエンドポイントで受信された、別の場所にあるサービスのメッセージを転送するかどうかを指定します。  
  
 ENABLED  
 転送アドレスが使用可能であれば、メッセージを転送します。  
  
 DISABLED  
 別の場所にあるサービスのメッセージを破棄します。 これは既定値です。  
  
 MESSAGE_FORWARD_SIZE **=** _forward_size_  
 転送するメッセージを格納する際に使用するエンドポイントに対して割り当てる最大記憶容量を、MB 単位で指定します。  
  
 **DATABASE_MIRRORING オプション**  
  
 以下の引数は DATABASE_MIRRORING オプションに固有のものです。  
  
 ROLE **=** { WITNESS | PARTNER | ALL }  
 エンドポイントによってサポートされるデータベース ミラーリング ロールを指定します。  
  
 WITNESS  
 エンドポイントがミラーリング プロセスにおいてミラーリング監視ロールを実行できるようにします。  
  
> [!NOTE]  
>  [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] の場合は、WITNESS が唯一の使用可能なオプションです。  
  
 PARTNER  
 エンドポイントがミラーリング プロセスにおいてパートナー ロールを実行できるようにします。  
  
 ALL  
 エンドポイントが、ミラーリング プロセスにおいてミラーリング監視およびパートナーの両方のロールを実行できるようにします。  
  
 これらのロールの詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  DATABASE_MIRRORING には既定のポートはありません。  
  
## <a name="remarks"></a>Remarks  
 ENDPOINT DDL ステートメントは、ユーザー トランザクション内では実行できません。 変更対象となるエンドポイントが、アクティブなスナップショット分離レベル トランザクションで使用されている場合でも、ENDPOINT DDL ステートメントは失敗しません。  
  
 ENDPOINT に対する要求は、次のユーザーが実行できます。  
  
-   **sysadmin** 固定サーバー ロールのメンバー  
  
-   エンドポイントの所有者  
  
-   エンドポイントで CONNECT 権限を与えられたユーザーまたはグループ  
  
## <a name="permissions"></a>アクセス許可  
 CREATE ENDPOINT 権限、または **sysadmin** 固定サーバー ロールのメンバーシップが必要です。 詳細については、「 [GRANT (エンドポイントの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)」を参照してください。  
  
## <a name="example"></a>例  
  
### <a name="creating-a-database-mirroring-endpoint"></a>データベース ミラーリング エンドポイントを作成する  
 次の例では、データベース ミラーリング エンドポイントを作成します。 使用可能などのポート番号も有効ですが、このエンドポイントではポート番号 `7022` を使用します。 エンドポイントは、Kerberos のみを使用する Windows 認証を使用するように構成されます。 `ENCRYPTION` オプションは既定値以外の `SUPPORTED` に設定され、暗号化データも暗号化されていないデータもサポートします。 エンドポイントは、パートナーおよびミラーリング監視のロールの両方をサポートするように構成されます。  
  
```sql  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (  
       AUTHENTICATION = WINDOWS KERBEROS,  
       ENCRYPTION = SUPPORTED,  
       ROLE=ALL);  
GO  
```  

### <a name="create-a-new-endpoint-pointing-to-a-specific-ipv4-address-and-port"></a>特定の IPv4 アドレスおよびポートを参照する新しいエンドポイントを作成する

```sql
CREATE ENDPOINT ipv4_endpoint_special
STATE = STARTED
AS TCP (
    LISTENER_PORT = 55555, LISTENER_IP = (10.0.75.1)
)
FOR TSQL ();

GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] TO public; -- Keep existing public permission on default endpoint for demo purpose
GRANT CONNECT ON ENDPOINT::ipv4_endpoint_special
TO login_name;
```

### <a name="create-a-new-endpoint-pointing-to-a-specific-ipv6-address-and-port"></a>特定の IPv6 アドレスおよびポートを参照する新しいエンドポイントを作成する

```sql
CREATE ENDPOINT ipv6_endpoint_special
STATE = STARTED
AS TCP (
    LISTENER_PORT = 55555, LISTENER_IP = ('::1')
)
FOR TSQL ();

GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] TO public;
GRANT CONNECT ON ENDPOINT::ipv6_endpoint_special

```
  
## <a name="see-also"></a>参照  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [DROP ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

