---
title: データ型を扱います。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d516901a3e44def9a0d6e19414bf0b972f9b37dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63229082"
---
# <a name="working-with-data-types"></a>データ型の処理
  データは、定義済みの長さを持つ文字列、特定の精度を持つ数値、または独自のルール セットを持つ別のオブジェクトであるユーザー定義データ型など、さまざまな型およびサイズで表現されます。 <xref:Microsoft.SqlServer.Management.Smo.DataType>で正しく処理できるように、オブジェクトがデータの種類を分類して[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 <xref:Microsoft.SqlServer.Management.Smo.DataType> オブジェクトは、データを受け入れるオブジェクトに関連付けられています。 次の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) オブジェクトに渡すデータは、<xref:Microsoft.SqlServer.Management.Smo.DataType> オブジェクト プロパティによって定義されている必要があります。  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 データを受け入れるオブジェクトの `DataType` プロパティは、次のいくつかの方法で設定することができます。  
  
-   既定のコンストラクターを使用して、<xref:Microsoft.SqlServer.Management.Smo.DataType> オブジェクト プロパティを明示的に指定する。  
  
-   オーバーロードされたコンストラクターを使用して、<xref:Microsoft.SqlServer.Management.Smo.DataType> プロパティをパラメーターとして指定する。  
  
-   オブジェクト コンストラクター内で <xref:Microsoft.SqlServer.Management.Smo.DataType> インラインを指定する。  
  
-   `Int` など、<xref:Microsoft.SqlServer.Management.Smo.DataType> クラスの静的メンバーの 1 つを使用する。 これによって、実際に <xref:Microsoft.SqlServer.Management.Smo.DataType> オブジェクトのインスタンスが返されます。  
  
 <xref:Microsoft.SqlServer.Management.Smo.DataType> オブジェクトには、データの型を定義するいくつかのプロパティがあります。 たとえば、<xref:Microsoft.SqlServer.Management.Smo.SqlDataType> プロパティは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型を指定します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型を表す定数値は <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 列挙にリストされます。 これは、`varchar`、`nchar`、`currency`、`integer`、`float`、および `datetime` などのデータ型を参照します。  
  
 データ型を確立したら、そのデータに対して特定のプロパティを設定する必要があります。 たとえば、`nchar` 型の場合、`Length` プロパティで文字列データの長さを設定する必要があります。 これは、有効桁数と小数点以下桁数を指定する必要のある数値に対しても同様です。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> データ型および <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> データ型は、ユーザーによって定義されるデータの型の定義を含んでいるオブジェクトを参照します。 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> は、<xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 列挙からの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型に基づいています。 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>に基づく[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET データ型。 これらは、組織で定義されているビジネス ルールに従ってデータベースで頻繁に再利用される型のデータを表現していることが普通です。 たとえば、複数の通貨を扱う会社では、金額や通貨基準を格納するデータ型が役に立ちます。  
  
 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 列挙には、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がサポートするすべてのデータ型のリストが含まれています。  
  
## <a name="examples"></a>使用例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>Visual Basic でのコンストラクター内の指定による DataType オブジェクトの構築  
 このコード例では、コンストラクターを使用して各種の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型に基づいたデータ型のインスタンスを作成する方法を示しています。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>、および XML 型にはすべて、オブジェクトを識別するための名前の値が必要です。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes1](SMO How to#SMO_VBDataTypes1)]  -->  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>Visual C# でのコンストラクター内の指定による DataType オブジェクトの構築  
 このコード例では、コンストラクターを使用して各種の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型に基づいたデータ型のインスタンスを作成する方法を示しています。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>、および XML 型にはすべて、オブジェクトを識別するための名前の値が必要です。  
  
```  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguments specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>Visual Basic での既定のコンストラクターを使用した DataType オブジェクトの構築  
 このコード例では、既定のコンストラクターを使用して各種の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型に基づいたデータ型のインスタンスを作成する方法を示します。 データ型の指定にはプロパティを使用します。  
  
 **注**、 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>、すべての XML 型は、オブジェクトを識別する名前の値を必要とします。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes2](SMO How to#SMO_VBDataTypes2)]  -->  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>Visual C# での既定のコンストラクターを使用した DataType オブジェクトの構築  
 このコード例では、既定のコンストラクターを使用して各種の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型に基づいたデータ型のインスタンスを作成する方法を示します。 データ型の指定にはプロパティを使用します。  
  
 **注**、 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>、すべての XML 型は、オブジェクトを識別する名前の値を必要とします。  
  
```  
{   
//Declare and create a DataType object variable.   
DataType dt;   
dt = new DataType();   
//Define the data type by setting the SqlDataType property.   
dt.SqlDataType = SqlDataType.VarChar;   
//The VarChar data type requires a value for the MaximumLength property.   
dt.MaximumLength = 100;   
}  
```  
  
  
