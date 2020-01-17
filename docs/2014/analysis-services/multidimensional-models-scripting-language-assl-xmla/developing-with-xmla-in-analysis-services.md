---
title: Analysis Services での XMLA による開発 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, data mining
- commands [XML for Analysis]
- data mining [XML for Analysis]
- XMLA, data mining
- XML for Analysis, Analysis Services tasks
- XMLA, Analysis Services tasks
ms.assetid: 54445ee7-720c-4683-99a6-e75b3dcca904
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00cb50fe4c71ad853e88ebd86b0891ca4bc24604
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727236"
---
# <a name="developing-with-xmla-in-analysis-services"></a>Analysis Services での XMLA による開発
  XML for Analysis (XMLA) は SOAP ベースの XML プロトコルで、HTTP 接続を使用してアクセスできるあらゆる標準的な多次元データ ソースへの汎用データ アクセスを提供することを目的に特別に設計されています。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、クライアント アプリケーションとの通信を行う場合に、XMLA を唯一のプロトコルとして使用します。 基本的に、Analysis Services によってサポートされるすべてのクライアント ライブラリでは、要求と応答は XMLA で作成されます。  
  
 開発者は、.NET Framework または COM インターフェイスに依存しないで、XMLA を使用してクライアント アプリケーションと [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を統合できます。 広範なプラットフォームでのホスティングを含むアプリケーションの要件は、XMLA および [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] への HTTP 接続を使用して満たすことができます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は XMLA の 1.1 仕様に完全に準拠していますが、データ定義、データ操作、データ制御のサポートを有効にするように拡張することもできます。 Analysis Services の拡張機能は、Analysis Services Scripting Language (ASSL) と呼ばれます。 XMLA と ASSL を組み合わせて使用すると、XMLA 単独より広範な機能セットを提供できます。 ASSL の詳細については、次を参照してください。 [Analysis Services スクリプト言語を使用した開発&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[接続およびセッション管理&#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに接続する方法、および XMLA でのセッションと状態保持を管理する方法について説明します。|  
|[エラーおよび警告の処理&#40;XMLA&#41;](handling-errors-and-warnings-xmla.md)|XMLA のメソッドやコマンドに関して、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] がどのようにエラーおよび警告情報を返すかについて説明します。|  
|[定義するオブジェクトを識別したり&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)|オブジェクト識別子とオブジェクト参照について、および XMLA コマンド内で識別子や参照を使用する方法について説明します。|  
|[トランザクションを管理する&#40;XMLA&#41;](managing-transactions-xmla.md)|使用する方法の詳細、 [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla)、 [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)、および[RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla)明示的に定義し、現在の XMLA で、トランザクションを管理するコマンドセッションです。|  
|[コマンドのキャンセル&#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|使用する方法について説明します、[キャンセル](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)コマンド、セッション、および XMLA での接続をキャンセルするコマンド。|  
|[バッチ操作の実行&#40;XMLA&#41;](performing-batch-operations-xmla.md)|使用する方法について説明します、[バッチ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)コマンドを複数の XMLA を実行するコマンドを直列または並列、同じトランザクション内で、または単一の XMLA を使用して、別のトランザクションとして[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)メソッド。|  
|[オブジェクトの変更の作成と&#40;XMLA&#41;](creating-and-altering-objects-xmla.md)|使用する方法について説明します、[作成](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)、 [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)、および[削除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla)と共に、Analysis Services スクリプト言語 (ASSL) 要素のコマンドは、定義、変更、または削除オブジェクトから、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンス。|  
|[ロックとデータベースをロック解除&#40;XMLA&#41;](locking-and-unlocking-databases-xmla.md)|使用する方法について詳しく、[ロック](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)と[Unlock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)ロックおよびロック解除するためのコマンドを[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データベース。|  
|[オブジェクトの処理 &#40;XMLA&#41;](processing-objects-xmla.md)|使用する方法について説明します、[プロセス](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)プロセスにコマンドを[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]オブジェクト。|  
|[パーティションのマージ&#40;XMLA&#41;](merging-partitions-xmla.md)|使用する方法について説明します、 [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)パーティションをマージするコマンド、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンス。|  
|[集計のデザイン&#40;XMLA&#41;](designing-aggregations-xmla.md)|使用する方法について説明します、 [DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla)反復でいずれかのコマンドをバッチ モードでの集計デザインの集計をデザインする[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]します。|  
|[データベースのバックアップ、復元、および同期 (XMLA)](backing-up-restoring-and-synchronizing-databases-xmla.md)|使用する方法について説明します、[バックアップ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)と[復元](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)バックアップおよび復元するためのコマンドを[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データベース バックアップ ファイルから。<br /><br /> 使用する方法についても説明します、[同期](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)を同期するコマンド、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]同じインスタンスまたは別のインスタンスで既存のデータベースでのデータベース。|  
|[挿入、更新、およびメンバーの削除&#40;XMLA&#41;](inserting-updating-and-dropping-members-xmla.md)|使用する方法について説明します、[挿入](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)、 [Update](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)、および[ドロップ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)コマンドを追加するには、変更、またはメンバーを書き込み許可ディメンションから削除します。|  
|[セルの更新&#40;XMLA&#41;](updating-cells-xmla.md)|使用する方法について説明します、 [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla)書き込み許可パーティション内のセルの値を変更するコマンド。|  
|[キャッシュの管理&#40;XMLA&#41;](managing-caches-xmla.md)|使用する方法の詳細、 [ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla)コマンドのキャッシュをクリアする[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]オブジェクト。|  
|[トレースの監視&#40;XMLA&#41;](monitoring-traces-xmla.md)|使用する方法について説明します、[購読](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla)コマンドにサブスクライブし、上の既存のトレースを監視、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンス。|  
  
## <a name="data-mining-with-xmla"></a>XMLA を使用したデータ マイニング  
 XML for Analysis は、データ マイニング スキーマ行セットを完全にサポートしています。 これらの行セットを使用してデータ マイニング モデルのクエリの情報を提供する、 [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)メソッド。 データ マイニング スキーマ行セットの詳細については、次を参照してください[データ マイニング スキーマ行セット。](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
 DMX の詳細については、次を参照してください。[データ マイニング拡張機能&#40;DMX&#41;参照](/sql/dmx/data-mining-extensions-dmx-reference)します。  
  
## <a name="namespace-and-schema"></a>名前空間とスキーマ  
  
### <a name="namespace"></a>Namespace  
 この仕様で定義されたスキーマが XML 名前空間を使用して https://schemas.microsoft.com/AnalysisServices/2003/Engine と標準の省略形"DDL"にします。  
  
### <a name="schema"></a>スキーマ  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクト定義言語の XML Schema Definition Language (XSD) スキーマの定義は、このセクションのスキーマ要素および階層の定義に基づいています。  
  
## <a name="extensibility"></a>機能拡張  
 オブジェクト定義言語スキーマの拡張性は、すべてのオブジェクトに含まれている `Annotation` 要素によって提供されます。 この要素には、次のルールに従って、XML 名前空間 (DDL を定義する対象の名前空間以外) の有効な XML を使用できます。  
  
-   XML には要素のみを使用できます。  
  
-   すべての要素に一意な名前を付ける必要があります。 `Name` の値が対象の名前空間を参照するように指定してください。  
  
 これらのルールは、`Annotation` タグの内容を名前/値ペアのセットとして Decision Support オブジェクト (DSO) 9.0 を介して公開するために設定されています。  
  
 子要素で囲まれていない `Annotation` タグ内のコメントおよび空白は保存されません。 また、すべての要素は読み取り書き込み要素である必要があり、読み取り専用の要素は無視されます。  
  
 スキーマで定義された要素の派生型の代替が許可されていないサーバーでは、オブジェクト定義言語スキーマは閉じられます。 このため、サーバーは、ここで定義された要素のセットのみを受け入れ、他の要素や属性は受け入れません。 不明な要素を使用すると、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] エンジンにエラーが発生します。  
  
## <a name="see-also"></a>参照  
 [Analysis Services スクリプト言語 (ASSL) での開発](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Microsoft OLAP アーキテクチャについて](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
