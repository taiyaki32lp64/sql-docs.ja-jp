---
title: イベント通知のダイアログ セキュリティの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], security
ms.assetid: 12afbc84-2d2a-4452-935e-e1c70e8c53c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 488b1efd533f038914f2d0186e29e28622531f02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048905"
---
# <a name="configure-dialog-security-for-event-notifications"></a>イベント通知のダイアログ セキュリティの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSB](../../includes/sssb-md.md)] ダイアログ セキュリティを構成する必要があります。 ダイアログ セキュリティは、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ダイアログの完全セキュリティ モデルに従って手動で構成する必要があります。 完全セキュリティ モデルでは、リモート サーバーとの間で送受信するメッセージの暗号化および暗号化解除が可能です。 イベント通知は一方向に送信されますが、エラーなどのメッセージは逆方向にも返されます。  
  
## <a name="configuring-dialog-security-for-event-notifications"></a>イベント通知のダイアログ セキュリティの構成  
 イベント通知のダイアログ セキュリティを実装するために必要な処理は、以下に示す手順のようになります。 これらの手順には、ソース サーバーとターゲット サーバーの両方で実行する必要のある操作が含まれています。 送信元サーバーとは、イベント通知が作成されるサーバーです。 ターゲット サーバーとは、イベント通知メッセージを受信するサーバーです。 ソース サーバーとターゲット サーバーで各手順の操作を実行する必要がある場合は、次の手順に進む前に両方のサーバーで完了する必要があります。  
  
> [!IMPORTANT]  
>  すべての証明書は、有効となる開始日と有効期限終了日を指定して作成する必要があります。  
  
 **ステップ 1: TCP ポート番号と送信先サービスの名前を確定します。**  
  
 ソース サーバーとターゲット サーバーの両方がメッセージを受信する TCP ポートを設定します。 送信先サービスの名前も決定する必要があります。  
  
 **手順 2: データベース レベルの認証で共有される暗号化と証明書を構成します。**  
  
 ソース サーバーとターゲット サーバーの両方で次の操作を実行します。  
  
|[転送元サーバー]|ターゲット サーバー|  
|-------------------|-------------------|  
|イベント通知とマスター キーを格納するデータベースを選択または作成します。|マスター キーを格納するデータベースを選択または作成します。|  
|送信元データベースにマスター キーが存在しない場合は、 [マスター キーを作成](../../t-sql/statements/create-master-key-transact-sql.md)します。 マスター キーは、送信元サーバーと送信先サーバーの両方のデータベースで、それぞれの証明書のセキュリティを確保するために必要となります。|送信先データベースにマスター キーが存在しない場合は、マスター キーを作成します。|  
|送信元データベースで[ログインの作成](../../t-sql/statements/create-login-transact-sql.md) とそれに対応する [ユーザー](../../t-sql/statements/create-user-transact-sql.md) の作成を行います。|送信先データベースでログインとそれに対応するユーザーを作成します。|  
|送信元データベースのユーザーが所有する[証明書を作成](../../t-sql/statements/create-certificate-transact-sql.md) します。|送信先データベースのユーザーが所有する証明書を作成します。|  
|ターゲット サーバーからアクセス可能なファイルに[証明書をバックアップ](../../t-sql/statements/backup-certificate-transact-sql.md)します。|送信元サーバーからアクセス可能なファイルに証明書をバックアップします。|  
|送信先データベースのユーザーと WITHOUT LOGIN を指定して[ユーザーを作成](../../t-sql/statements/create-user-transact-sql.md)します。 このユーザーは、バックアップ ファイルから作成された送信先データベースの証明書を所有します。 このユーザーをログインにマッピングする必要はありません。なぜなら、このユーザーの唯一の目的は、後述の手順 3. で作成する送信先データベースの証明書を所有することだからです。|送信元データベースのユーザーと WITHOUT LOGIN を指定してユーザーを作成します。 このユーザーは、バックアップ ファイルから作成された送信元データベースの証明書を所有します。 このユーザーをログインにマッピングする必要はありません。なぜなら、このユーザーの唯一の目的は、後述の手順 3. で作成する送信元データベースの証明書を所有することだからです。|  
  
 **ステップ 3: データベース レベルの認証で使用する証明書を共有し、権限を許可します。**  
  
 ソース サーバーとターゲット サーバーの両方で次の操作を実行します。  
  
|[転送元サーバー]|ターゲット サーバー|  
|-------------------|-------------------|  
|送信先データベースのユーザーを所有者に指定して、送信先の証明書のバックアップ ファイルから[証明書を作成](../../t-sql/statements/create-certificate-transact-sql.md) します。|送信元データベースのユーザーを所有者に指定して、送信元の証明書のバックアップ ファイルから証明書を作成します。|  
|送信元データベースのユーザーに、イベント通知を作成する[権限を許可](../../t-sql/statements/grant-transact-sql.md) します。 この権限の詳細については、「 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)します。|送信先データベースのユーザーに既存のイベント通知の [!INCLUDE[ssSB](../../includes/sssb-md.md)] コントラクト : `https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`に対する REFERENCES 権限を許可します。|  
|送信先サービスへの[リモート サービス バインドを作成](../../t-sql/statements/create-remote-service-binding-transact-sql.md) し、送信先データベースのユーザーの資格情報を指定します。 リモート サービス バインドは、ターゲット サーバーに送信されるメッセージが、送信元データベースのユーザーが所有する証明書の公開キーによって認証されることを保証します。|送信先データベースのユーザーに CREATE QUEUE 権限、CREATE SERVICE 権限、および CREATE SCHEMA 権限を[許可](../../t-sql/statements/grant-transact-sql.md) します。|  
||まだデータベースに送信先データベース ユーザーとして接続していない場合は、直ちに接続してください。|  
||イベント通知メッセージを受信する[キューを作成](../../t-sql/statements/create-queue-transact-sql.md) し、メッセージを配信する [サービスを作成](../../t-sql/statements/create-service-transact-sql.md) します。|  
||送信元データベースのユーザーに、送信先サービスに対する[SEND 権限を許可](../../t-sql/statements/grant-transact-sql.md) します。|  
|送信元データベースの Service Broker 識別子をターゲット サーバーに指定します。 この識別子は、 **sys.databases** カタログ ビューの [service_broker_guid](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 列にクエリを実行することで取得できます。 サーバー レベルのイベント通知の場合は、Service Broker 識別子として **msdb**を使用します。|送信先データベースの Service Broker 識別子を送信元サーバーに指定します。|  
  
 **手順 4: ルートを作成し、サーバー レベルの認証を設定します。**  
  
 ソース サーバーとターゲット サーバーの両方で次の操作を実行します。  
  
|[転送元サーバー]|ターゲット サーバー|  
|-------------------|-------------------|  
|送信先サービスへの[ルートを作成](../../t-sql/statements/create-route-transact-sql.md) し、送信先データベースの Service Broker 識別子と設定済み TCP ポート番号を指定します。|送信元サービスへのルートを作成し、送信元データベースの Service Broker 識別子と設定済み TCP ポート番号を指定します。 送信元サービスを指定するには、 `https://schemas.microsoft.com/SQL/Notifications/EventNotificationService`で提供されるサービスを使用します。|  
|**master** データベースに切り替えて、サーバー レベルの認証を構成します。|**master** データベースに切り替えて、サーバー レベルの認証を構成します。|  
|**master** データベースにマスター キーが存在しない場合は、 [マスター キーを作成](../../t-sql/statements/create-master-key-transact-sql.md)します。|**master** データベースにマスター キーが存在しない場合は、マスター キーを作成します。|  
|データベースを認証する[証明書を作成](../../t-sql/statements/create-certificate-transact-sql.md) します。|データベースを認証する証明書を作成します。|  
|ターゲット サーバーからアクセス可能なファイルに[証明書をバックアップ](../../t-sql/statements/backup-certificate-transact-sql.md)します。|送信元サーバーからアクセス可能なファイルに証明書をバックアップします。|  
|[エンドポイントを作成](../../t-sql/statements/create-endpoint-transact-sql.md)し、設定済み TCP ポート番号、FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *certificate_name*)、および認証で使用する証明書の名前を指定します。|エンドポイントを作成し、設定済み TCP ポート番号、FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *certificate_name*)、および認証で使用する証明書の名前を指定します。|  
|[ログインを作成](../../t-sql/statements/create-login-transact-sql.md)し、ターゲット サーバーのログインを指定します。|ログインを作成し、送信元サーバーのログインを指定します。|  
|送信先の認証子のログインに、エンドポイントに対する[CONNECT 権限を許可](../../t-sql/statements/grant-transact-sql.md) します。|送信元の認証子のログインに、エンドポイントに対する CONNECT 権限を許可します。|  
|[ユーザーを作成](../../t-sql/statements/create-user-transact-sql.md)し、送信先の認証子のログインを指定します。|ユーザーを作成し、送信元の認証子のログインを指定します。|  
  
 **手順 5: サーバー レベルの認証で使用する証明書を共有し、イベント通知を作成します。**  
  
 ソース サーバーとターゲット サーバーの両方で次の操作を実行します。  
  
|[転送元サーバー]|ターゲット サーバー|  
|-------------------|-------------------|  
|送信先の認証子のユーザーを所有者に指定して、送信先の証明書のバックアップ ファイルから[証明書を作成](../../t-sql/statements/create-certificate-transact-sql.md) します。|送信元の認証子のユーザーを所有者に指定して、送信元の証明書のバックアップ ファイルから証明書を作成します。|  
|イベント通知を作成する送信元データベースに切り替えます。まだ送信元データベースのユーザーとして接続していない場合は、直ちに接続します。|送信先データベースに切り替えて、イベント通知メッセージを受信します。|  
|[イベント通知を作成](../../t-sql/statements/create-event-notification-transact-sql.md)し、送信先データベースの Broker Service と識別子を指定します。||  
  
## <a name="see-also"></a>参照  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [イベント通知の実装](../../relational-databases/service-broker/implement-event-notifications.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)  
  
  
