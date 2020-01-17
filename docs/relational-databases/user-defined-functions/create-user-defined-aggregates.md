---
title: ユーザー定義集計の作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: c278b746-6323-4b32-b460-239915acc067
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e4291cbe79bf0eea51fdf10e2c13fea7f1e23a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138349"
---
# <a name="create-user-defined-aggregates"></a>ユーザー定義集計の作成
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  CLR アセンブリでプログラミングされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の内部にデータベース オブジェクトを作成できます。 CLR が提供する豊富なプログラミング モデルを利用できるデータベース オブジェクトには、トリガー、ストアド プロシージャ、関数、集計関数、型などがあります。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]が提供する組み込みの集計関数と同様に、ユーザー定義集計関数も一連の値に対して計算を実行し、その結果 1 つの値を返します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのユーザー定義集計関数の作成は、次の手順で行われます。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework でサポートされる言語のクラスとしてユーザー定義集計関数を定義します。 CLR でのユーザー定義集計のプログラミング方法の詳細については、「 [CLR ユーザー定義集計](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)」を参照してください。 適切な言語コンパイラを使用してこのクラスをコンパイルし、CLR アセンブリを作成します。  
  
-   CREATE ASSEMBLY ステートメントを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアセンブリを登録します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアセンブリを使用した作業方法の詳細については、「[アセンブリ &#40;データベース エンジン&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)」を参照してください。  
  
-   CREATE AGGREGATE ステートメントを使用して、登録済みのアセンブリを参照するユーザー定義集計を作成します。  
  
> [!NOTE]
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] で SQL Server プロジェクトを配置すると、そのプロジェクトで指定されたデータベースにアセンブリが登録されます。 また、プロジェクトを配置することで、 **SqlUserDefinedAggregate** 属性で注釈が付けられたすべてのクラス定義に対応するユーザー定義集計がデータベースに作成されます。 詳細については、「 [CLR データベース オブジェクトの配置](../../relational-databases/clr-integration/deploying-clr-database-objects.md)」を参照してください。  
> 
> [!NOTE]
>  CLR コードを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能は、既定では無効になっています。 マネージド コード モジュールを参照するデータベース オブジェクトを作成、変更、削除することはできますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure (Transact-SQL) [を使用して](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) clr enabled オプション [を有効にしないと、](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)では、これらの参照が実行されません。  
  
 **アセンブリを作成、変更、または削除するには**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **ユーザー定義集計を作成するには**  
  
-   [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [CLR &#40;共通言語ランタイム&#41; 統合のプログラミング概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
