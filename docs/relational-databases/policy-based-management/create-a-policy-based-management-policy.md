---
title: ポリシー ベースの管理ポリシーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policies
ms.assetid: b28bf963-89f9-4941-b6c1-6004fec347f1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cd95caaa746204084c0d4748cd8bb20fede39f9a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907180"
---
# <a name="create-a-policy-based-management-policy"></a>ポリシー ベースの管理ポリシーの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でポリシー ベースの管理ポリシーを作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してポリシーを作成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-policy"></a>ポリシーを作成するには  
  
1.  **オブジェクト エクスプローラー**で、プラス記号をクリックして、新しいポリシー ベースの管理ポリシーを作成するサーバーを展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  **[ポリシー]** フォルダーを右クリックし、 **[新しいポリシー]** をクリックします。  
  
5.  **[新しいポリシーの作成]** ダイアログ ボックスで、 **[名前]** ボックスに、新しいポリシーの名前を入力します。  
  
6.  作成されたポリシーを直ちに有効にする場合は、 **[有効]** チェック ボックスをオンにします。 評価モードが **[要求時]** である場合、 **[有効]** チェック ボックスは使用できません。  
  
7.  **[条件の確認]** ボックスの一覧で、既存の条件の 1 つを選択するか、 **[新しい条件]** をクリックします。 条件を編集するには、条件を選択し、省略記号ボタン ( **[...]** ) をクリックします。詳細については、「 [新しいポリシー ベースの管理条件の作成](../../relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) 」または「 [ポリシー ベースの管理条件のプロパティの表示または変更](../../relational-databases/policy-based-management/view-or-modify-the-properties-of-a-policy-based-management-condition.md)」を参照してください。  
  
8.  **[対象]** ボックスで、このポリシーの対象になる種類を 1 つ以上選択します。 一部の条件とファセットは、特定の種類の対象にしか適用できません。 使用可能な対象セットが、関連するボックスに表示されます。 **[すべて]** を展開して、一部の種類の対象に対してフィルター条件を選択します。 対象がこのボックスに表示されていない場合、条件の確認がサーバー レベルのスコープを持っています。  
  
9. **[評価モード]** ボックスで、このポリシーの動作を選択します。 有効な評価モードは、条件によって異なります。 どの評価モードが有効かの詳細については、「 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)」を参照してください。  
  
10. ポリシーをスケジュールで評価する場合は、評価モードを **[スケジュールで実行]** に設定し、 **[選択]** をクリックしてスケジュールを選択するか、 **[新規作成]** をクリックして新しいスケジュールを作成します。  
  
11. ポリシーを対象の種類のサブセットに制限するには、 **[サーバーの制限]** ボックスで制限条件を選択するか、新しい条件を作成します。  
  
     **[新しいポリシーの作成]** ダイアログ ボックスで使用可能なオプションの詳細については、「 [[新しいポリシーの作成] または [ポリシーを開く] ダイアログ ボックスの [全般] ページ](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) 」または「 [[新しいポリシーの作成] または [ポリシーを開く] ダイアログ ボックスの [説明] ページ](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md)」を参照してください。  
  
12. 完了したら、 **[OK]** をクリックします。  

