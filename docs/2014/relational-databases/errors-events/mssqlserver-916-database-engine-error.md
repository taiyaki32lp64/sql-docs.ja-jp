---
title: MSSQLSERVER_916 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 916 (Database Engine error)
ms.assetid: 73eb6581-99fe-49a5-9b42-e239d7ffe27f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aeeda48970696fa3d2f1da22f9aa318910bd53dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761754"
---
# <a name="mssqlserver916"></a>MSSQLSERVER_916
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|916|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|NOTUSER|  
|メッセージ テキスト|現在のセキュリティ コンテキストでは、サーバー プリンシパル "%.*ls" はデータベース "%.\*ls" にアクセスできません。|  
  
## <a name="explanation"></a>説明  
 ログインに、指定されたデータベースに接続するために必要な権限がありません。 この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続することができ、データベースの特定の権限を持っていないログインには、guest ユーザーの権限が与えられます。 これは、1 つのデータベース内のユーザーが、権限を持たない別のデータベースに接続することを防ぐためのセキュリティ措置です。 このエラー メッセージは、指定されたデータベースに対する CONNECT 権限を guest ユーザーが持っていないため、TRUSTWORTHY プロパティが設定されないときに生じる場合があります。 このエラー メッセージは、指定されたデータベースに対する CONNECT 権限を guest ユーザーが持っていないときに生じる場合があります。  
  
 msdb データベースに対する CONNECT 権限が拒否または取り消された場合、オブジェクト エクスプローラーから各データベースのポリシー ベースの管理の状態を表示しようとすると、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でこのエラーが発生する可能性があります。 オブジェクト エクスプローラーでは、現在のログインの権限を使用して、この情報を取得するために msdb データベースに対してクエリを実行します。このとき、エラーが発生します。 また、次のエラー メッセージも表示されます。  
  
 この要求のデータを取得できませんでした。 (Microsoft.SqlServer.Management.Sdk.Sfc)  
  
## <a name="user-action"></a>ユーザーの操作  
  
> [!WARNING]  
>  このセキュリティ措置を回避する前に、各種データベースで認証されているユーザーについて明確に把握している必要があります。 次の方法を実行すると、あるデータベースへの接続権限を持つユーザーが他のデータベースに接続できるようになり、悪意のあるユーザーにデータが公開される可能性があります。 包含データベースが有効化されている場合は、次の手順を実行すると、1 つのデータベースのデータベース所有者が、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス上で別のデータベースへのアクセス権を付与できるようになることがあります。  
  
 次のいずれかの方法でデータベースに接続できます。  
  
-   指定されたデータベースにアクセスするための権限を特定のログインに許可します。 次の例では、`Adventure-Works\Larry` データベースにアクセスするための権限をログイン `msdb` に許可します。  
  
     USE msdb ;  
  
     GO  
  
     GRANT CONNECT TO [Adventure-Works\Larry] ;  
  
-   エラー メッセージで指定されたデータベースに対する CONNECT 権限を guest ユーザーに許可します。 次の例では、`CONNECT` データベースに対する `msdb` 権限を、`guest` ユーザーに許可します。  
  
     USE msdb ;  
  
     GO  
  
     GRANT CONNECT TO guest ;  
  
-   ユーザーを認証したデータベースの TRUSTWORTHY プロパティを有効にします。  
  
     `ALTER DATABASE AdventureWorks SET TRUSTWORTHY ON;`  
  
  
