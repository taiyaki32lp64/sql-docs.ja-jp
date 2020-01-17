---
title: CLR トリガーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
author: rothja
ms.author: jroth
ms.openlocfilehash: 096a915f8a86e7dcf8acd5e029fa6e277b8a56c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075551"
---
# <a name="create-clr-triggers"></a>CLR トリガーの作成
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の内部には、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR (共通言語ランタイム) で作成されたアセンブリの形式でプログラミングされたデータベース オブジェクトを作成できます。 CLR で提供される豊富なプログラミング モデルを利用できるデータベース オブジェクトには、DML トリガー、DDL トリガー、ストアド プロシージャ、関数、集計関数、型などがあります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の CLR トリガー (DML トリガーまたは DDL トリガー) を作成するには、次の手順を実行します。  
  
-   トリガーを .NET Framework でサポートされる言語でクラスとして定義します。 CLR でのトリガーのプログラミング方法の詳細については、「 [CLR トリガー](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)」をご覧ください。 次に、適切な言語コンパイラを使用してクラスをコンパイルし、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] のアセンブリをビルドします。  
  
-   CREATE ASSEMBLY ステートメントを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアセンブリを登録します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアセンブリを使用した作業方法の詳細については、「[アセンブリ &#40;データベース エンジン&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)」をご覧ください。  
  
-   登録したアセンブリを参照するトリガーを作成します。  
  
> [!NOTE]
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] で SQL Server プロジェクトを配置すると、そのプロジェクトで指定されたデータベースにアセンブリが登録されます。 また、プロジェクトを配置することで、 **SqlTrigger** 属性で注釈が付けられたすべてのメソッドの CLR トリガーがデータベースに作成されます。 詳細については、「 [CLR データベース オブジェクトの配置](../../relational-databases/clr-integration/deploying-clr-database-objects.md)」を参照してください。  
> 
> [!NOTE]
>  CLR コードを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能は、既定では無効になっています。 マネージド コード モジュールを参照するデータベース オブジェクトを作成、変更、削除することはできますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure (Transact-SQL) [を使用して](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) clr enabled オプション [を有効にしないと、](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)では、これらの参照が実行されません。  
  
 **アセンブリを作成、変更、または削除するには**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **CLR トリガーを作成するには**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [DML トリガー](../../relational-databases/triggers/dml-triggers.md)   
 [CLR &#40;共通言語ランタイム&#41; 統合のプログラミング概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [CLR データベース オブジェクトからのデータ アクセス](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
