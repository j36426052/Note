# Git 記錄文件

## Git 安裝篇

記得修一下config

## Git 初學篇

最基本的 add, commit要會

**三個區域(名詞)**

<image src="figure/gitSpace.png" alt="git" width="500">

## Git 遠端連線

先用以下指令建立一個remote

~~~git
git remote add [origin] [url]
~~~

origin的意思是這個remote的name的感覺，而origin這個單字是約定成俗，沒有啥意思。

下一個指令是push

~~~git
git push [origin] [branchLocal]:[branchRemote]
~~~

就是把[branchLocal]推到[origin]這個節點上的[branchRemote]


## Git 合併分支

詳細可以參考:[合併發生衝突了，怎麼辦](https://gitbook.tw/chapters/branch/fix-conflict)

**超級和平篇**
有master, cat兩個branch，如果想要把cat合併進去，先切換到master(checkout master)，接著打

~~~Git
git merge cat
~~~
master就會把cat裡面的commit合併到自己裡面，然後cat還是擺在那裡。

**一點點修改篇**
假如有一個檔案 tem.txt, master和cat 兩個branch都修改了，執行完merge指令後會顯示合併失敗，並且在暫存區會多出衝突的檔案，檔案內會變成以下的樣子

~~~Git
other same code

<<<<<<<<<<< Head
  master side
===========
  cat side
»>>>>>>>>>> cat

other same code
~~~

將最後要留下的版本留著，修修改改之後，輸入指令
~~~
git add tem.txt
~~~
把暫存區的檔案準備commit出去，沒其他意外就commit。

## Git 指令表

**config**

|Git|do|
|-|-|
|git config --list|察看設定|
|git config --local/global user.name [userName] |設定帳號|
|git config --local/global user.email [email] |設定email|
**init/clone**
|Git|do|
|-|-|
|git clone [url]|從url那邊拷貝專案下來|
|git init|這個資料夾開始git|
|rm -rf .git|移除git|
**remote**
|Git|do|
|-|-|
|git remote add [origin] [git@~.git]|遠端連接|
|git remote set-url [origin] [git@~.git]|修改遠端連結|
|git remote remove [origin]|移除遠端連結|
|git remote -v|查詢遠端連結(url)|
|git push -u [origin] [masterLocal]:[masterRemote]|推上遠端並綁定(gitHub 常這樣)|
**git本人**
|Git|do|
|-|-|
|git status|常看git 狀態|
|git add .|把所有要變更的東西都加進去|
|git add [file]|把想要家的檔案加進去|
|git commit -m [message]|commit 加上訊息|
|git pull|把東西從遠端拉下來|
|git push [remote] [branch]|把東西推到遠端|
|git push -u [remote] [branch]|把東西推下來還有綁定|
|git restore --staged [file]|取消git add|
|git pull --rebase [remote] [branch]||

**查詢**
|Git|do|
|-|-|
|git config --list|查詢設定|
|which git|查詢git安裝位置|
|git --version|查詢git 版本|
|git status|查詢git add狀態|
|git log|查詢commit的log|
|git log --oneline --all --graph|單行/樹狀顯示|
|git log -p [fileName]|查詢檔案Log|
|git blame [FileName]|查詢檔案的每行編輯資訊|
|git reflog|查詢reflog(保留HEAD移動的軌跡，可以查詢到commit ID(找隱藏的用))|
|git help|查詢指令|


**Reset(切到某版本)**
|Git|do|
|-|-|
|git reset [commit]|切回到某一個commit|
|git reset [commit] --mixed||
|git reset [commit] --soft||
|git reset [commit] --hard||
|git reset [commit]^|退和前一次的commit|
|git reset [commit]~5|退回前五次的commit|


**Branch應用**

|Git|do|
|-|-|
|git branch|查詢所有本地分支|
|git branch -a|查詢所有遠端分支|
|git branch [newBranch]|當前commit新建分支|
|git branch [newBranch] [commit]|在那個commit建立分支（像是貼貼紙）|
|git branch [newBranch] [commitID]|
|git checkout [branch]|切換到某分支|
|git checkout -b [newBranch]|建立新分支並切換過去|
|git branch -d [branch]|刪除某分支t
|git branch -D [branch]|強制刪除某分支|
|git branch -m [branch] [newName]|將branch改名字(要先切到非改名的分支)|




## 參考資料
1. [Git 常用指令](https://ithelp.ithome.com.tw/articles/10241407)基本上都有，以這個為版形，詳細用補充的。
2. [Git clone](https://ithelp.ithome.com.tw/articles/10211807)
3. [為你自己學 Git](https://gitbook.tw/)
