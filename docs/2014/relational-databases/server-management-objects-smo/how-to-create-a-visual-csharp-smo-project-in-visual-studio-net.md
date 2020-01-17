---
title: Visual Studio .NET で Visual c# SMO プロジェクトの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 371da8231138fb43e9b001808b9fb88ad09543b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63131643"
---
# <a name="create-a-visual-c-smo-project-in-visual-studio-net"></a>Visual Studio .NET での Visual C# SMO プロジェクトの作成
  このセクションでは、簡単な SMO コンソール アプリケーションを構築する方法について説明します。  
  
 この例では、プログラムが SMO の型を参照できるように、名前空間をインポートします。 `Agent` 名前空間のインポートは省略可能です。 使用するプログラムを記述するときに使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント。 `Common` 名前空間は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへのセキュリティで保護された接続を確立するために必要です。 `SqlClient` 名前空間は、SQL 例外エラーの処理を行うために使用されます。  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Visual studio.net で Visual c# SMO プロジェクトを作成します。  
  
1.  [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] または [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)] を起動します。  
  
2.  **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3.  **プロジェクトの種類**ダイアログ ボックスで、 **Visual c#** 、し、 **Windows**します。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]インストールされたテンプレート ウィンドウで、 **Windows アプリケーション**します。  
  
4.  (省略可能)**名前**フィールドに、新しいアプリケーションの名前を入力  
  
5.  Visual C# アプリケーションの種類を選択します。 たとえば、次の選択**コンソール アプリケーション**します。  
  
6.  **[プロジェクト]** メニューの **[参照の追加]** を選択します。 **[参照の追加]** ダイアログ ボックスが表示されます。  
  
7.  クリックして**参照**で SMO アセンブリを探し、[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]フォルダー、し、次のファイルを選択します。 これらは、SMO アプリケーションのビルドに最低限必要なファイルです。  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
    > [!NOTE]  
    >  使用して、`Ctrl`キーでは、複数のファイルを選択します。  
  
8.  必要に応じて任意の SMO アセンブリを追加します。 たとえば、[!INCLUDE[ssSB](../../includes/sssb-md.md)] に特化したプログラミングを行っている場合は、以下のアセンブリを追加します。  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. **[開く]** をクリックします。  
  
10. **ビュー**  メニューのをクリックして**コード**。 - または - Program1.cs [デザイン] の Windows を選択して、コード ウィンドウを表示する windows フォームをダブルクリックします。  
  
11. コードでは、名前空間ステートメントの前に、次の `using` ステートメントを入力し、SMO 名前空間の型を修飾します。  
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
12. SMO では、Microsoft.SqlServer.Management.Smo の下に、Microsoft.SqlServer.Management.Smo.Agent などのさまざまな名前空間があります。 これらの名前空間は、必要に応じて追加します。  
  
13. SMO コードを追加できます。  
  
  
