---
title: エラーおよび警告 (XMLA) の処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- inline errors [XMLA]
- SOAP faults [XML for Analysis]
- XML for Analysis, errors
- faults [XML for Analysis]
- messages [XML for Analysis]
- XMLA, errors
- warnings [XML for Analysis]
- inline warnings [XMLA]
ms.assetid: ab895282-098d-468e-9460-032598961f45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 856886a5edfa5dcae604b44f5c2dca356ba0addb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702135"
---
# <a name="handling-errors-and-warnings-xmla"></a>エラーおよび警告の処理 (XMLA)
  XML for Analysis (XMLA) の場合は、エラー処理が必要な[Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)または[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)メソッドの呼び出しは実行されませんが正常に実行しますが、エラーまたは警告を生成またはが正常に実行、結果が返されますエラーを含みます。  
  
|[エラー]|レポーティング|  
|-----------|---------------|  
|XMLA メソッド呼び出しを実行できない|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] エラーの詳細を含む SOAP エラー メッセージを返します。<br /><br /> 詳細については、このセクションを参照してください。 [SOAP エラーの処理](#handling_soap_faults)します。|  
|メソッド呼び出しは成功したが、エラーまたは警告が発生した|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 含まれています、[エラー](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla)または[警告](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla)要素のエラーまたは警告は、それぞれ、[メッセージ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)のプロパティ、[ルート](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla)要素メソッド呼び出しの結果を格納するとします。<br /><br /> 詳細については、このセクションを参照してください。 [Handling Errors and Warnings](#handling_errors_and_warnings)します。|  
|メソッド呼び出しは成功したが、結果にエラーが含まれる|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インラインが含まれています`error`または`warning`要素のエラーまたは警告に、適切な内でそれぞれ[セル](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)または[行](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla)メソッドの呼び出しの結果の要素。<br /><br /> 詳細については、このセクションを参照してください。[処理インライン エラーおよび警告](#handling_inline_errors_and_warnings)します。|  
  
##  <a name="handling_soap_faults"></a> SOAP エラーの処理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、以下の状況が発生した場合に、SOAP エラーを返します。  
  
-   XMLA メソッドを含む SOAP メッセージが、整形式でないか、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスによって検証できなかった。  
  
-   XMLA メソッドを含む SOAP メッセージに関係する通信エラーまたはその他のエラーが発生した。  
  
-   XMLA メソッドが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスで実行できなかった。  
  
 XMLA の SOAP エラー コードは、"XMLForAnalysis" で始まり、その後にピリオドと 16 進数の HRESULT 結果コードが続きます。 たとえば、エラー コード "`0x80000005`" は "`XMLForAnalysis.0x80000005`" という形式になります。 SOAP エラー形式の詳細については、W3C による『Simple Object Access Protocol (SOAP) 1.1』の「Soap Fault」を参照してください。  
  
### <a name="fault-code-information"></a>エラー コード情報  
 次の表は、SOAP 応答の詳細セクションに含まれる XMLA エラー コード情報を示しています。 列は、SOAP エラーの詳細セクションに含まれるエラーの属性です。  
  
|列名|型|説明|Null を許容<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|メソッドの成功または失敗を示すリターン コード。 16 進数値は、`UnsignedInt` の値に変換する必要があります。|いいえ|  
|`WarningCode`|`UnsignedInt`|警告の状況を示すリターン コード。 16 進数値は、`UnsignedInt` の値に変換する必要があります。|はい|  
|`Description`|`String`|エラーを生成したコンポーネントによって返されたエラーまたは警告のテキストと説明。|はい|  
|`Source`|`String`|エラーまたは警告を生成したコンポーネントの名前。|はい|  
|`HelpFile`|`String`|エラーまたは警告について説明しているファイルまたはトピックへのパス、または URL。|はい|  
  
 <sup>1</sup>を示すかどうか、データが必要です返す必要があるまたはかどうか、データが省略可能な列が適用されない場合、null 文字列は許可されています。  
  
 次は、メソッド呼び出しが失敗した場合に発生した SOAP エラーの例です。  
  
```  
<?xml version="1.0"?>  
   <SOAP-ENV:Envelope  
   xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
   SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
      <SOAP-ENV:Fault>  
         <faultcode>XMLAnalysisError.0x80000005</faultcode>  
         <faultstring>The XML for Analysis provider encountered an error.</faultstring>  
         <faultactor>XML for Analysis Provider</faultactor>  
         <detail>  
<Error  
ErrorCode="2147483653"  
Description="An unexpected error has occurred."  
Source="XML for Analysis Provider"  
HelpFile="" />  
         </detail>  
      </SOAP-ENV:Fault>  
</SOAP-ENV:Envelope>  
```  
  
##  <a name="handling_errors_and_warnings"></a> エラーおよび警告の処理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、コマンドの実行後に以下の状況が発生した場合、`Messages` 要素内に `root` プロパティを返します。  
  
-   メソッド自体は失敗しなかったが、メソッドが成功した後に [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスでエラーが発生した。  
  
-   コマンドが成功したときに、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスによって警告が返される。  
  
 `Messages` プロパティは、`root` 要素に含まれる他のすべてのプロパティの後に続きます。このプロパティには、1 つ以上の `Message` 要素が含まれます。 さらに、各 `Message` 要素には、指定されたコマンドで発生したエラーまたは警告についてそれぞれ説明する 1 つの `error` または `warning` 要素のいずれかが含まれます。  
  
 エラーと警告に含まれているの詳細については、`Messages`プロパティを参照してください[メッセージ要素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)します。  
  
### <a name="handling-errors-during-serialization"></a>シリアル化実行時のエラーの処理  
 後にエラーが発生した場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンスが正常に実行コマンドの出力をシリアル化を開始した[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]を返します、[例外](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla)エラーの時点で別の名前空間内の要素。 その後 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスは、クライアントに送信する XML ドキュメントが有効なドキュメントになるように、開いている要素をすべて閉じます。 インスタンスは、エラーの説明を含む `Messages` 要素も返します。  
  
##  <a name="handling_inline_errors_and_warnings"></a> インライン エラーおよび警告の処理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、XMLA メソッド自体は失敗しなかったものの、XMLA メソッド呼び出しが成功した後に、メソッドによって返された結果内のデータ要素に固有のエラーが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスで発生した場合、インライン `error` または `warning` を返します。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インラインの提供`error`と`warning`問題の特定のセルやその他のデータにある場合は要素内に含まれる、`root`要素を使用して、 [MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla)セキュリティなどのデータ型が発生するエラーまたは書式設定セルのエラーです。 そのような場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、エラーまたは警告を含む `error` または `warning` 要素に、`Cell` または `row` 要素をそれぞれ返します。  
  
 次の例から返される行セット内のエラーを含む結果セットを示しています、`Execute`メソッドを使用して、[ステートメント](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)コマンド。  
  
```  
<return>  
   ...  
   <root>  
      ...  
      <CellData>  
      ...  
         <Cell CellOrdinal="10">  
            <Value>  
               <Error>  
                  <ErrorCode>2148497527</ErrorCode>   
                  <Description>Security Error.</Description>   
               </Error>  
            </Value>  
         </Cell>  
      </CellData>  
      ...  
   </root>  
   ...  
</return>  
```  
  
## <a name="see-also"></a>関連項目  
 [Analysis Services での XMLA による開発](developing-with-xmla-in-analysis-services.md)  
  
  
