---
title: 親子型ディメンションの財務アカウントの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], account
- account dimensions [Analysis Services]
- adding account intelligence
- account intelligence [Analysis Services]
ms.assetid: 2ba74e81-5b4b-407e-acdf-deb2f6accf0a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28a7cf6b3a712144daead54d521fb3cc6936c99e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075916"
---
# <a name="create-a-finance-account-of-parent-child-type-dimension"></a>親子型ディメンションの財務アカウントの作成
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] での勘定科目ディメンションとは、財務報告用の勘定科目一覧表を表す属性を持つディメンションを指します。  
  
 勘定科目ディメンションを使用すると、勘定科目における集計動作の推移を選択的に管理できます。 また、財務データを取り扱うビジネス インテリジェンス ソリューションで一般的に発生する標準外の集計上の問題を、標準メカニズムを使用して解決できるようにもなります。 標準メカニズムがない場合、このような標準外の集計上の問題は、カスタム ロールアップ数式、計算されたメンバー、多次元式 (MDX) スクリプトなどがなければ解決できません。  
  
 ディメンションを勘定科目ディメンションとして指定するには、ディメンションの `Type` プロパティを `Accounts` に設定します。  
  
## <a name="dimension-structure"></a>[ディメンション構造]  
 勘定科目ディメンションには、少なくとも次の 2 つの属性が含まれています。  
  
-   キー属性、属性を勘定科目ディメンションのディメンション テーブル内の各アカウントを識別します。  
  
-   アカウント属性、親属性の勘定科目ディメンション内のアカウントの階層的に配置方法について説明します。  
  
     属性を勘定科目属性として指定するには、属性の `Type` プロパティを `Account` に設定し、`Usage` プロパティを `Parent` に設定します。  
  
 勘定科目ディメンションには、次の属性をオプションで含めることもできます。  
  
-   アカウントは、ディメンションの各アカウントのアカウントの種類を定義する属性、属性を入力します。 勘定科目の種類の属性のメンバー名は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のデータベースまたはプロジェクトに対して定義された勘定科目の種類にマップされ、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によってこれらの勘定科目に対して使用される集計関数を示します。 単項演算子またはカスタム ロールアップ数式を使用しても、勘定科目属性の集計動作を指定することができますが、勘定科目の種類を使用すると、基になるリレーショナル データベースを変更しなくても一貫性のある動作を勘定科目一覧表に簡単に適用できるようになります。  
  
     勘定科目の種類の属性を指定するには、属性の `Type` プロパティを `AccountType` に設定します。  
  
-   勘定科目名属性、属性レポート目的で使用されます。 勘定科目名属性を指定するには、属性の `Type` プロパティを `AccountName` に設定します。  
  
-   アカウントは、レポート目的で使用される属性、属性を番号です。 勘定科目番号属性を指定するには、属性の `Type` プロパティを `AccountNumber` に設定します。  
  
 属性の種類の詳細については、「 [属性の種類の構成](attribute-properties-configure-attribute-types.md)」を参照してください。  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>ビジネス インテリジェンス ウィザードを使用した勘定科目インテリジェンスの追加  
 勘定科目ディメンションを定義し、定義したディメンションをキューブに追加したら、ビジネス インテリジェンス ウィザードを使用して、勘定科目の種類の特定とマップなどの勘定科目インテリジェンス機能をディメンションに追加することができます。 詳細については、「 [ディメンションへの勘定科目インテリジェンスの追加](bi-wizard-add-account-intelligence-to-a-dimension.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [属性と属性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [ビジネス インテリジェンス ウィザードの F1 ヘルプ](../business-intelligence-wizard-f1-help.md)   
 [ディメンションの種類](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
