---
title: アプリケーション ドメインと CLR 統合のセキュリティ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- application domains [CLR integration]
ms.assetid: 54ee904e-e21a-4ee7-b4ad-a6f6f71bd473
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3f2ff171562929a035cb80fed556c954508c5557
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62753774"
---
# <a name="application-domains-and-clr-integration-security"></a>アプリケーション ドメインと CLR 統合のセキュリティ
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、同じアプリケーション ドメインの同じ所有者に属するアセンブリを読み込みます。 一連のアセンブリが同じアプリケーション ドメインで実行されるので、.NET Framework リフレクション アプリケーション プログラミング インターフェイスやその他の手段を使用して、実行時にアセンブリを相互に検出することができ、遅延バインディングの形式で呼び出すことができます。 このような呼び出しは同じ所有者に属するアセンブリに対して行われるので、これらの呼び出しに対して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 権限はチェックされません。 アプリケーション ドメインでのアセンブリの配置方法は、主に、スケーラビリティ、セキュリティ、および分離の実現を目標に設計されていますが、この設計は今後のリリースで変更される可能性があります。 したがって、遅延バインディング メカニズムを使用して同じアプリケーション ドメインのアセンブリを検出する方法に依存しないでください。  
  
## <a name="see-also"></a>参照  
 [CLR 統合のセキュリティ](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
