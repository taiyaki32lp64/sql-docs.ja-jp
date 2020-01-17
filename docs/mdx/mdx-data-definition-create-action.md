---
title: CREATE ACTION ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b723a706521b24c9aa216c46f617d8ff94997137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098553"
---
# <a name="mdx-data-definition---create-action"></a>MDX データ操作 - CREATE ACTION


  キューブ、ディメンション、階層、または下位のオブジェクトと関連付けることができるアクションを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE ACTION CURRENTCUBE | Cube_Name  
   .Action_Name <action body>  
<action body> ::=   
FOR   
        CUBE   
    | Hierarchy_Name [MEMBERS]   
    | Level_Name [MEMBERS]   
    | CELLS   
    | SET }   
      AS 'MDX_Expression'   
        [, TYPE = '  
              { URL   
            | HTML   
            | STATEMENT   
               | DATASET   
            | ROWSET   
            | COMMANDLINE   
               | PROPRIETARY }   
         ']  
   [ , INVOCATION = 'INTERACTIVE | ON_OPEN | BATCH ' ]  
   [ , APPLICATION = String_Expression ]  
   [ , DESCRIPTION = String_Expression ]  
   [ , CAPTION = 'MDX_Expression' ]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 有効な文字列キューブ名を提供します。  
  
 *Action _ 名前*  
 作成するアクションの名前を指定する有効な文字列です。  
  
 *Hierarchy _ 名前*  
 階層名を提供する有効な文字列。  
  
 *レベル名*  
 レベル名を提供する有効な文字列。  
  
 *Member _ 名前*  
 メンバー名またはメンバー キーを提供する有効な文字列。  
  
 *MDX_Expression*  
 有効な MDX 式です。  
  
 *String_Expression*  
 有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 クライアント アプリケーションを作成して; 安全でないアクションを実行する可能性があります。クライアント アプリケーションが安全でない関数を使用することもできます。 このような状況を避けるためには、使用、 **Safety Options**プロパティ。 詳細については、「Safety Options プロパティ」を参照してください。  
  
> [!NOTE]  
>  このステートメントは、旧バージョンとの互換性のために用意されています。 新しく[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]ドリルスルーやレポートの操作などはサポートされていません。  
  
## <a name="action-types"></a>アクションの種類  
 次の表に、さまざまな種類で使用できるアクションの[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]します。  
  
|アクションの種類|説明|  
|-----------------|-----------------|  
|**URL**|返されるアクション文字列は、インターネット ブラウザーで開く URL です。<br /><br /> 注:この操作は値で始まらない場合`https://`または`https://`、アクションは、ブラウザーを使用できませんしない限り、 **SafetyOptions**に設定されている**DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**します。|  
|**HTML**|返されるアクション文字列は、HTML スクリプトです。 文字列をファイルに保存する必要があり、インターネット ブラウザーを使用して、ファイルを表示する必要があります。 この場合、スクリプト全体は、生成される HTML の一部として実行可能性があります。|  
|**ステートメント**|返されるアクション文字列は、設定によって実行される必要があるステートメント、 **:settext**文字列と呼び出し元にコマンド オブジェクトのメソッド、 **icommand::execute**メソッド。 コマンドが成功しなかった場合、エラーが返されます。|  
|**データセット**|返されるアクション文字列は、MDX ステートメントを設定して実行する必要がある、 **:settext**文字列と呼び出し元にコマンド オブジェクトのメソッド、 **icommand::execute**メソッド。 要求されたインターフェイス ID (IID) にする必要があります**IDataset**します。 データ セットが作成されている場合、コマンドは成功します。 クライアント アプリケーションでは、返されたデータセットをユーザーが表示できるようにする必要があります。|  
|**行セット**|ような**データセット**がの IID を要求する代わりに**IDataset**、クライアント アプリケーションの IID を要求する必要があります**IRowset**します。 行セットが作成されれば、コマンドは成功したことになります。 クライアント アプリケーションは、返された行セットを参照するユーザーに許可する必要があります。|  
|**コマンドライン**|クライアント アプリケーションでアクション文字列を実行します。 文字列は、コマンド ラインです。|  
|**独自**|クライアント アプリケーションの表示や、アプリケーションに特定のアクションのカスタムの非ジェネリックの知識がない場合、アクションを実行する必要がありますされません。 これらのオプションに適切な制限を設定して、クライアント アプリケーションが明示的に要求する場合を除き、独自のアクションは、クライアント アプリケーションに返されません、 **APPLICATION_NAME**します。|  
  
## <a name="invocation-types"></a>呼び出しの種類  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で使用できる呼び出しの種類は以下のとおりです。 呼び出しの種類は、アクションを実行するタイミングを判断するため、クライアント アプリケーションによってのみ使用されます。 呼び出しの種類は実際には、アクションの呼び出しの動作を決定できません。  
  
|呼び出しの種類|説明|  
|---------------------|-----------------|  
|**対話型**|ユーザーの対話を通じてクライアント アプリケーションでアクションを呼び出します。|  
|**ON_OPEN**|ターゲット オブジェクトを開いたときに、クライアント アプリケーションでアクションを呼び出す必要があります。 この呼び出しの種類は現在実装されていません。|  
|**バッチ**|クライアント アプリケーションは、対象のオブジェクトがバッチ操作にかかわった時点を判別してアクションを呼び出します。 この呼び出しの種類は現在実装されていません。|  
  
### <a name="scope"></a>スコープ  
 各アクションは、特定のキューブが定義され、そのキューブ内で一意の名前を持ちます。 アクションは、次の表に、スコープのいずれかのことができます。  
  
 キューブ スコープ  
 特定のディメンション、メンバー、またはセルのアクションの例えば："AS のターミナル エミュレーションの起動 400 実稼働システム"。  
  
 ディメンション スコープ  
 アクションは、特定のディメンションに適用されます。 この種のアクションは、選択された特定のレベルまたはメンバーに依存しません。  
  
 レベルのスコープ  
 特定のディメンション レベルに適用されるアクションです。 これらのアクションでは、そのディメンションのメンバーの具体的な選択に依存しません。  
  
 メンバー スコープ  
 アクションは、特定のレベル メンバーに適用されます。  
  
 セル スコープ  
 特定のセルだけに適用されるアクションです。  
  
 スコープの設定  
 アクションは、セットのみに適用されます。 名前、 **ActionParameterSet**は、アクションの式の中のアプリケーションで使用するために予約されています。  
  
## <a name="see-also"></a>関連項目  
 [MDX データ定義ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
