---
title: 変数値ファイル (MySQLToSQL) の作成 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Creating variable value files
- variable value file validation
ms.assetid: 1dc56a7b-8e3a-4576-ad4f-47050bf7e28a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: be1530bdec1c1523a873dc93b1d70e6e72c880ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103021"
---
# <a name="creating-variable-value-files-mysqltosql"></a>変数値ファイルの作成 (MySQLToSQL)
変数値ファイルは、別に 1 つのサーバーの移行から頻繁に変更されるように、送信元または送信先のサーバー名のコマンドのパラメーターの値を構成する XML ファイルです。 各ソース サーバーの値を格納するための複数の変数ファイルが作成されでマスター スクリプト ファイルで参照されている多数のデータベースの移行が発生したとき、 **-v**コマンド ライン スイッチします。 これにより、複数の変数ファイルの変数の値をいくつかのスクリプト ファイルの静的な値を維持するためにします。  
  
> [!NOTE]  
> 1.  変数の名前はプレフィックスし、$ (ドル) 記号が付いています。 変数は、変数値ファイルで値が割り当てられていない場合はその結果、コンソールの実行プロセスを停止するスクリプト ファイルの解析中にエラーが発生します。  
> 2.  エスケープ文字 **$** は **$$** します。 パラメーターの変数または静的な値の値を含むかどうか **$** し (ドル) シンボル **$$** 変数ではなく文字として扱うことを指定する必要があります。  
> 3.  保守容易性のために、内部で変数を宣言できます`'variable-group'`ユーザーの論理的な分離の要素は、変数を定義します。  この要素の使用は必須ではありません。  
  
**使用例:**  
  
**例 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<folder-name>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**例 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetUserName$ value="<user-name>"/>  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>変数値ファイルの検証  
ユーザーは、スキーマ定義ファイルに対して自分の変数値ファイルを検証できます簡単に **'ConsoleScriptVariablesSchema.xsd'** 'スキーマ' フォルダー内にあります。  
  
## <a name="next-step"></a>次の手順  
コンソールの運用には、次の手順は[サーバー接続ファイルを作成する&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>関連項目  
[サーバー接続ファイル (MySQL) を作成します。](https://msdn.microsoft.com/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  
