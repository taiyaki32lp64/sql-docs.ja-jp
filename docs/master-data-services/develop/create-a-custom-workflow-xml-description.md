---
title: カスタム ワークフローの XML の説明
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: eb5beeb5115c3a68ab34313ea9125c65a4f4e185
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729305"
---
# <a name="create-a-custom-workflow---xml-description"></a>カスタム ワークフローの作成 - XML の説明

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] では、ワークフローの開始時に、SQL Server MDS Workflow Integration Service によって <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> メソッドが呼び出されます。 このメソッドは、ワークフロー ビジネス ルールをトリガーしたアイテムに関するメタデータとデータを、XML のブロックとして受け取ります。 ワークフロー ハンドラーを実装するコードの例については、「[カスタム ワークフローの例 &#40;マスター データ サービス&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)」を参照してください。  
  
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
  
|タグ|[説明]|  
|---------|-----------------|  
|\<Type>|どのカスタム ワークフロー アセンブリを読み込むかを識別するために、**の**[ワークフローの種類][!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ボックスに入力したテキスト。|  
|\<SendData>|**の**[メッセージにメンバーのデータを含める][!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] チェック ボックスによって制御されるブール値。 値 1 は、\<MemberData> セクションが送信されることを示します。それ以外の場合、\<MemberData> セクションは送信されません。|  
|<Server_URL>|**の**[ワークフロー サイト][!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ボックスに入力したテキスト。|  
|<Action_ID>|**の**[ワークフロー名][!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ボックスに入力したテキスト。|  
|\<MemberData>|ワークフロー アクションをトリガーしたメンバーのデータが含まれます。 これは、\<SendData> の値が 1 の場合にのみ含められます。|  
|\<Enter*xxx*>|このタグ セットには、メンバーの作成に関するメタデータ (作成日時や作成者など) が含まれます。|  
|\<LastChg*xxx*>|このタグ セットには、メンバーへの最終変更に関するメタデータ (変更日時や変更者など) が含まれます。|  
|\<Name>|変更されたメンバーの最初の属性。 この例のメンバーには、Name 属性と Code 属性のみが含まれています。|  
|\<Code>|変更されたメンバーの次の属性。 この例のメンバーにさらに多くの属性が含まれていた場合、それらはこのタグの後に続きます。|  
  
## <a name="see-also"></a>参照  
 [カスタム ワークフローの作成 &#40;マスター データ サービス&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)   
 [カスタム ワークフローの例 &#40;マスター データ サービス&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)  
  
  
