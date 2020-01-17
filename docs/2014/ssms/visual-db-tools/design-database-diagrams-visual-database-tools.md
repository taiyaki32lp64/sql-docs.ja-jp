---
title: データベース ダイアグラムのデザイン (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65536
- vdt.DatabaseDesigner
helpviewer_keywords:
- Database Diagram Designer
- Visual Database Tools [SQL Server], database diagrams
- database diagrams [SQL Server], designing
- diagrams [SQL Server], designing
ms.assetid: 6d2c14e1-3d73-4d10-ae5b-7f2b5d6c4ea8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e348ace954e19c3e213c7de1779cbfbcb1768887
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316099"
---
# <a name="design-database-diagrams-visual-database-tools"></a>データベース ダイアグラムのデザイン (Visual Database Tools)
  データベース デザイナーは、接続先のデータベースをデザインしたりビジュアル化したりできるビジュアル ツールです。 データベースをデザインするときは、データベース デザイナーを使用して、テーブル、列、キー、インデックス、リレーションシップ、および制約の作成、編集、または削除を行うことができます。 データベースをビジュアル化するには、データベースに含まれるテーブル、列、キー、およびリレーションシップの一部または全部を表すダイアグラムを作成します。  
  
 ![テーブルのリレーションシップを説明するデータベース ダイアグラム](../../database-engine/media//dv3w7c1.gif "テーブル間のリレーションシップを説明するデータベース ダイアグラム")  
  
 1 つのデータベースから、いくつでもデータベース ダイアグラムを作成できます。また、1 つのデータベース テーブルは、複数のダイアグラムに含めることができます。 したがって、異なるダイアグラムを作成し、データベースの異なる部分をビジュアル化したり、デザインの異なる面を強調したりできます。 たとえば、大きなダイアグラムを作成した場合はすべてのテーブルと列を表示することができ、小さいダイアグラムの場合は列を表示しないですべてのテーブルだけを表示するようにできます。  
  
 作成したデータベース ダイアグラムは、関連するデータベースに格納されます。  
  
## <a name="tables-and-columns-in-a-database-diagram"></a>データベース ダイアグラムに表示されるテーブルと列  
 データベース ダイアグラムの中では、テーブルは、タイトル バー、行セレクター、一連のプロパティ列という 3 つの異なる機能で表示されます。  
  
 **タイトル バー** タイトル バーにはテーブルの名前が表示されます。  
  
 テーブルを変更し、まだ保存していない場合は、保存されていない変更があることを示すアスタリスク (*) がテーブル名の最後に表示されます。 変更したテーブルおよびダイアグラムの保存については、「 [データベース ダイアグラムの使用 (Visual Database Tools)](visual-database-tools.md)  
  
 **行セレクター** 行セレクターをクリックすると、テーブルの中のデータベース列を選択できます。 列がテーブルの主キーに含まれる場合は、行セレクターに鍵の記号が表示されます。 主キーについては、次を参照してください。 [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md)します。  
  
 **プロパティ列** プロパティ列は、テーブルの特定のビューにだけ表示されます。 テーブルは、5 種類のいずれのビューでも表示できるので、ダイアグラムのサイズとレイアウトを管理するときの参考になります。  
  
 テーブル ビューの詳細については、「[ダイアグラムに表示される情報の量のカスタマイズ (Visual Database Tools)](customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md)」を参照してください。  
  
## <a name="relationships-in-a-database-diagram"></a>データベース ダイアグラムにおけるリレーションシップ  
 データベース ダイアグラムでは、各リレーションシップの機能が、端点、線のスタイル、および関連テーブルという 3 つの異なる機能によって示されます。  
  
 **端点** 線の端点は、リレーションシップが一対一なのか一対多なのかを示しています。 リレーションシップの一方の端点には鍵が、もう一方の端点には数字の 8 に似た記号が表示されている場合は、一対多のリレーションシップです。 リレーションシップの両方の端点に鍵が表示されている場合は、一対一のリレーションシップです。  
  
 **線のスタイル** 端点ではなく線自体は、新しいデータを外部キー テーブルに追加するときに、データベース管理システム (DBMS) がリレーションシップに対して参照整合性を適用するかどうかを示しています。 線が実線の場合は、外部キー テーブルの行を追加または変更すると、リレーションシップに対する参照整合性が DBMS により適用されます。 線が点線の場合は、外部キー テーブルの行を追加または変更しても、リレーションシップに対する参照整合性は適用されません。  
  
 **関連テーブル** リレーションシップの線は、あるテーブルと別のテーブルの間に外部キー テーブルのリレーションシップが存在することを示します。 一対多のリレーションシップの場合は、線に数字の 8 に似た記号が付いている側のテーブルが外部キー テーブルです。 線の両方の端点が同じテーブルに接続している場合、そのリレーションシップは再帰リレーションシップです。 詳細については、「[再帰リレーションシップの作成 (Visual Database Tools)](draw-reflexive-relationships-visual-database-tools.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [データベース ダイアグラムの所有権について (Visual Database Tools)](understand-database-diagram-ownership-visual-database-tools.md)  
  
 [データベース ダイアグラム デザイナー内でのナビゲーション (Visual Database Tools)](navigate-in-database-diagram-designer-visual-database-tools.md)  
  
 [データベース ダイアグラム デザイナーの設定 (Visual Database Tools)](set-up-database-diagram-designer-visual-database-tools.md)  
  
 [旧エディションのデータベース ダイアグラムのアップグレード (Visual Database Tools)](upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
  
 [データベース ダイアグラム デザイナーを開く (Visual Database Tools)](open-database-diagram-designer-visual-database-tools.md)  
  
## <a name="see-also"></a>参照  
 [データベース ダイアグラムを扱う&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [データベース ダイアグラムでテーブルを操作する&#40;Visual Database Tools&#41;](work-with-tables-in-database-diagram-visual-database-tools.md)   
 [ダイアグラムのレイアウトの操作 (Visual Database Tools)](work-with-diagram-layout-visual-database-tools.md)  
  
  
