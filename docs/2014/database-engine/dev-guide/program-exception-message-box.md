---
title: 例外メッセージ ボックス プログラム |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 316afc6d5f3a87ff7431240681066ac5ee66ede6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780699"
---
# <a name="program-exception-message-box"></a>例外メッセージ ボックスのプログラミング
  例外メッセージ ボックスをアプリケーションで使用すると、<xref:System.Windows.Forms.MessageBox> クラスを使用した場合よりも高い柔軟性で、メッセージ エクスペリエンスを制御することができます。 詳細については、次を参照してください。[例外メッセージ ボックスのプログラミング](../../../2014/database-engine/dev-guide/exception-message-box-programming.md)します。 例外メッセージ ボックス .dll を取得および展開する方法の詳細については、「 [Deploying an Exception Message Box Application](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md)」をご覧ください。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>例外メッセージ ボックスを使用して例外を処理するには  
  
1.  Microsoft.ExceptionMessageBox.dll アセンブリへの参照をマネージド コード プロジェクトに追加します。  
  
2.  (省略可能)追加、 `using` (c#) または`Imports`([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET) ディレクティブを使用して、<xref:Microsoft.SqlServer.MessageBox>名前空間。  
  
3.  予想される例外を処理する try-catch ブロックを作成します。  
  
4.  `catch` ブロック内に、<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> クラスのインスタンスを作成します。 渡す、<xref:System.Exception>オブジェクトによって処理される、 `try` - `catch`ブロックします。  
  
5.  (省略可) <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> に次のプロパティを 1 つ以上設定します。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 例外メッセージ ボックスに表示するボタンを指定する列挙です。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 例外メッセージ ボックスの既定のボタンを指定する列挙です。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 使用する例外メッセージ ボックスの他の動作を制御する列挙です。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 例外メッセージ ボックスに表示する記号を指定する列挙です。  
  
6.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> メソッドを呼び出します。 例外メッセージ ボックスが属する親ウィンドウを渡します。  
  
7.  (省略可能)値に注意してください返された<xref:System.Windows.Forms.DialogResult>列挙型、ユーザーがボタンを判断する必要がある場合にクリックします。  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>例外なしで例外メッセージ ボックスを表示するには  
  
1.  Microsoft.ExceptionMessageBox.dll アセンブリへの参照をマネージド コード プロジェクトに追加します。  
  
2.  (省略可能)追加、 `using` (c#) または`Imports`(Visual Basic .NET) ディレクティブを使用する、<xref:Microsoft.SqlServer.MessageBox>名前空間。  
  
3.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> クラスのインスタンスを作成します。 <xref:System.String> 値としてメッセージ テキストを渡します。  
  
4.  (省略可) <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> に次のプロパティを 1 つ以上設定します。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 例外メッセージ ボックスに表示するボタンを指定する列挙です。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A> - 例外メッセージ ボックスのダイアログ ボックスのキャプションです。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 例外メッセージ ボックスのダイアログ ボックスの既定のボタンを指定する列挙です。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 使用する例外メッセージ ボックスの他の動作を制御する列挙です。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 例外メッセージ ボックスに表示する記号を指定する列挙です。  
  
5.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> メソッドを呼び出します。 例外メッセージ ボックスが属する親ウィンドウを渡します。  
  
6.  (省略可) ユーザーがクリックしたボタンを判断する必要がある場合は、返された <xref:System.Windows.Forms.DialogResult> 列挙値に注意します。  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>カスタマイズされたボタンのある例外メッセージ ボックスを表示するには  
  
1.  Microsoft.ExceptionMessageBox.dll アセンブリへの参照をマネージド コード プロジェクトに追加します。  
  
2.  (省略可能)追加、 `using` (c#) または`Imports`(Visual Basic .NET) ディレクティブを使用する、<xref:Microsoft.SqlServer.MessageBox>名前空間。  
  
3.  次の 2 つのうち、いずれかの方法で <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> クラスのインスタンスを作成します。  
  
    -   渡す、<xref:System.Exception>オブジェクトによって処理される、 `try` - `catch`ブロックします。  
  
    -   <xref:System.String> 値としてメッセージ テキストを渡します。  
  
4.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> に次のいずれかの値を設定します。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore> -が表示されます、**中止**、**再試行**、および**無視**ボタン。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom> - カスタム ボタンを表示します。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK> -表示、 **OK**ボタン。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel> -表示、 **[ok]** と**キャンセル**ボタン。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel> -が表示されます、**再試行**と**キャンセル**ボタン。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo> -表示**はい**と**なし**ボタン。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel> -表示 **[はい]** 、**いいえ**と**キャンセル**ボタン。  
  
5.  (省略可) カスタム ボタンを使用する場合は、<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A> メソッドのオーバーロードの 1 つを呼び出し、最多で 5 つのカスタム ボタンのテキストを指定します。  
  
6.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> メソッドを呼び出します。 例外メッセージ ボックスが属する親ウィンドウを渡します。  
  
7.  (省略可) ユーザーがクリックしたボタンを判断する必要がある場合は、返された <xref:System.Windows.Forms.DialogResult> 列挙値に注意します。 カスタム ボタンを使用する場合に、ユーザーがクリックしたボタンを判断するには、<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult> プロパティの <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A> の値に注意します。  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>ユーザーが例外メッセージ ボックスを表示するかどうかを決定できるようにするには  
  
1.  Microsoft.ExceptionMessageBox.dll アセンブリへの参照をマネージド コード プロジェクトに追加します。  
  
2.  (省略可能)追加、 `using` (c#) または`Imports`(Visual Basic .NET) ディレクティブを使用する、<xref:Microsoft.SqlServer.MessageBox>名前空間。  
  
3.  次の 2 つのうち、いずれかの方法で <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> クラスのインスタンスを作成します。  
  
    -   渡す、<xref:System.Exception>オブジェクトによって処理される、 `try` - `catch`ブロックします。  
  
    -   <xref:System.String> 値としてメッセージ テキストを渡します。  
  
4.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A> プロパティを `true`に設定します。  
  
5.  (省略可) 表示された例外メッセージ ボックスを再度表示するかどうかを確認するテキストを <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A> に指定します。 既定のテキストは、"今後、このメッセージを表示しない" です。  
  
6.  アプリケーションが実行されている間のみユーザーの指定を保持する場合は、<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A> の値をグローバルな <xref:System.Boolean> 変数に設定します。 例外メッセージ ボックスのインスタンスを作成する前に、この値を評価します。  
  
7.  ユーザーの指定を永続的に保持する必要がある場合は、次の操作を行います。  
  
    1.  CreateSubKe メソッドを呼び出して、アプリケーションが使用するカスタム レジストリ キーを開き、<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A> に返された RegistryKey オブジェクトを設定します。  
  
    2.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A> に使用するレジストリの名前を設定します。  
  
    3.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A> を `true` に設定します。  
  
    4.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> メソッドを呼び出します。 指定したレジストリ キーが評価され、レジストリ キーに格納されているデータが 0 の場合にのみ、例外メッセージ ボックスが表示されます。 ダイアログ ボックスが表示され、ユーザーがボタンをクリックする前にチェック ボックスをオンにした場合は、レジストリ キーのデータが 1 に設定されます。  
  
## <a name="example"></a>例  
 この例では、例外メッセージ ボックスを使用だけを持つ、 **[ok]** 処理された例外とその他のアプリケーションに固有の情報を含むアプリケーション例外からの情報を表示するボタンをクリックします。  
  
 [!code-csharp[HowTo#emb_showOKbutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showokbutton)]  
  
 [!code-vb[HowTo#emb_vb_showOKbutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showokbutton)]  
  
## <a name="example"></a>例  
 この例での例外メッセージ ボックスを使用して**はい**と**いいえ**からユーザーが選択したボタンします。  
  
 [!code-csharp[HowTo#emb_showYesNobutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showyesnobutton)]  
  
 [!code-vb[HowTo#emb_vb_showYesNobutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showyesnobutton)]  
  
## <a name="example"></a>例  
 次の例では、カスタム ボタンのある例外メッセージ ボックスを使用します。  
  
 [!code-csharp[HowTo#emb_showcustombutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showcustombutton)]  
  
 [!code-vb[HowTo#emb_vb_showcustombutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showcustombutton)]  
  
## <a name="example"></a>例  
 次の例では、チェック ボックスを使用して、例外メッセージ ボックスを表示するかどうかを判断します。  
  
 [!code-csharp[HowTo#emb_usecheckbox](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_usecheckbox)]  
  
 [!code-vb[HowTo#emb_vb_usecheckbox](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_usecheckbox)]  
  
## <a name="example"></a>例  
 次の例では、チェック ボックスとレジストリ キーを使用して、例外メッセージ ボックスを表示するかどうかを判断します。  
  
 [!code-csharp[HowTo#emb_useregkey](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_useregkey)]  
  
 [!code-vb[HowTo#emb_vb_useregkey](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_useregkey)]  
  
## <a name="example"></a>例  
 この例では、例外メッセージ ボックスを使用して、トラブルシューティングやデバッグに役立つ追加情報を表示します。  
  
 [!code-csharp[HowTo#emb_moreinfo](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_moreinfo)]  
  
 [!code-vb[HowTo#emb_vb_moreinfo](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_moreinfo)]  
  
  
