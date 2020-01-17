---
title: Data Quality Services の概念 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 837c71ee-48fa-4044-8744-2be9119aaa04
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6f1cba6a6a20fc804d29aeb0dbf43d7bebfbb225
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154456"
---
# <a name="data-quality-services-concepts"></a>Data Quality Services の概念
  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) のナレッジ マネージメント、データ品質プロジェクト、およびデータ品質管理の概念を簡単に説明します。  
  
##  <a name="Knowledge"></a> ナレッジ マネージメントの概念  
 DQS のナレッジ ベースは、データ クレンジングやデータ照合を通じてデータの品質を向上させるために使用される、データ スチュワードまたは IT プロフェッショナルが作成するメタデータのリポジトリです。 DQS のナレッジ マネージメントには、ナレッジ ベースを作成および管理するためのコンピューター支援型のプロセスと対話形式のプロセスが含まれます。  
  
 **ナレッジの検出**  
  
 ナレッジ検出は、組織のデータのサンプルを分析してデータに関するナレッジを構築するコンピューター支援型のプロセスです。 この分析の結果に基づいて、ナレッジを検証および強化し、それを適用してデータのクレンジング、照合、プロファイルを行うことができます。 詳細については、「 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)」をご覧ください。  
  
 **ドメインの管理**  
  
 ドメイン管理プロセスでは、ナレッジ検出プロセスで生成されたナレッジを変更したり拡張したりできます。 ナレッジ ベースのナレッジは対話形式で編集、更新、確認できます。 ナレッジ ベースは、ドメインの値とその状態、ドメイン ルール、用語ベースのリレーション、および参照データを含むデータ ドメインで構成されます。 ドメイン管理では、ドメインのプロパティの変更、ドメインへの参照データのアタッチ、ドメイン ルールの管理、ドメイン値の管理、データのリレーションの入力、ドメインの作成、削除、インポート、エクスポートを行うことができます。 また、複数の単一ドメインをまとめた複合ドメインを使用することもできます。 詳細については、「 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)」をご覧ください。  
  
 **[照合ポリシー]**  
  
 照合ポリシーには、データ重複除去の実行に使用される照合ルールが含まれます。 照合ポリシー プロセスでは、照合ルールを作成し、照合結果やプロファイル データに基づいてそれらを調整したり、ナレッジ ベースにポリシーを追加したりできます。 詳細については、「 [データ照合](../../2014/data-quality-services/data-matching.md)」をご覧ください。  
  
 **参照データ サービス**  
  
 参照データを使用すると、参照データの品質を保証する企業のサービスを利用して、データを検証、修正、および強化することができます。 Azure Marketplace のサービスを使用して参照データプロバイダーに接続することも、プロバイダーへの直接接続を使用することもできます。 詳細については、「 [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md)」をご覧ください。  
  
 DQS のナレッジ マネージメントの詳細については、「 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)」をご覧ください。  
  
##  <a name="Projects"></a> データ品質プロジェクトの概念  
 データ スチュワードは、データ品質に関する操作 (クレンジングおよび照合) を [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションでデータ品質プロジェクトを使用して実行します。  
  
 **データ クレンジング**  
  
 DQS でのデータ クレンジングは、DQS ナレッジ ベースのナレッジに基づいて行われます。 DQS のデータ クレンジングは、2 段階のプロセスから成ります。  
  
-   **コンピューター支援型のクレンジング**: DQS では、クレンジング プロジェクト用に選択したナレッジ ベースのナレッジを使用して、データ ソースの値に対する修正または提案を提示します。  
  
-   **インタラクティブなクレンジング**: データ スチュワードは、インタラクティブなクレンジング プロセスを実行して、コンピューター支援型のデータ クレンジング プロセスで提示されたデータ修正を変更したり拡張したりできます。 このプロセスでは、データ クレンジング プロセスで識別された信頼レベルや統計情報を使用することも、プロジェクトにおける独自の変更を手動で入力することもできます。  
  
 データ クレンジングの後で、データ スチュワードは、処理されたデータを SQL Server データベース、.csv ファイル、または Excel ファイルにエクスポートできます。 詳細については、「 [Data Cleansing](../../2014/data-quality-services/data-cleansing.md)」をご覧ください。  
  
 **データ照合**  
  
 データ スチュワードは、照合プロセスを使用して、わずかに異なる類似データを重複除去プロセスで調整できるようにデータを比較することができます。 DQS により、ナレッジ ベースに格納された照合ルールに基づいて重複除去が実行されます。照合プロセスのパラメーターは、データ スチュワードがデータ品質プロジェクトから指定します。 詳しくは、「 [Data Matching](../../2014/data-quality-services/data-matching.md)」をご覧ください。  
  
 **プロファイルと通知**  
  
 データ プロファイリングでは、データ品質プロジェクト実行中のクレンジングおよび照合アクティビティのために DQS で処理されているデータに関する統計と情報が、データ スチュワードに対してリアルタイムに表示されます。 データ プロファイルは、データ品質プロジェクトのクレンジングおよび照合アクティビティの有効性を評価するときに役立ちます。通知は、ユーザーがデータ クレンジングおよびデータ照合アクティビティを拡張する手段として使用できます。 詳細については、「 [Data Profiling and Notifications in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md)」をご参照ください。  
  
 DQS のデータ品質プロジェクトについて詳しくは、「[データ品質プロジェクト &#40;DQS&#41;](../../2014/data-quality-services/data-quality-projects-dqs.md)」をご覧ください。  
  
##  <a name="Admin"></a> データ品質管理の概念  
 DQS 管理者は、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションを使用して、さまざまな管理タスクを実行できます。  
  
 **[アクティビティ監視]**  
  
 アクティビティ監視では、データ範囲内で実行された各アクティビティの状態が表示され、DQS 管理者は各アクティビティのデータを確認しながらアクティビティを制御することができます。 詳細については、「 [Monitor DQS Activities](../../2014/data-quality-services/monitor-dqs-activities.md)」をご覧ください。  
  
 **Configuration**  
  
 構成オプションでは、次の操作を実行できます。  
  
-   参照データ サービスの設定を構成する。 詳細については、「 [Configure DQS to Use Reference Data](../../2014/data-quality-services/configure-dqs-to-use-reference-data.md)」をご覧ください。  
  
-   クレンジングおよび照合アクティビティのしきい値を設定する。 詳細については、「 [クレンジングと照合のしきい値の構成](../../2014/data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)」をご参照ください。  
  
-   プロファイル通知を有効または無効にする。 詳しくは、「[DQS のプロファイル通知の有効化または無効化](../../2014/data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)」をご覧ください。  
  
-   アクティビティ ベース レベルまたはより詳細なモジュール ベース レベルで、DQS ログ ファイルの重大度レベルを構成する。 詳細については、「 [Configure Severity Levels for DQS Log Files](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md)」をご覧ください。  
  
 **DQS セキュリティ**  
  
 DQS のセキュリティの設定には、SQL Server のセキュリティ メカニズムのロールを使用します。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションにおけるユーザーのアクセス レベルを決定する、3 つの DQS ロール (dqs_administrator、dqs_kb_editor、および dqs_kb_operator) があります。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションを使用して、ユーザーにロールを付与することはできません。SQL Server Management Studio を使用して行います。 詳細については、「 [DQS Security](../../2014/data-quality-services/dqs-security.md)」をご覧ください。  
  
 DQS 管理の詳細については、「 [DQS Administration](../../2014/data-quality-services/dqs-administration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Data Quality Services](../../2014/data-quality-services/data-quality-services.md)  
  
  
