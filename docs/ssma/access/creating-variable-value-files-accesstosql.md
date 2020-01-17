---
title: 変数値ファイル (AccessToSQL) の作成 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 051ded7d675f81998718b858c71488ba968ec680
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006593"
---
# <a name="creating-variable-value-files-accesstosql"></a>変数値ファイル (AccessToSQL) の作成
変数値ファイルは、サーバーの移行の間で頻繁に変更される (送信元または送信先のサーバー名) などのコマンドのパラメーター値を構成する XML ファイルです。 各ソース サーバーの値を格納するための複数の変数ファイルが作成されでマスター スクリプト ファイルで参照されている多数のデータベースの移行が発生すると、 **-v**コマンド ライン スイッチします。 この動作は、変数の複数のファイルで変数の値を持ついくつかのスクリプト ファイルの静的な値を維持するために役立ちます。  
  
> [!NOTE]  
> -  変数の名前はプレフィックスし、$ (ドル) 記号が付いています。 変数に変数値ファイルの値が割り当てられていない場合、スクリプト ファイルの解析中にエラーが発生、失速、コンソールの実行プロセスの結果として得られる。  
> -  エスケープ文字 **$** は **$$** します。 パラメーターの変数または静的な値の値が含まれている場合、 **$** し (ドル) シンボル **$$** 変数ではなく文字として扱うことを指定する必要があります。  
> -  保守容易性のために、内部で変数を宣言できます`'variable-group'`ユーザー定義変数の論理的な分離の要素。  この要素の使用は必須ではありません。  
  
**使用例:**  
  
**例 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**例 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>変数値ファイルの検証  
ユーザーは、スキーマ定義ファイルに対して自分の変数値ファイルを検証できます簡単に**ConsoleScriptVariablesSchema.xsd** 'スキーマ' フォルダー内にあります。  
  
## <a name="next-step"></a>次の手順  
コンソールの運用には、次の手順は[サーバー接続ファイルを作成する&#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>関連項目  
[サーバー接続ファイル (アクセス) を作成します。](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
