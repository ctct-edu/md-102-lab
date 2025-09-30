# ラボ 0701: Microsoft Deployment Toolkit を使用した Windows 11 の展開



## 概要



このラボでは、Microsoft Deployment Toolkit を使用して、Windows 11 オペレーティング システム イメージを作成および展開します。

### シナリオ



SEA-WS4 という名前の新しい Windows 11 仮想マシンを展開する必要があります。Microsoft Deployment Toolkit を使用して、Hyper-V で作成された仮想マシンにオペレーティング システムを展開することにしました。MDT で新しい展開共有を構成し、SEA-WS4 を展開する手順を実行するタスク シーケンスを構成します。

### タスク1: 新しいデプロイメント共有の作成



1. **SEA-SVR2** で、パスワード **Pa55w.rd** を使用して **Contoso\Administrator** としてサインインします。

2. タスク バーで **[File Exploler]** を選択し、**E:\Labfiles\ISOs** を参照します。

3. **Win11_21H2_Eval.iso**を右クリックし、[**mount]** を選択します。ISO は DVD ドライブ F としてマウントされます。

4. **File Explolerを**閉じます。

5. **[スタート]** を選択し、[**Microsoft Deployment Toolkit]** を展開して、[**Deployment Workbench**] を選択します。

6. **Deployment Workbench**で、[**Deployment Shares**]を右クリックし、[**New Deployment Share**]を選択します。

   > **[新しい展開共有ウィザード**] が開きます。

7. [**Path]** ページの **[Deployment share path]** で、値を **[E:\DeploymentShare**] に変更し、[**次へ**] を選択します。

8. [**Share]** ページで、**Share name**を確認しますが、変更しないでください。[**Next**] を選択します。

9. [**Descriptive Name**] ページで、既定値を受け入れて [**Next**] を選択します。

10. [**Options ]** ページで、以下のように構成し、[**Next**] を選択します。

    - Ask to set the local Administrator password: **Enabled**
    - その他のすべてのチェックボックス: **Disabled**

11. [**Summary]** ページで、情報を確認し、[**Next**] を選択します。

12. **Confirmation** ページで、プロセスが正常に完了したことを確認し、**Finish** を選択します。

13. [**Deployment Shares**] で、[**MDT Deployment Share**] フォルダーを展開します。

    > デプロイ共有用に構成できるさまざまなノードを確認します。

### タスク2: オペレーティング・システム・ファイルをデプロイメント共有に追加する

1. Deployment Workbench で、[**Deployment Shares**]、[**MDT Deployment Share**] の順に展開し、[**Operating Systems]** を選択します。

2. **[Operating Systems]** を右クリックし、[**Import Operating System]** を選択します。オペレーティングシステムのインポートウィザードが開きます。

3. **Import Operating System Wizard**の [**OS Type**] ページで、[**Full set of source files**] を選択し、[**Next**] を選択します。

4. [**Source**] ページの **[Source Directory] に「 F:\  」と入力**し、[**Next**] を選択します。

5. [**Destination ]** ページで、既定の宛先ディレクトリ名を **Windows 11 Enterprise x64** に変更し、[**Next**] を選択します。

6. [**Summary ]** ページで、情報を確認し、[**Next**] を選択します。

   > オペレーティング システムのソース ファイルが展開共有にコピーされます。

7. Confirmation  ページで、プロセスが正常に完了したことを確認し、**Finish** を選択します。

8. **Deployment Workbench**で、「**Operating Systems」**を選択した状態で、オペレーティングシステムが表示されることを確認します。

### タスク3: デプロイメント共有へのアプリケーションの追加

1. Deployment Workbench で、[**Deployment Shares**]、[**MDT Deployment Share**] の順に展開し、[**Applications]** を選択します。
2. **[Applications]** を右クリックし、[**New Application]** を選択します。[新規アプリケーションウィザード] が開きます。
3. **New Application Wizard**の [**Application Type**] ページで、[**Application with source files**] を選択し、[**Next**] を選択します。
4. [**Details ]** ページで、以下を構成し、[**Next**] を選択します。
   - パブリッシャー: **Microsoft**
   - アプリケーション名: **XML Notepad**
5. [**Source **] ページの [**Source directory**] に「**E:\Labfiles\Apps**」と入力し、[**Next**] を選択します。
6. [**Destination]** ページで、既定の宛先ディレクトリ名を受け入れ、[**Next**] を選択します。
7. [**Command Details]** ページの **[Command line]** に「**XmlNotepadSetup.msi /q」**　を入力し、[**Next**] を選択します。
8. [**Summary ]** ページで、情報を確認し、[**Next**] を選択します。
9. Confirmation  ページで、プロセスが正常に完了したことを確認し、**Finish** を選択します。

### タスク 4: MDT タスク シーケンスの作成

1. Deployment Workbench で、[**Deployment Shares**]、[**MDT Deployment Share**] の順に展開し、[**Task Sequences]** を選択します。

2. [**Task Sequences]** を右クリックし、[**New Task Sequence**] を選択します。**New Task Sequence Wizard**が開きます。

3. [**General Settings**] ページで、以下を構成し、[**Next**] を選択します。

   - タスク シーケンス ID: **001**
   - タスク シーケンス名: **Deploy Windows 11 Enterprise**

4. [**Select Template]** ページで、[**Standard Client Task Sequence**] を選択し、[**Next**] を選択します。

5. [**Select OS**] ページで、[**Windows 10 Enterprise Evaluation in Windows 11 Enterprise x64 install.wim]** を選択し、[**Next**] を選択します。

6. **[Specify Product Key]** ページで、[**Do not specify a product key at this time]** を選択し、[**Next**] を選択します。

7. [**OS Settings**] ページで、以下を構成し、[**Next**] を選択します。

   - Full Name: **User**
   - Organization: **Contoso Corporation**
   - Internet Explorer Home Page: **about:blank**

8. [**Admin Password**] ページで、[**Use the specified local Administrator password**] を選択し、両方のテキスト ボックスに「 **Pa55w.rd** 」と入力します。[**Next**] を選択します。

9. [**Summary ]** ページで、情報を確認し、[**Next**] を選択します。

10. Confirmation  ページで、プロセスが正常に完了したことを確認し、**Finish** を選択します。

11. 展開**Deployment Workbench**で、[**Task Sequences]** を選択した状態で、[**Deploy Windows 11 Enterprise**] タスク シーケンスが表示されていることを確認します。

12. [**Deploy Windows 11 Enterprise]** タスク シーケンスを右クリックし、[**Properties]** を選択します。

13. [**Task Sequence**] タブを選択します。

14. [**Validation]** ノードを展開し、[**Validate]** を選択します。

15. [**Properties ]** ページで、[**Ensure minimum memory]** と **[Ensure minimum processor speed]** の横にあるチェック マークを外します。

    > その他の変更は行わないでください。

16. [**Deploy Windows 11 Enterprise Properties]** ウィンドウで、[**OK]** を選択します。

### タスク 5: 展開共有のプロパティと Windows PE 設定の構成

1. デプロイメント・ワークベンチで、「**Deployment Shares** 」を展開し、「**MDT Deployment Share**」を選択します。

2. [**MDT Deployment Share**] を右クリックし、[**Properties]** を選択します。

3. **[MDT Deployment Share Properties]** ウィンドウの [**General**] タブで、展開共有の作成時に提供された情報を確認します。

4. [**Rules ]** タブを選択します。

   > [ルール] タブには、CustomSettings.ini ファイルの内容が表示されます。これらの値は、デプロイ共有の作成時にも提供されました。

5. [**Windows PE**] タブを選択します。

   > [Windows PE] タブには、Windows PE ブート ディスクを作成するためのオプションが用意されています。

6. [**Windows PE**] タブの **[Platform]** の横にあるドロップダウンリストで [**x64**] を選択します。

7. [**Windows PE Customizations]** セクションの **[Scratch space size**] の横にある [**64**] を選択します。

8. [**Features**] タブを選択し、次の機能パックの横にあるチェック ボックスをオンにします。

   - DISM Cmdlets

   - Microsoft Data Access Compenents (MDAC/ADO) support
   - Windows PowerShell

9. [**Monitoring]** タブを選択します。

10. [**Monitoring]** タブで、[**Enable monitoring for this deployment share]** の横にあるチェック ボックスをオンにします。

11. [**MDT Deployment Share Properties]** ウィンドウで、[**OK]** を選択します。

12. [**MDT Deployment Share**] を右クリックし、[**Update Deployment Share**] を選択します。展開共有の更新ウィザードが開きます。

13. [**Options]** ページで、[**Optimize the boot image updating process**] を選択し、[**Next**] を選択します。

14. **Summary** ページで、**Next** を選択します。

    > 展開共有は、Windows PE ファイルの更新と作成を開始します。完了するまでに数分かかります。

15. Confirmation  ページで、プロセスが正常に完了したことを確認し、**Finish** を選択します。

### タスク 6: MDT を使用した Windows 11 の展開

1. SEA-SVR2 のタスク バーで、[**Hyper-V Manager**] を選択します。

2. Hyper-V マネージャーで、[**Virtual Switch Manager]** を選択します。

3. [**New virtual network switch**] を選択し、詳細ウィンドウで **[External]** を選択します。[**Create Virtual Switch]** を選択します。

4. [**Virtual Switch Properties** ] ページの [**Name**] に「 **External network** 」と入力し、[**OK]** を選択して、[**Yes**] を選択します。

5. Hyper-V マネージャーで **[SEA-SVR2**] を選択し、[アクション] ウィンドウで [**New**] を選択し、[**Virtual Machine]** を選択します。

6. [**Before you Begin**] ページで、[**Next**] を選択します。

7. [**Specify Name and Location**] ページの [**Name**] ボックスに「 **SEA-WS4** 」と入力します。

8. [**Store the virtual machine in a different location]** の横にあるチェック ボックスをオンにし、[**Location]** の横に「**E:\Labfiles\VirtualMachines**」と入力します。[**Next**] を選択します。

9. [**Specify Generation**] ページで、[**Generation 2]** を選択し、[**Next**] を選択します。

10. [**Assign Memory]** ページの **[Startup memory]** の横に「**8192**」と入力し、[**Next**] を選択します。

11. [**Configure Networking]** ページの **[Connection]** の横にある **[External Network]** を選択し、 [**次へ**] を選択します。

12. [**仮想ハード ディスクの接続**] ページで、[**仮想ハード ディスクの作成**] を選択し、次のように入力して [**次へ**] をクリックします。

    - 名前: **SEA-WS4.vhdx**
    - 場所: **E:\Labfiles\VirtualMachines**
    - サイズ: **60 GB**

13. [**Installation Options]** ページで、[**Install an operating system from a bootable image file]** を選択し、以下を設定します。

    - Image file (.iso): **E:\DeploymentShare\Boot\LiteTouchPE_x64.iso**

14. [**Next**] を選択し、[**Finish]** を選択します。

15. Hyper-V マネージャーで、[**SEA-WS4**] を右クリックし、[**Settings]** を選択します。

16. [**Security]** を選択し、[**Enable Trusted Platform Module]** の横にあるチェック ボックスをオンにします。

17. **[Processor]** を選択し、仮想プロセッサの数を **2** に変更します。

18. [**OK**] を選択して [設定] ダイアログ ボックスを閉じます。

19. Hyper-V マネージャーで、[**SEA-WS4**]、[**Connect]**、[**Start]** の順に選択します。

20. コンピュータが起動したら、キーボードの任意のキーを押して、MDT 展開ウィザードを呼び出します。必要に応じてウィンドウを最大化します。

21. [**Welcome**] ページで、[**Run the Deployment Wizard to install a new Operating System] を選択します**。

22. [**Specify credentials for connecting to network shares**] ウィンドウで、次のように入力し、[**OK]** を選択します。

    - ユーザー名: **Administrator**
    - パスワード:**Pa55w.rd**
    - ドメイン: **Contoso**

23. [**Task Sequence]** ページで、[**Deploy Windows 11 Enterprise]** を選択し、[**Next**] を選択します。

24. [**Computer Details**] ページの **[Computer name**] の横に「**SEA-WS4**」と入力し、[**Next**] を選択します。

25. **[Move Data and Settings]** ページで、[**Next**] を選択します。

26. [**User Data (Restore)]** ページで、[**Next**] を選択します。

27. [**Locale and Time]** ページで、[**Next**] を選択します。

28. [**Applications]** ページで、[**Next**] を選択します。

29. [**Administrator Password]** ページで、両方のテキスト ボックスに「**Pa55w.rd**」と入力し、[**Next**] を選択します。

30. **Ready ** ページで、**Begin** を選択します。

    > インストールが開始されます。完了するまでに 15 分から 20 分かかり、必要に応じてインストール中に SEA-WS4 が再起動されます。

31. **Deployment Workbench**に切り替えます。

32. Deployment Workbench で、[**Deployment Shares**] を展開し、[**MDT Deployment Share**] を展開します。

33. **[Monitoring]** を選択し、詳細ペインで **[SEA-WS4**] をダブルクリックします。

    > デプロイ中に監視ステータスを確認します。

34. **SEA-WS4** に切り替えます。

35. インストールが完了すると、デスクトップが開き、展開が完了します。デプロイの概要で、 **[Finish]** を選択します。

36. **SEA-WS4** をシャットダウンし、[仮想マシン接続] ウィンドウを閉じます。

37. Hyper-V マネージャーで、[**SEA-WS4**] を右クリックし、[**Settings]** を選択します。

38. **[SEA-WS4 の設定**] で、[**SCSI Controller]** を展開し、[**DVD Drive**] を選択します。

39. 詳細ウィンドウの **[Media**] で [**None**] を選択し、[**OK]** を選択します。

40. **[SEA-WS4**]を右クリックし、[ **Checkpoint** ]を選択して、SEA-WS4の現在の状態のチェックポイントを作成します。

41. SEA-SVR2 では、**Hyper-V Manager** を閉じ、**Deployment Workbench** を閉じます。

42. **File Explorer** を開き、**DVD Drive F** を右クリックして、[**Eject**]を選択します。

43. **File Explorer** を閉じて、**SEA-SVR2** からサインアウトします。

**結果**: この演習を完了すると、Microsoft Deployment Toolkit を使用して Windows 11 ワークステーションを作成および展開できます。

**ラボの終わり**
