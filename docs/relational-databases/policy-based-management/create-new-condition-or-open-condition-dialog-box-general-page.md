---
title: '[新しい条件の作成] または [条件を開く] ダイアログ ボックスの [全般] ページ'
description: SQL Server Management Studio (SSMS) のポリシーベース管理のための [新しい条件の作成] または [条件を開く] ダイアログ ボックスの [全般] ページについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.condition.f1
ms.assetid: 106954bf-e4ba-412b-9c1a-907d06153dcd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c16d813af595e3698379026e219440ba0007db12
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558140"
---
# <a name="create-new-condition-or-open-condition-dialog-box-general-page"></a>[新しい条件の作成] または [条件を開く] ダイアログ ボックスの [全般] ページ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このダイアログ ボックスを使用すると、ポリシー ベースの管理条件を作成または変更できます。 条件とは、ポリシー ベースの管理で管理する対象に許可されている状態のセットをファセットについて指定するブール式です。 **[式]/[フィールド]** ボックスで選択できるプロパティは、使用するファセットによって異なります。 条件と各ファセットおよびポリシーとの関係の詳細については、「 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **Name**  
 新しい条件の場合は、新しい条件名を入力します。 既存の条件の場合は、その名前が表示されます。  
  
 **ファセット**  
 この条件で使用されるファセット。  
  
 **[AndOr]**  
 複数の式を追加する場合は、 **And** または **Or**を使用して式を結合するかどうかを指定します。 式が 1 つだけしかない場合は空白になります。  
  
 **フィールド**  
 各ファセットは、設定可能な 1 つまたは複数のプロパティを公開します。 [フィールド] ボックスで、この条件の式を作成するために使用できるプロパティの一覧からプロパティを選択します。  
  
 **[オペレーター]**  
 この式の比較演算子を選択します。 演算子には、=、!=、>、>=、<、<=、[NOT]LIKE、[NOT]IN があります。 プロパティによっては、使用できない演算子もあります。  
  
 **Value**  
 この式の値の設定。 許容値は、ファセットによって異なります。 値は、TRUE/FALSE、文字列、または数値です。 文字列値は、一重引用符で囲む必要があります。たとえば、 **'AdventureWorks'** です。 プロパティによっては、使用できない演算子もあります。  
  
## <a name="group-clauses"></a>句のグループ化  
 句をグループ化すると、クエリの他の部分とは別個の、単一のまとまりとして操作できます。これは、数式や論理ステートメントで式の前後をかっこで囲むのと似ています。 句のグループ化は、複雑なクエリを作成するときに役立ちます。  
  
 **句をグループ化するには**  
  
-   Shift キーまたは Ctrl キーを押しながら複数の句をクリックして範囲を選択します。 選択した領域を右クリックし、 **[句のグループ化]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
