---
title: ポリシー ベースの管理ポリシーのインポート | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e4978471f25c1bf38d841e11f560a6bd99dac53e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705316"
---
# <a name="import-a-policy-based-management-policy"></a>ポリシー ベースの管理ポリシーのインポート
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でポリシー ベースの管理ポリシー インスタンスをインポートする方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してポリシー インスタンスをインポートするには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの監視に使用できるポリシーが用意されています。 これらのポリシーは、既定では[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]にインストールされませんが、既定の場所である C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033 からインポートできます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-import-a-policy-instance"></a>ポリシー インスタンスをインポートするには  
  
1.  **オブジェクト エクスプローラー**で、プラス記号をクリックして、新しくインポートするポリシー インスタンスを配置するサーバーを展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  **[ポリシー]** フォルダーを右クリックし、 **[ポリシーのインポート]** をクリックします。  
  
5.  **[インポート]** ダイアログ ボックスで、ファイルのパスと名前を入力します。または、参照ボタン ( **[...]** ) を使用してポリシーを含んでいる XML ファイルを特定し、ファイルを選択します。 **[インポート]** ダイアログ ボックスで利用可能なオプションの詳細については、「 [Import Policies Dialog Box](import-policies-dialog-box.md)」を参照してください。  
  
6.  完了したら、 **[OK]** をクリックします。  
  
  
