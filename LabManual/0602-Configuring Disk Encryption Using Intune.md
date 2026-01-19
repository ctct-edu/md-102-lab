# 【手順の参考】ラボ 0602: Intune を使用したディスク暗号化の構成



## 概要



このラボでは、Intune を使用して BitLocker ディスク暗号化を構成します。
※ 暗号化することにより、非常に動作が重くなり、この後のラボ使用に支障をきたすため、コース中には実施しません。手順の参考として頂くか、すべての演習の後で最後に実施してください。

### 前提 条件



このラボの前に、次のラボを完了する必要があります。

- 0203-Intuneへのデバイス登録の管理

- 0204-Intune へのデバイスの登録

- 0301-構成プロファイルの作成と配備

  注: Entra ID への Windows Hello サインイン認証をセキュリティで保護するために使用されるテキスト メッセージを受信できる携帯電話も必要です。

### シナリオ



SEA-WS1 のすべての情報を暗号化する必要があることが決定されました。SEA-WS1 でフルディスク暗号化を設定し、起動時に追加の PIN 認証を要求するように求められました。

### タスク 1: Intune でデバイス構成ポリシーを構成する



1. ブラウザーで、アドレス バーに「**[https://intune.microsoft.com](https://intune.microsoft.com/)**」と入力し、**Enter キー**を押します。
2. 既定のテナント パスワードを使用して、**`admin@yourtenant.onmicrosoft.com`** としてサインインします。
3. Microsoft Intune管理センターで、ナビゲーション バーから **[エンドポイント セキュリティ**] を選択します。
4. エンドポイント**セキュリティ |[概要**] ページで、[**ディスクの暗号化]** を選択します。
5. エンドポイント**セキュリティ |[ディスク暗号化]** ブレードの詳細ウィンドウで、 **[+ ポリシーの作成]** を選択します。
6. **[プロファイルの作成**] ページで、次のオプションを選択し、[**作成]** を選択します。
   - プラットフォーム: **Windows**
   - プロファイル: **BitLocker**
7. **基本** ページで、次の情報を入力し、**次へ** を選択します。
   - 名前: **Contoso BitLocker**
   - 説明: **すべてのデバイスに対して BitLocker を有効にする**
8. [**Configurations settings]** タブで、[**BitLocker**] を展開し、次のオプションを構成します。
   - デバイスの暗号化を必須にする: **有効**
9. [**Configurations settings]** タブで、[**オペレーティング システム ドライブ]** を展開し、次のオプションを構成し、他のすべてのオプションは既定値のままにします。
   - Enforce drive encryption type on operating system drives: **Enabled**
   - Require additional authentication at startup: **Enabled**
   - Configure minimum PIN length for startup: **Enabled**
   - Choose how BitLocker-protected operating system drives can be recovered: **Enabled**
   - Do not enable BitLocker until recovery information is stored to AD DS for operating system drives: **True**
   - Omit recovery options from the BitLocker setup wizard: **True**
   - Save BitLocker recovery information to AD DS for operating system drives: **True**
10. [**次へ**] を2回選択します。
11. [**Assignments]** タブで、検索ボックスに「**Contoso**」と入力し、[**Contoso Developer Devices]** グループを選択して、[**次へ**] を選択します。
12. [**Review + create**] タブで、情報を確認し、[**保存]** を選択します。

### タスク 2: BitLocker 設定を確認して有効にする

1. **SEA-WS1** で、PIN **102938**を使用して **Aaron Nicholls** としてサインインします。

2. タスク バーで [**Start ]** を選択し、**Settings**アプリを選択します。

3. **Settings**アプリで、 **[Accounts ]** を選択し、 [**Access work or school**] を選択します。

4. [**Access work or school**] セクションで、 **[Connected to Contoso's Azure AD]** リンクを選択し、 [**Info**] を選択します。[**Sync]** を選択します。必要に応じてパスワード「Pa55w.rd1234!」でサインインします。

5. [**Encryption needed]** 通知を選択します。

   *注: 通知が表示されるまでに時間がかかる場合があります。Windows フォーカス アシストによって通知が表示されない場合もあります。通知はWindowsデスクトップの右下に表示され、手動で確認できます。*

6. [**Are you ready to start encryption?**] ダイアログで、[ **I don't have any other disk encryption software installed, encrypt all my disks]** の横にあるチェック ボックスをオンにし、[**Yes**] を選択します。

7. [**Choose how to unlock your drive at startup?]** ページで、[**Enter a PIN(Recommended)**] を選択します

8. [**Enter a PIN**] ページの [**PIN**] ボックスと [**Reenter PIN**] ボックスに「**123456**」と入力し、[**Set PIN**] を選択します。

9. [**How do you want to back up your recovery key?**] ページで、[**Print the recovery key**] を選択してPDF印刷し、任意のな名前でDocumentフォルダーに保存した後、[**Next**] を選択します。

10. [**Choose how much of your drive to encrypt**] ページで、[**Encrypt used disk space only**] を選択し、Desktopに保存した後、[**Next**] を選択します。

11. [**Choose which encryption mode to use**] ページで、[**New encryption mode (best for fixed drives on this device)]** が選択されていることを確認し、[**Next**] を選択します。

12. [**Are you ready to encrypt this drive]** ページで、[**Continue]** を選択します。暗号化が完了するまで待ちます。

13. [**Encryption of C: is complete**] メッセージが表示されたら、[**Close**] を選択し、**SEA-WS1** を再起動します。

14. **SEA-WS1** が再起動したら、**123456** と入力して **Enter** キーを押してドライブのロックを解除します。

### タスク 3: BitLocker 保護を確認する

1. PIN **102938**を使用して **Aaron Nicholls** として **SEA-WS1** にサインインします。
2. 102938タスク バーで、[**File Explorer]** を選択し、[**This PC**] を選択します。
3. ナビゲーション ウィンドウで、[**Local Disk (C:)]** を右クリックし、[**Show more options**] を選択して、[**Manage BitLocker]** を選択します。
4. [**BitLocker Drive Encryption]** ウィンドウで、[**C: BitLocker on ]** 状態が表示されていることを確認します。これは、ドライブが暗号化されていることを意味します。
5. 開いているすべてのウィンドウを閉じて、**SEA-WS1** からサインアウトします。

**結果**: この演習を完了すると、Intune を使用してディスク暗号化が正常に構成されます。

**ラボの終わり**