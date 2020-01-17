---
title: 'ステップ 1: Node.js 開発用に開発環境を構成する | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce89cc12c7493522de55adffb69fcbe3307cbdf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003764"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>ステップ 1: Node.js 開発用に開発環境を構成する
SQL Server 用の node.js ドライバーを使用してアプリケーションを開発するためには、前提条件を使用して開発環境を構成する必要があります。  最も一般的な方法は、ノードパッケージマネージャー (npm) を使用して面倒なモジュールをインストールすることですが、必要に応じて、単調なモジュールを[Github](https://github.com/pekim/tedious)で直接ダウンロードすることもできます。  
  
Node.js ドライバーは、SQL Server と Azure SQL Database で既定で有効になっている TDS プロトコルを使用することに注意してください。  追加の構成は必要ありません。  
  
## <a name="windows"></a>Windows  
  
1. **Node.js ランタイムと npm パッケージマネージャーのインストール**  
A. [Node.js](https://nodejs.org/en/download/)にアクセス  
B. 適切な Windows インストーラーの msi リンクをクリックします。   
c. ダウンロードが完了したら、msi を実行して node.js をインストールします。  
  
2. **Cmd.exe を開きます。**  
  
3. **プロジェクトディレクトリを作成**し、そこに移動します。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **ノードプロジェクトを作成します。**  プロジェクトの作成時に既定値を保持するには、プロジェクトが作成されるまで enter キーを押します。 この手順の最後に、プロジェクトディレクトリにパッケージの json ファイルが表示されます。  
```  
> npm init  
```  
  
5. **tedious モジュールをプロジェクトにインストールします。**  これは、ドライバーが SQL Server と通信するために使用する TDS プロトコルの実装です。  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **ターミナルを開く**  
  
2. **Node.js ランタイムをインストールする**  
```  
>sudo apt-get install node  
```  
3. **Npm のインストール (ノードパッケージマネージャー)**  
```  
> sudo apt-get install npm  
```  
4. **プロジェクトディレクトリを作成**し、そこに移動します。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **ノードプロジェクトを作成します。**  プロジェクトの作成時に既定値を保持するには、プロジェクトが作成されるまで enter キーを押します。 この手順の最後に、プロジェクトディレクトリにパッケージの json ファイルが表示されます。  
```  
> sudo npm init  
```  
  
6. **tedious モジュールをプロジェクトにインストールします。**  これは、ドライバーが SQL Server と通信するために使用する TDS プロトコルの実装です。  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Node.js ランタイムと npm パッケージマネージャーのインストール**  
A. [Node.js](https://nodejs.org/en/download/)にアクセス  
B. 適切な Mac OS インストーラーのリンクをクリックします。  
c. ダウンロードが完了したら、dmg を実行して node.js をインストールします。  
  
2. **ターミナルを開く**  
  
3. **プロジェクトディレクトリを作成**し、そこに移動します。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **ノードプロジェクトを作成します。**  プロジェクトの作成時に既定値を保持するには、プロジェクトが作成されるまで enter キーを押します。 この手順の最後に、プロジェクトディレクトリにパッケージの json ファイルが表示されます。  
```  
> npm init  
```  
  
5. **tedious モジュールをプロジェクトにインストールします。**  これは、ドライバーが SQL Server と通信するために使用する TDS プロトコルの実装です。  
```  
> npm install tedious  
```  
  
