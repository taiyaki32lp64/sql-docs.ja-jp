---
title: Visual Studio .NET で Visual Basic SMO プロジェクトを作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic [SMO]
ms.assetid: d7a3892c-0f1c-4c4d-8480-b58dce3720bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 662916720b9953e0374bedb29890a36ced0cfac0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62753347"
---
# <a name="create-a-visual-basic-smo-project-in-visual-studio-net"></a>Visual Studio .NET での Visual Basic SMO プロジェクトの作成
  このセクションでは、簡単な SMO コンソール アプリケーションを構築する方法について説明します。  
  
 この例では、プログラムが SMO の型を参照できるように、名前空間をインポートします。 `Agent` 名前空間のインポートは省略可能です。 使用するプログラムを記述するときに使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント。 `Common` 名前空間は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへのセキュリティで保護された接続を確立するために必要です。 `SqlClient` 名前空間は、SQL 例外エラーの処理を行うために使用されます。  
  
### <a name="creating-a-visual-basic-smo-project-in-visual-studionet"></a>Visual Studio .NET での Visual Basic SMO プロジェクトの作成  
  
1.  [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] または [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)] を起動します。  
  
2.  **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3.  **プロジェクトの種類**ダイアログ ボックスで、 **Visual Basic**、し、 **Windows**します。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]インストールされたテンプレート ウィンドウで、**コンソール アプリケーションです。**  
  
4.  (省略可能)**名前**フィールドに、新しいアプリケーションの名前を入力します。  
  
5.  クリックして**OK**を読み込む、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]コンソール アプリケーション テンプレート。  
  
6.  **[プロジェクト]** メニューの **[参照の追加]** を選択します。 **[参照の追加]** ダイアログ ボックスが表示されます。  
  
7.  クリックして**参照**C:\Program files \microsoft SQL server \120\sdk\assemblies フォルダー内で SMO アセンブリを検索、および、次のファイルを選択します。 これらは、SMO アプリケーションのビルドに最低限必要なファイルです。  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc  
  
    > [!NOTE]  
    >  使用して、`Ctrl`キーでは、複数のファイルを選択します。  
  
8.  必要に応じて任意の SMO アセンブリを追加します。 たとえば、[!INCLUDE[ssSB](../../includes/sssb-md.md)] に特化したプログラミングを行っている場合は、以下のアセンブリを追加します。  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. **[開く]** をクリックします。  
  
10. **ビュー**  メニューのをクリックして**コード**。 - または - コード ウィンドウを表示する Module1.vb ウィンドウを選択します。  
  
11. コードで、宣言の前に、次の入力**Imports** SMO 名前空間の型を修飾するステートメント。  
  
    ```  
    Imports Microsoft.SqlServer.Management.Smo  
    Imports Microsoft.SqlServer.Management.Common  
    ```  
  
12. SMO では、Microsoft.SqlServer.Management.Smo の下に、Microsoft.SqlServer.Management.Smo.Agent などのさまざまな名前空間があります。 これらの名前空間は、必要に応じて追加します。  
  
13. SMO コードを追加できます。  
  
  
