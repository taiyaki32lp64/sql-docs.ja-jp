---
title: カスタム ワークフロー XML の説明 (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a71ee85fc4dce4abd7d8ef91a8f22529ce8d5a0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483013"
---
# <a name="custom-workflow-xml-description-master-data-services"></a>カスタム ワークフロー XML の説明 (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] では、ワークフローの開始時に、SQL Server MDS Workflow Integration Service によって <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> メソッドが呼び出されます。 このメソッドは、ワークフロー ビジネス ルールをトリガーしたアイテムに関するメタデータとデータを、XML のブロックとして受け取ります。 ワークフロー ハンドラーを実装するコードの例については、「[カスタム ワークフローの例 &#40;マスター データ サービス&#41;](create-a-custom-workflow-example.md)」を参照してください。  
  
 次の例は、ワークフロー ハンドラーに送られる XML の内容を示したものです。  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 次の表に、この XML に含まれるタグの一部を示します。  
  
|Tag|説明|  
|---------|-----------------|  
|\<Type>|どのカスタム ワークフロー アセンブリを読み込むかを識別するために、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] の **[ワークフローの種類]** ボックスに入力したテキスト。|  
|\<SendData>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] の **[メッセージにメンバーのデータを含める]** チェック ボックスによって制御されるブール値。 値 1 は、\<MemberData> セクションが送信されることを示します。それ以外の場合、\<MemberData> セクションは送信されません。|  
|<Server_URL>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] の **[ワークフロー サイト]** ボックスに入力したテキスト。|  
|<Action_ID>|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] の **[ワークフロー名]** ボックスに入力したテキスト。|  
|\<MemberData>|ワークフロー アクションをトリガーしたメンバーのデータが含まれます。 これは、\<SendData> の値が 1 の場合にのみ含められます。|  
|\<Enter*xxx*>|このタグ セットには、メンバーの作成に関するメタデータ (作成日時や作成者など) が含まれます。|  
|\<LastChg*xxx*>|このタグ セットには、メンバーへの最終変更に関するメタデータ (変更日時や変更者など) が含まれます。|  
|\<Name>|変更されたメンバーの最初の属性。 この例のメンバーには、Name 属性と Code 属性のみが含まれています。|  
|\<Code>|変更されたメンバーの次の属性。 この例のメンバーにさらに多くの属性が含まれていた場合、それらはこのタグの後に続きます。|  
  
## <a name="see-also"></a>参照  
 [カスタム ワークフローの作成 &#40;マスター データ サービス&#41;](create-a-custom-workflow-master-data-services.md)   
 [カスタム ワークフローの例 &#40;マスター データ サービス&#41;](create-a-custom-workflow-example.md)  
  
  
