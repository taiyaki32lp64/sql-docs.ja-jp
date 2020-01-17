---
title: DDL イベント | Microsoft Docs
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f166963f1325379d4545f9d8a334e7b77590a14f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075479"
---
# <a name="ddl-events"></a>DDL イベント
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  次の表は、DDL トリガーまたはイベント通知を起動するために使用できる DDL イベントの一覧です。 各イベントは、キーワード間にアンダースコア文字 (_) を含めるように変更されたステートメント構文を備えた [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントまたはストアド プロシージャに対応しています。  
  
> [!IMPORTANT]  
>  DDL と同様の操作を実行するシステム ストアド プロシージャも、DDL トリガーとイベント通知を起動します。 実行されるシステム ストアド プロシージャへの応答を判断するために、DDL トリガーおよびイベント通知をテストしてください。 たとえば、CREATE TYPE ステートメントおよび **sp_addtype** ストアド プロシージャはどちらも、CREATE_TYPE イベントで作成される DDL トリガーおよびイベント通知を起動します。  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>サーバー スコープまたはデータベース スコープを持つ DDL ステートメント  
 DDL トリガーまたはイベント通知は、そのトリガーまたはイベント通知が作成されたデータベース、またはサーバー インスタンスのあらゆる場所で、次に示すイベントが発生したときにそのイベントに応答して起動されるように作成できます。  
  
||||  
|-|-|-|  
|CREATE_APPLICATION_ROLE (CREATE APPLICATION ROLE ステートメントと **sp_addapprole**に適用されます。 新しいスキーマが作成されると、このイベントは CREATE_SCHEMA イベントもトリガーします。)|ALTER_APPLICATION_ROLE (ALTER APPLICATION ROLE ステートメントと **sp_approlepassword**に適用されます。)|DROP_APPLICATION_ROLE (DROP APPLICATION ROLE ステートメントと **sp_dropapprole**に適用されます。)|  
|CREATE_ASSEMBLY|ALTER_ASSEMBLY|DROP_ASSEMBLY|  
|CREATE_ASYMMETRIC_KEY|ALTER_ASYMMETRIC_KEY|DROP_ASYMMETRIC_KEY|  
|ALTER_AUTHORIZATION|ALTER_AUTHORIZATION_DATABASE (ON DATABASE が指定されている場合の ALTER AUTHORIZATION ステートメント、および **sp_changedbowner**に適用されます。)||  
|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|  
|CREATE_CERTIFICATE|ALTER_CERTIFICATE|DROP_CERTIFICATE|  
|CREATE_CONTRACT|DROP_CONTRACT||  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|GRANT_DATABASE|DENY_DATABASE|REVOKE_DATABASE|  
|CREATE_DATABASE_AUDIT_SPEFICIATION|ALTER_DATABASE_AUDIT_SPEFICIATION|DENY_DATABASE_AUDIT_SPEFICIATION|  
|CREATE_DATABASE_ENCRYPTION_KEY|ALTER_DATABASE_ENCRYPTION_KEY|DROP_DATABASE_ENCRYPTION_KEY|  
|CREATE_DEFAULT|DROP_DEFAULT||  
|BIND_DEFAULT ( **sp_bindefault**に適用されます。)|UNBIND_DEFAULT ( **sp_unbindefault**に適用されます。)||  
|CREATE_EVENT_NOTIFICATION|DROP_EVENT_NOTIFICATION||  
|CREATE_EXTENDED_PROPERTY ( **sp_addextendedproperty**に適用されます。)|ALTER_EXTENDED_PROPERTY ( **sp_updateextendedproperty**に適用されます。)|DROP_EXTENDED_PROPERTY ( **sp_dropextendedproperty**に適用されます。)|  
|CREATE_FULLTEXT_CATALOG (CREATE FULLTEXT CATALOG ステートメントと、 **create** が指定されている場合の *sp_fulltextcatalog* に適用されます。)|ALTER_FULLTEXT_CATALOG (ALTER FULLTEXT CATALOG ステートメント、 **start_incremental** 、 *start_full*、 *Stop*、または *Rebuild*が指定されている場合の *sp_fulltextcatalog* 、および **enable** が指定されている場合の *sp_fulltext_database* に適用されます。)|DROP_FULLTEXT_CATALOG (DROP FULLTEXT CATALOG ステートメントと、 **drop** が指定されている場合の *sp_fulltextcatalog* に適用されます。)|  
|CREATE_FULLTEXT_INDEX (CREATE FULLTEXT INDEX ステートメントと、 **create** が指定されている場合の *sp_fulltexttable* に適用されます。)|ALTER_FULLTEXT_INDEX (ALTER FULLTEXT INDEX ステートメント、 **start_full** 、 *start_incremental*、または *stop*が指定されている場合の *sp_fulltextcatalog* 、 **sp_fulltext_column**、および **create** または *drop* 以外のアクションが指定されている場合の *sp_fulltext_table* に適用されます。)|DROP_FULLTEXT_INDEX (DROP FULLTEXT INDEX ステートメントと、 **drop** が指定されている場合の *sp_fulltexttable* に適用されます。)|  
|CREATE_FULLTEXT_STOPLIST|ALTER_FULLTEXT_STOPLIST|DROP_FULLTEXT_STOPLIST|  
|CREATE_FUNCTION|ALTER_FUNCTION|DROP_FUNCTION|  
|CREATE_INDEX|ALTER_INDEX (ALTER INDEX ステートメントと **sp_indexoption**に適用されます。)|DROP_INDEX|  
|CREATE_MASTER_KEY|ALTER_MASTER_KEY|DROP_MASTER_KEY|  
|CREATE_MESSAGE_TYPE|ALTER_MESSAGE_TYPE|DROP_MESSAGE_TYPE|  
|CREATE_PARTITION_FUNCTION|ALTER_PARTITION_FUNCTION|DROP_PARTITION_FUNCTION|  
|CREATE_PARTITION_SCHEME|ALTER_PARTITION_SCHEME|DROP_PARTITION_SCHEME|  
|CREATE_PLAN_GUIDE ( **sp_create_plan_guide**に適用されます。)|ALTER_PLAN_GUIDE (ENABLE、ENABLE ALL、DISABLE、または DISABLE ALL が指定されている場合の **sp_control_plan_guide** に適用されます。)|DROP_PLAN_GUIDE (DROP または DROP ALL が指定されている場合の **sp_control_plan_guide** に適用されます。)|  
|CREATE_PROCEDURE|ALTER_PROCEDURE (ALTER PROCEDURE ステートメントと **sp_procoption**に適用されます。)|DROP_PROCEDURE|  
|CREATE_QUEUE|ALTER_QUEUE|DROP_QUEUE|  
|CREATE_REMOTE_SERVICE_BINDING|ALTER_REMOTE_SERVICE_BINDING|DROP_REMOTE_SERVICE_BINDING|  
|CREATE_SPATIAL_INDEX|||  
|RENAME ( **sp_rename**に適用されます。)|||  
|CREATE_ROLE (CREATE ROLE ステートメント、 **sp_addrole**、および **sp_addgroup**に適用されます。)|ALTER_ROLE|DROP_ROLE (DROP ROLE ステートメント、 **sp_droprole**、および **sp_dropgroup**に適用されます。)|  
|ADD_ROLE_MEMBER|DROP_ROLE_MEMBER||  
|CREATE_ROUTE|ALTER_ROUTE|DROP_ROUTE|  
|CREATE_RULE|DROP_RULE||  
|BIND_RULE ( **sp_bindrule**に適用されます。)|UNBIND_RULE ( **sp_unbindrule**に適用されます。)||  
|CREATE_SCHEMA (CREATE SCHEMA ステートメント、 **sp_addrole**、 **sp_adduser**、 **sp_addgroup**、および **sp_grantdbaccess**に適用されます。)|ALTER_SCHEMA (ALTER SCHEMA ステートメントと **sp_changeobjectowner**に適用されます。)|DROP_SCHEMA|  
|CREATE_SEARCH_PROPERTY_LIST|ALTER_SEARCH_PROPERTY_LIST|DROP_SEARCH_PROPERTY_LIST|  
|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|  
|CREATE_SERVER_ROLE|ALTER_SERVER_ROLE|DROP_SERVER_ROLE|  
|CREATE_SERVICE|ALTER_SERVICE|DROP_SERVICE|  
|ALTER_SERVICE_MASTER_KEY|BACKUP_SERVICE_MASTER_KEY|RESTORE_SERVICE_MASTER_KEY|  
|ADD_SIGNATURE (非スキーマ スコープ オブジェクト (データベース、アセンブリ、トリガー) の署名操作用)|DROP_SIGNATURE||  
|ADD_SIGNATURE_SCHEMA_OBJECT (スキーマ スコープ オブジェクト (ストアド プロシージャ、関数) 用)|DROP_SIGNATURE_SCHEMA_OBJECT||  
|CREATE_SPATIAL_INDEX|ALTER_INDEX は、空間インデックスに使用できます。|DROP_INDEX は、空間インデックスに使用できます。|  
|CREATE_STATISTICS|DROP_STATISTICS|UPDATE_STATISTICS|  
|CREATE_SYMMETRIC_KEY|ALTER_SYMMETRIC_KEY|DROP_SYMMETRIC_KEY|  
|CREATE_SYNONYM|DROP_SYNONYM||  
|CREATE_TABLE|ALTER_TABLE (ALTER TABLE ステートメントと **sp_tableoption**に適用されます。)|DROP_TABLE|  
|CREATE_TRIGGER|ALTER_TRIGGER (ALTER TRIGGER ステートメントと **sp_settriggerorder**に適用されます。)|DROP_TRIGGER|  
|CREATE_TYPE (CREATE TYPE ステートメントと **sp_addtype**に適用されます。)|DROP_TYPE (DROP TYPE ステートメントと **sp_droptype**に適用されます。)||  
|CREATE_USER (CREATE USER ステートメント、 **sp_adduser**、および **sp_grantdbaccess**に適用されます。)|ALTER_USER (ALTER USER ステートメントと **sp_change_users_login**に適用されます。)|DROP_USER (DROP USER ステートメント、 **sp_dropuser**、および **sp_revokedbaccess**に適用されます。)|  
|CREATE_VIEW|ALTER_VIEW|DROP_VIEW|  
|CREATE_XML_INDEX|ALTER_INDEX は、XML インデックスに使用できます。|DROP_INDEX は、XML インデックスに使用できます。|  
|CREATE_XML_SCHEMA_COLLECTION|ALTER_XML_SCHEMA_COLLECTION|DROP_XML_SCHEMA_COLLECTION|  
  
## <a name="ddl-statements-that-have-server-scope"></a>サーバー スコープを持つ DDL ステートメント  
 DDL トリガーまたはイベント通知は、サーバー インスタンスのあらゆる場所で次に示すイベントが発生したときに、そのイベントに応答して起動されるように作成できます。  
  
||||  
|-|-|-|  
|ALTER_AUTHORIZATION_SERVER|ALTER_SERVER_CONFIGURATION|ALTER_INSTANCE (ローカル サーバー インスタンスが指定されている場合の **sp_configure** と **sp_addserver** に適用されます。)|  
|CREATE_AVAILABILITY_GROUP|ALTER_AVAILABILITY_GROUP|DROP_AVAILABILITY_GROUP|  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|CREATE_CRYPTOGRAPHIC_PROVIDER|ALTER_CRYPTOGRAPHIC_PROVIDER|DROP_CRYPTOGRAPHIC_PROVIDER|  
|CREATE_DATABASE|ALTER_DATABASE (ALTER DATABASE ステートメントと **sp_fulltext_database**に適用されます。)|DROP_DATABASE|  
|CREATE_ENDPOINT|ALTER_ENDPOINT|DROP_ENDPOINT|  
|CREATE_EVENT_SESSION|ALTER_EVENT_SESSION|DROP_EVENT_SESSION|  
|CREATE_EXTENDED_PROCEDURE ( **sp_addextendedproc**に適用されます。)|DROP_EXTENDED_PROCEDURE ( **sp_dropextendedproc**に適用されます。)||  
|CREATE_LINKED_SERVER ( **sp_addlinkedserver**に適用されます。)|ALTER_LINKED_SERVER ( **sp_serveroption**に適用されます。)|DROP_LINKED_SERVER (リンク サーバーが指定されている場合の **sp_dropserver** に適用されます。)|  
|CREATE_LINKED_SERVER_LOGIN ( **sp_addlinkedsrvlogin**に適用されます。)|DROP_LINKED_SERVER_LOGIN ( **sp_droplinkedsrvlogin**に適用されます。)||  
|CREATE_LOGIN (暗黙的に作成する必要がある存在しないログインで使用される場合の CREATE_LOGIN ステートメント、 **sp_addlogin**、 **sp_grantlogin**、 **xp_grantlogin**、および **sp_denylogin** に適用されます。)|ALTER_LOGIN ( **Auto_Fix**が指定されている場合の ALTER LOGIN ステートメント、 **sp_defaultdb**、 **sp_defaultlanguage**、 **sp_password** 、および *sp_change_users_login* に適用されます。)|DROP_LOGIN (DROP LOGIN ステートメント、 **sp_droplogin**、 **sp_revokelogin**、および **xp_revokelogin**に適用されます。)|  
|CREATE_MESSAGE ( **sp_addmessage**に適用されます。)|ALTER_MESSAGE ( **sp_altermessage**に適用されます。)|DROP_MESSAGE ( **sp_dropmessage**に適用されます。)|  
|CREATE_REMOTE_SERVER ( **sp_addserver**に適用されます。)|ALTER_REMOTE_SERVER ( **sp_setnetname**に適用されます。)|DROP_REMOTE_SERVER (リモート サーバーが指定されている場合の **sp_dropserver** に適用されます。)|  
|CREATE_RESOURCE_POOL|ALTER_RESOURCE_POOL|DROP_RESOURCE_POOL|  
|GRANT_SERVER|DENY_SERVER|REVOKE_SERVER|  
|ADD_SERVER_ROLE_MEMBER|DROP_SERVER_ROLE_MEMBER||  
|CREATE_SERVER_AUDIT|ALTER_SERVER_AUDIT|DROP_SERVER_AUDIT|  
|CREATE_SERVER_AUDIT_SPECIFICATION|ALTER_SERVER_AUDIT_SPECIFICATION|DROP_SERVER_AUDIT_SPECIFICATION|  
|CREATE_WORKLOAD_GROUP|ALTER_WORKLOAD_GROUP|DROP_WORKLOAD_GROUP|  
  
## <a name="see-also"></a>参照  
 [DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)   
 [イベント通知](../../relational-databases/service-broker/event-notifications.md)   
 [DDL イベント グループ](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
