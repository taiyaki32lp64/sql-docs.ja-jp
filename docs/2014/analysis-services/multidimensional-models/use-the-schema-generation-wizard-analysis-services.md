---
title: 使用して、スキーマ生成ウィザード (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Schema Generation Wizard, steps
- relational schema [Analysis Services], Schema Generation Wizard
ms.assetid: 8c710745-d41d-4c31-b6a2-2956229df75a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e434493813f0237533ca2e50ff089974f3556f34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072653"
---
# <a name="use-the-schema-generation-wizard-analysis-services"></a>スキーマ生成ウィザードの使用 (Analysis Services)
  スキーマ生成ウィザードが生成フェーズで必要とする情報の量は限られています。 スキーマ生成ウィザードでリレーショナル スキーマを生成するために必要な情報のほとんどは、プロジェクトで既に作成した [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] キューブおよびディメンションから抽出されます。 また、サブジェクト領域データベース スキーマの生成方法とスキーマ内のオブジェクトの名前付け方法をカスタマイズすることもできます。  
  
## <a name="start-the-wizard"></a>ウィザードの起動  
 スキーマ生成ウィザードを開くには、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] で次のいずれかの方法を使用します。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト オブジェクトを右クリックして、コンテキスト メニューの **[リレーショナル スキーマの生成]** をクリックします。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト オブジェクトをクリックして、 **[データベース]** メニューの **[リレーショナル スキーマの生成]** をクリックします。  
  
-   スキーマ生成ウィザードをディメンション ウィザードから直接起動します。これを行うには、ディメンション ウィザードの最後のページにある **[今すぐスキーマを生成する]** チェック ボックスをオンにします。  
  
## <a name="step-1-specify-targets"></a>手順 1:ターゲットを指定します。  
 スキーマ生成ウィザードがサブジェクト領域データベースのスキーマを生成するデータ ソース ビュー (DSV) を指定する必要があります。 既存の DSV を選択することもできますが、通常は、データ ソースに基づいて新しい DSV を作成します。 データ ソースは、既存の接続または新しい接続に基づいて作成できます。また、別のオブジェクトに基づいて作成することもできます。 スキーマ生成ウィザードは、データ ソース ビューにサブジェクト領域データベースのスキーマを生成するだけでなく、データ ソースによって参照されるデータベースにもスキーマを生成します。 スキーマ生成ウィザードは、サブジェクト領域データベース自体を作成しませんが、代わりに、ユーザーが指定した既存のデータベースのキューブおよびディメンションをサポートするリレーショナル スキーマを作成します。  
  
 スキーマ生成ウィザードによって基になるオブジェクトが生成されると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のディメンションおよびキューブは、データ ソースのビュースタイル バインドを使用して、生成されたテーブルや列にバインドされます。  
  
> [!NOTE]  
>  以前に生成されたオブジェクトから [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のディメンションおよびキューブをアンバインドするには、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のディメンションおよびキューブがバインドされているデータ ソース ビューを削除し、スキーマ生成ウィザードを使用してそのキューブやディメンションの新しいデータ ソース ビューを定義します。  
  
## <a name="step-3-specify-schema-options-for-the-subject-area-database"></a>手順 3:サブジェクト領域データベースのスキーマ オプションを指定します。  
 スキーマ生成ウィザードには、サブジェクト領域データベースに生成するスキーマを定義するいくつかのオプションがあります。 これらのオプションは、ウィザードの **[サブジェクト領域データベース スキーマのオプション]** ページで指定できます。  
  
### <a name="specifying-the-schema-owner"></a>スキーマの所有者の指定  
 スキーマの所有者は、 **[所有しているスキーマ]** の値を有効な文字列に設定して指定できます。 スキーマの既定の所有者は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトですが、任意のスキーマの所有者を指定できます。  
  
### <a name="specifying-primary-keys-indexes-and-constraints"></a>主キー、インデックス、および制約の指定  
 既定では、スキーマ生成ウィザードはサブジェクト領域データベースの各ディメンション テーブルに主キー制約を作成します。 主キーは、対応する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ディメンションのキー属性として指定された属性に対応します。 この制約によって、ほとんどの環境で処理パフォーマンスが向上し、コストは最小化されます。 主キーをサブジェクト領域データベースに作成しない場合でも、論理主キーは常にデータ ソース ビューに作成されます。 ディメンション テーブルで主キー制約を定義するには、 **[ディメンション テーブルに主キーを作成する]** を選択します。  
  
 また、既定では、ウィザードによって各ファクト テーブルの外部キー列にインデックスが作成されます。 これらのインデックスによって、ほとんどの環境で処理パフォーマンスが向上します。 新しいデータをサブジェクト領域データベースから取得するために [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が生成した処理クエリには、通常、ファクト テーブルとディメンション テーブルの間の JOIN ステートメントが非常に多く含まれているので、一般的にパフォーマンスが向上します。 各ファクト テーブルの外部キー列にインデックスを定義するには、 **[インデックスを作成する]** を選択します。  
  
 最後に、既定ではウィザードによってファクト テーブルと各ディメンション テーブルの間の参照整合性が保証されます。 参照整合性を保証しない場合でも、スキーマ生成ウィザードはデータベースおよびデータ ソース ビューにこれらのリレーションシップを作成します。 参照整合性を保証するには、 **[参照整合性を適用する]** を選択します。  
  
### <a name="preserving-data-for-incremental-generation"></a>増分生成のデータの保存  
 既定では、スキーマ生成ウィザードは、データベース スキーマが再生成されるときにデータを保存しようとします。 スキーマが変更されてスキーマ生成ウィザードで行を削除する必要がある場合は、行を削除する前に警告が表示されます。 たとえば、ディメンションを削除した場合や、ディメンションの属性を変更したときにデータ型が変わった場合には、行を削除して参照整合性の問題を解決する必要があります。 データベース スキーマを再生成するときにデータを保存するには、 **[再生成時にデータを保存する]** を選択します。  
  
## <a name="step-4-specify-naming-conventions"></a>手順 4:名前付け規則を指定します。  
 スキーマ生成ウィザードの **[名前付け規則の指定]** ページで、サブジェクト領域データベースに特定のオブジェクトを生成するときにウィザードが使用する名前付け規則を定義できます。 **[名前付け規則の指定]** ページで使用できるオプションの詳細については、「[[名前付け規則の指定] &#40;スキーマ生成ウィザード&#41; &#40;Analysis Services - 多次元データ&#41;](../specify-naming-conventions-schema-generation-analysis-services-multidimensional-data.md)」を参照してください。  
  
  
