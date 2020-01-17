---
title: ALTER BROKER PRIORITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_BROKER_TSQL
- ALTER BROKER PRIORITY
- ALTER BROKER
- ALTER_BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER BROKER PRIORITY statement
- ssbdiagnose
ms.assetid: 15fda1b2-e4dd-4f9d-935a-2e38926075b2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 06ab8c327709fa6bfb504217bdd083aaed98f870
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066001"
---
# <a name="alter-broker-priority-transact-sql"></a>ALTER BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ交換の優先度のプロパティを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
{ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = { PriorityValue | DEFAULT } ]  
              )  
}  
[;]  
  
```  
  
## <a name="arguments"></a>引数  
 *ConversationPriorityName*  
 変更するメッセージ交換の優先度の名前を指定します。 名前は、現在のデータベース内のメッセージ交換の優先度を参照する必要があります。  
  
 SET  
 指定したメッセージ交換の優先度をメッセージ交換に適用するかどうかを決定するための条件を指定します。 SET は必須であり、これには次の条件のうち、少なくとも 1 つを指定する必要があります: CONTRACT_NAME、LOCAL_SERVICE_NAME、REMOTE_SERVICE_NAME、または PRIORITY_LEVEL。  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 メッセージ交換の優先度をメッセージ交換に適用するかどうかを決定するための条件として使用するコントラクトの名前を指定します。 *ContractName* は [!INCLUDE[ssDE](../../includes/ssde-md.md)] 識別子であり、現在のデータベース内のコントラクトの名前を指定する必要があります。  
  
 *ContractName*  
 メッセージ交換の優先度を適用できるのは、メッセージ交換を開始した BEGIN DIALOG ステートメントで ON CONTRACT *ContractName* が指定されたメッセージ交換だけであることを指定します。  
  
 ANY  
 使用するコントラクトに関係なく、メッセージ交換の優先度をどのメッセージ交換にも適用できることを指定します。  
  
 CONTRACT_NAME を指定しない場合、メッセージ交換の優先度のコントラクト プロパティは変更されません。  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 メッセージ交換の優先度をメッセージ交換のエンドポイントに適用するかどうかを決定するための条件として使用するサービスの名前を指定します。  
  
 *LocalServiceName* は [!INCLUDE[ssDE](../../includes/ssde-md.md)] 識別子であり、現在のデータベース内のサービスの名前を指定する必要があります。  
  
 *LocalServiceName*  
 メッセージ交換の優先度を次のメッセージ交換のエンドポイントに適用できることを指定します。  
  
-   発信側サービス名が *LocalServiceName* に一致する任意の発信側メッセージ交換のエンドポイント。  
  
-   発信先サービス名が *LocalServiceName* に一致する任意の発信先メッセージ交換のエンドポイント。  
  
 ANY  
 -   エンドポイントで使用されるローカル サービスの名前に関係なく、メッセージ交換の優先度をどのメッセージ交換のエンドポイントにも適用できることを指定します。  
  
 LOCAL_SERVICE_NAME を指定しない場合、メッセージ交換の優先度のローカル サービス プロパティは変更されません。  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' | **ANY**}  
 メッセージ交換の優先度をメッセージ交換のエンドポイントに適用するかどうかを決定するための条件として使用するサービスの名前を指定します。  
  
 *RemoteServiceName* は **nvarchar(256)** 型のリテラルです。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] は *RemoteServiceName* 文字列をバイト単位で照合します。 この比較では、大文字と小文字が区別され、現在の照合順序は考慮されません。 発信先サービスは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] の現在のインスタンス内にあっても、[!INCLUDE[ssDE](../../includes/ssde-md.md)] のリモート インスタンス内にあってもかまいません。  
  
 '*RemoteServiceName*'  
 メッセージ交換の優先度を次のメッセージ交換のエンドポイントに割り当てることを指定します。  
  
-   関連付けられている発信先サービス名が *RemoteServiceName* に一致する任意の発信側メッセージ交換のエンドポイント。  
  
-   関連付けられている発信側サービス名が *RemoteServiceName* に一致する任意の発信先メッセージ交換のエンドポイント。  
  
 ANY  
 エンドポイントに関連付けられているリモート サービスの名前に関係なく、メッセージ交換の優先度をどのメッセージ交換のエンドポイントにも適用することを指定します。  
  
 REMOTE_SERVICE_NAME を指定しない場合、メッセージ交換の優先度のリモート サービス プロパティは変更されません。  
  
 PRIORITY_LEVEL = { *PriorityValue* | **DEFAULT** }  
 メッセージ交換の優先度で指定されているコントラクトおよびサービスを使用する任意のメッセージ交換のエンドポイントに割り当てる優先度レベルを指定します。 *PriorityValue* には、1 (最も低い優先度) ～ 10 (最も高い優先度) の整数リテラルを指定する必要があります。  
  
 PRIORITY_LEVEL を指定しない場合、メッセージ交換の優先度の優先度レベル プロパティは変更されません。  
  
## <a name="remarks"></a>Remarks  
 ALTER BROKER PRIORITY で変更されるプロパティは、既存のメッセージ交換には適用されません。 既存のメッセージ交換は、開始されたときに割り当てられた優先度のままです。  
  
 詳細については、「[CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 メッセージ交換の優先度を作成する権限は、既定では **db_ddladmin** 固定データベース ロールまたは **db_owner** 固定データベース ロールのメンバーと **sysadmin** 固定サーバー ロールのメンバーに与えられています。 データベースに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-only-the-priority-level-of-an-existing-conversation-priority"></a>A. 既存のメッセージ交換の優先度レベルのみ変更する  
 優先度レベルを変更しますが、コントラクト、ローカル サービス、またはリモート サービスの各プロパティは変更しません。  
  
```  
ALTER BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-changing-all-of-the-properties-of-an-existing-conversation-priority"></a>B. 既存のメッセージ交換の優先度のプロパティをすべて変更する  
 優先度レベル、コントラクト、ローカル サービス、リモート サービスの各プロパティを変更します。  
  
```  
ALTER BROKER PRIORITY SimpleContractPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContractB,  
         LOCAL_SERVICE_NAME = TargetServiceB,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceB',  
         PRIORITY_LEVEL = 8);  
```  
  
## <a name="see-also"></a>参照  
 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys.conversation_priorities &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
