---
title: 方法:テーブル デザイナーを使用してデータベース オブジェクトを作成する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.design.table.scriptpanel
- sql.data.tools.design.table.context.view
ms.assetid: 9c9479c1-9bfc-4039-837e-e53fce67723d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cab6b6114dd7ea7364df890be67579f91bee4339
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897173"
---
# <a name="how-to-create-database-objects-using-table-designer"></a>方法:テーブル デザイナーを使用してデータベース オブジェクトを作成する
**SQL Server オブジェクト エクスプローラー**の新しい **[SQL Server]** ノードは視覚的に SSMS とよく似ていますが、それだけではなく、SSMS で提供されるものとよく似た機能を持つコンテキスト メニューを使用して、新しいオブジェクトを作成することもできます。  
  
たとえば、 **[データベース]** ノードの下に、新しいデータベースを作成できます。 同様に、特定のデータベースを選択し、新しいテーブル デザイナーを使用して、テーブル定義および関連するプログラミング オブジェクトを即座に作成または編集できます。 テーブル デザイナーをスクリプト ペインに切り替えて、そのテーブルを定義するスクリプトを直接編集することもできます。  
  
### <a name="to-create-a-new-database"></a>新しいデータベースを作成するには  
  
1.  **SQL Server オブジェクト エクスプローラー**の **[SQL Server]** ノードの下で、接続されているサーバー インスタンスを展開します。  
  
2.  **[データベース]** ノードを右クリックし、 **[新しいデータベースの追加]** をクリックします。  
  
3.  新しいデータベースの名前を **Trade** に変更します。  
  
### <a name="to-create-new-tables-using-the-table-designer"></a>テーブル デザイナーを使用して新しいテーブルを作成するには  
  
1.  新しく作成した **[Trade]** ノードを展開します。 **[テーブル]** ノードを右クリックし、 **[新しいテーブルの追加]** をクリックします。  
  
2.  新しいウィンドウでテーブル デザイナーが開きます。 デザイナーは、列グリッド、スクリプト ペイン、およびコンテキスト ペインで構成されています。 列グリッドには、テーブル内のすべての列が表示されます。 デザイナーの他のコンポーネントは、後の手順で使用します。  
  
3.  スクリプト ペインで、新しいテーブルの名前を `Suppliers` に変更します。 具体的には、まず次の行を探します。  
  
    ```  
    CREATE TABLE [dbo].[Table1]  
    ```  
  
    これを次の行に置き換えます。  
  
    ```  
    CREATE TABLE [dbo].[Suppliers]  
    ```  
  
4.  列グリッドで空の行をクリックし、テーブルに新しい列を追加します。  **[名前]** に「**CompanyName**」、 **[データ型]** に「**nvarchar (128)** 」と入力し、 **[Null を許容]** チェック ボックスはオフにします。 Tab キーでフィールドを離れると、スクリプト ペインの内容が直ちに更新されます。  
  
5.  新しい列をもう 1 つ追加します。 **[名前]** に「**Address**」、 **[データ型]** に「**nvarchar (MAX)** 」と入力し、 **[Null を許容]** チェック ボックスはオフにします。  
  
    > [!WARNING]  
    > 接続されているデータベースのオブジェクトを編集する場合は、ローカル ドライブに保存しないでください。 データベースへの変更を正しく保存するには、次の「[接続されているデータベースを Power Buffer で更新する方法](../ssdt/how-to-update-a-connected-database-with-power-buffer.md)」の手順に従って、変更を適用します。  
  
6.  これまでの手順を繰り返して、テーブルをもう 1 つ、**Customer** という名前で作成します。 今回は列グリッドを使用して、以下に示す列を Customer テーブルに追加します。 さらに、テーブルの名前が `[dbo].[Customer]` になるようにスクリプトを変更します。  
  
    |[オブジェクト名]|データ型|**[NULL を許容]**|  
    |--------|-------------|-------------------|  
    |Id|INT|オフ|  
    |[オブジェクト名]|nvarchar (128)|オフ|  
  
7.  もう 1 つ、**Products** という名前のテーブルを作成します。 列グリッドを使用して、以下に示す列を Products テーブルに追加します。 さらに、テーブルの名前が `[dbo].[Products]` になるようにスクリプトを変更します。  
  
    |[オブジェクト名]|データ型|**[NULL を許容]**|  
    |--------|-------------|-------------------|  
    |Id|INT|オフ|  
    |[オブジェクト名]|nvarchar (128)|オフ|  
    |ShelfLife|INT|オン|  
    |SupplierId|INT|オン|  
    |CustomerId|INT|オン|  
  
### <a name="to-create-a-new-check-constraint-using-the-table-designer"></a>テーブル デザイナーを使用して新しい CHECK 制約を作成するには  
  
1.  テーブル デザイナーのコンテキスト ペインには、テーブル定義 (キー、制約、トリガーなど) の論理ビューが表示されます。オブジェクトを選択すると、個々の列に対するリレーションシップが強調表示されます。  
  
    Products テーブルについて、テーブル デザイナーのコンテキスト ペインで **[CHECK 制約]** ノードを右クリックし、 **[新しい CHECK 制約の追加]** をクリックします。  
  
2.  ノード カウントが自動的に 1 カウント分、インクリメントされます。  
  
3.  スクリプト ペインをクリックし、制約の既定の定義を次のように変更します。  
  
    ```  
    CONSTRAINT [CK_Products_ShelfLife] CHECK ([ShelfLife] <5),  
    ```  
  
    この制約は、列の ShelfLife の値を 5 未満に制限しています。  
  
### <a name="to-create-new-foreign-key-references-using-the-table-designer"></a>テーブル デザイナーを使用して新しい外部キー参照を作成するには  
  
1.  Products テーブルについて、コンテキスト ペインで **[外部キー]** ノードを右クリックし、 **[新しい外部キーを追加]** をクリックします。  
  
2.  ノード カウントが自動的に 1 カウント分、インクリメントされます。  
  
3.  スクリプト ペインをクリックし、外部キー参照の既定の定義を次のように変更します。  
  
    ```  
    CONSTRAINT [FK_Products_SupplierId] FOREIGN KEY ([SupplierId]) REFERENCES [dbo].[Suppliers] ([Id]),  
    ```  
  
4.  これまでの手順を繰り返して、Products テーブルに外部キー参照をもう 1 つ追加します。 今回は、既定の定義を次のように変更します。  
  
    ```  
    CONSTRAINT [FK_Products_CustomerId] FOREIGN KEY ([CustomerId]) REFERENCES [dbo].[Customer] ([Id])  
    ```  
  
## <a name="see-also"></a>参照  
[テーブルとリレーションシップの管理およびエラーの修正](../ssdt/manage-tables-relationships-and-fix-errors.md)  
  
