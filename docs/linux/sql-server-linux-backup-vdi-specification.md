---
title: VDI バックアップの仕様 - SQL Server on Linux
description: SQL Server バックアップ仮想デバイス インターフェイスの仕様。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: c2dafa8f1c0811771cbbc684b24d2c92e989dff5
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810969"
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>SQL Server on Linux の VDI クライアント SDK の仕様

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このドキュメントでは、SQL Server on Linux の仮想デバイス インターフェイス (VDI) クライアント SDK によって提供されるインターフェイスについて説明します。 独立系ソフトウェア ベンダー (ISV) は、仮想バックアップ デバイス アプリケーション プログラミング インターフェイス (API) を使用して、自社の製品に SQL Server を統合することができます。 全般的に、Linux 上の VDI は Windows 上の VDI と同様に動作しますが、次の点が変更されます。

- Windows 共有メモリが POSIX 共有メモリになります。
- Windows セマフォが POSIX セマフォになります。
- HRESULT や DWORD などの Windows 型は、同等の整数に変更されます。
- COM インターフェイスは削除され、C++ クラスのペアに置き換えられます。
- SQL Server on Linux では名前付きインスタンスがサポートされていないため、インスタンス名への参照は削除されました。 
- 共有ライブラリは、/opt/mssql/lib/libsqlvdi.so にインストールされている libsqlvdi.so に実装されます

このドキュメントは、Windows 上の MS SQL Server の VDI の仕様について説明している **vbackup.chm** の内容を補うものです。 [Windows 上の SQL VDI の仕様](https://www.microsoft.com/download/details.aspx?id=17282)をダウンロードしてください。

また、[SQL Server サンプルの GitHub リポジトリ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux)で、サンプルの VDI バックアップ ソリューションを参照してください。

## <a name="user-permissions-setup"></a>ユーザーのアクセス許可の設定

Linux では、POSIX プリミティブは、それを作成したユーザーとその既定のグループによって所有されます。 SQL Server によって作成されたオブジェクトの場合、既定では mssql ユーザーと mssql グループによって所有されます。 SQL Server と VDI クライアントの間の共有を許可するには、次の 2 つの方法のいずれかを使用することをお勧めします。

1. mssql ユーザーとして VDI クライアントを実行する
   
   mssql ユーザーに切り替えるには、次のコマンドを実行します。
   
   ```bash
   sudo su mssql
   ```

2. mssql ユーザーを vdiuser のグループに追加し、vdiuser を mssql グループに追加する。
   
   次のコマンドを実行します。

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   サーバーを再起動して、SQL Server と vdiuser の新しいグループを取得します

## <a name="client-functions"></a>クライアント関数

この章では、各クライアント関数について説明します。 説明には次の情報が含まれます。

- 関数の目的
- 関数の構文
- パラメーター リスト
- 戻り値
- Remarks

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**目的** この関数は、仮想デバイス セットを作成するために使用されます。

**構文**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| | **name** | これにより、仮想デバイス セットが識別されます。 CreateFileMapping() によって使用される命名規則に従う必要があります。 円記号 (\) 以外の任意の文字を使用できます。 これは文字列です。 この文字列には、ユーザーの製品名または会社名とデータベース名をプレフィックスとして付けることをお勧めします。 |
| |**cfg** | これは、仮想デバイス セットの構成です。 詳細については、このドキュメントで後述する「構成」を参照してください。

| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR** | 関数が正常に実行されました。 |
| |**VD_E_NOTSUPPORTED** |構成の 1 つ以上のフィールドが無効であるか、サポートされていません。 |
| |**VD_E_PROTOCOL** | 仮想デバイス セットが既に存在しています。

**解説** Create メソッドは、バックアップまたは復元操作ごとに 1 回だけ呼び出す必要があります。 Close メソッドを呼び出した後、クライアントでは、インターフェイスを再利用して別の仮想デバイス セットを作成できます。

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**目的** この関数は、サーバーによって仮想デバイス セットが構成されるのを待機するために使用されます。
**構文**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| | **timeout** | これはミリ秒単位のタイムアウト値です。 タイムアウトが発生しないようにするには、INFINITE または負の整数を使用します。
| | **cfg** | 正常に実行されると、サーバーによって選択された構成がこの引数に格納されます。 詳細については、このドキュメントで後述する「構成」を参照してください。

| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR** | 構成が返されました。
| |**VD_E_ABORT** |SignalAbort が呼び出されました。
| |**VD_E_TIMEOUT** |関数がタイムアウトしました。

**解説** この関数は、警告可能な状態でブロックします。 呼び出しが正常に終了すると、仮想デバイス セット内のデバイスを開くことができます。


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**目的** この関数は、仮想デバイス セット内のいずれかのデバイスを開くために使用されます。
**構文**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| | **name** |これにより、仮想デバイス セットが識別されます。
| | **ppVirtualDevice** |関数が成功した場合、仮想デバイスへのポインターが返されます。 このデバイスは、GetCommand と CompleteCommand に使用されます。

| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR** |関数が正常に実行されました。
| |**VD_E_ABORT** | 中止が要求されました。
| |**VD_E_OPEN** |  すべてのデバイスが開いています。
| |**VD_E_PROTOCOL** |  セットが初期化中の状態ではないか、この特定のデバイスが既に開いています。
| |**VD_E_INVALID** |デバイス名が無効です。 これは、セットの構成要素として認識されている名前の 1 つではありません。

**解説** VD_E_OPEN は、問題がなくても返される場合があります。 クライアントでは、このコードが返されるまで、ループを使って OpenDevice を呼び出すことができます。
複数のデバイス (たとえば、*n* 個デバイス) が構成されている場合は、仮想デバイス セットから一意のデバイス インターフェイスが *n* 個返されます。

`GetConfiguration` 関数は、デバイスが開けるようになるまで待機するために使用できます。
この関数が成功しなかった場合は、ppVirtualDevice によって null 値が返されます。
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**目的** この関数は、デバイスのキューに登録されている次のコマンドを取得するために使用されます。 要求された場合、この関数は次のコマンドを待機します。

**構文**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| |**timeout** |これは、ミリ秒単位の待機時間です。 無期限に待機するには、INFINTE を使用します。 コマンドをポーリングするには、0 を使用します。 現在使用できるコマンドがない場合は、VD_E_TIMEOUT が返されます。 タイムアウトが発生した場合は、クライアントによって次のアクションが決定されます。
| |**Timeout** |これは、ミリ秒単位の待機時間です。 無期限に待機するには、INFINTE または負の値を使用します。 コマンドをポーリングするには、0 を使用します。 タイムアウトするまでにいずれのコマンドも使用可能にならなかった場合は、VD_E_TIMEOUT が返されます。 タイムアウトが発生した場合は、クライアントによって次のアクションが決定されます。
| |**ppCmd** |コマンドが正常に返された場合は、このパラメーターによって、実行するコマンドのアドレスが返されます。 返されるメモリは読み取り専用です。 コマンドが完了すると、このポインターは CompleteCommand ルーチンに渡されます。 各コマンドの詳細については、このドキュメントで後述する「コマンド」を参照してください。
        
| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR** |コマンドがフェッチされました。
| |**VD_E_CLOSE** |デバイスがサーバーによって閉じられました。
| |**VD_E_TIMEOUT** |使用可能なコマンドがなく、タイムアウトになりました。
| |**VD_E_ABORT** |クライアントまたはサーバーが SignalAbort を使用して強制的にシャットダウンされました。

**解説** VD_E_CLOSE が返された場合は、SQL Server によってデバイスが閉じられたことを意味します。 これは通常のシャットダウンの一部です。 すべてのデバイスが閉じられると、クライアントによって ClientVirtualDeviceSet::Close が呼び出され、仮想デバイスセットが閉じられます。
このルーチンで、コマンドを待機するためにブロックする必要がある場合、スレッドは警告可能な状態のまま維持されます。

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**目的** この関数は、コマンドが終了したことを SQL Server 通知するために使用されます。 コマンドについては、適切な完了情報が返される必要があります。 詳細については、このドキュメントで後述する「コマンド」を参照してください。

**構文** 

   ```
   int ClientVirtualDevice::CompleteCommand (
   VDC_Command pCmd,        // the command
   int  completionCode,     // completion code
   unsigned long    bytesTransferred,   // bytes transferred
   int64_t  position        // current position
   );
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| |**pCmd** |これは、以前に ClientVirtualDevice::GetCommand から返されたコマンドのアドレスです。
| |**completionCode** |これは、完了状態を示す状態コードです。 このパラメーターは、すべてのコマンドについて返される必要があります。 返されるコードは、実行されるコマンドに対して適切なものである必要があります。 ERROR_SUCCESS は、コマンドが正常に実行されたことを示すために、すべてのケースで使用されます。 使用可能なコードの完全な一覧については、vdierror.h ファイルを参照してください。 各コマンドの典型的な状態コードの一覧は、このドキュメントで後述する「コマンド」に示されています。
| |**bytesTransferred** |これは、正常に転送されたバイト数です。 この値は、データ転送コマンド Read および Write 用にのみ返されます。
| |**position** |これは、GetPosition コマンドのみを対象とした応答です。
        
| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR** |正常に完了しました。
| |**VD_E_INVALID** |pCmd がアクティブなコマンドではありませんでした。
| |**VD_E_ABORT** |中止が指示されました。
| |**VD_E_PROTOCOL** |デバイスが開いていません。

**解説** なし

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**目的** この関数は、異常終了が発生することを通知するために使用されます。

**構文** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| |なし | 適用なし
        
| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR**|中止の通知が正常に送信されました。

**解説** クライアントでは、バックアップ操作または復元操作をいつでも中止できます。 このルーチンは、すべての操作を中止する必要があることを通知するものです。 仮想デバイス セット全体の状態は、異常終了した状態になります。 後続のコマンドは、いずれのデバイスについても返されません。 未完了のコマンドはすべて自動的に完了し、完了コードとして ERROR_OPERATION_ABORTED が返されます。 クライアントでは、クライアントに提供されたバッファーの未処理の使用を安全に終了した後、ClientVirtualDeviceSet::Close を呼び出す必要があります。 詳細については、このドキュメントで前述している「異常終了」を参照してください。

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**目的** この関数は、ClientVirtualDeviceSet::Create によって作成された仮想デバイス セットを閉じるために使用されます。 これにより、仮想デバイス セットに関連付けられているすべてのリソースが解放されます。

**構文** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| |なし |適用なし
        
| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR** |これは、仮想デバイス セットが正常に閉じられた場合に返されます。
| |**VD_E_PROTOCOL** |仮想デバイス セットが開かれていないため、アクションは実行されませんでした。
| |**VD_E_OPEN** |デバイスがまだ開いたままでした。

**解説** Close の呼び出しは、仮想デバイス セットによって使用されているすべてのリソースを解放する必要があるというクライアント宣言です。 クライアントでは、Close を呼び出す前に、データ バッファーと仮想デバイスに関連するすべてのアクティビティが終了していることを確認する必要があります。 OpenDevice によって返されたすべての仮想デバイス インターフェイスは、Close によって無効化されます。
クライアントでは、Close 呼び出しが返された後、仮想デバイス セット インターフェイスに対して Create 呼び出しを発行することが許可されます。 この呼び出しによって、後続のバックアップまたは復元操作用に、新しい仮想デバイス セットが作成されます。
1 つ以上の仮想デバイスが開いたままの状態で Close が呼び出された場合は、VD_E_OPEN が返されます。 その場合、SignalAbort が内部でトリガーされ、可能であれば、適切なシャットダウンが行われます。 VDI リソースは解放されます。 クライアントでは、ClientVirtualDeviceSet::Close を呼び出す前に、各デバイスで VD_E_CLOSE が通知されるまで待機する必要があります。 仮想デバイス セットが既に異常終了状態になっていることがクライアントでわかっている場合は、GetCommand から VD_E_CLOSE が通知されるのを待たず、共有バッファーでのアクティビティが終了した後すぐに、ClientVirtualDeviceSet::Close を呼び出すことができます。
詳細については、このドキュメントで前述している「異常終了」を参照してください。

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**目的** この関数は、仮想デバイス セットをセカンダリ クライアントで開くために使用されます。 プライマリ クライアントでは、既に Create と GetConfiguration を使用して仮想デバイス セットが設定されている必要があります。

**構文** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| |**setName** |これにより、セットが識別されます。 この名前は大文字と小文字が区別されます。また、ClientVirtualDeviceSet::Create を呼び出す際にプライマリ クライアントによって使用された名前と一致する必要があります。

| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR** |関数が正常に実行されました。
| |**VD_E_PROTOCOL** |仮想デバイス セットが作成されていないか、このクライアントで既に開かれているか、またはセカンダリ クライアントからのオープン要求を受け入れる準備が仮想デバイス セットで整っていません。
| |**VD_E_ABORT** |操作を中止しています。

**解説** 複数のプロセス モデルを使用している場合、セカンダリ クライアントの正常終了と異常終了を検出する役割は、プライマリ クライアントが担います。

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**目的** アプリケーションによっては、ClientVirtualDevice::GetCommand によって返されるバッファーを操作するために、複数のプロセスが必要になる場合があります。 その場合、コマンドを受け取るプロセスでは、GetBufferHandle を使用して、バッファーを識別するプロセス独立ハンドルを取得することができます。 その後、このハンドルによって、同じ仮想デバイス セットを開いている他のプロセスと通信することができます。 そのプロセスでは、ClientVirtualDeviceSet::MapBufferHandle を使用して、バッファーのアドレスが取得されます。 このアドレスは、パートナーとは異なるアドレスになる可能性があります。なぜなら、各プロセスが異なるアドレスでバッファーをマッピングしている可能性があるからです。

**構文** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| |**pBuffer** |これは、Read または Write コマンドから取得されたバッファーのアドレスです。
| |**BufferHandle** |バッファーの一意の識別子が返されます。

| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR** |関数が正常に実行されました。
| |**VD_E_PROTOCOL** |仮想デバイス セットは現在開いていません。
| |**VD_E_INVALID** |pBuffer は有効なアドレスではありません。

解説 GetBufferHandle 関数を呼び出すプロセスでは、データ転送が完了したときに ClientVirtualDevice::CompleteCommand を呼び出す必要があります。

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**目的** この関数は、他のプロセスから取得したバッファー ハンドルから有効なバッファー アドレスを取得するために使用されます。 

**構文** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| パラメーター | 引数 | 説明
| ----- | ----- | ------ |
| |**dwBuffer** |これは、ClientVirtualDeviceSet::GetBufferHandle によって返されるハンドルです。
| |**ppBuffer** |これは、現在のプロセスで有効なバッファーのアドレスです。

| 戻り値 | 引数 | 説明
| ----- | ----- | ------ |
| |**NOERROR** |関数が正常に実行されました。
| |**VD_E_PROTOCOL** |仮想デバイス セットは現在開いていません。
| |**VD_E_INVALID** |ppBuffer は無効なハンドルです。

**解説** ハンドルが正しく通信されるように注意する必要があります。 ハンドルは、1 つの仮想デバイス セットに対してローカルです。 ハンドルを共有するパートナーでは、バッファー ハンドルが、最初に取得された仮想デバイス セットのスコープ内でのみ使用されていることを確認する必要があります。


