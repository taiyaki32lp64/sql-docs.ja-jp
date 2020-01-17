---
title: ストアド プロシージャの拡張の作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- warnings [SQL Server]
- extended stored procedures [SQL Server], debugging
- extended stored procedures [SQL Server], creating
- messages [SQL Server], extended stored procedures
ms.assetid: 9f7c0cdb-6d88-44c0-b049-29953ae75717
author: rothja
ms.author: jroth
ms.openlocfilehash: 3c22077de3bf41bc09864ac2c7f24dbdd4ecc3e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032039"
---
# <a name="creating-extended-stored-procedures"></a>拡張ストアド プロシージャの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに CLR Integration を使用してください。  
  
 拡張ストアド プロシージャは、次に示すプロトタイプを備えた関数です。  
  
 SRVRETCODE *xp_extendedProcName* **(** SRVPROC **\*);**  
  
 プレフィックス xp_ は省略可能です。 拡張ストアド プロシージャ名は、サーバーにインストールされたコード ページや並べ替え順に関係なく、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでの参照時には常に大文字と小文字が区別されます。 DLL を作成する際は、次の点に注意します。  
  
-   エントリ ポイントが必要である場合は、DllMain 関数を記述します。  
  
     この関数は省略可能です。ソース コードに記述されていない場合は、コンパイラにより独自のバージョン (何も実行せずに TRUE を返す) がリンクされます。 DllMain 関数を記述した場合は、スレッドまたは処理が DLL にアタッチされる際、または DLL からデタッチされる際に、オペレーティング システムによってこの関数が呼び出されます。  
  
-   DLL 外部から呼び出す関数 (拡張ストアド プロシージャ関数) はすべて、エクスポートする必要があります。  
  
     関数をエクスポートするには、.def ファイルの EXPORTS セクションには、その名前の一覧を作成または方式では、Microsoft コンパイラ拡張子でソース コード内の関数名をプレフィックスにすることができます (注意\__declspec() が 2 つのアンダー スコアで始まる)。  
  
 拡張ストアド プロシージャ DLL を作成するには、次のファイルが必要です。  
  
|ファイル|説明|  
|----------|-----------------|  
|Srv.h|拡張ストアド プロシージャ API ヘッダー ファイル|  
|Opends60.lib|Opends60.dll のインポート ライブラリ|  
  
 拡張ストアド プロシージャ DLL を作成するには、ダイナミック リンク ライブラリ プロジェクトを作成します。 DLL の作成に関する詳細については、開発環境のドキュメントを参照してください。  
  
 すべての拡張ストアド プロシージャ DLL で次の関数を実装およびエクスポートすることを強くお勧めします。  
  
```  
__declspec(dllexport) ULONG __GetXpVersion()  
{  
   return ODS_VERSION;  
}  
```  
  
> [!NOTE]  
>  __declspec(dllexport) は Microsoft 固有のコンパイラ拡張子です。 お使いのコンパイラでこのディレクティブがサポートされない場合は、DEF ファイルの EXPORTS セクションでこの関数をエクスポートする必要があります。  
  
 ときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]トレースを使用して起動フラグ T260 またはシステム管理者特権を持つユーザーは、DBCC TRACEON (260) を実行している場合と、拡張ストアド プロシージャ DLL が _ _getxpversion()、警告メッセージをサポートしていないこと (エラー 8131。拡張ストアド プロシージャ DLL '%' ではエクスポートされません\__GetXpVersion().) がエラー ログに出力されます。 (なお\__GetXpVersion() が 2 つのアンダー スコアで始まります)。  
  
 拡張ストアド プロシージャ DLL により __GetXpVersion() がエクスポートされ、この関数によって返されるバージョンがサーバーで要求されるバージョンよりも低い場合、この関数によって返されたバージョンとサーバーが必要とするバージョンを示す警告メッセージがエラー ログに出力されます。 間違った値を返す場合、このメッセージが発生した場合\__GetXpVersion()、または以前のバージョンの srv.h をコンパイルします。  
  
> [!NOTE]  
>  拡張ストアド プロシージャでは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Win32 関数 SetErrorMode を呼び出さないでください。  
  
 実行時間の長い拡張ストアド プロシージャの場合は、srv_got_attention を定期的に呼び出すことにより、接続が強制的に切断された場合やバッチが中断された場合に、その拡張ストアド プロシージャが自身を終了できるようにすることをお勧めします。  
  
 拡張ストアド プロシージャ DLL をデバッグするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Binn ディレクトリにその拡張ストアド プロシージャをコピーします。 デバッグ セッションの実行可能ファイルを指定するには、パスとファイル名を入力してください、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]実行可能ファイル (たとえば、C:\Program files \microsoft SQL Server\MSSQL13 します。MSSQLSERVER\MSSQL\Binn\Sqlservr.exe)。 Sqlservr 引数については、次を参照してください。 [sqlservr アプリケーション](../../tools/sqlservr-application.md)します。  
  
## <a name="see-also"></a>参照  
 [srv_got_attention&#40;拡張ストアド プロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)  
  
  
