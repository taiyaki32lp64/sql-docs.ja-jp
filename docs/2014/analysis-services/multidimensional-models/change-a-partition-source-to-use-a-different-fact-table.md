---
title: 複数のファクト テーブルを使用するパーティション ソースの変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- fact tables [Analysis Services]
- partitions [Analysis Services], fact tables
ms.assetid: 5508312f-8e46-4802-9362-6688ca03d098
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 94ab489420b4661cea27b942c39dff91a219a38d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076713"
---
# <a name="change-a-partition-source-to-use-a-different-fact-table"></a>別のファクト テーブルを使用するためのパーティション ソースの変更
  キューブのパーティションを作成する場合、複数のファクト テーブルを使用するように選択できます。 複数のテーブルは、単一のデータ ソース ビュー、複数のデータ ソース ビュー、または複数のデータ ソースから得たものである場合があります。 データ ソース ビューには、複数のデータ ソースから得た複数のテーブルが含まれている場合もあります。  
  
 キューブのパーティションのファクト テーブルとディメンションはすべて、キューブのファクト テーブルおよびディメンションと同一構造であることが必要です。 たとえば、同一構造の複数のファクト テーブルに、異なる年度のデータや異なる製品ラインのデータを格納できます。  
  
 ファクト テーブルはパーティション ウィザードの **[基になる情報の指定]** で指定します。 このページの **[検索対象]** の横の [パーティション ソース] で、検索するデータ ソースまたはデータ ソース ビューを指定します。 次に、 **[テーブルの検索]** をクリックし、 **[使用できるテーブル]** で使用するテーブルを選択します。  
  
 複数のファクト テーブルを使用する場合は、パーティション間でデータが重複していないことを確認してください。 たとえば、あるファクト テーブルに 2012 年のトランザクションのみが含まれ、別のファクト テーブルに 2013 年のトランザクションのみが含まれる場合、これらのテーブルに含まれるデータは重複しません。 同様に、異なる製品ラインや異なる地域のファクト テーブルにも重複データは含まれません。  
  
 重複データを含む複数のファクト テーブルを使用することは可能ですが、お勧めはできません。 使用する場合は、パーティション内でフィルターを使用して、あるパーティションで使用されるデータが、別のパーティションで使用されないようにする必要があります。 詳細については、「[ローカル パーティションの作成と管理 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ローカル パーティションの作成と管理 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)  
  
  
