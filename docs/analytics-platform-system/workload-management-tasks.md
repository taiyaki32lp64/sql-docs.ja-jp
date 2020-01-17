---
title: ワークロード管理タスク
description: 分析プラットフォームシステムのワークロード管理タスク。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 88d95eb0a2e0805930cb5f01f5af05b8fc6b3f2e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399414"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Analytics Platform System のワークロード管理タスク
分析プラットフォームシステムのワークロード管理タスク。

## <a name="view-login-members-of-each-resource-class"></a>各リソースクラスのログインメンバーを表示する
SQL Server PDW で、各リソースクラスのサーバーロールのログインメンバーを表示する方法について説明します。 このクエリを使用して、各ログインによって送信された要求に対して許可されるリソースのクラスを確認します。  
  
リソースクラスの説明については、「[ワークロード管理](workload-management.md)」を参照してください。  
  
このクエリは、各リソースクラスのメンバーシップの一覧を表示します。 リソースクラスには、mediumrc、largerc、xlargerc の3つがあります。  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  ( l.[type] = 'S' OR l.[type] = 'U' OR l.[type] = 'G' )  
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
```  
  
ログインがこの一覧にない場合、その要求は既定のリソースを受け取ります。 ログインが複数のリソースクラスのメンバーである場合は、最大のクラスが優先されます。  
  
リソース割り当ては、[ワークロード管理](workload-management.md)の一覧に表示されます。  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>要求に割り当てられたシステムリソースの変更
SQL Server PDW 要求が実行されているリソースクラスを判別し、その要求のシステムリソースを変更する方法について説明します。 要求のリソースを変更するには、 [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)ステートメントを使用して、要求を送信するログインのリソースクラスのメンバーシップを変更する必要があります。  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>手順 1: 要求を実行しているログインのリソースクラスを特定します。  
このクエリでは、リソースクラスのサーバーロールメンバーシップのメンバーであるログインが表示されます。 リソースクラスには、 **mediumrc**、 **largerc**、 **xlargerc**の3つがあります。  
  
> [!IMPORTANT]  
> このクエリは、 **CONTROL SERVER**権限を持つログインによって実行される必要があります。 **CONTROL SERVER**権限を持たないログインによって実行される場合、このクエリでは、現在のログインのロールメンバーシップのみが返されます。  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  l.[type] = 'S'   
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
GO  
```  
  
リソースクラスのサーバーロールのメンバーであるログインが存在しない場合、結果のテーブルは空になります。 この場合、クエリによって、次のような名前のログインが返されます。この場合、の要求を送信すると、リソースクラスのシステムリソースよりも小さい既定のシステムリソースが要求によって受信されます。 ログインが複数のリソースクラスのメンバーである場合は、最大のクラスが優先されます。  
  
各リソースクラスのリソース割り当ての一覧については、「[ワークロード管理](workload-management.md)」を参照してください。  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>手順 2: 異なるリソースクラスのメンバーシップを持つログインで要求を実行する  
要求を実行するには、次の2つの方法があります。  
  
-   より大きいか小さいリソースクラスのメンバーである別のログインで要求を実行します。  
  
-   リソースクラスロールの1つに必要なログインを追加します。 このオプションは注意して選択してください。ログインのリソースクラスを変更すると、ログインによって送信されたすべての要求のシステムリソースレベルが変更されます。  
  
Largerc がサーバーロールのメンバーであるとします。 次の例は、xlargerc サーバーロールにログインを追加する方法を示しています。  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
これで、largerc と xlargerc サーバーロールのメンバーになりました。 Xlargerc が要求を送信すると、要求はシステムリソースを受信します。  
  
次の例では、mediumrc サーバーロールにを移動します。  新しいロールに変更するには、ログインを xlargerc および largerc サーバーロールから削除し、mediumrc サーバーロールに追加する必要があります。  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
これで、mediumrc サーバーロールのメンバーになりました。  次の例では、要求に既定のシステムリソースが使用されるように変更されています。  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
リソースクラスロールのメンバーシップの変更の詳細については、「 [ALTER SERVER role](../t-sql/statements/alter-server-role-transact-sql.md)」を参照してください。  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>ログインを要求の既定のシステムリソースに変更する
SQL Server PDW ログインに割り当てられたシステムリソース割り当てを既定の量に変更する方法について説明します。 
  
リソースクラスの説明については、「[ワークロード管理](workload-management.md)」を参照してください。  
  
ログインがリソースクラスのサーバーロールのメンバーでない場合、ログインによって送信された要求は、既定の量のシステムリソースを受け取ります。  
  
現在、ログインの状態がすべてのリソースクラスのサーバーロールのメンバーであり、要求が既定のリソースのみを受け取るように戻す場合を考えてみます。  次の例では、3つのリソースクラスサーバーロールすべてからメンバーシップを削除することにより、既定のリソースをの要求に割り当てます。  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>待機中の要求に必要な同時実行スロットの数を表示します
SQL Server PDW での実行を待機している要求によって必要とされる同時実行スロットの数を確認する方法について説明します。  
  
詳細については、「[ワークロード管理](workload-management.md)」を参照してください。  
  
要求は、実行されないまま待機している可能性があります。 要求のトラブルシューティングを行う方法の1つは、要求に必要な同時実行スロットの数を確認することです。  次の例は、待機中の要求ごとに必要な同時実行スロットの数を示しています。  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>参照  
[ワークロード管理](workload-management.md)  
  
