---
title: アセンブリ (データベース エンジン) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4830a677125cb03e2c53ed78065d94d5265d4a83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920780"
---
# <a name="assemblies-database-engine"></a>アセンブリ (データベース エンジン)
  このセクションのトピックでは、アセンブリの理解、設計、および実装に役立つ情報について説明します。  
  
 アセンブリのインスタンスで使用される DLL ファイルは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]関数、ストアド プロシージャ、トリガー、ユーザー定義集計、およびによってホストされているマネージ コード言語のいずれかで記述されているユーザー定義型を展開する、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]共通言語ランタイム (CLR) ではなく[!INCLUDE[tsql](../../../includes/tsql-md.md)]します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のアセンブリは、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 共通言語ランタイムで作成されたマネージド アプリケーション モジュール (.dll ファイル) を参照するオブジェクトです。 アセンブリには、クラス メタデータとマネージド コードが含まれています。 SQL Server のインスタンスにアセンブリをアップロードすることが、次のいずれかのデータベース オブジェクトを作成するための最初の手順になります。  
  
-   CLR 関数。 詳細については、次を参照してください。 [CLR 関数の作成](../user-defined-functions/create-clr-functions.md)です。  
  
-   CLR ストアド プロシージャ。 詳細については、次を参照してください。 [CLR ストアド プロシージャ](../../database-engine/dev-guide/clr-stored-procedures.md)します。  
  
-   CLR トリガー。 詳細については、次を参照してください。 [CLR トリガーを作成する](../triggers/create-clr-triggers.md)します。  
  
-   ユーザー定義集計関数。 詳細については、次を参照してください。[作成ユーザー定義集計](../user-defined-functions/create-user-defined-aggregates.md)します。  
  
-   ユーザー定義型。 詳細については、「[ユーザー定義型の使用](../native-client/features/using-user-defined-types.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、アセンブリによって次の関数が実行されます。  
  
-   上記の 1 つ以上の CLR データベース オブジェクトの機能を実行するマネージド コードを含む関数。  
  
-   アセンブリのバージョン番号とカルチャ、アセンブリのクラスの一覧を一意に識別する省略可能なパブリック キー、アセンブリで定義されたメソッド、アセンブリのプロセッサ アーキテクチャなどのメタデータを含む関数。  
  
-   コード アクセス権を管理することにより、マネージド コードがリソース外部にアクセスできる程度を管理する関数。  
  
-   アセンブリによって参照される他のアセンブリの依存関係に関するメタデータを含む関数。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[アセンブリのデザイン](assemblies-designing.md)|アセンブリを作成する前の注意事項について説明します。 これには、アセンブリのパッケージ化、コード アクセス権、その他の制限事項などがあります。|  
|[アセンブリの実装](assemblies-implementing.md)|アセンブリを作成または削除する方法、アセンブリを変更するタイミングとその方法、およびアセンブリに関するメタデータの取得方法について説明します。|  
|[アセンブリに関する情報の取得](assemblies-getting-information.md)|アセンブリに関するメタデータに対してクエリを実行可能なカタログ ビューや関数を一覧します。|  
  
## <a name="see-also"></a>参照  
 [CLR &#40;共通言語ランタイム&#41; 統合のプログラミング概念](common-language-runtime-clr-integration-programming-concepts.md)  
  
  
