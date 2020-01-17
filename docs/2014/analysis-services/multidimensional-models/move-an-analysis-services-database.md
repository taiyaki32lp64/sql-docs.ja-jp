---
title: Analysis Services データベースの移動 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- moving databases [Anlysis Services]
- moving databases
- operations [Analysis Services - multidimensional data]
ms.assetid: fa644e5d-e276-445e-98d9-673afcfb83fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 02d084aea4491982d560f1cf0b8dc449b8502f09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073599"
---
# <a name="move-an-analysis-services-database"></a>Analysis Services データベースの移動
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のデータベース管理者 (DBA) が多次元式またはテーブル モデル データベースを別の場所に移動することは少なくありません。 こうした状況は、パフォーマンス向上のためにデータベースを別のディスクに移動したり、データベース拡張のための領域を確保したり、製品をアップグレードしたりするなど、ビジネス上のニーズによって頻繁に発生します。  
  
 データベースの移動方法は多数あります。 このドキュメントでは、次の一般的なシナリオについて説明します。  
  
-   SSMS の対話的使用  
  
-   AMO を使用したプログラム  
  
-   XMLA を使用したスクリプト  
  
 どのシナリオにおいても、ユーザーはデータベース フォルダーにアクセスし、ファイルを目的の場所に移動する方法を使用する必要があります。  
  
> [!NOTE]  
>  パスワードを割り当てずにデータベースをデタッチすると、そのデータベースはセキュリティで保護されていない状態のままになります。 データベースにパスワードを割り当てて、機密情報を保護することをお勧めします。 また、対応するアクセス セキュリティをデータベース フォルダー、サブフォルダー、ファイルに適用して、不正アクセスを防ぐ必要があります。  
  
## <a name="procedures"></a>手順  
  
#### <a name="moving-a-database-interactively-using-ssms"></a>SSMS を使用したデータベースの対話的移動  
  
1.  SSMS の左側または右側のペインで、移動するデータベースを探します。  
  
2.  クリックし、データベースを右クリックして**デタッチしています.**  
  
3.  デタッチするデータベースにパスワードを割り当て、 **[OK]** をクリックしてデタッチ コマンドを実行します。  
  
4.  ファイルを移動するための、オペレーティング システムのメカニズムまたは標準的な方法を使用して、データベース フォルダーを新しい場所に移動します。  
  
5.  SSMS の左側または右側のペインで、 **[データベース]** フォルダーを探します。  
  
6.  右クリックし、**データベース**フォルダーと選択**アタッチしています.**  
  
7.  **[フォルダー]** テキスト ボックスに、データベース フォルダーの移動先を入力します。 また、[参照] ボタンを使用することができます (**.**) データベース フォルダーを検索します。  
  
8.  選択、`ReadWrite`データベースのモード。  
  
9. 手順 3. で使用したパスワードを入力し、 **[OK]** をクリックしてアタッチ コマンドを実行します。  
  
#### <a name="moving-a-database-programmatically-using-amo"></a>AMO を使用したプログラムによるデータベースの移動  
  
1.  C# アプリケーションで、次のサンプル コードを調整して、指定されたタスクを完了します。  
  
 `private void MoveDb(Server server, string dbName,`  
  
 `string dbInitialLocation, string dbFinalLocation,`  
  
 `string dbPassword, ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `//Verify dbInitialLocation exists before continuing`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `//Save current cursor and change cursor to Cursors.WaitCursor`  
  
 `db = server.Databases[dbName];`  
  
 `db.Detach(dbPassword);`  
  
 `//Add your own code to copy the database files to the destination where you intend to attach the database`  
  
 `//Verify dbFinalLocation exists before continuing`  
  
 `server.Attach(dbFinalLocation, dbReadWriteMode, dbPassword);`  
  
 `//Restore cursor to its original`  
  
 `}`  
  
 `}`  
  
1.  C# アプリケーションで、必要なパラメーターを指定して `MoveDb()` を呼び出します。  
  
2.  コードをコンパイルして実行し、データベースを移動します。  
  
#### <a name="moving-a-database-by-script-using-xmla"></a>XMLA を使用したスクリプトによるデータベースの移動  
  
1.  SSMS で新しい XMLA タブを開きます。  
  
2.  次の XMLA 用のスクリプト テンプレートをコピーします。  
  
 `<Detach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  `%dbName%` をデータベースの名前に置き換え、 `%password%` をパスワードに置き換えます。 テンプレートに含まれている文字 % は削除する必要があります。  
  
2.  XMLA コマンドを実行します。  
  
3.  ファイルを移動するための、オペレーティング システムのメカニズムまたは標準的な方法を使用して、データベース フォルダーを新しい場所に移動します。  
  
4.  新しい XMLA タブに、次の XMLA 用のスクリプト テンプレートをコピーします。  
  
 `<Attach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="https://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  `%dbFolder%` をデータベース フォルダーの完全な UNC パスに置き換え、`%ReadOnlyMode%` を対応する値 `ReadOnly` または `ReadWrite` に置き換え、`%password%` をパスワードに置き換えます。 テンプレートに含まれている文字 % は削除する必要があります。  
  
2.  XMLA コマンドを実行します。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Analysis Services データベースのインポートとデタッチ](attach-and-detach-analysis-services-databases.md)   
 [データベースの格納場所](database-storage-location.md)   
 [データベースの ReadWriteMode](database-readwritemodes.md)   
 [Attach 要素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Detach 要素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [ReadWriteMode 要素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [DbStorageLocation 要素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
