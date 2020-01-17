---
title: 方法:テーブル デザイナーを使用してテーブルおよびリレーションシップを管理する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.design.table.columnspecification.index.dialog
- sql.data.tools.design.table.columnsgrid.view
- sql.data.tools.design.table.scriptpanel
ms.assetid: 322a2903-d7a6-4f52-9048-1bd413b4c799
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 91fddb94bf028ec884a4589c7c4a88bd3be923e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097484"
---
# <a name="how-to-use-the-table-designer-to-manage-tables-and-relationships"></a>方法:テーブル デザイナーを使用してテーブルおよびリレーションシップを管理する
Transact\-SQL エディターと同様に、テーブル デザイナーを使用すると、テーブル固有のプログラミング オブジェクトを含め、SQL Server データベースのテーブル構造を視覚的に作成および編集できます。  接続されているデータベースまたはプロジェクトに対して新しいテーブルを作成するときや、SQL Server オブジェクト エクスプローラーまたはソリューション エクスプローラーでテーブルを編集するためにダブルクリックしたときに、テーブル デザイナーが起動します。  
  
デザイナーは、列グリッド、スクリプト ペイン、およびコンテキスト ペインで構成されています。 列グリッドには、テーブル内のすべての列が表示されます。 このグリッドでは、列を追加、編集、および削除できます。  コンテキスト ペインには、テーブル定義 (キー、インデックス、制約、トリガーなど) の論理ビューが表示されます。オブジェクトを選択すると、個々の列に対するリレーションシップが強調表示されます。 このウィンドウでテーブルに新しいオブジェクトを追加し、プロパティ グリッドで選択したオブジェクトのプロパティを編集できます。 スクリプト ペインでは、テーブル構造の定義が表示され、コンテキスト ペインまたは列グリッドで選択されているオブジェクトのスクリプトが強調表示されます。 列グリッドとコンテキスト ペインを表示した状態で、スクリプトをサイド バイ サイドで編集できます。 これら 3 つのペインのいずれかで変更を行うと、残り 2 つのペインにその変更が直ちに反映されます。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」および「[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)」に示されている手順で作成したエンティティを使用します。  
  
### <a name="to-create-a-new-table"></a>新しいテーブルを作成するには  
  
1.  これまでの手順で使用していた TradeDev プロジェクトを開きます。  
  
2.  **ソリューション エクスプローラー**で **[dbo]** フォルダーを展開し、 **[テーブル]** フォルダーを右クリックして、 **[追加]** をポイントし、 **[テーブル]** をクリックします。  
  
3.  新しいテーブルに **Shipper** という名前を付け、 **[追加]** をクリックします。  
  
4.  テーブル デザイナーが開きます。 列グリッドで、テーブルに新しい列を追加し、名前を **ShipperName** に、データ型を **int** に指定します。  
  
5.  **[プロパティ]** ウィンドウで列のプロパティを編集することもできます。 **[ShipperName]** 列をクリックし、 **[プロパティ]** ウィンドウで、この列の**データ型**を **nvarchar** に、**長さ**を **128** に変更します。 フォーカスをフィールドから外すと、デザイナーのスクリプト ペインおよび列グリッドが自動的に更新され、変更が反映されます。  
  
### <a name="to-create-a-new-foreign-key-constraint"></a>新しい外部キー制約を作成するには  
  
1.  デザイナーのコンテキスト ペインで **[外部キー]** ノードを右クリックし、 **[新しい外部キーを追加]** をクリックします。  
  
2.  ノード カウントが自動的に 1 カウント分、インクリメントされます。 制約の既定の名前をそのままにして Enter キーを押します。  
  
3.  スクリプト ペインで、制約の既定の定義を次のように変更します。  
  
    ```  
    CONSTRAINT [FK_Shipper_Products] FOREIGN KEY ([Id]) REFERENCES [dbo].[Products]([Id])  
    ```  
  
    オフライン プロジェクトでデータベース エンティティを作成および編集する操作は、接続されているデータベースに対して行うタスクと同じである点に注意してください。  
  
## <a name="see-also"></a>参照  
[方法:テーブル デザイナーを使用してデータベース オブジェクトを作成する](../ssdt/how-to-create-database-objects-using-table-designer.md)  
  
