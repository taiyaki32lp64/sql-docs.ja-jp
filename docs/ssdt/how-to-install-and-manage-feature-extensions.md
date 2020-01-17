---
title: 方法:機能拡張のインストールと管理 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9cdc8cd5-c36f-4bee-a191-87ed457803e7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a7d2f4fa27623a75bd49a32a7ce800801f63e9f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929596"
---
# <a name="how-to-install-and-manage-feature-extensions"></a>方法:機能拡張のインストールと管理
データベース コードを分析するルール、データベース単体テストの条件、およびビルド/配置コントリビューターを追加すると、SQL Server Data Tools などの Visual Studio エディションに用意されている機能を拡張できます。 ただし、機能拡張を自分で作成したか、他のユーザーが作成したかにかかわらず、機能拡張を使用するには、あらかじめインストールしておく必要があります。  
  
機能拡張をインストールする場所は、機能拡張の種類と、使用する場所によって変わります。 最新エディションの Visual Studio では、一部のコンポーネントのインストール場所は SQL Server のインストール ディレクトリから Visual Studio ディレクトリ内に移動されました。 そのため、複数バージョンのソフトウェアを簡単に併用できるようになりましたが、複数バージョンの SQL Server Data Tools やコマンド ラインから使用する場合は、状況に応じて複数の場所に機能拡張をインストールする必要があります。  
  
### <a name="installing-extensions-for-use-inside-visual-studio"></a>Visual Studio 内で使用する機能拡張のインストール  
  
|拡張機能の種類|インストール場所|  
|------------------|--------------------|  
|SQL Server の単体テストのカスタム テスト条件|<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\TestConditions|  
|ビルド コントリビューター<br /><br />配置コントリビューター<br /><br />静的コード分析ルール|<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions|  
  
<Visual Studio Install Dir> は、使用している Visual Studio のバージョンとインストール場所によって変わります。 Visual Studio 2012 の場合、通常は C:\Program Files (x86)\\MicrosoftVisual Studio 11.0 です。 Visual Studio 2013 の場合、通常は C:\Program Files (x86)\\MicrosoftVisual Studio 12.0 です。  
  
機能拡張は、コマンド ライン サービスの一部として実行できます。  
  
|拡張機能の種類|コマンド ライン サービス|インストール フォルダー|  
|------------------|------------------------|------------------|  
|SQL Server の単体テストのカスタム テスト条件|MSBuild または MSTest を使用して、Visual Studio 2013 の開発者コマンド プロンプトなどのコマンド ライン ツールから単体テストを実行できます。|Visual Studio 内で実行する場合と同じです。|  
|ビルド コントリビューター<br /><br />配置コントリビューター|[SqlPackage.exe](../tools/sqlpackage.md)。または、データベース プロジェクトをビルドするときに MSBuild のターゲットの配置または公開を使用します。|MSBuild:Visual Studio 内で実行する場合と同じです。<br /><br />[SqlPackage.exe](../tools/sqlpackage.md):Visual Studio ディレクトリ内にある場合は、上記と同じです。<br /><br />SqlPackage.exe と他の DacFx DLL がそのディレクトリ以外の場所にある場合、機能拡張は同じディレクトリか、C:\Program Files (x86)\\MicrosoftSQL Server\120\DAC\bin\Extensions 内に配置する必要があります。|  
|静的コード分析ルール|MSBuild を使用して、プロジェクトをビルドし、静的コード分析を実行できます。<br /><br />また、作成したアプリケーションから、CodeAnalysisService API を使用してコード分析を実行することもできます。 この場合、機能拡張のルックアップ ルールは、SqlPackage.exe を使用する場合と同様に機能します。|ビルド コントリビューターと配置コントリビューターで同じフォルダーが使用されます|  
  
> [!NOTE]  
> プログラム ファイル フォルダー内のインストール ディレクトリにアクセスするには、コンピューターの管理者アクセス許可を持っている必要があります。 適切なアクセス許可を持っていない場合は、ネットワーク管理者に問い合わせてください。  
  
**セキュリティに関する考慮事項**  
  
自分で作成していない機能拡張をインストールする場合、あらかじめ次のリスクを理解しておく必要があります。  
  
-   機能拡張のインストール プログラムは、悪意のあるプログラムで、インストールが許可されると保護されたリソースにアクセスできるようになる可能性があります。  
  
-   機能拡張自体に悪意があり、機能拡張を使用するユーザーが十分な権限が持っている場合は、保護されているリソースを制御できるようになる可能性があります。  
  
リスクを最小限に抑えるために、ソースがわかっている場合にのみ機能拡張をインストールするようにしてください。 信頼できないソースから機能拡張を入手する場合、インストールして使用する前に、機能拡張のソース コードとそのインストール プログラム (存在する場合) を調べる必要があります。  
  
## <a name="to-install-a-custom-feature-extension"></a>カスタムの機能拡張をインストールするには  
署名したアセンブリ (.dll) を正しいインストール フォルダーにコピーします。 Visual Studio を閉じて、開き直します。 機能拡張を使用できるようになります。  
  
## <a name="see-also"></a>参照  
[データベース機能の拡張](../ssdt/extending-the-database-features.md)  
  
