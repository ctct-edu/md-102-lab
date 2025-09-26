# ラボ 0201: Entra Join の構成と管理



## 概要



このラボでは、Entra ID 参加設定を構成し、Windows デバイスに対して標準と Entra ハイブリッド結合の両方のシナリオを実行します。

### 前提 条件



このラボの前に、次のラボを完了する必要があります。

- 0102 - Microsoft Entra Connect を使用した ID の同期

  > 注: Entra ID への Windows Hello サインイン認証をセキュリティで保護するために使用されるテキスト メッセージを受信できる携帯電話も必要です。

## 演習 1: Entra Join の構成



### シナリオ



すべてのユーザーがデバイスを Entra ID に参加できるように、Entra ID デバイス設定を構成する必要があります。また、ユーザーが最大 20 台のデバイスにのみ参加できること、および Allan Deyoung がすべての Entra 参加済みデバイスのローカル管理者として追加されていることを確認する必要があります。最後に、Joni Sherman をテナントに SEA-WS1 に参加させることで、Entra join が期待どおりに機能することを確認します。

### タスク1: Entra参加デバイス設定の構成



1. ブラウザーを起動し、アドレス バーに **[「https://entra.microsoft.com](https://entra.microsoft.com/)** 」と入力して、**Enter キー**を押します。

3. ユーザーとしてサインインし、テナント管理者パスワードを使用します。[**サインインしたままにする?]** プロンプトが表示されたら、[**いいえ**] を選択します。`Admin@yourtenant.onmicrosoft.com`

   > Microsoft Entra 管理センターが開きます。

4. Microsoft Entra 管理センターのナビゲーション ウィンドウで、 **[デバイス]** を選択し、[**すべてのデバイス**] を選択します。

   > まだデバイスに参加していないため、デバイスが見つからないことに注意してください。

5. **デバイス上 |[すべてのデバイス]** ページで、[**デバイス設定**] を選択します。

6. **デバイス|デバイスの設定** ページの  [**ユーザーはデバイスを Microsoft Entra に参加させることができます]** で、[**すべて]** が選択されていることを確認します。

   > これは、すべての Entra ユーザーが Windows 10 以降のデバイスを Microsoft Entra に参加させることが許可されていることを示します。この設定は、Entra ハイブリッド参加済みデバイス、または Windows Autopilot 自己展開モードを使用して参加したデバイスには適用されないことに注意してください。

7. [**Microsoft Entra を使用してデバイスを登録または参加させるには、多要素認証が必要です]** セクションで、設定が [**いいえ**] に設定されていることを確認します。

8. [**ユーザーあたりのデバイスの最大数]** セクションで、[**20**] を選択します。

9. **[ローカル管理者設定]** で、 **[管理 Microsoft Entra に参加済みのすべてのデバイスの追加のローカル管理者]** のリンクを選択します。[Device Administrators | 割り当て] ページが開きます。

10. [Device Administrators | 割り当て] ページで、[**+ 割り当ての追加**] を選択します。

11. [検索] ボックスに「**Allan Deyoung**」と入力し、**Allan Deyoung** ユーザー オブジェクトを選択して、[**追加]** を選択します。

    > Allan Deyoung は、すべての Entra 参加済みデバイスのデバイス管理者として追加されます。

12. ページ上部のナビゲーションリンクで **[デバイス|デバイスの設定]** を選択します。

13. **[デバイス|デバイスの設定]**  ページで、[**保存]** を選択します。

14. Entra管理センターのナビゲーションメニューで **[認証方法]** を選択します。

15. [**SMS]** を選択します。

16. [**有効にする**] を選択します。(スライドバーが青くなればOKです)

17. ページの下部にある [**保存**] を選択します。

### タスク2: Entra Joinの実行

1. **SEA-WS1** に切り替え、**Pa55w.rd** のパスワードで**管理者**としてサインインします。
2. タスク バーで、[**Start （Windowsアイコン）]** を選択し、[**Settings]** を選択します。
3. [**Settings**] ウィンドウで、[**Accounts]** を選択します。
4. [Accounts] ページで、[**Access work or school**] を選択します。
5. [**Access work or school**] ページで、[**Connect]** を選択します。
6. [**Microsoft account] ウィンドウで、**[**Join this device to Entra ID]** を選択します。
7. [**Sign in**]** ページで、「**[JoniS@yourtenant.onmicrosoft.com](mailto:JoniS@yourtenant.onmicrosoft.com)**」と入力し、[**次へ**] を選択します。
8. [**Enter password**] ページで、インストラクターから提供されたテナント パスワード(User password)を入力し、[**Sign in]** を選択します。
9. これが**Make sure this is your organization** ダイアログ ボックスで、**Join** を選択します。
10. [**You're all set!**] ページで、[**Done]** を選択します。
11. [**Access work or school**] ページで、 **[Connected to Contoso's Azure AD]** が表示されていることを確認します。
12. [**Settings** ] ページを閉じます。

### タスク3: Entra結合の検証

1. SEA-WS1 で、[**スタート（Windowsアイコン）]** を右クリックし、[**Windows Terminal (Admin)]** を選択します。[User Account Control] で、[**Yes**] を選択します。

2. PowerShell コンソールで、次のように入力し、**Enter** キーを押します。

   ```
   dsregcmd /status
   ```

   

3. **[Device State]** の下の出力で、 **[AzureAdJoined: YES]** が表示されていることを確認します。

   > これは、デバイスが Entra に参加していることを示します。

4. PowerShell を閉じます。

5. 、[**Start （Windowsアイコン）]** を右クリックし、[**Computer Management]** を選択します。

6. [Computer Management] で、[**Local Users and Groups]** を展開し、[**Groups]** を選択します。

7. [**Administrators]** グループをダブルクリックします。

   > Joni Sherman が SEA-WS1 のローカル管理者として追加されました。また、セキュリティ識別子 (SID) で表される 2 つのセキュリティ プリンシパルにも注意してください。これら 2 つの SID は、Entra ID グローバル管理者ロールと、Entra 参加済みデバイス管理者ロールを表します。

8. 開いているすべてのウィンドウを閉じて、SEA-WS1 からサインアウトします。

9. Microsoft Edge の Microsoft Entra 管理センターで、[**デバイス]** を選択し、[**すべてのデバイス**] を選択します。

   > [デバイス(Devices)] ペインに、SEA-WS1 がリストされていることに注意してください。

10. [**参加の種類]** が **[Microsoft Entra joined**] として表示され、所有者が **Joni Sherman** であることを確認します。

    > また、MDM 列に [なし] と表示されていることにも注意してください。これは、このデバイスがまだ Microsoft Intune によって管理されていないことを示します。

### タスク4: EntraユーザーとしてWindowsにサインインする



1. **SEA-WS1** に切り替え、インストラクターから提供されたテナント パスワードを使用して **`JoniS@yourtenant.onmicrosoft.com`** としてサインインします。

   > プロファイルが作成されるまで待ちます。

2. [**Use Windows Hello with your account]** ページで、[**OK]** を選択します。

3. [**Let's keep your account secure]** ページで、[**Next**] を選択します。

4. [**Keep your account secure]** ページで、[**I want to set up a different method]** を選択します。

5. [**Choose a different method**] ダイアログ ボックスで、[**Phone**] を選択します。

6. **[Phone** ] ページの[Country code] で [**Japan(+81)**] を選択後 [**Enter phone number**] フィールドに、テキスト メッセージを受信できる携帯電話番号を入力します。[**Next**] を選択します。

7. 確認コードを受け取ったら、[Phone ] ページでコードを入力し、[**Next**] を選択します。

8.  [**Next**] を選択し、 **[Done]** を選択します。

9. [**Set up a PIN**] ページの [**New PIN**] ボックスと [**Confirm PIN**] ボックスに「**`102938`**」と入力し、[**OK]** を選択します。

10. **[All set!]** ページで、[**OK]** を選択します。

### タスク 5: Entra から Windows デバイスを削除する

1. タスク バーで、[**Start （Windowsアイコン）]** を選択し、[**Settings]** を選択します。
2. [**Settings**] ウィンドウで、[**Accounts]** を選択します。
3. [Accounts] ページで、[**Access work or school**] を選択します。
4. [**Access work or school**] ページで、[**Connect]** を選択します。
5. [**職場または学校へのアクセス**] ページで、 **[Connected to Contoso's Azure AD]** をクリックします。
6. [**Disconnect **] を選択し、[**Yes**] を選択します。
7. [**Disconnect from the organization**] ページで、[**Disconnect**] を選択します。
8. **[Windows Security**] ダイアログ ボックスの **[Email address]** ボックスに「**Admin**」と入力し、[**Password ]** ボックスに「**Pa55w.rd**」と入力します。[**OK]** を選択します。
9. [ **Restart your PC** ] ダイアログ ボックスで、[**Restart now**] を選択します。SEA-WS1 が再起動します。
10. SEA-CL2 が再起動したら、パスワード **Pa55w.rd** を使用して **Contoso\Administrator** としてサインインします。

**結果**: この演習を完了すると、Microsoft Entra デバイス設定を構成し、デバイスを Entra に参加させ、Entra からデバイスを削除します。

## 演習 2: Entra ハイブリッド joinの構成



### シナリオ



一部の Contoso Windows デバイスは、現在、ローカルの Active Directory ドメイン サービスに参加しています。これらのデバイスがクラウド サービスにシームレスにアクセスできるようにするには、Entra ハイブリッド参加を有効にする予定です。Entra Connect 同期を再構成し、SEA-CL2 でプロセスをテストすることで、Entra ハイブリッド結合をテストします。

### タスク 1: 環境の準備

1. **SEA-SVR1** に切り替えます。
2. **[Start （Windowsアイコン）]** を選択し、[**Windows Administrative Tools]** を展開して、[**Active Directory Users and Computers]** を選択します。
3. **[Active Directory Users and Computers]** で、[**Contoso.com**] を右クリックし、[**New]** をポイントして、[**Organizational Unit]** を選択します。
4. [**New-Object - Organizational Unit **] ダイアログ ボックスで、「**`Entra ID clients`**」と入力し、[**OK]** を選択します。
5. ナビゲーション ウィンドウで、[**Seattle Clients**] OUを選択します。
6. **SEA-CL2** を右クリックし、[**Move]** を選択します。
7. [**Move]** ダイアログ ボックスで、 [**Entra ID clients**] を選択し、 **[OK]** を選択します。
8. **Active Directory Users and Computers を閉じます**。

### タスク 2: Entra Connect 同期での Entra ハイブリッド参加の構成

1. **SEA-SVR1** の**デスクトップ**で、[**Azure AD Connect]** をダブルクリックします。

2. [**Microsoft Entra Connect Sync]** ウィンドウで、 [**Configure**] を選択します。

3. **[ Additional tasks** ] ページで、[ **Configure device options** ] を選択し、[**Next**] を選択します。

4. **[Overview **] ページで、[**Next**] を選択します。

5. [**Connect to Microsoft Entra ID**] ページで、 [**Next**] を選択します。

6. [**Sign in to your account ]** ウィンドウで、テナント管理者アカウントを選択し、テナント パスワードを入力して **[Sign in]** を選択します。

7. [**Device options**] ページで、 **[Configure Hybrid Microsoft Entra ID join]** を選択し、 [**Next**] を選択します。

8. [**Device operating systems**] ページで、[**Windows 10 or later domain-joined devices**] を選択し、[**Next**] を選択します。

9. **[SCP configuration**] ページで、[**Contoso.com**] の横にあるチェックボックスをオンにします。

10. [**Authentication Service]** ドロップダウンから **[Microsoft Entra ID]** を選択し、 **[Add]** を選択します。

11. [**Enterprise Admin Credentials**] ウィンドウで、**User name**として「**Contoso\Administrator**」と入力し、**パスワード**として「**Pa55w.rd**」と入力します。[**OK**] を選択し、[**Next**] を選択します。

12. **Ready to configure** ページで、**Configure** を選択して構成を実行します。

13. 構成が完了したら、[**Exit]** を選択します。

14. **SEA-CL2**に切り替えます。

15. サインイン ページで、画面右下[**電源**] ボタンを選択し、[**Restart**] を選択します。

    > **手記****SEA-CL2** を再起動すると、Entra Connect Sync を再構成して作成された SCP をより迅速に検出できるようになります。

16. **SEA-CL2** が再起動したら、**Pa55w.rd** のパスワードを使用して **Contoso\Administrator** としてサインインします。

### タスク3: 新しいOUを同期するようにEntra Connect Syncを再構成する

1. **SEA-SVR1** の**デスクトップ**で、[**Azure AD Connect]** をダブルクリックします。

2. [**Microsoft Entra Connect Sync]** ウィンドウで、 [**Configure**] を選択します。

3. **[ Additional tasks** ] ページで、[ **Customize synchronization options** ] を選択し、[**Next**] を選択します。

4. [**Connect to Microsoft Entra ID**] ページで、 [**Next**] を選択します。

5. [**Sign in to your account ]** ウィンドウで、テナント管理者アカウントを選択し、テナント パスワードを入力して **[Sign in]** を選択します。

6. [**Connect your directories**] ページで、[**Next**] を選択します。

7. [**ドDomain and OU filtering]** ページで、[**Sync selected domains and OUs]** が選択されていることを確認し、[**Contoso.com**] を展開します。

8. [**Entra ID clients]** の横にあるチェック ボックスをオンにします。**他に変更を加えず**、[**Next**] を選択します。

9. [**Optional features]** ページで、変更を加えず、[**Next**] を選択します。

10. [**Ready to configure]** ウィンドウで、[**Configure ]** を選択して構成を実行し、同期を開始します。

11. 構成が完了したら、[**Exit]** を選択します。

    > **注**: Entra Connect Sync は、同期する OU を変更すると自動的に同期されるようになりました。**同期サービス**を使用して、同期ステータスを監視できます。

### タスク4: Entraハイブリッド参加の確認

1. **SEA-CL2**に切り替えます。

2. **[Start （Windowsアイコン）]** を右クリックし、[**Shut down or sign out**] を選択して、[**Restart**] を選択します。

   *注: 再起動すると、SEA-CL2 で Entra ハイブリッド参加がトリガーされます。*

3. **SEA-CL2** が再起動したら、**Pa55w.rd** のパスワードを使用して **Contoso\Administrator** としてサインインします。

4. [**スタート（Windowsアイコン）]** を右クリックし、[**Windows Terminal (Admin)]** を選択します。

5. **Windows PowerShell** ウィンドウで、次のコマンドを入力し、**Enter キー**を押します。

   ```
   dsregcmd /status
   ```

   

6. [**Device State]** の下の出力で、 **[AzureAdJoined : YES]** と **[DomainJoined : YES]** が表示されていることを確認します。

   > **注**:デバイスがまだEntra IDに参加していない場合は、**SEA-SRV1**に切り替えて、次のコマンドを実行します。完了したら、SEA-CL2 に戻し、コンピュータをもう一度再起動します。

   ```
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

   

7. SEA-CL2 のすべてのウィンドウを閉じて、サインアウトします。

8. ブラウザーのMicrosoft Entra 管理センターに切り替えます。

9. [**デバイス]** > [**すべてのデバイス**] を選択します。

10. **SEA-CL2** に、行 **[参加の種類**] の値として **Microsoft Entra hybrid joined**があることを確認します。必要に応じて、SEA-CL2 がリストされていない場合は [**更新]** ボタンを選択します。

    

**結果**: この演習を完了すると、Entra ハイブリッド結合が正常に構成され、検証されます。

**ラボの終わり**
