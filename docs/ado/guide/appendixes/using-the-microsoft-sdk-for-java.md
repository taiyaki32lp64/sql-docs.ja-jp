---
title: Java 用の Microsoft SDK の使用 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0e6c5f2eb5ad792141e77122ff9e132d97f62ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926463"
---
# <a name="using-the-microsoft-sdk-for-java"></a>Microsoft SDK for Java を使用する

> [!IMPORTANT]
> Microsoft では、2004 年 1 月で Visual j のサポートが廃止されました。

Microsoft SDK for Java は、Microsoft Internet Explorer の環境の開発キットです。 Java プログラムや JDK 1.1 および Microsoft Win32 仮想マシン (Microsoft VM) に基づくアプレットの開発に役立つツール、情報、およびサンプルが提供されます。 Microsoft SDK for Java は、関連付けられていないに Microsoft Visual j します。 この SDK をダウンロードするには、ここをクリックします。  
  
 Jactivex.exe ユーティリティでは、タイプ ライブラリからクラスを生成しますが、コマンドラインで呼び出すことができますのみ。 この機能は、Visual j 開発環境と統合されていません。 Java タイプ ライブラリのウィザードによって生成されたクラスとは異なりは、SDK によって作成されたクラス ラッパーにステップ インできます。 これは、コードで ADO のラッパー クラスを使用する方法をデバッグするために役立ちます。  
  
 このメカニズムは、ADO のタイプ ライブラリを読み取って、アプリケーション内でインスタンス化できるクラスが生成されます。 次の場所にそれらのクラスが生成されます: \\< windows directory\>\Java\trustlib\msado15 します。  
  
 Java 用 Microsoft SDK を使用して Java で ADO アプリケーションを作成することは、根本的にまったく同じでは、ソース コードの観点から Java 型ライブラリのウィザードを使用してです。 サンプル コードでは、次を参照してください。 [ADO Java クラス ラッパー](../../../ado/guide/appendixes/ado-java-class-wrappers.md)します。 唯一の違いは、最初に、次の手順で示したラッパー クラスを生成する方法です。  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Microsoft sdk for Java ADO プロジェクトを作成するには  
  
1.  コマンド プロンプトで、次を実行します。 Microsoft SDK for Java の Bin ディレクトリを格納するパスを設定または、その場所からのコマンドを実行する必要があります。 通常、Microsoft SDK for Java は、Visual Studio と同じ場所にインストールされます。 これは、1 つのコマンド ステートメントです。  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  生成されたクラスをコンパイルするには、次のコマンドを実行します。 トレースできるように、デバッグ シンボルの生成を/g:t スイッチがオンにします。Java の記号。 リリース ビルドの場合は、それを削除します。  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  これらのファイルを使用するには、プロジェクトを開く Visual j で。 **プロジェクト**] メニューの [選択**プロジェクトに追加**します。 選択**ファイル**、すべての追加とします。Trustlib\msado15 ディレクトリをプロジェクトで生成された JAVA ファイル。  
  
## <a name="see-also"></a>参照  
 [ADO Java クラス ラッパー](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
