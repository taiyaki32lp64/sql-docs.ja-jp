---
title: SQL Server の単体テストのカスタム テスト条件 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 32a15d61-e908-4ae1-a238-4fd0f988d8c8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1292666a44f93d8b8dd551975eed4b7ea46f5ffe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984562"
---
# <a name="custom-test-conditions--for-sql-server-unit-tests"></a>SQL Server の単体テストのカスタム テスト条件
SQL Server 単体テストにはカスタムのテスト条件を追加できます。 ただし、拡張機能を作成したか、他のユーザーが作成した拡張機能をインストールしているかにかかわらず、テスト条件は最初にインストールしないと、使用できません。  
  
自分で作成したのではないテスト条件をインストールする前に、次のリスクを理解する必要があります。  
  
-   テスト条件のインストール プログラムは、悪意のあるプログラムで、インストールが許可されると保護されたリソースにアクセスできるようになる可能性があります。  
  
-   テスト条件自体に悪意があり、拡張機能を使用するユーザーに十分な権限がある場合に、保護されたリソースを制御できるようになる可能性があります。  
  
リスクを最小限に抑えるには、不明なソースからはカスタムのテスト条件をインストールしないようにしてください。 信頼できないソースからテスト条件を入手する場合、インストールする前に、テスト条件のソース コードとそのインストール プログラム (存在する場合) を調べる必要があります。  
  
カスタムのテスト条件をインストールするには、署名したアセンブリ (.dll) を %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions フォルダーにコピーします。 このフォルダーが存在しない場合は作成します。 このディレクトリにコピーするには、コンピューターの管理特権が必要です。  
  
> [!NOTE]  
> 次の場合は、Visual Studio 2010 と Visual Studio 2012 バージョンのテスト条件をインストールする必要があります。  
>   
> -   SQL Server 単体テストのビルドに使用される可能性があるコンピューターにカスタムのテスト条件をインストールする場合。  
> -   これらの単体テストが Visual Studio 2010 と Visual Studio 2012 で使用される場合。  
  
SQL Server 単体テストのカスタムのテスト条件の詳細については、以下を参照してください。  
  
-   [方法: SQL Server 単体テスト デザイナーのテスト条件を作成する](../ssdt/how-to-create-test-conditions-for-the-sql-server-unit-test-designer.md)  
  
-   [方法: Visual Studio 2010 のカスタム テスト条件を、以前のリリースから SQL Server Data Tools にアップグレードする](../ssdt/how-to-upgrade-visual-studio-2010-custom-test-condition-to-ssdt.md)  
  
-   [チュートリアル: カスタム テスト条件を使用してストアド プロシージャの結果を検証する](../ssdt/walkthrough-use-custom-test-condition-to-verify-stored-procedure-results.md)  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストを使用したデータベース コードの検証](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
