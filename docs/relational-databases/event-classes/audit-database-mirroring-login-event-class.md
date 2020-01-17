---
title: Audit Database Mirroring Login イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- Audit Database Mirroring Login event class
- database mirroring [SQL Server], event notifications
ms.assetid: d0bd436d-aade-4208-a7e5-75cf3b5d0ce9
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bb9c8b9774be0daa74b30bfd51ee97bf1e2271c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903453"
---
# <a name="audit-database-mirroring-login-event-class"></a>Audit Database Mirroring Login イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は **Audit Database Mirroring Login** イベントを作成して、データベース ミラーリングのトランスポートのセキュリティに関する監査メッセージを報告します。  
  
## <a name="audit-database-mirroring-login-event-class-data-columns"></a>Audit Database Mirroring Login イベント クラスのデータ列  
  
|データ列|型|[説明]|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|このイベント クラスでは使用しません。|10|はい|  
|**ClientProcessID**|**int**|このイベント クラスでは使用しません。|9|はい|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**EventClass**|**int**|キャプチャされたイベント クラスの種類。 **Audit Database Mirroring Login** の場合は常に **154**。|27|いいえ|  
|**EventSequence**|**int**|このイベントのシーケンス番号。|51|いいえ|  
|**EventSubClass**|**int**|イベント サブクラスの種類です。各イベント クラスについての詳細な情報を提供します。 次の表に、このイベントのイベント サブクラス値を示します。|21|はい|  
|**FileName**|**nvarchar**|リモートのデータベース ミラーリング エンドポイントで構成されたサポート済みの認証方式。 複数の方式を使用できる場合は、受け入れ側 (対象) のエンドポイントにより、最初に試行される方式が決まります。 有効な値は次のとおりです。<br /><br /> <br /><br /> **None**。 認証方式が構成されていません。<br /><br /> **NTLM**: NTLM 認証が必要です。<br /><br /> **KERBEROS**: Kerberos 認証が必要です。<br /><br /> **NEGOTIATE**: Windows が認証方式をネゴシエートします。<br /><br /> **CERTIFICATE**: エンドポイントに構成されている証明書が必要です。これは、 **master** データベースに格納されています。<br /><br /> **NTLM, CERTIFICATE**: NTLM またはエンドポイントの証明書を認証方式として受け付けます。<br /><br /> **KERBEROS, CERTIFICATE**: Kerberos またはエンドポイントの証明書を認証方式として受け付けます。<br /><br /> **NEGOTIATE, CERTIFICATE**: Windows が認証方式、または認証に使用できるエンドポイントの証明書をネゴシエートします。<br /><br /> **CERTIFICATE, NTLM**: エンドポイントの証明書または NTLM を認証方式として受け付けます。<br /><br /> **CERTIFICATE, KERBEROS**: エンドポイントの証明書または Kerberos を認証方式として受け付けます。<br /><br /> **CERTIFICATE, NEGOTIATE**: エンドポイントの証明書を認証方式として受け付けるか、Windows が認証方式をネゴシエートします。|36|いいえ|  
|**HostName**|**nvarchar**|このイベント クラスでは使用しません。|8|はい|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|いいえ|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが属している Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|このイベントが生成された接続を所有するユーザーの名前。|6|はい|  
|**ObjectName**|**nvarchar**|この接続に使用する接続文字列。|34|いいえ|  
|**OwnerName**|**nvarchar**|ローカルのデータベース ミラーリング エンドポイントで構成されたサポート済みの認証方式。 複数の方式を使用できる場合は、受け入れ側 (対象) のエンドポイントにより、最初に試行される方式が決まります。 有効な値は次のとおりです。<br /><br /> <br /><br /> **None**。 認証方式が構成されていません。<br /><br /> **NTLM**: NTLM 認証が必要です。<br /><br /> **KERBEROS**: Kerberos 認証が必要です。<br /><br /> **NEGOTIATE**: Windows が認証方式をネゴシエートします。<br /><br /> **CERTIFICATE**: エンドポイントに構成されている証明書が必要です。これは、 **master** データベースに格納されています。<br /><br /> **NTLM, CERTIFICATE**: NTLM またはエンドポイントの証明書を認証方式として受け付けます。<br /><br /> **KERBEROS, CERTIFICATE**: Kerberos またはエンドポイントの証明書を認証方式として受け付けます。<br /><br /> **NEGOTIATE, CERTIFICATE**: Windows が認証方式、または認証に使用できるエンドポイントの証明書をネゴシエートします。<br /><br /> **CERTIFICATE, NTLM**: エンドポイントの証明書または NTLM を認証方式として受け付けます。<br /><br /> **CERTIFICATE, KERBEROS**: エンドポイントの証明書または Kerberos を認証方式として受け付けます。<br /><br /> **CERTIFICATE, NEGOTIATE**: エンドポイントの証明書を認証方式として受け付けるか、Windows が認証方式をネゴシエートします。|37|いいえ|  
|**ProviderName**|**nvarchar**|この接続に使用する認証方式。|46|いいえ|  
|**RoleName**|**nvarchar**|接続のロール。 **initiator** または **target**のいずれかです。|38|いいえ|  
|**ServerName**|**nvarchar**|トレースされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SPID**|**int**|クライアントに関連付けられているプロセスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられているサーバー プロセス ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**状態**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のソース コード内のイベントが生成された場所を示します。 イベントが生成された場所によって、状態コードが異なることがあります。 マイクロソフトのサポート エンジニアはこの状態コードを使用して、イベントが生成されたソース コード内の場所を特定することができます。|30|いいえ|  
|**TargetUserName**|**nvarchar**|ログイン状態。 次のいずれかです。<br /><br /> **INITIAL**<br /><br /> **WAIT LOGIN NEGOTIATE**<br /><br /> **ONE ISC**<br /><br /> **ONE ASC**<br /><br /> **TWO ISC**<br /><br /> **TWO ASC**<br /><br /> **WAIT ISC Confirm**<br /><br /> **WAIT ASC Confirm**<br /><br /> **WAIT REJECT**<br /><br /> **WAIT PRE-MASTER SECRET**<br /><br /> **WAIT VALIDATION**<br /><br /> **WAIT ARBITRATION**<br /><br /> **ONLINE**<br /><br /> **ERROR**<br /><br /> <br /><br /> 注:ISC は、セキュリティ コンテキストの送信 (Initiate Security Context) を表します。 ASC は、セキュリティ コンテキストの受け入れ (Accept Security Context) を表します。|39|いいえ|  
|**TransactionID**|**bigint**|トランザクションに対してシステムが割り当てた ID。|4|いいえ|  
  
 次の表に、このイベント クラスのサブクラス値を示します。  
  
|ID|サブクラス|[説明]|  
|--------|--------------|-----------------|  
|1|Login Success|Login Success イベントは、隣接するデータベース ミラーリングのログイン プロセスが正常に完了したことを報告するイベントです。|  
|2|Login Protocol Error|Login Protocol Error イベントは、形式は正しくても、ログイン プロセスの現在の状態では無効なメッセージをデータベース ミラーリング ログインが受け取ったことを報告するイベントです。 このメッセージは、失われたか、誤った順序で送信されている可能性があります。|  
|3|Message Format Error|Message Format Error イベントは、期待する形式に一致しないメッセージをデータベース ミラーリング ログインが受け取ったことを報告するイベントです。 このメッセージは破損しているか、データベース ミラーリングが使用しているポートに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のプログラムがメッセージを送信している可能性があります。|  
|4|Negotiate Failure|Negotiate Failure イベントは、ローカルのデータベース ミラーリング エンドポイントとリモートのデータベース ミラーリング エンドポイントが同時に使用できない認証をサポートしていることを報告するイベントです。|  
|5|Authentication Failure|Authentication Failure イベントは、データベース ミラーリング エンドポイントがエラーのために接続を認証できないことを報告するイベントです。 Windows 認証の場合は、データベース ミラーリング エンドポイントが Windows 認証を使用できないことを示しています。 証明書ベースの認証の場合は、データベース ミラーリング エンドポイントが証明書にアクセスできないことを示しています。|  
|6|Authorization Failure|Authorization Failure イベントは、データベース ミラーリング エンドポイントが接続の認証を拒否したことを報告するイベントです。 Windows 認証の場合は、接続のセキュリティ ID に一致するデータベース ユーザーが見つからないことを示しています。 証明書ベースの認証の場合は、メッセージにより渡された公開キーが **master** データベース内の証明書に対応していないことを示しています。|  
  
## <a name="see-also"></a>参照  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
