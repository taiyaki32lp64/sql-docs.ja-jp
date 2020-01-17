---
title: CLR 関数の作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CLR functions [SQL Server]
- user-defined functions [SQL Server], CLR
ms.assetid: a82df075-2243-4e19-bfe1-ae6d65dabd0f
author: rothja
ms.author: jroth
ms.openlocfilehash: 0234987ec9bdb6e71348e98d3096505a36e31743
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138539"
---
# <a name="create-clr-functions"></a>CLR 関数の作成
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内部には、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR (共通言語ランタイム) で作成されたアセンブリの形式でプログラミングされたデータベース オブジェクトを作成できます。 共通言語ランタイムが提供する豊富なプログラミング モデルを利用できるデータベース オブジェクトには、集計関数、関数、ストアド プロシージャ、トリガー、型などがあります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の CLR 関数を作成するには、次の手順に従います。  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]がサポートする言語のクラスの静的メソッドとして、関数を定義します。 共通言語ランタイムでの関数のプログラミング方法の詳細については、「 [CLR ユーザー定義関数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)」を参照してください。 次に、適切な言語コンパイラを使用してクラスをコンパイルし、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] のアセンブリをビルドします。  
  
-   CREATE ASSEMBLY ステートメントを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアセンブリを登録します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアセンブリの詳細については、「[アセンブリ &#40;データベース エンジン&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)」を参照してください。  
  
-   [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) ステートメントを使用して、登録したアセンブリを参照する関数を作成します。  
  
> [!NOTE]
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] で SQL Server プロジェクトを配置すると、そのプロジェクトで指定されたデータベースにアセンブリが登録されます。 また、プロジェクトを配置することで、 **SqlFunction** 属性で注釈が付けられたすべてのメソッドの CLR 関数がデータベースに作成されます。 詳細については、「 [CLR データベース オブジェクトの配置](../../relational-databases/clr-integration/deploying-clr-database-objects.md)」を参照してください。  
> 
> [!NOTE]
>  CLR コードを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能は、既定では無効になっています。 マネージド コード モジュールを参照するデータベース オブジェクトを作成、変更、削除することはできますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure (Transact-SQL) [を使用して](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) clr enabled オプション [を有効にしないと、これらの参照は](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)で実行されません。  
  
## <a name="accessing-external-resources"></a>外部リソースへのアクセス  
 CLR 関数は、ファイル、ネットワーク リソース、Web サービス、他のデータベース ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のリモート インスタンスを含む) などの外部リソースへのアクセスに使用できます。 これは、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]、 `System.IO`、 `System.WebServices`など、 `System.Sql`のさまざまなクラスを使用して実現できます。 このためには、このような関数を含むアセンブリに、少なくとも EXTERNAL_ACCESS 権限セットを構成します。 詳細については、「 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)がサポートする言語のクラスの静的メソッドとして、関数を定義します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のリモート インスタンスへのアクセスには、SQL クライアント マネージド プロバイダーを使用できます。 ただし、接続を開始したサーバーへのループバック接続は、CLR 関数ではサポートされていません。  
  
 **SQL Server のアセンブリを作成、変更、削除するには**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **CLR 関数を作成するには**  
  
-   [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
## <a name="accessing-native-code"></a>ネイティブ コードへのアクセス  
 CLR 関数では、マネージド コードから PInvoke を使用することにより、C や C++ で記述されたコードなどのネイティブ (アンマネージド) コードにアクセスできます (詳細については、「[マネージド コードからのネイティブ関数の呼び出し](https://go.microsoft.com/fwlink/?LinkID=181929)」を参照してください)。 これにより、レガシ コードを CLR UDF として再利用したり、パフォーマンスが重要な UDF をネイティブ コードで記述したりできます。 そのためには、UNSAFE アセンブリを使用する必要があります。 UNSAFE アセンブリの使用に関する注意事項は、「 [CLR 統合のコード アクセス セキュリティ](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md) 」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ユーザー定義関数の作成 &#40;データベース エンジン&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)   
 [ユーザー定義集計の作成](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)   
 [ユーザー定義関数の実行](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)   
 [ユーザー定義関数の表示](../../relational-databases/user-defined-functions/view-user-defined-functions.md)   
 [CLR &#40;共通言語ランタイム&#41; 統合のプログラミング概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
