---
title: クロス ドメイン ルールの作成
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.testcdrule.f1
- sql13.dqs.dm.cdrules.f1
ms.assetid: 0f3f5ba4-cc47-4d66-866e-371a042d1f21
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 070ef5db87ac28b59f01e3927f876f9c757e6caa
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245468"
---
# <a name="create-a-cross-domain-rule"></a>クロス ドメイン ルールの作成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でナレッジ ベースの複合ドメインに対するクロス ドメイン ルールを作成する方法について説明します。 クロス ドメイン ルールとは、複合ドメインに含まれる単一ドメインの値の間の関係をテストするルールです。 ドメイン値が正確で、ビジネス要件に準拠していると見なされるためには、クロス ドメイン ルールが複合ドメイン全体に当てはまる必要があります。 クロス ドメイン ルールは、ドメイン値の検証、修正、および標準化のために使用されます。  
  
 クロス ドメイン ルールの If 句と Then 句は、それぞれ複合ドメイン内の 1 つの単一ドメインに対して定義されます。 それぞれの句を異なる単一ドメインに対して定義する必要があります。 クロス ドメイン ルールは、複数の単一ドメインに関連付ける必要があります。複合ドメインに対して単純なドメイン ルール (単一ドメインのみに対するルール) を定義することはできません。 そのため、単一ドメインに対してドメイン ルールを定義します。 If 句と Then 句のそれぞれに 1 つ以上の条件を含めることができます。  
  
 クロス ドメイン ルールに明確な条件が含まれている場合、その条件では、特定の値だけでなくその値のシノニムにもルールのロジックが適用されます。 If 句と Then 句の明確な条件とは、"値が次の値と等しい"、"値が次の値と等しくない"、"値が次の中に存在する"、または "値が次の中に存在しない" です。 たとえば、複合ドメインに対する "For 'City', if Value is equal to 'Los Angeles', then for 'State', Value is equal to 'CA'" というクロス ドメイン ルールについて考えます。 'Los Angeles' と 'LA' がシノニムであれば、'Los Angeles CA' と 'LA CA' は正しくなり、'Los Angeles WA' と 'LA WA' はエラーになります。  
  
 クロス ドメイン ルールの明確な *Then* 句の **"値が次の値と等しい"** では、単にクロス ドメイン ルールの有効性について知らせるだけでなく、データ クレンジング アクティビティ中にデータの修正も行います。 詳細については、「 [Cleanse Data in a Composite Domain](../data-quality-services/cleanse-data-in-a-composite-domain.md#CDCorrection) 」の「 [Data Correction using Definitive Cross-Domain Rules](../data-quality-services/cleanse-data-in-a-composite-domain.md)」を参照してください。  
  
 クロス ドメイン ルールは、単一ドメインのみに影響するすべての単純なルールの後に考慮されます。 値が単一ドメインのルールに適合する場合しか、クロス ドメイン ルールは適用されません。 ルールの対象となる複合ドメインと単一ドメインはすべて、ルールを実行する前に定義されている必要があります。  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Prerequisites"></a>応募  
 クロス ドメイン ルールを作成するには、複合ドメインを作成して開いておく必要があります。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 クロス ドメイン ルールを作成するには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="Create"></a>クロスドメインルールの作成  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、ナレッジ ベースを開くか作成します。 アクティビティとして **[ドメイン管理]** を選択した後に、 **[開く]** または **[作成]** をクリックします。 詳細については、「 [ナレッジ ベースの作成](../data-quality-services/create-a-knowledge-base.md) 」または「 [ナレッジ ベースを開く](../data-quality-services/open-a-knowledge-base.md)」を参照してください。  
  
    > [!NOTE]  
    >  Data Quality Service クライアントのドメイン管理用のページには、それぞれ異なるドメイン管理操作に対応する 5 つのタブが含まれています。 ウィザード ベースのプロセスではないため、任意の管理操作を個別に実行することができます。  
  
3.  
  **[ドメイン管理]** ページの **[ドメイン リスト]** から、ドメイン ルールを作成する複合ドメインを選択するか、新しい複合ドメインを作成します。 新しいドメインを作成する必要がある場合は、「 [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)」を参照してください。  
  
4.  
  **[CD のルール]** タブをクリックします。  
  
5.  
  **[新しいドメイン ルールの追加]** をクリックし、ルールの名前と説明を入力します。  
  
6.  ルールが実行されるようにする場合は、 **[アクティブ]** を選択します (既定値)。実行されないようにする場合は選択を解除します。  
  
7.  次の手順に従って If 句を作成します。  
  
    1.  If 句のペインのドメイン リストで、複合ドメインに含まれている単一ドメインの中から、If 句の対象にする単一ドメインを 1 つ選択します。 複合ドメイン内の任意の単一ドメインを選択できます。  
  
    2.  句の最初の条件のドロップダウン リストから条件を選択します。  
  
    3.  条件に値が必要な場合は、条件に対応するテキスト ボックスに値を入力します。  
  
    4.  If 句に別の条件が必要な場合は、 **[選択した句に新しい条件を追加]** をクリックします。 演算子と条件を選択し、必要に応じて条件の値を入力します。  
  
    5.  条件の順序を変更するには、条件の左側をクリックして選択し、上矢印または下矢印をクリックします。  
  
    6.  条件を非表示にするには、ドメイン名の左にあるマイナス記号をクリックします。 条件を表示するには、プラス記号をクリックします。  
  
8.  Then 句のペインのドメイン リストで If 句の対象以外の単一ドメインを選択し、Then 句を作成します。 Then 句の作成手順は If 句の作成手順と同じです。  
  
9. 以下のテストの手順に進みます。  
  
##  <a name="Test"></a>クロスドメインルールのテスト  
  
1.  次の手順に従ってクロス ドメイン ルールをテストします。  
  
    1.  複合ドメインのペインの右上隅にある **[テスト データについて選択したドメイン ルールを実行します]** アイコンをクリックします。  
  
    2.  
  **[ドメイン ルールのテスト]** ダイアログ ボックスで、 **[ドメイン ルールの新しいテスト用語を追加]** アイコンをクリックします。  
  
    3.  If 句に関連付けられている単一ドメインと Then 句に関連付けられている単一ドメインのそれぞれについて、テスト値を入力します。 If 句に入力したテスト値は、その句の条件を満たす必要があります。条件を満たさない場合、 **[有効性]** 列に疑問符が表示され、クロス ドメイン ルールがテスト データに適用されません。  
  
    4.  
  **[ドメイン ルールの新しいテスト用語を追加]** アイコンをもう一度クリックして、別の一連のテスト値を追加します。  
  
    5.  [**すべての用語でドメインルールをテスト**する] アイコンをクリックします。 一連のテスト値が有効な場合は、その行の **[有効性]** 列にチェック マークが表示されます。 一連のテスト値が有効でない場合は、その行の [有効性] 列に感嘆符付きの三角形が表示されます。  
  
    6.  テストが完了したら、 **[複合ドメイン ルールのテスト]** ダイアログ ボックスの **[閉じる]** をクリックします。  
  
2.  クロス ドメイン ルールが完成したら、 **[完了]** をクリックし、「 [End the Domain Management Activity](https://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)」の説明に従ってドメイン管理アクティビティを完了します。  
  
##  <a name="FollowUp"></a>補足情報: クロスドメインルールを作成した後  
 クロス ドメイン ルールを作成した後、ドメインで他のドメイン管理タスクを実行したり、ナレッジ検出を実行してナレッジをドメインに追加したり、照合ポリシーをドメインに追加することができます。 詳しくは、「[ナレッジ検出の実行](../data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」、または「[照合ポリシーの作成](../data-quality-services/create-a-matching-policy.md)」をご覧ください。  
  
  
