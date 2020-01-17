---
title: カスタム ワークフローの例
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c15f708a6deb8da2b0ea32efc70635ef50124621
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729289"
---
# <a name="create-a-custom-workflow---example"></a>カスタム ワークフローの作成 - 例

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] では、カスタム ワークフロー クラス ライブラリを作成するときに、Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender インターフェイスを実装するクラスを作成します。 このインターフェイスには、ワークフローの開始時に SQL Server MDS Workflow Integration Service によって呼び出される 1 つのメソッド (<xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>) が含まれます。 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> メソッドには、2 つのパラメーターが含まれます。1 つは *workflowType* で、これには、**の**[ワークフローの種類][!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ボックスに入力したテキストが含まれます。もう 1 つは *dataElement* で、これには、ワークフロー ビジネス ルールをトリガーしたアイテムのメタデータとアイテム データが含まれます。  
  
## <a name="custom-workflow-example"></a>カスタム ワークフローの例  
 次のコード例は、<xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> メソッドを実装して、ワークフロー ビジネス ルールをトリガーした要素の XML データから Name、Code、および LastChgUserName 属性を抽出する方法と、ストアド プロシージャを呼び出して、それらの属性を別のデータベースに挿入する方法を示しています。 アイテム データ XML の例と、それに含まれるタグの説明については、「[カスタム ワークフロー XML の説明 &#40;マスター データ サービス&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md)」を参照してください。  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Data.SqlClient;  
using System.Xml;  
  
using Microsoft.MasterDataServices.Core.Workflow;  
  
namespace MDSWorkflowTestLib  
{  
    public class WorkflowTester : IWorkflowTypeExtender  
    {  
        #region IWorkflowTypeExtender Members  
  
        public void StartWorkflow(string workflowType, System.Xml.XmlElement dataElement)  
        {  
            // Extract the attributes we want out of the element data.  
            XmlNode NameNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Name");  
            XmlNode CodeNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Code");  
            XmlNode EnteringUserNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/LastChgUserName");  
  
            // Open a connection on the workflow database.  
            SqlConnection workflowConn = new SqlConnection(@"Data Source=<Server instance>; Initial Catalog=WorkflowTest; Integrated Security=True");  
  
            // Create a command to call the stored procedure that adds a new user to the workflow database.  
            SqlCommand addCustomerCommand = new SqlCommand("AddNewCustomer", workflowConn);  
            addCustomerCommand.CommandType = System.Data.CommandType.StoredProcedure;  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Name", NameNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Code", CodeNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@EnteringUser", EnteringUserNode.InnerText));  
  
            // Execute the command.  
            workflowConn.Open();  
            addCustomerCommand.ExecuteNonQuery();  
            workflowConn.Close();  
        }  
  
        #endregion  
    }  
}  
```  
  
## <a name="see-also"></a>参照  
 [カスタム ワークフローの作成 &#40;マスター データ サービス&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
