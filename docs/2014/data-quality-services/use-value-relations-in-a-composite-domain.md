---
title: 複合ドメインでの値のリレーションの使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.cdvaluerelations.f1
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6f6bc24d0224e31f008be0ffaf77266446c15527
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481103"
---
# <a name="use-value-relations-in-a-composite-domain"></a>複合ドメインでの値のリレーションの使用
  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) ナレッジ検出の実行中に複合ドメインで検出された値の組み合わせを表示する方法について説明します。 このページには、値の組み合わせの発生回数が示されます。 値の管理は複合ドメインでサポートされないため、これらの値に対して操作を実行することはできません。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
 値のリレーションを表示するには、複合ドメインを作成して開いておく必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 複合ドメインの値のリレーションを表示するには、DQS_MAIN データベースに対する dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="Use"></a> 値のリレーションの表示  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)]「[Data Quality Client アプリケーションの実行](../../2014/data-quality-services/run-the-data-quality-client-application.md)」をご覧ください。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、ナレッジ ベースを開くか作成します。 アクティビティとして **[ドメイン管理]** を選択した後に、 **[開く]** または **[作成]** をクリックします。 詳細については、「 [ナレッジ ベースの作成](../../2014/data-quality-services/create-a-knowledge-base.md) 」または「 [ナレッジ ベースを開く](../../2014/data-quality-services/open-a-knowledge-base.md)」を参照してください。  
  
3.  **[ドメイン管理]** ページの **[ドメイン リスト]** から、ドメイン ルールを作成する複合ドメインを選択するか、新しい複合ドメインを作成します。 新しいドメインを作成する必要がある場合は、「 [Create a Composite Domain](../../2014/data-quality-services/create-a-composite-domain.md)」を参照してください。  
  
4.  **[値のリレーション]** タブをクリックします。  
  
5.  各値の組み合わせの表示頻度を表示します。  
  
    > [!NOTE]  
    >  **"値"** テーブルには、複合ドメイン内に存在する値の各組み合わせが表示されます。 各値は、適用先の単一ドメインに表示されます。 値のリレーション テーブルの既定の並べ替えは頻度順ですが、別の列をクリックしてその列で並べ替えることができます。 頻度が 20 以上の値だけが表示されます。  
  
6.  テーブル内の値はいずれも変更できません。 その他の操作を実行している場合は、 **[完了]** をクリックし、ドメイン管理アクティビティを完了します。 それ以外の場合は、 **[キャンセル]** をクリックします。  
  
##  <a name="FollowUp"></a>補足情報: 値のリレーションを表示した後  
 値のリレーションを表示した後、ドメインで他のドメイン管理タスクを実行したり、ナレッジ検出を実行してナレッジをドメインに追加したり、照合ポリシーをドメインに追加することができます。 詳しくは、「[ナレッジ検出の実行](../../2014/data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../../2014/data-quality-services/managing-a-domain.md)」、または「[照合ポリシーの作成](../../2014/data-quality-services/create-a-matching-policy.md)」をご覧ください。  
  
  
