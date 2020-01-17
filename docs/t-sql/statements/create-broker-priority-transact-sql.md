---
title: CREATE BROKER PRIORITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE BROKER PRIORITY
- PRIORITY_TSQL
- CREATE_BROKER_PRIORITY_TSQL
- PRIORITY
- CREATE BROKER
- BROKER_TSQL
- BROKER
- CREATE_BROKER_TSQL
- BROKER PRIORITY
- BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE BROKER PRIORITY statement
ms.assetid: e0bbebfa-b7c3-4825-8169-7281f7e6de98
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 18e916c3f9a9d99ea177d0d266cb20bee44a3868
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064679"
---
# <a name="create-broker-priority-transact-sql"></a>CREATE BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  優先順位と、その優先順位を割り当てる [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ交換を判断するための一連の条件を定義します。 優先順位は、メッセージ交換の優先度で指定されているものと同じコントラクトとサービスの組み合わせを使用するすべてのメッセージ交換のエンドポイントに割り当てられます。 優先度は、1 (低) から 10 (高) までの範囲の値です。 既定値は 5 です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
[ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = {PriorityValue | DEFAULT } ]  
       )  
]  
[;]  
  
```  
  
## <a name="arguments"></a>引数  
 *ConversationPriorityName*  
 メッセージ交換の優先度の名前を指定します。 名前は現在のデータベース内で一意であり、[!INCLUDE[ssDE](../../includes/ssde-md.md)] の[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。  
  
 SET  
 指定したメッセージ交換の優先度をメッセージ交換に適用するかどうかを決定するための条件を指定します。 指定する場合、SET には、次の条件のうち、少なくとも 1 つを指定する必要があります: CONTRACT_NAME、LOCAL_SERVICE_NAME、REMOTE_SERVICE_NAME、または PRIORITY_LEVEL。 SET を指定しない場合は、3 つの条件にはすべて既定値が設定されます。  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 メッセージ交換の優先度をメッセージ交換に適用するかどうかを決定するための条件として使用するコントラクトの名前を指定します。 *ContractName* は [!INCLUDE[ssDE](../../includes/ssde-md.md)] 識別子であり、現在のデータベース内のコントラクトの名前を指定する必要があります。  
  
 *ContractName*  
 メッセージ交換の優先度を適用できるのは、メッセージ交換を開始した BEGIN DIALOG ステートメントで ON CONTRACT *ContractName* が指定されたメッセージ交換だけであることを指定します。  
  
 ANY  
 使用するコントラクトに関係なく、メッセージ交換の優先度をどのメッセージ交換にも適用できることを指定します。  
  
 既定値は ANY です。  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 メッセージ交換の優先度をメッセージ交換のエンドポイントに適用するかどうかを決定するための条件として使用するサービスの名前を指定します。  
  
 *LocalServiceName* は [!INCLUDE[ssDE](../../includes/ssde-md.md)] 識別子です。 この値には、現在のデータベース内にあるサービスの名前を指定する必要があります。  
  
 *LocalServiceName*  
 メッセージ交換の優先度を次のメッセージ交換のエンドポイントに適用できることを指定します。  
  
-   発信側サービス名が *LocalServiceName* に一致する任意の発信側メッセージ交換のエンドポイント。  
  
-   発信先サービス名が *LocalServiceName* に一致する任意の発信先メッセージ交換のエンドポイント。  
  
 ANY  
 -   エンドポイントで使用されるローカル サービスの名前に関係なく、メッセージ交換の優先度をどのメッセージ交換のエンドポイントにも適用できることを指定します。  
  
 既定値は ANY です。  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' | **ANY**}  
 メッセージ交換の優先度をメッセージ交換のエンドポイントに適用するかどうかを決定するための条件として使用するサービスの名前を指定します。  
  
 *RemoteServiceName* は **nvarchar(256)** 型のリテラルです。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] は *RemoteServiceName* 文字列をバイト単位で照合します。 この比較では、大文字と小文字が区別され、現在の照合順序は考慮されません。 発信先サービスは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] の現在のインスタンス内にあっても、[!INCLUDE[ssDE](../../includes/ssde-md.md)] のリモート インスタンス内にあってもかまいません。  
  
 '*RemoteServiceName*'  
 メッセージ交換の優先度を次のメッセージ交換のエンドポイントに適用できることを指定します。  
  
-   関連付けられている発信先サービス名が *RemoteServiceName* に一致する任意の発信側メッセージ交換のエンドポイント。  
  
-   関連付けられている発信側サービス名が *RemoteServiceName* に一致する任意の発信先メッセージ交換のエンドポイント。  
  
 ANY  
 エンドポイントに関連付けられているリモート サービスの名前に関係なく、メッセージ交換の優先度をどのメッセージ交換のエンドポイントにも適用できることを指定します。  
  
 既定値は ANY です。  
  
 PRIORITY_LEVEL = { *PriorityValue* | **DEFAULT** }  
 メッセージ交換の優先度で指定されているコントラクトおよびサービスを使用するすべてのメッセージ交換のエンドポイントに割り当てる優先度を指定します。 *PriorityValue* には、1 (最も低い優先度) ～ 10 (最も高い優先度) の整数リテラルを指定する必要があります。 既定値は 5 です。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、メッセージ交換のエンドポイントに優先順位を割り当てます。 この優先順位によって、エンドポイントに関連付けられている操作の優先度が制御されます。 各メッセージ交換には、2 つのメッセージ交換エンドポイントがあります。  
  
-   発信側メッセージ交換エンドポイントは、メッセージ交換の一方を発信側サービスおよび発信側キューに関連付けます。 発信側メッセージ交換エンドポイントは、BEGIN DIALOG ステートメントが実行されたときに作成されます。 発信側メッセージ交換エンドポイントに関連付けられる操作には、次のものがあります。  
  
    -   発信側サービスから送信する。  
  
    -   発信側キューから受信する。  
  
    -   発信側キューから次に使用できるメッセージ交換グループを取得する。  
  
-   発信先メッセージ交換エンドポイントは、メッセージ交換の相手側を発信先のサービスおよびキューに関連付けます。 発信先メッセージ交換エンドポイントは、メッセージ交換がターゲット キューへのメッセージの送信に使用されたときに作成されます。 発信先メッセージ交換エンドポイントに関連付けられる操作には、次のものがあります。  
  
    -   ターゲット キューから受信する。  
  
    -   発信先サービスから送信する。  
  
    -   ターゲット キューから次に使用できるメッセージ交換グループを取得する。  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、メッセージ交換エンドポイントが作成されるときに、メッセージ交換の優先順位を割り当てます。 メッセージ交換エンドポイントでは、メッセージ交換が終了するまでその優先度レベルが保持されます。 新しい優先度や、既存の優先度に対する変更は、既存のメッセージ交換には適用されません。  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] でメッセージ交換のエンドポイントに割り当てる優先度レベルは、そのエンドポイントのプロパティに最も一致するコントラクトおよびサービスの条件を持つメッセージ交換の優先度の優先順位です。 その検索順序を次の表に示します。  
  
|操作のコントラクト|操作のローカル サービス|操作のリモート サービス|  
|------------------------|-----------------------------|------------------------------|  
|*ContractName*|*LocalServiceName*|*RemoteServiceName*|  
|*ContractName*|*LocalServiceName*|ANY|  
|*ContractName*|ANY|*RemoteServiceName*|  
|*ContractName*|ANY|ANY|  
|ANY|*LocalServiceName*|*RemoteServiceName*|  
|ANY|*LocalServiceName*|ANY|  
|ANY|ANY|*RemoteServiceName*|  
|ANY|ANY|ANY|  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、指定されたコントラクト、ローカル サービス、およびリモート サービスが、操作で使用されるものと一致する優先度を最初に検索します。 その優先度が見つからなかった場合、[!INCLUDE[ssSB](../../includes/sssb-md.md)] では、コントラクトおよびローカル サービスが操作で使用されるものと一致し、かつリモート サービスが ANY と指定された優先度を検索します。 この検索を、上の表に示されているすべての組み合わせに対して継続します。 一致する優先度が見つからない場合、その操作には既定の優先度 5 が割り当てられます。  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、メッセージ交換の各エンドポイントに優先度レベルを個別に割り当てます。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] で発信側と発信先の両方のメッセージ交換エンドポイントに優先順位を割り当てるようにするには、両方のエンドポイントをメッセージ交換の優先度に含める必要があります。 発信側と発信先のメッセージ交換エンドポイントが別々のデータベースにある場合、各データベースでメッセージ交換の優先度を作成する必要があります。 通常は、メッセージ交換の両方のエンドポイントに対して同じ優先度レベルを指定しますが、異なる優先順位を指定することもできます。  
  
 優先順位は、メッセージまたはメッセージ交換グループ ID をキューから受信する操作に常に適用されます。 優先順位は、[!INCLUDE[ssDE](../../includes/ssde-md.md)]のいずれかのインスタンスから別のインスタンスにメッセージを送信するときにも適用されます。  
  
 優先順位は、次の場合はメッセージの送信時に使用されません。  
  
-   HONOR_BROKER_PRIORITY データベース オプションが OFF に設定されているデータベースからの送信。 詳細については、「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。  
  
-   データベース エンジンの同一インスタンスのサービス間での送信。  
  
-   データベースでメッセージ交換の優先度が作成されていない場合は、データベース内のすべての [!INCLUDE[ssSB](../../includes/sssb-md.md)] 操作に既定の優先度 5 が割り当てられます。  
  
## <a name="permissions"></a>アクセス許可  
 メッセージ交換の優先度を作成する権限は、既定では db_ddladmin 固定データベース ロールまたは db_owner 固定データベース ロールのメンバー、および sysadmin 固定サーバー ロールのメンバーに与えられています。 データベースに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-assigning-a-priority-level-to-both-directions-of-a-conversation"></a>A. メッセージ交換の両方向に優先度レベルを割り当てる  
 この 2 つのメッセージ交換の優先度では、`TargetService` と `InitiatorAService` の間で `SimpleContract` を使用するすべての操作に優先度レベル 3 が割り当てられるようにします。  
  
```  
CREATE BROKER PRIORITY InitiatorAToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = InitiatorServiceA,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 3);  
CREATE BROKER PRIORITY TargetToInitiatorAPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceA',  
         PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-setting-the-priority-level-for-all-conversations-that-use-a-contract"></a>B. 特定のコントラクトを使用するすべてのメッセージ交換の優先度レベルを設定する  
 `SimpleContract` というコントラクトを使用するすべての操作に優先度レベル `7` を割り当てます。 これは、`SimpleContract` とローカル サービスまたはリモート サービスを指定する優先度が他にないことを前提にしています。  
  
```  
CREATE BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 7);  
```  
  
### <a name="c-setting-a-base-priority-level-for-a-database"></a>C. データベースの基本の優先度レベルを設定する  
 2 つの特定のサービスに対するメッセージ交換の優先度を定義し、次に、その他のすべてのメッセージ交換のエンドポイントに一致するメッセージ交換の優先度を定義します。 これは既定の優先度 (常に 5) に代わるものではありませんが、既定値が割り当てられる項目数を最小限にします。  
  
```  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/ClaimPriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = //Adventure-Works.com/Expenses/ClaimService,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 9);  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/ApprovalPriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = //Adventure-Works.com/Expenses/ClaimService,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/BasePriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 3);  
```  
  
### <a name="d-creating-three-priority-levels-for-a-target-service-by-using-services"></a>D. サービスを使用して、1 つの発信先サービスに対して 3 つの優先順位を作成する  
 次の 3 つのパフォーマンス レベルを備えたシステムをサポートします: ゴールド (高)、シルバー (中)、ブロンズ (低)。 コントラクトは 1 つですが、各レベルには個別の発信側サービスがあります。 すべての発信側サービスは、中心となる 1 つの発信先サービスと通信します。  
  
```sql  
CREATE BROKER PRIORITY GoldInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = GoldInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY GoldTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'GoldInitiatorService',  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY SilverInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = SilverInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY SilverTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'SilverInitiatorService',  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY BronzeInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = BronzeInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 2);  
CREATE BROKER PRIORITY BronzeTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'BronzeInitiatorService',  
         PRIORITY_LEVEL = 2);  
```  
  
### <a name="e-creating-three-priority-levels-for-multiple-services-using-contracts"></a>E. コントラクトを使用して、複数のサービスに対して 3 つの優先順位を作成する  
 次の 3 つのパフォーマンス レベルを備えたシステムをサポートします: ゴールド (高)、シルバー (中)、ブロンズ (低)。 各レベルには、個別のコントラクトがあります。 これらの優先度は、そのコントラクトを使用するメッセージ交換によって参照されるすべてのサービスに適用されます。  
  
```sql  
CREATE BROKER PRIORITY GoldPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = GoldContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY SilverPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SilverContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY BronzePriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = BronzeContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 2);  
```  
  
## <a name="see-also"></a>参照  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [CREATE CONTRACT &#40;Transact-SQL&#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)   
 [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md)   
 [sys.conversation_priorities &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
