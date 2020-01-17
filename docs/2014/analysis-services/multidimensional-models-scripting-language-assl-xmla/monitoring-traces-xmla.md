---
title: トレースの監視 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 678c6d2312261475f4b970b1535ce1faa1f00930
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62729074"
---
# <a name="monitoring-traces-xmla"></a>トレースの監視 (XMLA)
  使用することができます、[購読](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla)XML for Analysis (XMLA) のインスタンスで定義されている既存のトレースを監視するためにコマンド[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]します。 `Subscribe` コマンドは、トレースの結果を行セットとして返します。  
  
## <a name="specifying-a-trace"></a>トレースの指定  
 [オブジェクト](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)のプロパティ、`Subscribe`コマンドは、いずれかへのオブジェクト参照を含める必要があります、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンスまたはでトレースを[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンス。 `Object` プロパティが指定されていない場合、またはトレース識別子が `Object` プロパティで指定されていない場合、`Subscribe` コマンドは、コマンドの SOAP ヘッダーで指定されている明示的なセッションに対する既定のセッション トレースを監視します。  
  
## <a name="returning-results"></a>結果の返送  
 `Subscribe` コマンドは、指定されたトレースによってキャプチャされたトレース イベントを含む行セットを返します。 `Subscribe`によってコマンドが取り消されるまでトレース結果を返します、[キャンセル](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)コマンド。  
  
 行セットに含まれる列は、次の表のとおりです。  
  
|[列]|データ型|説明|  
|------------|---------------|-----------------|  
|EventClass|Integer|トレースによって受信されたイベントのイベント クラス。|  
|EventSubclass|Long integer|トレースによって受信されたイベントのイベント サブクラス。|  
|CurrentTime|DATETIME|イベントの開始時刻 (取得できた場合)。 フィルター選択を行うには、'YYYY-MM-DD' および 'YYYY-MM-DD HH:MM:SS' の形式である必要があります。|  
|StartTime|DATETIME|イベントの開始時刻 (取得できた場合)。 フィルター選択を行うには、'YYYY-MM-DD' および 'YYYY-MM-DD HH:MM:SS' の形式である必要があります。|  
|EndTime|DATETIME|イベントの終了時刻 (取得できた場合)。 フィルター選択を行うには、'YYYY-MM-DD' および 'YYYY-MM-DD HH:MM:SS' の形式である必要があります。<br /><br /> プロセスまたはアクションの開始を記述するイベント クラスの場合、この列は設定されません。|  
|Duration|Long integer|イベントで経過した時間の合計 (ミリ秒単位)。|  
|CPUTime|Long integer|イベントで経過したプロセッサ時間 (ミリ秒単位)。|  
|JobID|Long integer|プロセスのジョブ識別子。|  
|SessionID|String|イベントが発生したセッションの識別子。|  
|SessionType|String|イベントが発生したセッションの種類。|  
|ProgressTotal|Long integer|イベントによって報告された進行状況の総数または量。|  
|IntegerData|Long integer|イベントに関連付けられている整数データ。 この列の内容は、イベント クラス、およびイベントのサブクラスによって異なります。|  
|ObjectID|String|イベントが発生したオブジェクトの識別子。|  
|ObjectType|String|ObjectName で指定されたオブジェクトの種類。|  
|ObjectName|String|イベントが発生したオブジェクトの名前。|  
|ObjectPath|String|イベントが発生したオブジェクトの階層パス。 パスは、ObjectName で指定されたオブジェクトの親に関するオブジェクト識別子の、コンマ区切りの文字列として表されます。|  
|ObjectReference|String|ObjectName で指定されたオブジェクトへのオブジェクト参照を表す XML 表現。|  
|NestLevel|Integer|イベントが発生したトランザクションのレベル。|  
|NumSegments|Long integer|イベントが発生したコマンドによって影響を受ける、またはアクセスされるデータ セグメントの数。|  
|重大度|Integer|イベントの例外の重大度レベル。 この列には、以下の値のいずれかが含まれます。<br /><br /> 値: 0 = 成功<br /><br /> 値: 1 = 情報<br /><br /> 値: 2 = 警告<br /><br /> 値: 3 = エラー|  
|成功|ブール値|コマンドが成功したか、失敗したかを示します。|  
|[エラー]|Long integer|イベントのエラー番号 (ある場合)。|  
|ConnectionID|String|イベントが発生した接続の識別子。|  
|DatabaseName|String|イベントが発生したデータベースの名前。|  
|NTUserName|String|イベントに関連付けられているユーザーの Windows ユーザー名。|  
|NTDomainName|String|イベントに関連付けられているユーザーの Windows ドメイン。|  
|ClientHostName|String|クライアント アプリケーションが実行されているコンピューターの名前。 この列には、クライアント アプリケーションによって渡された値が格納されます。|  
|ClientProcessID|Long integer|クライアント アプリケーションのプロセス識別子。|  
|ApplicationName|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、クライアント アプリケーションによって渡された値が格納されます。|  
|NTCanonicalUserName|String|イベントに関連付けられているユーザーの Windows の正規のユーザー名。|  
|SPID|String|イベントが発生したセッションのサーバー プロセス ID (SPID)。 この列の値は、イベントが発生した XMLA メッセージの SOAP ヘッダーで指定されたセッション ID に直接対応します。|  
|TextData|String|イベントに関連付けられたテキスト データ。 この列の内容は、イベント クラス、およびイベントのサブクラスによって異なります。|  
|ServerName|String|イベントが発生した [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスの名前。|  
|RequestParameters|String|イベントが発生したパラメーター化クエリまたは XMLA コマンドのパラメーター。|  
|RequestProperties|String|イベントが発生した XMLA メソッドのプロパティ。|  
  
## <a name="see-also"></a>参照  
 [Analysis Services での XMLA による開発](developing-with-xmla-in-analysis-services.md)  
  
  
