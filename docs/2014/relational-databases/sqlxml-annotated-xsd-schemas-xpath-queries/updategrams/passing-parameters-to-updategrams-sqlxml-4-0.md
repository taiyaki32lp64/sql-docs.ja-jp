---
title: (SQLXML 4.0) アップデート グラムにパラメーターを渡す |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nullvalue attribute
- passing parameters [SQLXML]
- parameters [SQLXML]
- updategrams [SQLXML], passing parameters
- null values [SQLXML]
ms.assetid: 2354e6e7-1860-471f-8711-4e374c5a4ed2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92238e27c364c8f09721a55d00c750022b53a18f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014732"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>アップデートグラムへのパラメーターの引き渡し (SQLXML 4.0)
  アップデートグラムはテンプレートであり、パラメーターを渡すことができます。 テンプレートに渡すパラメーターの詳細については、次を参照してください。[アップデート グラムのセキュリティに関する考慮事項&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)します。  
  
 アップデートグラムでは、パラメーター値として NULL を渡すことができます。 NULL パラメーター値を渡すには、`nullvalue` 属性を指定し、 `nullvalue` 属性に割り当てられる値をパラメーター値として指定します。 アップデートグラムでは、この値は NULL として扱われます。  
  
> [!NOTE]  
>  `<sql:header>` および `<updg:header>` では、`nullvalue` を修飾子なしで指定し、`<updg:sync>` では、`nullvalue` を `updg:nullvalue` のように修飾子付きで指定します。  
  
## <a name="examples"></a>使用例  
 次の例を使用して実際のサンプルを作成するで指定された要件を満たす必要があります[SQLXML の例を実行するための要件](../../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
 アップデート グラムの例を使用する前に、次のことを確認してください。  
  
-   例では、アップデートグラムでマッピング スキーマを指定せず、既定のマッピングを使用します。 マッピング スキーマを使用するアップデート グラムの例については、次を参照してください。[アップデート グラムで注釈が付けられたマッピング スキーマの指定&#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)します。  
  
### <a name="a-passing-parameters-to-an-updategram"></a>A. アップデートグラムにパラメーターを渡す  
 この例では、アップデートグラムで HumanResources.Shift テーブル内の従業員の姓を変更します。 アップデート グラムには、2 つのパラメーターが渡されます。ShiftID を一意に識別し、名前を使用します。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
  <updg:param name="ShiftID"/>  
  <updg:param name="Name" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="$ShiftID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="$Name" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のアップデートグラムをメモ帳にコピーし、UpdategramWithParameters.xml としてファイルに保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を準備する[SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)後に次の行を追加することで、アップデート グラムを実行する、 `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value  
    cmd.Parameters.Append cmd.CreateParameter("@ShiftID",  2, 1,  0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@Name",   200, 1, 50, "New Name")  
    ```  
  
### <a name="b-passing-null-as-a-parameter-value-to-an-updategram"></a>B. アップデートグラムにパラメーター値として NULL を渡す  
 アップデートグラムを実行するときに、NULL に設定するパラメーターに "isnull" 値を割り当てます。 アップデートグラムでは "isnull" パラメーター値が NULL に変換され、それに従って処理が行われます。  
  
 次のアップデートグラムでは、従業員の役職を NULL に設定します。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header nullvalue="isnull" >  
  <updg:param name="EmployeeID"/>  
  <updg:param name="ManagerID" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Employee EmployeeID="$EmployeeID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Employee ManagerID="$ManagerID" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のアップデートグラムをメモ帳にコピーし、UpdategramPassingNullvalues.xml としてファイルに保存します。  
  
2.  SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を準備する[SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)後に次の行を追加することで、アップデート グラムを実行する、 `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>参照  
 [アップデート グラムのセキュリティに関する考慮事項&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
