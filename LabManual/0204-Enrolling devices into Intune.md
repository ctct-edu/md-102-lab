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



1. **Pa55w.rd** のパスワードを使用して **SEA-WS1** に**管理者**としてサインインします。
2. [**スタート]** を選択し、[**設定]** を選択します。
3. **[設定]** で **[アカウント]** を選択します。
4. [アカウント] ページで、[**職場または学校へのアクセス**] を選択します。
5. [**職場または学校へのアクセス**] ページで、[**接続]** を選択します。
6. [**Microsoft アカウント**] ウィンドウで、[**このデバイスを Microsoft Entra ID に参加させる]** を選択します。
7. サインイン **ページで、「****`Aaron@yourtenant.onmicrosoft.com`**」と入力し、**次へ** を選択します。
8. [**パスワードの入力**] ページで、「**Pa55w.rd**」と入力し、[**サインイン]** を選択します。
9. これが**組織であることを確認する** ダイアログ ボックスで、**参加** を選択します。
10. [**準備完了です!]** ページで、情報を読み、[**完了]** を選択します。
11. [**職場または学校へのアクセス**] セクションで、 **[Contoso の Azure AD に接続済み]** が表示されていることを確認します。
12. [**Contoso の Azure AD に接続]** を選択し、 [**情報**] を選択します。
13. Contoso が管理する領域に関する情報をメモし、下にスクロールして **[同期]** を選択します。これにより、デバイスが Intune と強制的に同期されます。
14. **[設定**]ウィンドウを閉じます。

### タスク 2: Entra ID と Intune へのデバイス登録を検証する



1. **SEA-WS1** タスクバーで、[**スタート]** を選択し、「**cert**」と入力して、[**コンピューター証明書の管理]** を選択します。**[ユーザー アカウント制御**] で、[**はい**] を選択します。
2. **証明書**コンソールのナビゲーションペインで、[**個人用**] を展開し、[**証明書]** ノードを選択します。次の証明書が詳細ウィンドウに一覧表示されていることを確認します。

- Microsoft Intune MDM デバイス CA

- MS 組織アクセス

- MS-組織-P2P-アクセス [2025]

  これは、デバイスが Entra と Intune に登録されていることを示します。

1. [証明書] ウィンドウを閉じます。

2. **[スタート]** を右クリックし、[**Windows ターミナル (管理者)]** を選択します。プロンプトが表示されたら、[**はい**] を選択します。

3. PowerShell コンソールで、次のように入力し、**Enter** キーを押します。

   ```
   dsregcmd /status
   ```

   

4. In the output under **Device State**, verify that **AzureAdJoined : YES** is displayed. This indicates that the device is Azure AD joined.

5. In the output under **Tenant Details**, verify that the following three entries exist:

   ```
   mdmUrl : https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc
   mdmTouUrl : https://portal.manage.microsoft.com/TermsofUse.aspx
   mdmComplianceUrl : https://portal.manage.microsoft.com/?portalAction=Compliance
   ```

   

   > Note: These entries indicate that the device is enrolled in Intune.

### Task 3: Sign in as an Entra user



1. Sign out of **SEA-WS1**.
2. Select **Other user**, and sign in as **`Aaron@yourtenant.onmicrosoft.com`** with the password **Pa55w.rd**. Wait for the profile to be created.
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
