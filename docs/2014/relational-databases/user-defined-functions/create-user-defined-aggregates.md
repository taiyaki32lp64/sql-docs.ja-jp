---
title: ユーザー定義集計の作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: c278b746-6323-4b32-b460-239915acc067
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 23d5180928f4f3335aa17dff61b50e6fdd19549f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196467"
---
# <a name="create-user-defined-aggregates"></a>ユーザー定義集計の作成
  CLR アセンブリでプログラミングされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の内部にデータベース オブジェクトを作成できます。 CLR が提供する豊富なプログラミング モデルを利用できるデータベース オブジェクトには、トリガー、ストアド プロシージャ、関数、集計関数、型などがあります。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]が提供する組み込みの集計関数と同様に、ユーザー定義集計関数も一連の値に対して計算を実行し、その結果 1 つの値を返します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのユーザー定義集計関数の作成は、次の手順で行われます。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework でサポートされる言語のクラスとしてユーザー定義集計関数を定義します。 CLR でのユーザー定義集計のプログラミング方法の詳細については、「 [CLR ユーザー定義集計](../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)」を参照してください。 適切な言語コンパイラを使用してこのクラスをコンパイルし、CLR アセンブリを作成します。  
  
-   CREATE ASSEMBLY ステートメントを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアセンブリを登録します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアセンブリを使用した作業方法の詳細については、「[アセンブリ &#40;データベース エンジン&#41;](../clr-integration/assemblies-database-engine.md)」を参照してください。  
  
-   CREATE AGGREGATE ステートメントを使用して、登録済みのアセンブリを参照するユーザー定義集計を作成します。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] で SQL Server プロジェクトを配置すると、そのプロジェクトで指定されたデータベースにアセンブリが登録されます。 また、プロジェクトを配置することで、`SqlUserDefinedAggregate` 属性で注釈が付けられたすべてのクラス定義に対応するユーザー定義集計がデータベースに作成されます。 詳細については、「 [CLR データベース オブジェクトの配置](../clr-integration/deploying-clr-database-objects.md)」を参照してください。  
  
> [!NOTE]  
>  CLR コードを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能は、既定では無効になっています。 マネージド コード モジュールを参照するデータベース オブジェクトを作成、変更、削除することはできますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure (Transact-SQL) [を使用して](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) clr enabled オプション [を有効にしないと、](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)では、これらの参照が実行されません。  
  
 **アセンブリを作成、変更、または削除するには**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **ユーザー定義集計を作成するには**  
  
-   [CREATE AGGREGATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-aggregate-transact-sql)  
  
## <a name="see-also"></a>関連項目  
 [CLR &#40;共通言語ランタイム&#41; 統合のプログラミング概念](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
