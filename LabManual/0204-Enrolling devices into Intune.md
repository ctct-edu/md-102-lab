# ラボ 0204: Microsoft Intune へのデバイスの登録



## 概要



このラボでは、Windows クライアントを Entra ID に参加させ、デバイスが Microsoft Intune に自動的に登録されていることを確認します。

### 前提 条件



このラボの前に、次のラボを完了する必要があります。

- 0101 - Entra IDでのアイデンティティの管理

- 0102 - Entra Connect を使用した ID の同期

- 0203-Intuneへのデバイス登録の管理

  > 注: Entra ID への Windows Hello サインイン認証をセキュリティで保護するために使用されるテキスト メッセージを受信できる携帯電話も必要です。

### シナリオ



Aaron Nicholls に適切なライセンスを割り当て、Windows デバイスを Entra ID に参加させ、Microsoft Intune に自動的に登録するプロセスをテストします。

### タスク 1: Windows デバイスを Microsoft Intune に自動的に登録する

※開始前にEntra管理センターで「**Aaron@yourtenant.onmicrosoft.com**」のパスワードをリセットしてください。

1. **SEA-WS1** に切り替え、**Pa55w.rd** のパスワードで**管理者**としてサインインします。
2. タスク バーで、[**Start （Windowsアイコン）]** を選択し、[**Settings]** を選択します。
3. [**Settings**] ウィンドウで、[**Accounts]** を選択します。
4. [Accounts] ページで、[**Access work or school**] を選択します。
5. [**Access work or school**] ページで、[**Connect]** を選択します。
6. [**Microsoft account] ウィンドウで、**[**Join this device to Entra ID]** を選択します。
7. [**Sign in**] ページで、「**Aaron@yourtenant.onmicrosoft.com**」と入力し、[**次へ**] を選択します。
8. [**Enter password**] ページでパスワードを入力し、[**Sign in]** を選択します。
9. これが**Make sure this is your organization** ダイアログ ボックスで、**Join** を選択します。
10. [**You're all set!**] ページで、[**Done]** を選択します。
11. [**Access work or school**] ページで、 **[Connected to Contoso's Azure AD]** が表示されていることを確認します。
12. [**Connected to Contoso's Azure AD]** を選択し、 [**Info**] を選択します。
13. Contoso が管理する領域に関する情報をメモし、下にスクロールして **[Sync]** を選択します。これにより、デバイスが Intune と強制的に同期されます。
14. **[Settings **]ウィンドウを閉じます。

### タスク 2: Entra ID と Intune へのデバイス登録を検証する

1. **SEA-WS1** タスクバーで、[**Start （Windowsアイコン）]** を選択し、「**cert**」と入力して、[**Manage computer certificates]** を選択します。**[ User Account Control**] で、[**Yes**] を選択します。

2. **Certificates **コンソールのナビゲーションペインで、**Personal** を展開し、**Certificates** ノードを選択します。次の証明書が詳細ウィンドウに一覧表示されていることを確認します。

   - Microsoft Intune MDM Device CA

   - MS-Organization-Access

   - MS-Organization-P2P-Access [2025]

     これは、デバイスが Entra と Intune に登録されていることを示します。

3. [Certificates] ウィンドウを閉じます。

4. SEA-WS1 で、[**スタート（Windowsアイコン）]** を右クリックし、[**Windows Terminal (Admin)]** を選択します。[User Account Control] で、[**Yes**] を選択します。

5. PowerShell コンソールで、次のように入力し、**Enter** キーを押します。

   ```
   dsregcmd /status
   ```

6. **[Device State]** の下の出力で、 **[AzureAdJoined: YES]** が表示されていることを確認します。これは、デバイスが Azure AD に参加していることを示します。

7. [**Temnant Details]** の出力で、次の 3 つのエントリが存在することを確認します。

   ```
   mdmUrl : https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc
   mdmTouUrl : https://portal.manage.microsoft.com/TermsofUse.aspx
   mdmComplianceUrl : https://portal.manage.microsoft.com/?portalAction=Compliance
   ```

   > 注: これらのエントリは、デバイスが Intune に登録されていることを示します



### Task 3: Sign in as an Entra user

1. **SEA-WS1**からサインアウトします。
2.  **Other user** を選択し、パスワード **Pa55w.rd** を使用して **`Aaron@yourtenant.onmicrosoft.com`** としてサインインします。プロファイルが作成されるまで待ちます。
3. At the **Use Windows Hello with your account** page, select **OK**.
4. On the **Let's keep your account secure** page, select **Next**.
5. On the **Keep your account secure** page, select **I want to set up a different method**.
6. In the **Choose a different method** dialog box, select **Phone** and then select **Confirm**.
7. On the **Phone** page, in the **Enter phone number** field, enter your mobile phone number which is able to receive text messages. Select **Next**.
8. When you receive the verification code, enter the code on the Phone page and then select **Next**.
9. On the verification page, select **Next** and then select **Done**.
10. On the **Set up a PIN** page, in the **New PIN** and **Confirm PIN** boxes, type **102938** and then select **OK**.
11. On the **All set!** page, select **OK**.
12. Sign out of **SEA-WS1**.

### タスク 4: Intune コンソールでのデバイス登録の確認



1. パスワード **Pa55w.rd** を使用して、**Contoso\Administrator** として **SEA-SVR1** に切り替えます。

2. Microsoft Edge で、アドレス バーに「**[https://intune.microsoft.com](https://intune.microsoft.com/)**」と入力し、**Enter キー**を押します。テナント管理者アカウントでサインインします。

3. ナビゲーション ウィンドウで、 **[デバイス]** を選択します。

4. **デバイス上 |** **[プラットフォーム別のデバイスの管理]** の概要ブレードで、**Windows** の横に **1** が表示されていることを確認します。表示に時間がかかる場合があります。

5. **デバイス上 |[概要**] ブレードで [**すべてのデバイス**] を選択し、**SEA-WS1** が一覧表示されていることを確認します。

6. SEA-WS1 の場合、[**管理元]** 列には **Intune** と表示され、[**所有権]** 列には **[企業]** と表示されます。

   *注: このビューには、Intune に登録されているデバイスが一覧表示されます。Entra と Intune の間で自動登録を構成したため、Entra に参加または登録されているすべてのデバイスが自動的に Intune に登録されることに注意してください。登録を設定する前に参加したデバイスは、Entra に参加または登録されるだけで、Intune には登録されません。*

7. **Microsoft Edge** で新しいタブを開き、アドレス バーに**[「https://entra.microsoft.com](https://entra.microsoft.com/)**」と入力して、**Enter キー**を押します。

8. Microsoft Entra 管理センターで、 **[Entra ID]** を展開します。

9. **[デバイス]** を選択し、[**すべてのデバイス**] を選択します。

   > SEA-WS1に注意してください。[結合の種類] 列には **[Microsoft Entra 参加済み**] と表示され、[MDM] 列には **Microsoft Intune** が表示されます。

10. 開いているすべてのWindowsを閉じます。

**結果**: この演習を完了すると、Windows クライアントを Entra ID に正常に参加させ、デバイスが Microsoft Intune に自動的に登録されたことを確認できます。

**ラボの終わり**
