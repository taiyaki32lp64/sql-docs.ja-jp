---
title: SQL Server 拡張イベント (Xevent) を使用して、Analysis Services の監視 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b57cc2fe-52dc-4fa9-8554-5a866e25c6d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d6abfca98386ef691add200d433af827ed44836
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079743"
---
# <a name="use-sql-server-extended-events-xevents-to-monitor-analysis-services"></a>SQL Server 拡張イベント (XEvent) を使用した Analysis Services の監視
  Analysis Services の使用を通じてトレース機能を提供する[拡張イベント](../../relational-databases/extended-events/extended-events.md)します。  
  
 拡張イベントは、高い拡張性と柔軟な構成を備えた、サーバー システムのためのイベント インフラストラクチャです。 拡張イベントは軽量なパフォーマンス監視システムであり、使用されるパフォーマンス リソースはごくわずかです。  
  
 すべてのイベントをキャプチャする Analysis Services とに定義されている、特定のコンシューマーにターゲット[拡張イベント](../../relational-databases/extended-events/extended-events.md)、Xevent を通じてします。  
  
## <a name="initiating-extended-events-in-analysis-services"></a>Analysis Services での拡張イベントの開始  
 拡張イベントのトレースは、以下のような XMLA のオブジェクト作成スクリプト コマンドを使用して有効にします。  
  
```  
<Execute ...>  
   <Command>  
      <Batch ...>  
         <Create ...>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session ...>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" .../>  
                        </event>  
                        <target package="PACKAGE0" name="asynchronous_file_target">  
                           <parameter name="filename" value="data_filename.xel"/>  
                           <parameter name="metadatafile" value="metadata_filename.xem"/>  
                        </target>  
                     </event_session>  
                  </ddl300_300:XEvent>  
               </Trace>  
            </ObjectDefinition>  
         </Create>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 ユーザーは、トレースのニーズに応じて、次の要素を定義します。  
  
 *trace_id*  
 このトレースの一意識別子を定義します。  
  
 *trace_name*  
 このトレースに付ける名前を指定します (通常は、人間が判読できるトレースの定義です)。 *trace_id* の値を名前として使用するのが一般的です。  
  
 *AS_event*  
 公開する Analysis Services イベントを指定します。 イベントの名前については、「 [Analysis Services トレース イベント](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events) 」を参照してください。  
  
 *data_filename*  
 イベント データを含むファイルの名前を指定します。 この名前には、トレースを繰り返し送信する場合にデータが上書きされないように、タイムスタンプを使用したサフィックスが付けられます。  
  
 *metadata_filename*  
 イベント メタデータを含むファイルの名前を指定します。 この名前には、トレースを繰り返し送信する場合にデータが上書きされないように、タイムスタンプを使用したサフィックスが付けられます。  
  
## <a name="stopping-extended-events-in-analysis-services"></a>Analysis Services での拡張イベントの停止  
 拡張イベントのトレース オブジェクトを停止するには、以下のような XMLA のオブジェクト削除スクリプト コマンドを使用して、そのオブジェクトを削除する必要があります。  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch ...>  
         <Delete ...>  
            <Object>  
               <TraceID>trace_id</TraceID>  
            </Object>  
         </Delete>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 ユーザーは、トレースのニーズに応じて、次の要素を定義します。  
  
 *trace_id*  
 削除するトレースの一意識別子を定義します。  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
  
