---
title: Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: a5393c1a-cc37-491a-a260-7aad84dbff68
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5c636138358dda82c758ab2db70fab8d315f9b9d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294032"
---
# <a name="loop-through-excel-files-and-tables-by-using-a-foreach-loop-container"></a>Foreach ループ コンテナーを使用して Excel のファイルおよびテーブルをループ処理する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  このトピックの手順では、Foreach ループ コンテナーと適切な列挙子を使用して、フォルダー内の Excel ブックまたは Excel ブック内のテーブルをループ処理する方法について説明します。  

> [!IMPORTANT]
> Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題については、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。
 
## <a name="to-loop-through-excel-files-by-using-the-foreach-file-enumerator"></a>Foreach File 列挙子を使用して Excel ファイルをループ処理するには  
  
1.  ループの反復ごとに現在の Excel のパスとファイル名を受け取る文字列変数を作成します。 検証で問題が発生しないようにするには、変数の初期値として Excel の有効なパスとファイル名を割り当てます (この手順の後半で示すサンプル式では、 `ExcelFile`という変数名を使用します)。  
  
2.  必要に応じて、Excel 接続文字列の Extended Properties 引数の値を保持する別の文字列変数を作成します。 この引数には、Excel のバージョンを指定したり、最初の行に列名が含まれているかどうか、およびインポート モードが使用されるかどうかを判断する一連の値が格納されます (この手順の後半で示すサンプル式では、初期値が " `ExtProperties`" である`Excel 12.0;HDR=Yes`という名前の変数を使用しています)。  
  
     Extended Properties 引数の値を格納している変数を使用しない場合は、接続文字列を含む式に引数の値を手動で追加する必要があります。  
  
3.  Foreach ループ コンテナーを **[制御フロー]** タブに追加します。Foreach ループ コンテナーの構成方法については、「 [Foreach ループ コンテナーを構成する](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)」を参照してください。  
  
4.  **[Foreach ループ エディター]** の **[コレクション]** ページで [Foreach File 列挙子] を選択し、Excel ブックが存在するフォルダーを指定して、ファイル フィルター (通常は *.xlsx) を指定します。  
  
5.  **[変数のマッピング]** ページで、ループの反復ごとに現在の Excel のパスとファイル名を受け取るユーザー定義文字列変数に、インデックス 0 をマップします。 (この手順の後半で示すサンプル式では、 `ExcelFile`という変数名を使用します)。  
  
6.  **[Foreach ループ エディター]** を閉じます。  
  
7.  「 [パッケージの接続マネージャーを追加、削除、または共有する](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)」(パッケージでの接続マネージャーの追加、削除、または共有) の説明に従って、Excel 接続マネージャーをパッケージに追加します。 接続時に検証エラーが発生しないように、既存の Excel ブック ファイルを選択してください。  
  
    > [!IMPORTANT]  
    >  この Excel 接続マネージャーを使用するデータ フロー コンポーネントとタスクを構成する際、検証エラーが発生しないようにするには、 **[Excel 接続マネージャー]** で既存の Excel ブックを選択します。 以下の手順に従って **ConnectionString** プロパティ用の式を構成した後は、接続マネージャーは実行時にこのブックを使用しなくなります。 パッケージを作成して構成したら、[プロパティ] ウィンドウで **ConnectionString** プロパティの値を削除することができます。 ただし、この値を削除すると、Excel 接続マネージャーの接続文字列プロパティは Foreach ループが実行されるまで無効になります。 したがって、接続マネージャーを使用するタスクまたはパッケージでは、検証エラーが発生しないように、 **DelayValidation** プロパティを **True** に設定してください。  
    >   
    >  また、Excel 接続マネージャーの **RetainSameConnection** プロパティでは既定値の **False** を使用する必要があります。 この値を **True**に変更すると、ループの各反復処理で最初の Excel ブックが繰り返し開かれるようになります。  
  
8.  新しい Excel 接続マネージャーを選択し、[プロパティ] ウィンドウで **[式]** プロパティをクリックして、参照ボタンをクリックします。  
  
9. **[プロパティ式エディター]** で、 **ConnectionString** プロパティを選択し、参照ボタンをクリックします。  
  
10. 式ビルダーで、次の式を入力します。  
  
    ```  
    "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=\"" + @[User::ExtProperties] + "\""  
    ```  
  
     拡張プロパティ引数の値の前後に必要な内側の引用符をエスケープするために、エスケープ文字 "\\" を使用していることに注意してください。  
  
     Extended Properties 引数は省略できません。 引数の値を格納している変数を使用しない場合は、次の例に示すように、式に引数の値を手動で追加する必要があります。  
  
    ```  
    "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=Excel 12.0"  
    ```  
  
11. Foreach ループ コンテナー内で、Excel 接続マネージャーを使用して、指定したファイルの場所とパターンに一致した各 Excel ブックに対して同じ操作を実行するタスクを作成します。  
  
## <a name="to-loop-through-excel-tables-by-using-the-foreach-adonet-schema-rowset-enumerator"></a>Foreach ADO.NET Schema Rowset 列挙子を使用して Excel テーブルをループ処理するには  
  
1.  Microsoft ACE OLE DB Provider を使用して Excel ブックに接続する ADO.NET 接続マネージャーを作成します。 **[接続マネージャー]** ダイアログ ボックスの [すべて] ページで、Extended Properties プロパティの値として Excel のバージョン (ここでは、Excel 12.0) を入力します。 詳細については、「 [パッケージでの接続マネージャーの追加、削除、または共有](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)」 を参照してください。  
  
2.  ループの反復ごとに現在のテーブルの名前を受け取る文字列変数を作成します。  
  
3.  Foreach ループ コンテナーを **[制御フロー]** タブに追加します。Foreach ループ コンテナーの構成方法については、「 [Foreach ループ コンテナーを構成する](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)」を参照してください。  
  
4.  **[Foreach ループ エディター]** の **[コレクション]** ページで、Foreach ADO.NET Schema Rowset 列挙子を選択します。  
  
5.  **[コレクション]** の値として、以前に作成した ADO.NET 接続マネージャーを選択します。  
  
6.  **[スキーマ]** の値として、[テーブル] を選択します。  
  
    > [!NOTE]  
    >  Excel ブック内のテーブルの一覧には、ワークシート ($ サフィックスが付きます) と名前付き範囲が含まれます。 ワークシートのみ、または名前付き範囲のみを一覧からフィルター選択する場合は、そのためのカスタム コードをスクリプト タスクで記述する必要があります。 詳しくは、「 [スクリプト タスクを使用した Excel ファイルの操作](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)」をご覧ください。  
  
7.  **[変数のマッピング]** ページで、以前に作成した文字列変数にインデックス 2 をマップし、現在のテーブルの名前を保持します。  
  
8.  **[Foreach ループ エディター]** を閉じます。  
  
9. Foreach ループ コンテナー内で、Excel 接続マネージャーを使用して、指定したブック内の各 Excel テーブルに対して同じ操作を実行するタスクを作成します。 スクリプト タスクを使用して、列挙されるテーブル名を調べたり各テーブルを操作したりする場合、スクリプト タスクの ReadOnlyVariables プロパティに文字列変数を追加することを忘れないでください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む](../load-data-to-from-excel-with-ssis.md)  
 [Foreach ループ コンテナーを構成する](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)   
 [プロパティ式を追加または変更する](../../integration-services/expressions/add-or-change-a-property-expression.md)   
 [Excel 接続マネージャー](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Excel ソース](../../integration-services/data-flow/excel-source.md)   
 [Excel 変換先](../../integration-services/data-flow/excel-destination.md)   
 [スクリプト タスクを使用した Excel ファイルの操作](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
