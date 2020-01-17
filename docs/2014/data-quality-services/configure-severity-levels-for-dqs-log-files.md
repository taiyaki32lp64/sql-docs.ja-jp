---
title: DQS ログ ファイルの重大度レベルの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.admin.config.log.f1
helpviewer_keywords:
- severity levels
- log files,severity levels
- dqs log files,severity levels
- logging,severity levels
- configure severity levels
ms.assetid: 66ffcdec-4bf7-4dd5-a221-fd9baefeeef4
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4aeffaf9098e2476db4a0faf95811f3ea5204aaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480924"
---
# <a name="configure-severity-levels-for-dqs-log-files"></a>DQS ログ ファイルの重大度レベルの構成
  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] を使用して [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)](DQS) の各種のアクティビティやモジュールの重大度レベルを構成する方法について説明します。 重大度レベルとは、DQS で発生するイベントの重大度を定義したものです。 DQS のイベントの重大度レベルは次のとおりです。ここでは、重大度が高いものから順に示しています。  
  
-   **Fatal**: 予期しない深刻な結果を引き起こす可能性がある重大な実行時エラー。  
  
-   **Error**: その他の実行時エラー。  
  
-   **Warn**: エラーの原因になる可能性があるイベントに関する警告。  
  
-   **Info**: エラーまたは警告以外の一般的なイベントに関する情報。 (DQS のプロセスが開始されたなど)。  
  
-   **Debug**: イベントに関する詳細な情報。  
  
 DQS の各種のアクティビティやモジュールの重大度レベルを構成することで、DQS の対応するアクティビティやモジュールについて、DQS ログ ファイルに書き込む情報をフィルター処理できます。 たとえば、DQS のアクティビティの重大度レベルを **Warn**に設定すると、DQS のアクティビティに関連するメッセージのうち、警告メッセージとそれよりも重大度が高いメッセージ (Error と Fatal) だけがログに記録されます。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 ログの重大度設定を構成するには、DQS_MAIN データベースの dqs_administrator ロールが必要です。  
  
##  <a name="ConfigureActivity"></a> アクティビティ レベルでの重大度レベルの構成  
 DQS のドメイン管理、ナレッジ検出、照合ポリシー、データ クレンジング、データ照合、および参照データ サービスの各アクティビティについて、ログの重大度設定を構成することができます。 そのためには次を行います。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)]「[Data Quality Client アプリケーションの実行](../../2014/data-quality-services/run-the-data-quality-client-application.md)」をご覧ください。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で **[構成]** をクリックします。  
  
3.  次に **[ログの設定]** タブをクリックします。重大度レベルを選択できる DQS のアクティビティ ( **[ドメイン管理]** 、 **[ナレッジ検出]** 、 **[プロジェクトのクレンジング (例: RDS)]** 、 **[一致するポリシーと一致するプロジェクト]** 、および **[RDS]** ) が表示されます。  
  
4.  DQS のアクティビティについて、ログに記録する重大度レベルを選択します。 レベルとして **[Fatal]** 、 **[Error]** 、 **[Warn]** 、 **[Info]** 、 **[Debug]** のいずれかを選択できます。 たとえば、ナレッジ検出アクティビティに対する重大なメッセージだけを DQS ログ ファイルに書き込む場合は、 **[ナレッジ検出]** アクティビティのドロップダウン リストで **[Fatal]** を選択します。  
  
    > [!NOTE]  
    >  既定では、各アクティビティについて **[Error]** が選択されています。 つまり、既定では、各アクティビティのエラー メッセージと重大なメッセージが DQS ログ ファイルに書き込まれます。  
  
5.  **[閉じる]** をクリックします。  
  
##  <a name="ConfigureModule"></a> モジュール レベルでの重大度レベルの構成 (上級者向け)  
 **[ログの設定]** タブの **[詳細設定]** セクションでは、モジュール レベルでログの重大度設定を構成することができます。 モジュールとは、DQS の機能に含まれる個々の機能を実装する DQS システムのアセンブリです。 たとえば、ドメイン管理アクティビティには、ドメイン ルールの定義、ルールの条件の定義、複合ドメインのクロス ドメイン ルールの定義など、さまざまな機能が含まれています。  
  
 アクティビティ レベルよりも詳しい調査が必要なときは、 アクティビティ内の特定のモジュールで発生している問題を調べることができます。 モジュール レベルでログの重大度を構成することで、問題をより正確に切り分けて追跡することができます。  
  
 アクティビティ レベルで指定したログの重大度設定によって、そのアクティビティを構成するすべてのモジュールのログの重大度設定が決まります。 ただし、アクティビティ レベルとモジュール レベルでログの重大度設定が異なる場合は、モジュール レベルの重大度設定が使用されます。  
  
> [!NOTE]
>  -   既定では、 **[詳細設定]** セクションで **Microsoft.Ssdqs.Core.Startup** モジュールが事前に構成されており、重大度レベルは **[Info]** に設定されています。 この設定により、DQS のサービスの開始と終了に関するイベントのうち、重大度が Info のイベントとそれよりも重大度が高いイベント (Warn、Error、および Fatal) がログに記録されます。  
> -   モジュール レベルでのログの重大度レベルの構成は、DQS システムのアセンブリについて理解している DQS の上級ユーザー以外にはお勧めしません。  
  
 モジュール レベルでログの重大度レベルを構成するには、次の手順を実行します。  
  
1.  **[ログの設定]** タブで、 **[詳細設定]** の下矢印をクリックして領域を表示します。  
  
2.  表示されたグリッドで、 **[モジュール]** 列のドロップダウン リストからモジュール名を選択します。  
  
3.  次に、 **[重大度]** 列のドロップダウン リストからモジュールの重大度レベルを選択します。 レベルとして **[Fatal]** 、 **[Error]** 、 **[Warn]** 、 **[Info]** 、 **[Debug]** のいずれかを選択できます。  
  
     たとえば、ドメイン管理アクティビティに含まれるドメイン ルールの定義機能に対してドメイン管理アクティビティとは異なる粒度を設定するには、 **[Microsoft.Ssdqs.DomainRules.Define]** モジュールを選択し、別の重大度レベルを選択します。 同様に、クロス ドメイン ルール機能に対して異なる粒度を設定するには、 **[Microsoft.Ssdqs.DomainRules.Condition.CrossDomain]** モジュールを選択し、別の重大度レベルを選択します。  
  
4.  必要に応じて、他のモジュールに対して手順 2. および 3. を繰り返します。 **[モジュールを追加します]** アイコンと **[モジュールを削除します]** アイコンをクリックして、グリッドの行を追加したり削除したりすることもできます。  
  
5.  **[閉じる]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [DQS ログ ファイルの詳細設定の構成](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md)  
  
  
