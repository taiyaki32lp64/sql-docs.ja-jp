---
title: ストアド プロシージャ (Analysis Services) に対する権限の付与 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01793166-a3e5-4856-8302-21b82d494e69
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a363336af1bee8c3f84ff620f667c7c0d510b73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080728"
---
# <a name="grant-permissions-on-stored-procedures-analysis-services"></a>ストアド プロシージャに対する権限の付与 (Analysis Services)
  ストアド プロシージャ、またはアセンブリ、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]で記述された、外部ルーチンは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET プログラミング言語の機能を拡張する[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]します。 アセンブリには、言語間の統合、例外処理、バージョン管理のサポート、展開のサポート、およびデバッグのサポートを利用する開発者が使用できます。  
  
 アセンブリを登録するには、サーバー管理者である必要があります。 参照してください[サーバーの管理者アクセス許可の付与&#40;Analysis Services&#41;](instances/grant-server-admin-rights-to-an-analysis-services-instance.md)します。  
  
## <a name="security-context-for-stored-procedure-execution"></a>ストアド プロシージャの実行のセキュリティ コンテキスト  
 すべてのユーザーがストアド プロシージャを呼び出すことができます。 ストアド プロシージャは、その構成方法により、プロシージャを呼び出すユーザーのコンテキスト、または匿名ユーザーのコンテキストのいずれかで実行できます。 匿名ユーザーにはセキュリティ コンテキストがないため、匿名アクセスを許可するには、この機能を [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスの構成と共に使用します。  
  
 ユーザーがストアド プロシージャを呼び出してから、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] でストアド プロシージャが実行されるまでに、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、ストアド プロシージャ内のアクションが評価されます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、ユーザーに与えられた権限と、プロシージャの実行に使用される権限セットの共通部分に基づき、ストアド プロシージャ内のアクションを評価します。 ストアド プロシージャに、ユーザーのデータベース ロールでは実行できないアクションある場合、そのアクションは実行されません。  
  
 ストアド プロシージャの実行に使用する権限セットを以下に示します。  
  
-   **安全な**安全のためのアクセス許可セットで保護されたリソースがストアド プロシージャにアクセスできない、 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework です。 この権限セットでは、計算のみが可能です。 これは最も安全な権限で、情報が [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] の外に漏れることがないほか、権限が昇格される心配もなく、データ改ざんの攻撃のリスクを最小限に抑えることができます。  
  
-   **外部アクセス**外部アクセス権限セットでは、ストアド プロシージャは外部リソースにアクセス マネージ コードを使用しています。 ストアド プロシージャをこの権限セットに設定すると、サーバー不安定の原因となるプログラミング エラーは発生しません。 ただし、この権限セットは、情報がサーバーの外に漏れる結果をもたらす場合があり、権限の昇格や、データ改ざんの攻撃の可能性があります。  
  
-   **Unrestricted**無制限のアクセス許可セットでは、ストアド プロシージャは外部リソースにアクセス任意のコードを使用しています。 この権限セットが指定されている場合、ストアド プロシージャに対してセキュリティも信頼性も保証されません。  
  
## <a name="see-also"></a>参照  
 [多次元モデルのアセンブリの管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
