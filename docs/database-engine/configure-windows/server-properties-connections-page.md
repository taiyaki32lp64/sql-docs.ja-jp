---
title: サーバーのプロパティ ([接続] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.connections.f1
ms.assetid: 33be8ac5-12dd-4b8a-99e0-68261c219dd2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 15ab408465890a13fc6e87efd2f2e15e8f8a7fad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025490"
---
# <a name="server-properties---connections-page"></a>サーバーのプロパティ - [接続] ページ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このページを使用すると、接続オプションを表示したり変更したりできます。  
  
## <a name="connections"></a>接続  
 **[コンカレント接続の最大数 (0 = 無制限)]**  
 0 以外の値に設定した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で許可される接続の数を制限します。  
  
> [!CAUTION]  
>  この値を 1 や 2 などの小さい値に設定することにより、管理者が接続してサーバー管理できないように指定できます。ただし、専用管理者接続には常に接続できます。  
  
## <a name="default-connection-options"></a>[既定の接続オプション]  
 **Default connection options**  
 次の表に示すような既定の接続オプションを指定します。  
  
|構成オプション|[説明]|  
|--------------------------|-----------------|  
|**[disable deferred constraint checking]**|中間制約チェックまたは遅延制約チェックを制御します。|  
|**暗黙のトランザクション**|ステートメント実行時にトランザクションを暗黙的に開始するかどうかを制御します。|  
|**[cursor close on commit]**|コミット実行後のカーソルの動作を制御します。|  
|**[ansi warnings]**|集計警告の切り詰めと NULL を制御します。|  
|**[ansi padding]**|固定長変数の埋め込みを制御します。|  
|**[ANSI NULL]**|等価演算を使用する場合に `NULL` 処理を制御します。|  
|**[arithmetic abort]**|クエリ実行中にオーバーフローまたは 0 除算のエラーが発生した場合に、クエリを終了します。|  
|**[arithmetic ignore]**|クエリ実行中にオーバーフローまたは 0 除算エラーが発生した場合に、NULL を返します。|  
|**引用符で囲まれた識別子 (quoted identifier)**|式を評価するときに、単一引用符と二重引用符を区別します。|  
|**[no count]**|各ステートメントの最後に返される、何行処理されたかを示すメッセージを表示しないようにします。|  
|**[ANSI NULL Default On]**|ANSI 互換の NULL 値の許可属性を使用するようにセッションの動作を変更します。 新しい列で、NULL 値を許可するかどうかが明示的に定義されていない場合は、NULL 値を許可するように定義されます。|  
|**[ANSI NULL Default Off]**|ANSI 互換の NULL 値の許可属性を使用しないようにセッションの動作を変更します。 新しい列で、NULL 値を許容するかどうかが明示的に定義されていない場合は、NULL を許可しないと定義されます。|  
|**[concat null yields null]**|NULL 値を文字列と連結した場合に、NULL を返します。|  
|**[numeric round abort]**|式の精度が低下した場合にエラーを生成します。|  
|**[xact abort]**|Transact-SQL ステートメントで実行時エラーが発生した場合、トランザクションをロールバックします。|  
  
 接続オプションの詳細については、オンライン ブックで該当するオプションを参照してください。  
  
## <a name="remote-server-connections"></a>[リモート サーバー接続]  
 **[このサーバーへのリモート接続を許可する]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを実行するリモート サーバーからのストアド プロシージャの実行を制御します。 このチェック ボックスをオンにすることは、 **sp_configureremote access** オプションを 1 に設定することと同じです。 このチェック ボックスをオフにすると、ストアド プロシージャはリモート サーバーから実行されません。  
  
 **[リモート クエリのタイムアウト (秒単位、0 = タイムアウトなし)]**  
 リモート操作の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] タイムアウトまでの時間 (秒) を指定します。既定は 600 秒 (10 分) 間の待機です。  
  
 **[サーバー間通信で使用する分散トランザクションを要求する]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) トランザクションにより、サーバー間のプロシージャのアクションを保護します。 詳細については、「 [remote proc trans サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-remote-proc-trans-server-configuration-option.md)」を参照してください。  
  
## <a name="property-page-display-options"></a>[プロパティ] ページの [表示] オプション  
 **[構成した値]**  
 このペインの各オプションに構成されている値を表示します。 これらの値を変更した場合は、 **[実行中の値]** をクリックして、変更後の値が反映されているかどうかを確認してください。 値が反映されていない場合は、最初に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを再起動する必要があります。  
  
 **[実行中の値]**  
 このペイン上のオプションの、現在実行中の値を表示します。 これらの値は読み取り専用です。  
  
## <a name="see-also"></a>参照  
 [オプション &#40;クエリ実行:SQL Server:[詳細設定] ページ&#41;](https://msdn.microsoft.com/library/3ec788c7-22c3-4216-9ad0-81a168d17074)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
