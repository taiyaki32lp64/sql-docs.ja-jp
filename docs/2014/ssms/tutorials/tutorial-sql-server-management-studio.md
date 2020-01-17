---
title: チュートリアル:SQL Server Management Studio |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.tutorialstart.ssms.f1
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: d2bade70-07cf-4d94-b5d2-88aecb538ed1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b6cd02b0679990e7781faf2195b17444cadb53e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62753464"
---
# <a name="tutorial-sql-server-management-studio"></a>チュートリアル:SQL Server Management Studio
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のチュートリアルでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インフラストラクチャを管理するための統合環境について説明します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを構成、監視、および管理するためのグラフィカル インターフェイスを提供します。 さらに、データベースやデータ ウェアハウスなどの、アプリケーションで使用されるデータ層コンポーネントを配置、監視、およびアップグレードすることもできます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、スクリプトを編集およびデバッグするための [!INCLUDE[tsql](../../includes/tsql-md.md)]、MDX、DMX、XML の各言語エディターも提供します。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] での情報の操作方法と機能の活用方法を学習します。 このチュートリアルは、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を除く [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションに同梱された [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] の完全インストールを想定した内容となっています。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の基本インストールや、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] に付属の [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] インストールは、このチュートリアルに書かれている内容とは、機能が若干異なります。  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] に慣れ親しむには、実践的な経験を積むのが最も効果的です。 このチュートリアルでは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のコンポーネントを管理する方法と、頻繁に使用する機能へのアクセス方法について説明します。  
  
 このチュートリアルは、次の 3 つのレッスンで構成されています。  
  
 [レッスン 1:SQL Server Management Studio での基本操作](lesson-1-basic-navigation-in-sql-server-management-studio.md)  
 このレッスンでは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]のコンポーネントを使用する方法、環境レイアウトを再構成する方法、および既定のレイアウトを復元する方法を学習します。  
  
 [レッスン 2:書き込み TRANSACT-SQL](lesson-2-writing-transact-sql.md)  
 このレッスンでは、クエリ エディターを開く方法、コードの管理方法、クエリ エディターのその他の新機能を使用する方法を学習します。  
  
 [レッスン 3:テンプレート、ソリューション、およびスクリプト プロジェクトの操作](lesson-3-working-with-templates-solutions-and-script-projects.md)  
 このレッスンでは、テンプレートを使用して、スクリプトをソリューションやプロジェクトにまとめる方法を学習します。  
  
## <a name="requirements"></a>必要条件  
 このチュートリアルは、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]には慣れていないが、データベースの概念と [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語を理解している、熟練のデータベース管理者およびデータベース開発者を対象としています。  
  
 このチュートリアルを使用するには、システムに以下のコンポーネントがインストールされている必要があります。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 以降のバージョンおよび [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベース。 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。 サンプル データベースをインストールするには、「 [SQL Server のサンプルとサンプル データベースのインストール](http://sqlserversamples.codeplex.com)」を参照してください。  
  
-   Internet Explorer 9.0 以降  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジンのチュートリアル](../../relational-databases/database-engine-tutorials.md)  
  
  
