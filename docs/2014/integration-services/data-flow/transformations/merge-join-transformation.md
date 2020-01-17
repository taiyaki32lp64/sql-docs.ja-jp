---
title: マージ結合変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointrans.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0ef70f4f9d28fc23c0ac0a168447cc1b8867cd27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900168"
---
# <a name="merge-join-transformation"></a>Merge Join Transformation
  マージ結合変換では、FULL、LEFT、または INNER 結合を使用して並べ替えた 2 つのデータセットを結合した出力が生成されます。 たとえば、LEFT 結合を使用して、製品情報を含むテーブルを、製品が製造された国または地域を一覧表示するテーブルと結合します。 その結果、すべての製品とその製造元である国または地域を一覧表示するテーブルが生成されます。  
  
 マージ結合変換は、次の方法で構成できます。  
  
-   FULL、LEFT、または INNER 結合のうち、どの結合を使用するかを指定します。  
  
-   結合で使用する列を指定します。  
  
-   NULL 値を、他の NULL と等しい値として処理するかどうかを指定します。  
  
    > [!NOTE]  
    >  NULL 値どうしを等しい値として扱わない場合、マージ結合変換では、SQL Server データベース エンジンによる処理方法と同様に NULL 値が処理されます。  
  
 この変換は、2 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
## <a name="input-requirements"></a>入力要件  
 マージ結合変換では、入力データが並べ替えられている必要があります。 この重要な要件の詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。  
  
## <a name="join-requirements"></a>結合要件  
 マージ結合変換では、結合列のメタデータが一致している必要があります。 たとえば、数値データ型の列と文字データ型の列は結合できません。 データが文字列データ型の場合、2 番目の入力の列の長さは、マージ先の最初の入力の列の長さ以下である必要があります。  
  
## <a name="buffer-throttling"></a>バッファー スロットル  
 マイクロソフトが行った変更により、マージ結合変換によってメモリが過度に消費されるリスクが軽減したため、`MaxBuffersPerInput` プロパティの値を構成する必要はなくなりました。 この問題は、マージ結合の複数の入力からデータが不均一なレートで生成される場合に発生することがありました。  
  
## <a name="related-tasks"></a>Related Tasks  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 この変換のプロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [マージ結合変換を使用してデータセットを拡張する](merge-join-transformation.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>参照  
 [マージ結合変換エディター](../../merge-join-transformation-editor.md)   
 [マージ変換](merge-transformation.md)   
 [全体結合変換](union-all-transformation.md)   
 [Integration Services の変換](integration-services-transformations.md)  
  
  
