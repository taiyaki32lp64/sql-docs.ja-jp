---
title: Data Quality Services の概要 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- Domains
ms.assetid: 5350214c-7333-41d0-ae83-1b7d8454ebec
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 19ef3eacc2fc1dbe6408ea1b51c5135ba37740e5
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154469"
---
# <a name="introduction-to-data-quality-services"></a>Data Quality Services の概要
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) で提供されているデータ品質ソリューションを使用すると、データ スチュワードまたは IT プロフェッショナルは、データの品質を維持し、データをビジネス使用に適したものにすることができます。 DQS は、データ ソースの整合性と品質を管理する、コンピューター支援型のインタラクティブなナレッジ ドリブン ソリューションです。 DQS を利用すると、データについてのナレッジを発見し、構築して、管理できます。 その後、そのナレッジを使用して、データのクレンジング、マッチング、プロファイリングを実行できます。 また、DQS データ品質プロジェクトに含まれる参照データ プロバイダーのクラウド ベースのサービスを利用することもできます。  
  
##  <a name="BusinessNeed"></a> DQS に関するビジネス ニーズ  
 不正確なデータの原因として、ユーザーの入力エラー、転送または格納時の破損、データ辞書定義の不一致、データ品質およびデータ処理に関するその他の問題などが考えられます。 異なるデータ標準を使用する異なるソースからデータを集計すると、任意のルールが適用されたり履歴データが上書きされたりして、データの一貫性が損なわれる可能性があります。 不正確なデータは、業務の遂行や顧客へのサービス提供に影響を及ぼして、信頼性や収益の損失、顧客の不満足、コンプライアンスの問題につながります。 システムが自動化されている場合、不正確なデータでは機能しないこともあり、手動で処理を実行する時間と労力の浪費になります。 誤ったデータは、データ解析、レポート作成、データ マイニング、データ ウェアハウスに大混乱をもたらす可能性があります。  
  
 企業や公共機関の効率性を確保するためには高品質なデータが非常に重要です。 どのような規模の組織でも、DQS を使用することで、データの情報価値を高め、データを使用目的にいっそう適したものにすることができます。 データ品質ソリューションは、データの信頼性、アクセス可能性、再利用可能性を高めることができます。 データの完全性、正確性、適合性、整合性を向上させ、ビジネス インテリジェンスやデータ ウェアハウスのワークロードおよび稼働状態の OLTP システムにおいて不適切なデータによって発生する問題を解決できます。  
  
 DQS を利用すると、データベースの専門家やプログラマでないビジネス ユーザー、インフォメーション ワーカー、IT プロフェッショナルが、最小限のセットアップで (つまり、準備にかかる時間を最小限に抑えて)、組織のデータの品質に関する操作を作成、管理、および実行できます。  
  
##  <a name="Answer"></a>DQS を使用したニーズへの回答  
 データ品質を絶対的に定義する用語はありません。 データ品質は、データが意図された目的に対して適切かどうかに依存します。 DQS は、正しくない可能性のあるデータを識別し、データが実際に正しくない可能性の評価を提供します。 DQS は、ユーザーがデータの妥当性を判断できるように、データのセマンティックな理解を提供します。 DQS を利用することで、不完全性、適合性の欠如、矛盾、不正確、無効、およびデータ重複に関連する問題を解決できます。  
  
 DQS は、データ品質の問題を解決するための以下の機能を備えています。  
  
-   **データ クレンジング:** コンピューター支援型と対話形式の両方のプロセスを使用して、不正確または不完全なデータを修正、削除、補強します。 詳細については、「 [Data Cleansing](../../2014/data-quality-services/data-cleansing.md)」をご参照ください。  
  
-   **マッチング:** 一致を構成するものを決定して重複除去を実行できるようにするルール ベースのプロセスで、セマンティックな重複を識別します。 詳細については、「 [Data Matching](../../2014/data-quality-services/data-matching.md)」をご参照ください。  
  
-   **参照データ サービス:** 参照データ プロバイダーのサービスを使用して、データの品質を検証します。 Azure Marketplace DataMarket の参照データサービスを使用して、データのクレンジング、検証、照合、および強化を簡単に行うことができます。 詳細については、「 [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md)」をご覧ください。  
  
-   **プロファイリング:** ナレッジ発見、ドメイン管理、マッチング、データ クレンジングの各プロセスのすべてのステージにおいて、データ ソースを分析してデータの品質の内部状況がわかる情報を提供します。 プロファイリングは DQS データ品質ソリューションの強力なツールです。 ナレッジ管理、マッチング、データ クレンジングと同程度にプロファイリングが重要性を持つデータ品質ソリューションを作成できます。 詳細については、「 [Data Profiling and Notifications in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md)」をご参照ください。  
  
-   **監視:** データ品質活動の状態を追跡して特定します。 監視により、データ品質ソリューションが設計意図のとおりに動作していることを確認できます。 詳細については、「 [DQS Administration](../../2014/data-quality-services/dqs-administration.md)」をご参照ください。  
  
-   **ナレッジ ベース:** Data Quality Services は、DQS で構築されたナレッジに基づいてデータを分析するナレッジ ドリブン ソリューションです。 これにより、データについてのナレッジを継続的に拡充し、それによってデータの品質を継続的に向上させる、データ品質プロセスを作成できます。  
  
 次の図は DQS のプロセスを示したものです。  
  
 ![DQS プロセス](../../2014/data-quality-services/media/dqs-process.gif "DQS プロセス")  
  
##  <a name="KnowledgeDrivenSolution"></a> ナレッジ ドリブン ソリューション  
 DQS のナレッジ ベースは、3 種類のナレッジ (そのままの状態のナレッジ、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]によって生成されるナレッジ、ユーザーが生成するナレッジ) のリポジトリです。 DQS を使用すると、データに関するナレッジをナレッジ ベースに格納し、ビジネス ルールを追加し、必要に応じてナレッジを修正した後、それを適用してデータの整合性と正確性をテストできます。 ナレッジ ベースを構築した後は、継続的に改善し、複数のデータ品質向上プロセスで再利用できます。  
  
 ナレッジ ベース内のナレッジは、正しくない可能性のあるデータを識別し、データの変更を提案します。 データの一致を発見して、ユーザーがデータ重複除去を実行できるようにします。 DQS では、データ品質プロバイダーによって保守および保証されているクラウド ベースの参照データとソース データを比較できます。 データ スチュワードまたは IT プロフェッショナルは、ナレッジ ベース内のナレッジと、データに対する変更の両方を検証し、クレンジング、重複除去、および参照データ サービスを実行します。  
  
 1 つのナレッジ ベースは、特定の種類のデータ ソースに関するすべてのナレッジを格納します。 たとえば、顧客データベースと従業員データベースを個別のナレッジ ベースで管理できます。 ナレッジは、それぞれがデータ フィールド内の 1 つのデータ型のセマンティック表現である、1 つまたは複数のデータ ドメインに格納されています。 顧客データベースのナレッジ ベースは、会社名、住所、連絡先、連絡先情報などのドメインを持つ可能性があります。 ドメインには、信頼できる値、無効な値、およびエラーを生じるデータの一覧が含まれます。 ドメインのナレッジには、シノニムの関連付け、用語の関係、検証とビジネス ルール、および一致ポリシーが含まれます。 データ スチュワードは、このナレッジを有効活用することで、ドメイン内の値の特定のインスタンスを修正するかどうかという判断を情報に基づいて行うことができます。  
  
 DQS では、ナレッジ ベースに関するインポートおよびエクスポート操作を実行できます。 DQS ファイルを使用してドメインまたはナレッジ ベースをインポートまたはエクスポートできます。 Excel ファイルから値またはドメインをインポートできます。 また、ナレッジ ベースに基づくクレンジング プロセスによって発見された値を、インポートしてドメインに戻すこともできます。 これらの操作により、継続的にナレッジ ベースを改善し、決定と発見によって得られたナレッジをナレッジ ベースに還元できます。  
  
 DQS ナレッジ ベース ソリューションでは、データ クレンジングに 2 段階の基本的な手順を使用します。  
  
-   **ナレッジ マネージメント** プロセス (ナレッジ ベースの構築)  
  
-   **データ品質プロジェクト** (ナレッジ ベースのナレッジに基づいたソース データに対する変更内容の提示)  
  
 詳しくは、「[DQS のナレッジ ベースとドメイン](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)」および「[データ品質プロジェクト &#40;DQS&#41;](../../2014/data-quality-services/data-quality-projects-dqs.md)」をご覧ください。  
  
##  <a name="Components"></a> DQS のコンポーネント  
 Data Quality Services は [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] と [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]で構成されます。 これらのコンポーネントにより、他の SQL Server 操作と切り離して Data Quality Services を実行できます。 どちらも、SQL サーバー セットアップ プログラム内からインストールされます。  
  
 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] は、SQL Server Management Studio で管理および監視できる 3 つの SQL Server カタログ (DQS_MAIN、DQS_PROJECTS、DQS_STAGING_DATA) として実装されます。 DQS_MAIN には、DQS ストアド プロシージャ、DQS エンジン、パブリッシュ済みナレッジ ベースが含まれています。 DQS_PROJECTS には、ナレッジ ベース管理と DQS プロジェクト アクティビティに必要なデータが格納されます。 DQS_STAGING_DATA は、ソース データをコピーし、DQS 操作を実行して処理後のデータをエクスポートするための中間的なステージング データベースを提供します。  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] はスタンドアロン アプリケーションであり、ナレッジ管理、データ品質プロジェクト、および管理を 1 つのユーザー インターフェイスで実行できます。 アプリケーションはデータ スチュワードと DQS 管理者の両方のために設計されています。 ナレッジ検出、ドメイン管理、マッチング ポリシー作成、データ クレンジング、マッチング、プロファイリング、監視、サーバー管理を実行するスタンドアロンの実行可能ファイルです。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] は、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] と同じコンピューターにインストールして実行することも、別のリモートのコンピューターにインストールして実行することもできます。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] の多くの操作は、使用しやすいようにウィザード ドリブンになっています。  
  
##  <a name="Processes"></a> Integration Services およびマスター データ サービスでのデータ品質機能  
 Data Quality Services で提供されるデータ品質機能は、SQL Server Integration Services (SSIS) のコンポーネントおよびマスター データ サービス (MDS) の機能に組み込まれており、これらのサービス内でデータ品質プロセスを実行できます。  
  
 **[!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]**  
  
 [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)] は、Integration Services パッケージの一部としてデータ クレンジングを実行できるようにします。 パッケージを実行すると、データ クレンジングがバッチ ファイルとして実行されます。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションでクレンジング プロジェクトを実行する代わりに、これを使用できます。 データの品質を自動的に保証できます。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーション内でデータ クレンジング プロジェクトの対話手順を実行する必要はありません。 他の Integration Services コンポーネントを含むデータ フローにデータ クレンジング プロセスを組み込むことができます。 詳細については、「[DQS クレンジング変換](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)」を参照してください。  
  
 **マスター データ サービスのデータ品質プロセス**  
  
 Data Quality Services の機能はマスター データ サービス (MDS) に統合されているので、Microsoft Excel 用 Microsoft SQL Server 2014 Master Data Services アドインでソース データおよびマスター データに対して重複除去を実行できます。 マッチングを実行するには、MDS によって管理されているデータを Excel ワークシートに読み込み、MDS によって管理されていないデータと結合してから、Excel 内でマッチングを実行します。 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] コンポーネントを MDS と共にインストールする必要があります。 詳細については、「  [Excel 用 MDS アドインでのデータ品質照合](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server 2014 の各エディションがサポートする機能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
