---
title: ストアド プロシージャの作成 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7beb77adf595b055a6c1e4a7543b428a06ce7640
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62703089"
---
# <a name="creating-stored-procedures"></a>ストアド プロシージャの作成
  ストアド プロシージャを使用するには、これを共通言語ランタイム (CLR) クラスまたはコンポーネント オブジェクト モデル (COM) クラスに関連付ける必要があります。 クラスは、の形式では、通常のサーバーにインストールする必要があります、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® ダイナミック リンク ライブラリ (DLL)、およびサーバー上またはアセンブリとして登録されている、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データベース。  
  
 ストアド プロシージャはサーバーまたはデータベースに登録されています。 サーバーのストアド プロシージャは、どのクエリ コンテキストからでも呼び出すことができます。 データベースのストアド プロシージャは、データベース コンテキストが、ストアド プロシージャが定義されているデータベースの場合にのみアクセスできます。 あるアセンブリの関数が別のアセンブリの関数を呼び出す場合は、両方のアセンブリを同じコンテキスト (サーバーまたはデータベース) に登録する必要があります。 サーバーまたは、展開済みの[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データベース サーバーで使用できます[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]アセンブリに登録します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの場合は、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] デザイナーを使用してプロジェクトにアセンブリを登録できます。  
  
> [!IMPORTANT]  
>  COM アセンブリにより、セキュリティ上のリスクが生じる可能性があります。 このリスクやその他の考慮事項により、[!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)] では、COM アセンブリが非推奨とされました。 COM アセンブリは、今後のリリースではサポートされない可能性があります。  
  
## <a name="registering-a-server-assembly"></a>サーバー アセンブリの登録  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のオブジェクト エクスプローラーで、サーバー アセンブリは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスの Assemblies フォルダーに一覧表示されます。 サーバー アセンブリには .NET (CLR) アセンブリと COM ライブラリの両方を含めることができます。  
  
### <a name="to-create-a-server-assembly"></a>サーバー アセンブリを作成するには  
  
1.  インスタンスを展開[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]オブジェクト エクスプ ローラーで右クリックし、**アセンブリ**フォルダー、およびクリック**新しいアセンブリ**します。 これが表示されます、**サーバー アセンブリの登録** ダイアログ ボックス。  
  
2.  **型**アセンブリの種類を指定します。  
  
    -   マネージド コード (CLR) DLL の場合は、.NET アセンブリを指定します。  
  
    -   ネイティブ コード (COM) DLL の COM DLL を指定します。  
  
3.  **ファイル名**、ストアド プロシージャを含む DLL を指定します。  
  
4.  **アセンブリ名**アセンブリの名前を指定します。  
  
5.  これが、デバッグ ビルドの場合、ライブラリのデバッグを使用しているストアド プロシージャ、選択、**デバッグ情報を含める**チェック ボックスをオンします。 ストアド プロシージャのデバッグの詳細については、次を参照してください。[ストアド プロシージャのデバッグ](debugging-stored-procedures.md)します。  
  
6.  クリックすることができます**ok**即座に、またはダイアログ ボックスのツールバーで、アセンブリの登録でコマンドをクリックすることができます、**スクリプト**をクエリ ウィンドウ、ファイル、またはクリップボードへの登録操作をスクリプト化 メニュー。  
  
 サーバー アセンブリを登録した後は、オブジェクト エクスプ ローラーでアセンブリを右クリックし、をクリックして構成できます**プロパティ**します。  
  
## <a name="registering-a-database-assembly-on-the-server"></a>サーバーへのデータベース アセンブリの登録  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のオブジェクト エクスプローラーで、データベース アセンブリは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの Assemblies フォルダーに一覧表示されます。 データベース アセンブリには .NET (CLR) アセンブリと COM ライブラリの両方を含めることができます。  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>サーバーでデータベース アセンブリを作成するには  
  
1.  インスタンスを展開、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]オブジェクト エクスプ ローラーでデータベースを右クリックして、**アセンブリ**フォルダー、およびクリック**新しいアセンブリ**します。 これが表示されます、**データベース アセンブリの登録** ダイアログ ボックス。  
  
2.  **型**アセンブリの種類を指定します。  
  
    -   マネージド コード (CLR) DLL の場合は、.NET アセンブリを指定します。  
  
    -   ネイティブ コード (COM) DLL の場合は、COM DLL を指定します。  
  
3.  **ファイル名**、ストアド プロシージャを含む DLL を指定します。  
  
4.  **アセンブリ名**アセンブリの名前を指定します。  
  
5.  これが、デバッグ ビルドの場合、ライブラリのデバッグを使用しているストアド プロシージャ、選択、**デバッグ情報を含める**チェック ボックスをオンします。 ストアド プロシージャのデバッグの詳細については、次を参照してください。[ストアド プロシージャのデバッグ](debugging-stored-procedures.md)します。  
  
6.  クリックすることができます**ok**即座に、またはダイアログ ボックスのツールバーで、アセンブリの登録でコマンドをクリックすることができます、**スクリプト**をクエリ ウィンドウ、ファイル、またはクリップボードへの登録操作をスクリプト化 メニュー。  
  
 データベース アセンブリを登録した後は、オブジェクト エクスプ ローラーでアセンブリを右クリックし、をクリックして構成できます**プロパティ**します。  
  
## <a name="registering-a-database-assembly-in-a-project"></a>プロジェクトへのデータベース アセンブリの登録  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のソリューション エクスプローラーで、データベース アセンブリは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの Assemblies フォルダーに一覧表示されます。 データベース アセンブリには .NET (CLR) アセンブリと COM ライブラリの両方を含めることができます。  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>Analysis Services プロジェクトにデータベース アセンブリを作成するには  
  
1.  インスタンスを展開、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]オブジェクト エクスプ ローラーでデータベースを右クリックして、**アセンブリ**フォルダー、およびクリック**新しいアセンブリ参照**します。 これが表示されます、**参照の追加** ダイアログ ボックス。 **.NET**のタブ、**参照の追加**ダイアログ ボックスは、既存の .NET (CLR) アセンブリを一覧表示中に、**プロジェクト**タブには、プロジェクトが一覧表示されます。  
  
2.  既存のコンポーネントまたはプロジェクトをクリックしてをクリックし、**追加**に追加する、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]プロジェクト。 COM DLL への参照を追加するには、クリックして、**参照**ファイルを検索するタブ。 **選択されたプロジェクトとコンポーネント**一覧には、名前、種類、バージョン、およびプロジェクトに追加する各コンポーネントの場所が表示されます。  
  
3.  追加するコンポーネントの選択が完了したら**OK**に追加する、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]プロジェクト。  
  
## <a name="script-format-for-an-assembly"></a>アセンブリのスクリプト形式  
 .NET アセンブリの登録は簡単です。 .NET アセンブリは次の形式を使用してバイナリ形式でデータベースに追加されます。  
  
```  
<Create>  
   <ObjectDefinition>  
      <Assembly>  
         <Files>  
            <File>  
               <Name>filename</Name>  
               <Type>filetype</Type>  
               <Data>  
                  <Block>binarydatablock</Block>  
                  <Block>binarydatablock</Block>  
                  ...  
               </Data>  
            </File>  
         </Files>  
         <PermissionSet>PermissionSet</PermissionSet>  
      </Assembly>  
   <ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>参照  
 [多次元モデルのアセンブリの管理](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [ストアド プロシージャの定義](defining-stored-procedures.md)  
  
  
