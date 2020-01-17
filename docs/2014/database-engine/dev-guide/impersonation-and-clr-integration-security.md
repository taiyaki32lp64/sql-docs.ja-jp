---
title: 権限借用と CLR 統合のセキュリティ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- execution context [CLR integration]
- user impersonation [CLR integration]
- context [CLR integration]
ms.assetid: 1495a7af-2248-4cee-afdb-9269fb3a7774
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2c32691a065c2bfc43868d6b4105fbf1395a63ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781130"
---
# <a name="impersonation-and-clr-integration-security"></a>権限借用と CLR 統合のセキュリティ
  マネージド コードが外部リソースにアクセスする際に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、そのルーチンを実行している現在の実行コンテキストの権限を自動的には借用しません。 `EXTERNAL_ACCESS` および `UNSAFE` アセンブリのコードは、現在の実行コンテキストの権限を明示的に借用することができます。  
  
> [!NOTE]  
>  権限借用の動作の変更については、次を参照してください。 [SQL Server 2014 におけるデータベース エンジン機能の重大な変更](../breaking-changes-to-database-engine-features-in-sql-server-2016.md)します。  
  
 インプロセス データ アクセス プロバイダーには、`SqlContext.WindowsIdentity` というアプリケーション プログラミング インターフェイスが用意されています。これを使用して、現在のセキュリティ コンテキストに関連付けられたトークンを取得できます。 `EXTERNAL_ACCESS` アセンブリと `UNSAFE` アセンブリのマネージド コードでは、このメソッドを使用してコンテキストを取得し、.NET Framework `WindowsIdentity.Impersonate` メソッドを使用してそのコンテキストの権限を借用できます。 ユーザー コードから明示的に権限を借用するときは、次の制限事項が適用されます。  
  
-   マネージド コードが権限を借用している状態のときは、インプロセス データ アクセスは許可されません。 コードで、権限借用を元に戻してから、インプロセス データ アクセスを呼び出すことができます。 このためには、元の `WindowsImpersonationContext` メソッドの戻り値 (`Impersonate` オブジェクト) を格納し、この `Undo` の `WindowsImpersonationContext` メソッドを呼び出す必要があります。  
  
     つまり、インプロセス データ アクセスは、常に、セッションに対して有効な現在のセキュリティ コンテキストで行われます。 マネージド コード内の明示的な権限借用によりこれを変更することはできません。  
  
-   (たとえば、スレッドを作成してコードを非同期に実行する `UNSAFE` アセンブリを経由するなどして) 非同期に実行されているマネージド コードの場合、インプロセス データ アクセスは一切許可されません。 これは、権限借用の有無には関係ありません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とは異なる権限を借用したコンテキストでコードを実行している場合、インプロセス データ アクセスの呼び出しを行うことはできません。つまり、インプロセス データ アクセスの呼び出しを行う前に、権限借用のコンテキストを元に戻す必要があります。 マネージド コードからのインプロセス データ アクセスでは常に、マネージド コードへの [!INCLUDE[tsql](../../includes/tsql-md.md)] エントリ ポイントの本来の実行コンテキストが承認に使用されます。  
  
 既に説明したように、`EXTERNAL_ACCESS` アセンブリと `UNSAFE` アセンブリはどちらも、現在のセキュリティ コンテキストの権限を自主的に借用する場合以外は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントでオペレーティング システム リソースにアクセスします。 このため、`EXTERNAL_ACCESS` アセンブリの作成者には、`SAFE` アセンブリの作成者よりも高いレベルの信頼度が必要です。この信頼度は、`EXTERNAL ACCESS` ログイン レベルの権限で指定されます。 `EXTERNAL ACCESS` 権限は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントでコードを実行できるログインのみに許可する必要があります。  
  
## <a name="see-also"></a>参照  
 [CLR 統合のセキュリティ](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [接続の権限借用と資格情報](../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
  
  
