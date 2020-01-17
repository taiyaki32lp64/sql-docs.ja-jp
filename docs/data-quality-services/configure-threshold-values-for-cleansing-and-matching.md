---
title: クレンジングと照合のしきい値の構成
description: SQL Server Data Quality Services (DQS) でコンピューター支援型のクレンジングおよび照合アクティビティを実行するときに使用されるしきい値を構成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 4fcbc8e4e6d6a9c1df07d8e1b1aa68c08c162817
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557894"
---
# <a name="configure-threshold-values-for-cleansing-and-matching---data-quality-services-dqs"></a>クレンジングと照合のしきい値を構成する-Data Quality Services (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、コンピューター支援型のクレンジングおよび照合アクティビティの最中に [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) で使用されるしきい値を構成する方法について説明します。  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 これらのしきい値を構成するには、DQS_MAIN データベースの dqs_administrator ロールが必要です。  
  
##  <a name="Configure"></a>しきい値の構成  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で **[構成]** をクリックします。  
  
3.  次に、[**全般設定**] タブをクリックします。このタブでは、クレンジングおよび照合アクティビティのしきい値を指定できます。  
  
4.  クレンジング アクティビティのしきい値を指定するには、 **[インタラクティブなクレンジング]** の下の次のボックスに適切な値を指定します。  
  
    -   **提案の最小スコア**: コンピューター支援型のクレンジングプロセスで、値の置換を提案するために DQS によって使用される最小スコアまたは信頼レベルです。 割合値に相当する値を 10 進数表記で入力します。 たとえば、75% であれば「0.75」と入力します。 この値は **[自動修正の最小スコア]** ボックスに指定した値以下である必要があります。 既定値は 0.7 です。  
  
    -   **自動修正の最小スコア**: コンピューター支援型のクレンジングプロセスで自動的に値を修正するために DQS によって使用される最小スコアまたは信頼レベルです。 割合値に相当する値を 10 進数表記で入力します。 たとえば、90% であれば「0.9」と入力します。 既定値は 0.8 です。  
  
5.  照合アクティビティのしきい値を指定するには、 **[照合]** の下の **[最小レコード スコア]** ボックスに適切な値を指定します。 この値は、あるレコードが別のレコードと一致すると見なされる最小スコアを表します。 既定値は 80% です。  
  
6.  [**閉じる**] をクリックします。  
  
  
