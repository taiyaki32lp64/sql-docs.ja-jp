---
title: 方法:Visual Studio 2010 のデータベース プロジェクトを SQL Server のデータベース プロジェクトに変換してターゲットを別のプラットフォームに変更する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.projectconversion.dialog
- sql.data.tools.ImportDAC
ms.assetid: 7e5acf94-5c46-44c7-9ff5-ca7926f5332a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 84815176ca9b32614e851800a59ea2951010ce4c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897321"
---
# <a name="how-to-convert-a-visual-studio-2010-database-projects-to-sql-server-database-projects-and-retarget-to-a-different-platform"></a>方法:Visual Studio 2010 のデータベース プロジェクトを SQL Server のデータベース プロジェクトに変換してターゲットを別のプラットフォームに変更する
SQL Server Data Tools (SSDT) では、Visual Studio 2010 で作成された SQL Server データベース、CLR、およびデータ層アプリケーションの各既存プロジェクトを新しい SQL Server データベース プロジェクトに変換できます。 そうすることにより、新しくなった Transact\-SQL 編集機能や、プロジェクトのターゲットを Microsoft SQL Server 2012 や SQL Azure にコード検証付きで変更できる機能など、SSDT で提供される新しいデータベース開発機能を利用できるようになります。 変換プロセスでは、対応する型が SSDT にあるオブジェクト (テーブル、ビュー、ストアド プロシージャ、プロパティ ファイル、またはスクリプト) が、アクセス許可および DAC ポリシー ファイルを含めて変換されます。 変換できない成果物は、変換ログ レポート内で強調表示されます。  
  
次の表は、すべてのプロジェクト成果物のうち、SSDT で変換できるものと変換できないものを示しています。  
  
|変換できるプロジェクト成果物|変換できないプロジェクト成果物|  
|-------------------------------------------|----------------------------------------------|  
|プロジェクト ファイル<br /><br />.dbproj (Visual Studio 2010 データベースおよびサーバー プロジェクト、データ層アプリケーション プロジェクト) プロジェクト ファイル。<br /><br />CLR の .csproj および .vbproj プロジェクト ファイルは変換できますが、データ損失が生じる可能性があります。|データベース単体テスト プロジェクト。<br /><br />部分プロジェクト (.files アイテムなど)。|  
|プロパティ ファイル<br /><br />*.sqldeployment、.sqlsettings、および .sqlpolicy ファイルは、対応するプロジェクト プロパティ ページに変換されます。<br /><br />.sqlpermissions ファイルは Transact\-SQL スクリプトに変換されます|プロジェクト プロパティ<br /><br />Server.sqlsettings。<br /><br />.sqlcmd ファイルで定義されている SQLCMD 変数。|  
|.sql ファイルは、既存のフォルダー構造を使用してインポートされます。|機能拡張ファイル。|  
|配置前スクリプトおよび配置後スクリプト。|データベース参照は、プロジェクトの変換後に、手動で再確立する必要があります。|  
|スキーマ比較ファイル。|データ生成ファイル。|  
  
### <a name="to-convert-a-project"></a>プロジェクトを変換するには  
  
1.  SQL Server 2005 または 2008 データベース プロジェクトを開きます。  
  
2.  **"SQL Server データベース プロジェクトに変換する"** ウィザードが自動的に開きます。 **[SQL Server データベース プロジェクトに変換する]** を選択し、 **[OK]** をクリックします。 既存のファイルをバックアップするという既定の設定はオンにしておきます。  
  
3.  変換レポートが自動的に生成され、変換されたすべてのファイルが一覧表示されます。 変換プロセスの詳細情報を表示するには、プロジェクト ファイル名の横にある **+** 記号をクリックします。  
  
4.  **ソリューション エクスプローラー**で、プロジェクト ファイル、プロパティ ファイル、およびスキーマ オブジェクトがすべて変換されていることを確認します。  
  
### <a name="to-change-a-projects-target-platform"></a>プロジェクトのターゲット プラットフォームを変更するには  
  
1.  **ソリューション エクスプローラー**で、新しく変換されたプロジェクトを右クリックし、 **[プロパティ]** をクリックして、 **[プロジェクトの設定]** ダイアログ ボックスを開きます。  
  
2.  **[ターゲット プラットフォーム]** ボックスの一覧で、SSDT でサポートされている任意のプラットフォームをクリックします。  
  
## <a name="see-also"></a>参照  
[方法:ターゲット プラットフォームを変更し、データベース プロジェクトを公開する](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)  
  
