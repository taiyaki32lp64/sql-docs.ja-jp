---
title: セキュリティ ロール (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], roles
- Analysis Services objects, roles
- security [Analysis Services], roles
- roles [Analysis Services], about roles
- server roles [Analysis Services]
- database roles [Analysis Services]
- roles [Analysis Services]
- storing data [Analysis Services], roles
- access rights [Analysis Services], roles
ms.assetid: 5b7e9cef-ff68-4d8e-99bc-e0094ced1baa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e63ef1a2463f65e108ade9a43b748e02831da57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62725256"
---
# <a name="security-roles--analysis-services---multidimensional-data"></a>セキュリティ ロール (Analysis Services - 多次元データ)
  ロールは、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] で使用されます。 一般的に、ロールでは、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]インスタンスによって管理されるオブジェクトに定義されている特定のアクセス権や権限を持つ Microsoft Windows ユーザーおよびグループのセキュリティ識別子 (SID) が関連付けられます。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]には次の 2 種類のロールが用意されています。  
  
-   サーバー ロール。管理者が [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]インスタンスにアクセスできるようにするための固定ロールです。  
  
-   データベース ロール。管理者以外のユーザーによるオブジェクトやデータへのアクセスを制御するために、管理者によって定義されるロールです。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のセキュリティは、ロールと権限に基づいて管理されます。 ロールはユーザーのグループです。 ユーザー (メンバーとも呼ばれる) はロールに追加したり、ロールから削除したりできます。 オブジェクトに対する権限はロールによって指定されます。ロールのすべてのメンバーは、そのロールが権限を持つオブジェクトを使用できます。 ロールのすべてのメンバーは、オブジェクトに対して等しい権限を持ちます。 権限はオブジェクトに対して適用されます。 各オブジェクトは、そのオブジェクトに対して許可された権限のコレクションを持ちます。複数の異なる権限セットを 1 つのオブジェクトに付与できます。 オブジェクトの権限コレクションに含まれる各権限には、1 つのロールが割り当てられています。  
  
## <a name="role-and-role-member-objects"></a>Role オブジェクトと Role Member オブジェクト  
 ロールは、ユーザー (メンバー) のコレクションを格納するオブジェクトです。 ロール定義は、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]のユーザーのメンバーシップを設定します。 権限はロールに基づいて割り当てられます。したがって、ユーザーがオブジェクトにアクセスするためには、いずれかのロールのメンバーになる必要があります。  
  
 <xref:Microsoft.AnalysisServices.Role> オブジェクトは、Name、ID、および Members の各パラメーターで構成されます。 Members は文字列のコレクションです。 各メンバーには "domain\username" という形式のユーザー名が含まれます。 Name はロールの名前を表す文字列です。 ID はロールの一意な識別子を表す文字列です。  
  
### <a name="server-role"></a>サーバー ロール  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] サーバー ロールは、Windows ユーザーおよびグループによる [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]インスタンスへの管理アクセスを定義します。 このロールのメンバーは、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンスのすべての [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]データベースおよびオブジェクトにアクセスでき、次のタスクを実行できます。  
  
-   SQL Server Management Studio または [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]を使用して、データベースの作成やサーバーレベルのプロパティの設定など、サーバーレベルの管理機能を実行する。  
  
-   分析管理オブジェクト (AMO) を使用して、プログラムで管理機能を実行する。  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のデータベース ロールを保守する。  
  
-   トレースを開始する (プロセス アクセス権を持つデータベース ロールによって実行可能な処理イベントを除く)。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] の各インスタンスには、そのインスタンスを管理できるユーザーを定義するサーバー ロールがあります。 このロールの名前と ID は Administrators で、データベース ロールとは異なり、サーバー ロールは削除できず、権限を追加または削除することもできません。 つまり、ユーザーは [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]のインスタンスのサーバー ロールに含まれているかどうかによって、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]のインスタンスの管理者であるかどうかが決定されます。  
  
### <a name="database-roles"></a>データベース ロール  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のデータベース ロールは、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] データベース内のオブジェクトおよびデータへのユーザー アクセスを定義します。 データベース ロールは [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] データベース内に個別のオブジェクトとして作成され、そのロールが作成されたデータベースのみに適用されます。 Windows ユーザーおよびグループは、管理者によってこのロールに含まれています。管理者は、このロール内の権限も定義します。  
  
 ロールの権限は、メンバーがデータベース内のオブジェクトとデータだけでなく、データベース自体にアクセスして管理できるようにするものです。 各権限には 1 つまたは複数のアクセス権が関連付けられており、アクセス権によってデータベース内の特定のオブジェクトへのアクセスをさらに詳細に制御できるようになっています。  
  
## <a name="permission-objects"></a>Permission オブジェクト  
 権限は、各ロールについて、オブジェクト (キューブやディメンションなど) に関連付けられます。 権限は、ロールのメンバーがオブジェクトに対して実行できる操作を指定します。  
  
 <xref:Microsoft.AnalysisServices.Permission> クラスは抽象クラスです。 そのため、対応するオブジェクトに権限を定義するには、派生クラスを使用する必要があります。 オブジェクトごとに権限の派生クラスが定義されます。  
  
|オブジェクト|クラス|  
|------------|-----------|  
|<xref:Microsoft.AnalysisServices.Database>|<xref:Microsoft.AnalysisServices.DatabasePermission>|  
|<xref:Microsoft.AnalysisServices.DataSource>|<xref:Microsoft.AnalysisServices.DataSourcePermission>|  
|<xref:Microsoft.AnalysisServices.Dimension>|<xref:Microsoft.AnalysisServices.DimensionPermission>|  
|<xref:Microsoft.AnalysisServices.Cube>|<xref:Microsoft.AnalysisServices.CubePermission>|  
|<xref:Microsoft.AnalysisServices.MiningStructure>|<xref:Microsoft.AnalysisServices.MiningStructurePermission>|  
|<xref:Microsoft.AnalysisServices.MiningModel>|<xref:Microsoft.AnalysisServices.MiningModelPermission>|  
  
 権限によって使用可能となるアクションを以下の一覧に示します。  
  
|操作|値|説明|  
|------------|------------|-----------------|  
|[処理]|{`true`, `false`}<br /><br /> 既定値 = `false`|`true` を指定した場合、メンバーはこのオブジェクトと、このオブジェクトに含まれる任意のオブジェクトを処理できます。<br /><br /> Process 権限はマイニング モデルには適用されません。 <xref:Microsoft.AnalysisServices.MiningModel> 権限は常に <xref:Microsoft.AnalysisServices.MiningStructure> から継承されます。|  
|ReadDefinition|{`None`, `Basic`, `Allowed`}<br /><br /> 既定値 = `None`|オブジェクトに関連付けられたデータ定義 (ASSL) をメンバーが読み取れるかどうかを指定します。<br /><br /> `Allowed` を指定した場合、メンバーはオブジェクトに関連付けられた ASSL を読み取ることができます。<br /><br /> `Basic` および `Allowed` は、オブジェクトに含まれるオブジェクトによって継承されます。 `Allowed` は `Basic` および `None` をオーバーライドします。<br /><br /> オブジェクトで DISCOVER_XML_METADATA を使用する場合、`Allowed` を指定する必要があります。 リンク オブジェクトとローカル キューブを作成する場合、`Basic` を指定する必要があります。|  
|Read|{`None`, `Allowed`}<br /><br /> 既定値 = `None` (DimensionPermission の場合は、既定値 = `Allowed`)|スキーマ行セットおよびデータ コンテンツへの読み取りアクセスがメンバーにあるかどうかを指定します。<br /><br /> `Allowed` を指定した場合は、データベースへの読み取りアクセスが許可され、データベースを検出できるようになります。<br /><br /> キューブに対して `Allowed` を指定した場合は、<xref:Microsoft.AnalysisServices.CellPermission> および <xref:Microsoft.AnalysisServices.CubeDimensionPermission> による制限がない限り、スキーマ行セットおよびキューブ コンテンツへの読み取りアクセスが許可されます。<br /><br /> ディメンションに対して `Allowed` を指定した場合は、<xref:Microsoft.AnalysisServices.CubeDimensionPermission> による制限がない限り、ディメンション内のすべての属性への読み取り権限が許可されます。 Read (読み取り) 権限は、<xref:Microsoft.AnalysisServices.CubeDimensionPermission> の静的継承でのみ使用されます。 ディメンションに対して `None` を指定した場合は、ディメンションが非表示になり、集計可能な属性への既定のメンバーのアクセスのみが許可されます。ディメンションに集計不能な属性が含まれる場合はエラーが発生します。<br /><br /> <xref:Microsoft.AnalysisServices.MiningModelPermission> に対して `Allowed` を指定した場合は、スキーマ行セット内のオブジェクトの表示権限と、予測結合の実行権限が許可されます。<br /><br /> **NoteAllowed**するデータベース内のオブジェクトに対する読み取りまたは書き込みが必要です。|  
|書き込み|{`None`, `Allowed`}<br /><br /> 既定値 = `None`|親オブジェクトのデータへの書き込みアクセスがメンバーにあるかどうかを指定します。<br /><br /> <xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.Cube>、および <xref:Microsoft.AnalysisServices.MiningModel> の各サブクラスにアクセスが適用されます。 データベースの <xref:Microsoft.AnalysisServices.MiningStructure> サブクラスには適用されません。検証エラーが発生します。<br /><br /> <xref:Microsoft.AnalysisServices.Dimension> に対して `Allowed` を指定した場合は、ディメンション内のすべての属性への書き込み権限が許可されます。<br /><br /> <xref:Microsoft.AnalysisServices.Cube> に対して `Allowed` を指定した場合は、Type=writeback として定義された各パーティションについて、キューブのセルへの書き込み権限が許可されます。<br /><br /> <xref:Microsoft.AnalysisServices.MiningModel> に対して `Allowed` を指定した場合は、モデル コンテンツの変更権限が許可されます。<br /><br /> [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] では、<xref:Microsoft.AnalysisServices.MiningStructure> に対して `Allowed` を指定しても特に意味はありません。 **注:** 書き込みに設定することはできません`Allowed`読み取りも設定しない限り、 `Allowed`|  
|管理**に注意してください。** データベースのアクセス許可でのみ|{`true`, `false`}<br /><br /> 既定値 = `false`|メンバーがデータベースを管理できるかどうかを指定します。<br /><br /> `true` を指定した場合は、データベース内のすべてのオブジェクトへのアクセスが許可されます。<br /><br /> メンバーは特定のデータベースに対してのみ管理権限を持つことができます。他のデータベースを管理することはできません。|  
  
## <a name="see-also"></a>参照  
 [オブジェクトと操作へのアクセスの承認 &#40;Analysis Services&#41;](../authorizing-access-to-objects-and-operations-analysis-services.md)  
  
  
