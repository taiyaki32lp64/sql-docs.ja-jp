---
title: Workload 要素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e81ea0aac9cfe7676abba18bc7dffb2e1561597b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678720"
---
# <a name="workload-element-dta"></a>Workload 要素 (DTA)
  チューニング セッションで使用するワークロードを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|`DTAInput` 要素につき 1 回の出現が必要です。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[データベース エンジン チューニング アドバイザーの起動および使用](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**子要素**|[File 要素 &#40;DTA&#41;](file-element-dta.md)<br /><br /> [Workload の Database 要素 &#40;DTA&#41;](database-element-for-workload-dta.md)<br /><br /> [EventString 要素 &#40;DTA&#41;](eventstring-element-dta.md)|  
  
## <a name="remarks"></a>コメント  
 ワークロードとは、チューニングするデータベースに対して実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのセットです。 データベース エンジン チューニング アドバイザーは、ワークロードとして [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト、トレース ファイル、およびトレース テーブルを使用できます。  
  
 XML 入力ファイルでワークロードを指定し、 **dta** ツールを使用してコマンド ラインでもワークロードを指定した場合、コマンド ラインで指定したワークロードがチューニングに使用されます。 コマンド ラインで指定したチューニング オプションはすべて、XML 入力ファイルで指定したオプションをオーバーライドします。 唯一の例外は、ユーザー定義の構成が XML 入力ファイルに評価モードで入力されている場合だけです。 たとえば、XML 入力ファイルの `Configuration` 要素に構成が入力されていて、チューニング オプションの 1 つとして `EvaluateConfiguration` 要素も指定されている場合は、XML 入力ファイルで指定されたチューニング オプションがコマンド ラインで入力されたチューニング オプションをオーバーライドします。  
  
 各チューニング セッションには 1 つのワークロードを指定する必要があります。  
  
## <a name="example"></a>例  
 次のコード例を指定します、 **MyDatabase.MyDBOwner.TuningTable001**トレース テーブルを`Workload`要素。 **TuningTable001** は SQL Server Profiler でチューニング テンプレートを使用し、トレース出力をテーブルとして保存することによって作成されたものです。  
  
```  
<DTAXML ...>  
  <DTAInput>  
    <Server>  
...code removed here...  
    </Server>  
    <Workload>  
      <Database>  
        <Name>MyDatabase</Name>  
        <Schema>  
          <Name>MyDBOwner</Name>  
            <Table>  
              <Name>TuningTable001</Name>  
            </Table>  
        </Schema>  
      </Database>  
    </Workload>  
...code removed here...  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>関連項目  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
