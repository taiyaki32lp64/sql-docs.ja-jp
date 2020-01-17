---
title: 'ステップ 1: Ruby 開発用に開発環境を構成する | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38af92d3cb0354bc4b75131a349f6a1c26e90490
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992464"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>ステップ 1: Ruby 開発用に開発環境を構成する
SQL Server 用の Ruby ドライバーを使用してアプリケーションを開発するためには、前提条件を使用して開発環境を構成する必要があります。    
  
Ruby ドライバーでは TDS プロトコルが使用されていることに注意してください。これは SQL Server と Azure SQL Database で既定で有効になっています。  追加の構成は必要ありません。  
  
  
## <a name="windows"></a>Windows  
  
1.  **Ruby インストーラーのダウンロード**  
コンピューターに Ruby がインストールされていない場合は、インストールしてください。 新しい ruby ユーザーの場合は、Ruby 2.2. X インストーラーを使用することをお勧めします。 これらの機能により、安定した言語と、互換性と更新ができるパッケージ (gem) の詳細な一覧が提供されます。 [Ruby ダウンロードページ](https://rubyinstaller.org/downloads/)にアクセスして、該当する 2.1. x インストーラーをダウンロードします。 たとえば、64ビットコンピューターの場合は、Ruby 2.1.6 (x64) インストーラーをダウンロードします。   
  
2.  **Ruby のインストール**  
インストーラーをダウンロードしたら、次の手順を実行します。  
A. ファイルをダブルクリックしてインストーラーを起動します。  
B. 言語を選択し、使用条件に同意します。  
c.  [インストールの設定] 画面で、[Ruby の実行可能ファイルをパスに追加する] の横のチェックボックスをオンにして、この Ruby インストールで rb ファイルと rbw ファイルを関連付けます。  
  
3.  **Ruby DevKit のダウンロード**  
RubyInstaller ページから DevKit をダウンロードする  
  
4.  **Ruby DevKit をインストールする**  
ダウンロードが完了したら、次の手順を実行します。  
A. ファイルをダブルクリックします。 ファイルの抽出先を確認するメッセージが表示されます。  
B. ... をクリックします。 をクリックし、C:\ devkit を選択します。 このフォルダーは、[新しいフォルダーの作成] をクリックして最初に作成する必要があります。  
c. [OK] をクリックし、[Extract] をクリックしてファイルを抽出します。  
  
5. **Cmd.exe を開きます。**  
  
6. **Ruby DevKit の初期化**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **TinyTDS gem をインストールする**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **ターミナルを開く**  
  
2. **Ruby バージョンマネージャー (rvm) と前提条件のインストール**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Rvm を使用して Ruby をインストールする**  
たとえば、Ruby のバージョン2.3.0 をインストールします。  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;最後のコマンドの出力に、バージョン2.3.0 が実行されていることが示されていることを確認します。  
  
4.  **FreeTDS のインストール**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **TinyTDS のインストール**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
OS には依存関係があるため、Mac OS X には既に Ruby が事前にインストールされていることに注意してください。    
  
1.  **ターミナルを開く**  
  
2. **Homebrew パッケージマネージャーのインストール**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **FreeTDS のインストール**  
```  
> brew install FreeTDS  
```  
  
4.  **TinyTDS gem をインストールする**  
```  
> gem install tiny_tds  
```
