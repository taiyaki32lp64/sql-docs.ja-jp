---
title: ドメインの管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: c5ab71a3-0dac-45b1-be8e-93bf7e0e03ce
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 93b5666bd2d57fb0a8ffae435818a02ba152217c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484126"
---
# <a name="managing-a-domain"></a>ドメインの管理
  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でのドメインの使用について説明します。 ドメインは、分析対象のデータ ソースの特定のフィールドに含まれているデータのセマンティック表現です。 ドメインは、データ ソースに対して作成するナレッジ ベースの一部で、サンプル データ ソースを分析するか、データをインポートして構築するナレッジは、ナレッジ ベースで定義されたドメインに追加されます。 これらのドメインのナレッジは、データ品質プロジェクトでクレンジングおよび照合を実行するために後で使用されます。 ドメインは、Data Quality Services のすべてのアクティビティの中核になります。  
  
 ドメインは、データ ソース フィールドにマップされ、ナレッジ検出、ドメイン管理、および照合の各アクティビティで作成されます。 データ ソースからデータを読み込む方法とレポートにデータを出力する方法は、ドメインのプロパティで定義します。 参照データ プロバイダーを使用してデータをクレンジングする場合は、参照データ サービスを単一または複合ドメインにアタッチします。 ドメインのデータに適用されるルールを作成すると、ドメインに対する用語ベースのリレーションを作成できます。 ドメインのデータを表示および修正できます。  
  
 共通データに関するナレッジを含む 2 つ以上の個別のドメインで構成される複合ドメインを作成することもできます。 詳しくは、「[複合ドメインの管理](../../2014/data-quality-services/managing-a-composite-domain.md)」をご覧ください。  
  
## <a name="domain-properties"></a>ドメインのプロパティ  
 ドメインを作成する際には、ソース データからドメインを作成する方法とドメイン値を出力する方法に関する次のオプションがあります。 詳しくは、「[ドメインのプロパティの設定](../../2014/data-quality-services/set-domain-properties.md)」をご覧ください。  
  
-   ドメインの作成に使用するデータの型を選択します。 各ドメイン データ型でサポートされているデータ型については、「 [DQS ドメインに対してサポートされる SQL Server のデータ型と SSIS のデータ型](../../2014/data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md)」を参照してください。  
  
-   シノニムではなく先頭の値のみがドメインから出力されるように指定します。  
  
-   ドメイン値がデータ型に応じて特定の形式で出力されるように指定します。  
  
-   データ型が文字列の場合は、文字列がデータ ソースからドメインに読み込まれるときに特殊文字を削除することによって文字列を正規化します。  
  
-   データ型が文字列の場合は、DQS スペル チェックを実行して文字列の構文、スペル、および文構造をチェックし、発生する可能性があるエラーを **[ドメイン管理]** の **[ドメイン値]** ページに表示することができます。 これには、スペル チェックを実行する言語の指定が含まれます。  
  
-   データ型が文字列で、構文エラーが文字列で発生しないことがわかっている場合は、DQS が構文エラーを識別しないように指定できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 ドメインを使用すると、次の操作を実行できます。  
  
|||  
|-|-|  
|特定のデータ型を持つデータ フィールドのセマンティック表現を作成し、ドメインの作成方法を指定して、ドメインの出力形式を設定する|[ドメインを作成する](../../2014/data-quality-services/create-a-domain.md)|  
|ドメインを別のドメインにリンクして、ドメインが同じ設定と値を共有できるようにする|[リンク ドメインを作成する](../../2014/data-quality-services/create-a-linked-domain.md)|  
|参照データ サービスを単一または複合ドメインにアタッチする|[参照データにドメインまたは複合ドメインをアタッチする](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)|  
|ナレッジ ベース内の値を変更または拡張する|[ドメイン値を変更する](../../2014/data-quality-services/change-domain-values.md)|  
|検証と標準化の規則を使用する|[ドメイン ルールを作成する](../../2014/data-quality-services/create-a-domain-rule.md)|  
|リレーションを使用してドメインの値の一部である用語を修正する|[用語ベースのリレーションを作成する](../../2014/data-quality-services/create-term-based-relations.md)|  
|ドメイン管理アクティビティを完了、終了、またはキャンセルする|[ドメイン管理アクティビティの終了](../../2014/data-quality-services/end-the-domain-management-activity.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|ナレッジ検出を実行し、対話方式でナレッジを管理して、ナレッジ ベースを構築します。|[ナレッジ ベースの作成](../../2014/data-quality-services/building-a-knowledge-base.md)|  
|ナレッジをナレッジ ベースにインポートするか、ナレッジ ベースからナレッジをエクスポートします。|[ナレッジのインポートとエクスポート](../../2014/data-quality-services/importing-and-exporting-knowledge.md)|  
|複合ドメインを作成し、ナレッジをドメインに追加します。|[複合ドメインの管理](../../2014/data-quality-services/managing-a-composite-domain.md)|  
  
  
