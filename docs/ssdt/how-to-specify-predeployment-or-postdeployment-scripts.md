---
title: 方法:配置前スクリプトまたは配置後スクリプトを指定する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 7f78f517-f13d-4f4b-84b9-e804cb490b2c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e8bbc783901c7dd93515424ae811fe66239e9f33
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199299"
---
# <a name="how-to-specify-predeployment-or-postdeployment-scripts"></a>方法:配置前スクリプトまたは配置後スクリプトを指定する
配置前スクリプトと配置後スクリプトでは、データベース プロジェクトから生成されるメインの配置スクリプトの前後に Transact\-SQL ステートメントが実行されます。 Visual Studio でスキーマ比較結果からターゲットを更新するとき、配置前スクリプトは実行されません。 1 つのプロジェクトに含めることができる配置前スクリプトと配置後スクリプトはそれぞれ 1 つだけです。 これらのスクリプトはさまざまな目的で使用できます。 例:  
  
-   配置前スクリプトでは、配置後スクリプトでデータの書式を再設定して変更対象のテーブルに適用する前に、変更対象のテーブルのデータを一時テーブルにコピーできます。  
  
-   配置後スクリプトでは、テーブル内に存在する必要がある参照データを挿入できます。 データを挿入する前に、テーブルに既にデータが格納されているかどうかをテストできます。 テーブルが空でない場合は、既存のデータをクリアするか、データベースを配置する前に必ず作成し直すように指定する必要があります。 配置後スクリプトには、次のようなステートメントを追加できます。  
  
```  
IF (EXISTS(SELECT * FROM [dbo].[MyReferenceTable]))  
BEGIN  
    DELETE FROM [dbo].[MyReferenceTable]  
END  
```  

## <a name="to-add-and-modify-a-pre--or-post-deployment-script"></a>配置前スクリプトまたは配置後スクリプトを追加および変更するには  
  
1.  **ソリューション エクスプローラー**で、データベース プロジェクトを展開して Scripts フォルダーを表示します。  
  
2.  Scripts フォルダーを右クリックし、[追加] をポイントします。  
  
3.  コンテキスト メニューの [スクリプト] をクリックします。  
  
4.  [配置前スクリプト] または [配置後スクリプト] を選択します。 必要に応じて、既定以外の名前を指定します。 [追加] をクリックして完了します。  
  
5.  Scripts フォルダーで、追加したファイルをダブルクリックします。  
  
    Transact\-SQL エディターが開き、ファイルの内容が表示されます。  
  
スクリプトで SQLCMD 構文と変数を使用して、データベース プロジェクトのプロパティに設定できます。 例:  
  
-   配置前スクリプトまたは配置後スクリプトで、SQLCMD 構文を使用してファイルの内容を含めることができます。 ファイルは、定義した順に含まれ実行されます (例: `:r .\myfile.sql`)。  
  
-   配置後スクリプトで、SQLCMD 構文を使用して変数を参照できます。 SQLCMD 変数は、プロジェクトのプロパティまたは公開プロファイルで設定します。  
  
    ```  
    :setvar TableName MyTable  
    SELECT * FROM [$(TableName)]  
    ```  
  
スクリプトで SQLCMD を使用する方法の詳細については、「[データベース プロジェクトの設定](../ssdt/database-project-settings.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)  
  
