---
title: 方法:エラーを修正する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 0d504e00-4ff0-4fdf-b874-85280bbd8668
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ba41850e214de60da9a7e64f328939e4660a9367
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035169"
---
# <a name="how-to-fix-errors"></a>方法:エラーを修正する
エラー一覧ペインには、配置エラーおよびビルド エラーが表示されます。 データベース エンティティおよびその定義を編集する際に、Transact\-SQL エディターまたはテーブル デザイナーでの編集によって生じた構文エラーおよびセマンティック エラーも、この一覧に表示されます。 各タブでスクリプトの編集を行うと、エラー一覧は動的に更新されます。 特定されたエラーを追跡することにより、トラブルシューティングを進めることができます。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」および「[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)」に示されている手順で作成したエンティティを使用します。  
  
### <a name="to-fix-errors"></a>エラーを修正するには  
  
1.  **ソリューション エクスプローラー**で **Product** テーブル (Product.sql) を右クリックし、 **[デザイナーの表示]** をクリックします。  
  
2.  デザイナーの列グリッドで **[ShelflLife]** 列を右クリックし、 **[削除]** をクリックして、この列をテーブルから削除します。  
  
3.  画面の下部にある**エラー一覧**ペインには、次のような警告およびエラーが直ちに表示されます。  
  
**警告 SQL71502:関数: [dbo].[GetProductsBySupplier] にはオブジェクトに対して未解決の参照があります。オブジェクトが存在しないか、または次のようなオブジェクトを参照しているために参照があいまいになっています: [dbo].[Product].[p]::[ShelfLife] or [dbo].[Product].[ShelfLife]。エラー SQL71501:制約のチェック: [dbo].[CK_Product_ShelfLife] にはオブジェクト [dbo].[Product].[ShelfLife] に対して未解決の参照があります。**  
  
4.  **[エラー一覧]** を右クリックし、コンテキスト メニューを使用して、結果を並べ替えることができます。表示するエントリをフィルターで選択することも、各エントリに対して表示する情報の列を選択することもできます。  
  
    特定された最初の警告をダブルクリックし、その警告を生成したスクリプト ファイルまで追跡します。 問題のあるコードのセクションが強調表示されます。 これは、この例で、前に作成したテーブル値関数の `RETURN` ステートメントと `SELECT` ステートメントの両方で `ShelfLife` 列が使用されているためです。  
  
5.  Transact\-SQL エディターで、関数から `ShelfLife` を削除します。  
  
6.  2 つ目のエラーも同じように、CHECK 制約を削除することによって修正します。  
  
7.  問題を修正すると、警告およびエラーが**エラー一覧**から直ちに消えます。  
  
## <a name="see-also"></a>参照  
[Transact-SQL エディターを使用したスクリプトの編集と実行](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
