---
title: リソース ガバナー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, overview
- Resource Governor
ms.assetid: 2bc89b66-e801-45ba-b30d-8ed197052212
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8d2cdad589ac9c669ae06672260bd99a1de72e8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62704875"
---
# <a name="resource-governor"></a>[リソース ガバナー]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソース ガバナーは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のワークロードとシステム リソースの消費を管理するために使用できる機能です。 リソース ガバナーを使用すると、受信するアプリケーション要求で使用可能な CPU、物理 IO、およびメモリの量に制限を指定できます。  
  
## <a name="benefits-of-resource-governor"></a>リソース ガバナーの利点  
 リソース ガバナーでは、受け取った要求に応じてリソース消費を制限することにより、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のワークロードとリソースを管理することができます。 リソース ガバナーでは、同程度のサイズの複数のクエリや要求を 1 つのエンティティとして扱う場合、それらをワークロードと呼んでいます。 これは必須ではありませんが、ワークロードのリソースの使用パターンが統一化されていると、リソース ガバナーから得られる利点も増えます。 リソース制限は、実行中のワークロードへの影響を最小限に抑えながらリアルタイムで再構成できます。  
  
 複数の個別のワークロードが同一サーバー上に存在する環境でリソース ガバナーを使用すると、指定された制限に基づいてこれらのワークロードを区別し、要求された共有リソースを割り当てることができます。 それらのリソースは CPU、物理 IO、およびメモリです。  
  
 リソース ガバナーを使用すると、次のことが可能です。  
  
-   複数のクライアント ワークロードを提供する SQL Server の 1 つのインスタンスで、マルチテナント機能とリソースの分離を提供します。 つまり、サーバー上の使用可能なリソースをワークロード間で分散し、ワークロードがリソースの確保を求めて競合したときに発生する可能性のある問題を最小限に抑えることができます。  
  
-   複数のワークロードが存在するマルチユーザー環境で、予測可能なパフォーマンスを実現し、ワークロード テナントの SLA をサポートします。  
  
-   IO サブシステムを飽和させ、他のワークロードに悪影響を与える可能性のある DBCC CHECKDB などの操作に対して、ランナウェイ クエリの分離と制限または IO リソースの調整を行います。  
  
-   リソース使用のチャージバックに対して詳細なリソースの追跡を追加し、サーバー リソースの消費者に予測可能な請求情報を提供します。  
  
## <a name="resource-governor-constraints"></a>リソース ガバナーの制約  
 このリリースのリソース ガバナーには次の制約があります。  
  
-   リソース管理は [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]に制限されています。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ではリソース ガバナーを使用できません。  
  
-   SQL Server のインスタンス間のワークロードの監視機能、または管理機能はありません。  
  
-   リソース ガバナーで OLTP ワークロードを管理することは可能ですが、このような種類のクエリは通常短時間で、CPU 上の滞留期間が短いために帯域幅制御を適用できない場合があります。 この結果、CPU 使用率 % として返される統計が偏る可能性があります。  
  
-   物理 IO を制御する機能は、ユーザー操作のみに適用され、システム タスクには適用されません。 システム タスクには、トランザクション ログへの書き込み操作およびレイジー ライターの IO 操作が含まれます。 ほとんどの書き込み操作は通常システム タスクによって実行されるため、リソース ガバナーは主にユーザーの読み取り操作に適用されます。  
  
-   内部リソース プールで IO のしきい値を設定することはできません。  
  
## <a name="resource-concepts"></a>リソースの概念  
 次に示す 3 つの概念は、リソース ガバナーを理解し、使用するための基本となります。  
  
-   **リソース プール。** リソース プールは、サーバーの物理リソースを表します。 プールは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス内部の仮想 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスと考えることができます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールすると、2 つのリソース プール (内部と既定) が作成されます。 リソース ガバナーでは、ユーザー定義のリソース プールもサポートされます。 詳細については、「 [リソース ガバナー リソース プール](resource-governor-resource-pool.md)」を参照してください。  
  
-   **ワークロード グループ。** ワークロード グループは、分類基準が類似しているセッション要求のコンテナーとして機能します。 ワークロードは、セッションの全体的な監視を可能にし、セッションのポリシーを定義します。 各ワークロード グループはリソース プールに存在します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールすると、2 つのワークロード グループ (内部と既定) が作成され、対応するリソース プールにマップされます。 リソース ガバナーでは、ユーザー定義のワークロード グループもサポートされます。 詳細については、「 [リソース ガバナー ワークロード グループ](resource-governor-workload-group.md)」を参照してください。  
  
-   **分類。** 分類プロセスにより、着信セッションがセッションの特性に基づいてワークロード グループに割り当てられます。 分類ロジックは、分類子関数と呼ばれるユーザー定義関数を記述することで調整できます。 リソース ガバナーでは、分類規則を実装するための、ユーザー定義の分類関数もサポートされます。 詳細については、「 [リソース ガバナーの分類子関数](resource-governor-classifier-function.md)」を参照してください。  
  
> [!NOTE]  
>  リソース ガバナーでは、専用管理者接続 (DAC) が制御されません。 内部のワークロード グループおよびリソース プールで実行される DAC クエリは、分類する必要がありません。  
  
 リソース ガバナーのコンテキストでは、上記の概念をコンポーネントとして扱うことができます。 次の図は、これらのコンポーネントと、データベース エンジン環境でのその相互関係を示しています。 処理の観点から見たフローを簡単に示すと次のようになります。  
  
-   セッション (セッション 1/ *n*) に着信接続が存在します。  
  
-   セッションが分類されます (分類)。  
  
-   セッション ワークロードがワークロード グループ (グループ 4 など) にルーティングされます。  
  
-   ワークロード グループは、自身が関連付けられているリソース プール (プール 2 など) を使用します。  
  
-   リソース プールは、アプリケーション (アプリケーション 3 など) に必要なリソースの提供と制限を行います。  
  
 ![リソース ガバナーの機能コンポーネント](../../database-engine/media/rg-basic-funct-components.gif "リソース ガバナーの機能コンポーネント")  
  
## <a name="resource-governor-tasks"></a>リソース ガバナーのタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|リソース ガバナーを有効にする方法について説明します。|[リソース ガバナーの有効化](resource-governor.md)|  
|リソース ガバナーを無効にする方法について説明します。|[リソース ガバナーを無効にしたとき](disable-resource-governor.md)|  
|リソース プールを作成、変更、および削除する方法について説明します。|[リソース ガバナー リソース プール](resource-governor-resource-pool.md)|  
|ワークロード グループを作成、変更、移動、および削除する方法について説明します。|[リソース ガバナー ワークロード グループ](resource-governor-workload-group.md)|  
|ユーザー定義の分類子関数を作成およびテストする方法について説明します。|[リソース ガバナーの分類子関数](resource-governor-classifier-function.md)|  
|テンプレートを使用してリソース ガバナーを構成する方法について説明します。|[テンプレートを使用してリソース ガバナーを構成する](configure-resource-governor-using-a-template.md)|  
|リソース ガバナーのプロパティを表示する方法について説明します。|[リソース ガバナー プロパティの表示](view-resource-governor-properties.md)|  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのインスタンス &#40;SQL Server&#41;](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  
