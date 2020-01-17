---
title: '手順 1: pymssql Python 開発環境を構成する |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bf2942b79cf7e72efbb36a53019de8208cd3b8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935827"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>ステップ 1: pymssql Python 開発用に開発環境を構成する
SQL Server 用の Python ドライバーを使用してアプリケーションを開発するためには、前提条件を使用して開発環境を構成する必要があります。    
  
Python SQL ドライバーでは、SQL Server と Azure SQL Database で既定で有効になっている TDS プロトコルが使用されていることに注意してください。  追加の構成は必要ありません。  
  
## <a name="windows"></a>Windows  
  
1. **Python ランタイムと pip パッケージマネージャーをインストールする**  
A. [Python.org](https://www.python.org/downloads/)にアクセス  
B. 適切な Windows インストーラーの msi リンクをクリックします。   
c. ダウンロードが完了したら、msi を実行して Python ランタイムをインストールします  
  
2. **Pymssql モジュール**を[ここ](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)からダウンロード  
  
    正しい .whl ファイルを選択していることを確認します。  例:64 ビットコンピューターで Python 2.7 を使用している場合は、: pymssql-2.1.1-cp27-none-win_amd64 を選択します。 ファイルをダウンロードしたら、C:/Python27.pdb ですフォルダーに配置します。  
      
3. **Cmd.exe を開きます。**  
  
4. **Pymssql モジュールのインストール**     
    たとえば、64ビットコンピューターで Python 2.7 を使用している場合は、次のようになります。  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Python ランタイムと pip パッケージマネージャーをインストール**する Python は、Ubuntu のほとんどのディストリビューションにプレインストールされています。  コンピューターに python がインストールされていない場合は、 [python.org](https://www.python.org/downloads/)からソースの tar ファイルをダウンロードしてローカルでビルドするか、パッケージマネージャーを使用することができます。  
```  
> sudo apt-get install python   
```  
  
2.  **ターミナルを開く**  
  
3.  **Pymssql モジュールと依存関係のインストール**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Python ランタイムと pip パッケージマネージャーをインストールする**  
A. [Python.org](https://www.python.org/downloads/)にアクセス  
B. 適切な Mac インストーラー pkg リンクをクリックします。   
c. ダウンロードが完了したら、pkg を実行して Python ランタイムをインストールします  
  
2.  **ターミナルを開く**  
  
3. **Homebrew パッケージマネージャーのインストール**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **FreeTDS モジュールのインストール**  
```  
> brew install FreeTDS  
```  
  
5.  **Pymssql モジュールのインストール**  
```  
> sudo -H pip install pymssql  
```
