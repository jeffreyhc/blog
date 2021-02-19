---
layout: post
title: Github Pages + Jekyll 搭建個人部落格
categories:
  - note
tags:
  - GitHub Pages
  - Jekyll
  - Hydeout
---

```
這個主題感覺挺合適作為此部落格的第一篇文章，順便把架設過程需要注意的眉眉角角紀錄一下，
由於本文偏向紀錄下自己比較不熟悉的部分，申請GitHub帳號或是安裝Git環境之類的部分就直接跳過~
```
<!--more-->
### GitHub Pages是什麼? 什麼時候會用到它?
GitHub Pages是GitHub提供的靜態網頁託管服務，靜態網頁基本上指的就是不包含資料庫的網頁，
也就是說，如果你的網頁不需要具有使用者登入功能，只包含html, css, javascript就可以使用這個服務發布。

至於什麼時候會用到這個服務，例如在寫了一個專案後，我們可能會想要為這個專案做一個官方網站，
又或是想要寫部落格，但覺得目前常見的pixnet, udn都不符合自己的需求，
想要自己架網站但又不想大費周章租用伺服器，這時候就是使用這個服務的好時機。

### 使用GitHub Pages架的網站的網址是什麼?
首先，GitHub Pages分為 **user/organization site** 以及 **project site** 兩種，
這兩者的差別是建立repository的時候設定的名字，舉個例子，我的帳號是jeffreyhc，
如果將repository的名字設定為`jeffreyhc.github.io`，那麼之後部落格的網址就會是`https://jeffreyhc.github.io/`；
但如果是設定一個名字，例如本站就是創了一個名為`blog`的repository，部落格的網址就會是`https://jeffreyhc.github.io/blog/`。

還想知道更詳細可以參考官方文件: [Types of GitHub Pages sites](https://docs.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites)。

### 選擇GitHub Pages發布的來源
創好repository後就要決定我們的網頁要基於哪個branch做發布，由於這個部落格是另外創的一個repository，這邊我的source就直接選master branch。
![github_pages_setting]({{ site.baseurl }}/assets/images/github_pages_setting.png)
除了可以選來源的branch，還可以選要基於根目錄或是doc資料夾，如果是一個已經存在一段時間的專案，也可以將網頁資料放在`/doc`中，就可以在設定頁面中選擇基於`/doc`的資料夾發布。

還想知道更詳細可以參考官方文件: [Publishing sources for GitHub Pages sites](https://docs.github.com/en/github/working-with-github-pages/about-github-pages#publishing-sources-for-github-pages-sites)

### 在開始寫部落格之前
#### 如果我不會寫網頁怎麼辦?
這時候Static Site Generator(SSG)就可以幫上我們的忙，我們只要專注在寫出文章的部分，接著透過SSG就會產生寫好的網頁。這樣的形式剛好很適合拿來寫部落格，每次要寫新文章只要增加一個新的檔案，寫完後push到GitHub上，文章就會自動發布出來。

當然，會寫網頁的人還可以修改自己的模板以增加新功能或是讓產生出來的網頁更符合自己的需求。

至於要選哪個SSG呢?考慮過後我決定採用GitHub官方文件中建議使用的[Jekyll](https://jekyllrb.com/)。
#### 安裝Jekyll
參考官方網站的[安裝教學](https://jekyllrb.com/docs/installation/)，我雖然是用windows，但由於我有裝Linux子系統，因此是參考[Installation via Bash on Windows 10](https://jekyllrb.com/docs/installation/windows/#installation-via-bash-on-windows-10)安裝的，
記得安裝完Ruby先照著這篇[Running Jekyll as Non-Superuser (no sudo!)](https://jekyllrb.com/docs/troubleshooting/#no-sudo)設定完，接下來安裝Jekyll時才不用切到root。

安裝完Jekyll如果能看到自己用的版本就是安裝成功啦!
![jekyll_version]({{ site.baseurl }}/assets/images/jekyll_version.png)

#### 選擇模板
安裝完Jekyll接著就是要選一個自己看得順眼的模板啦，本站使用的是基於[Hyde](https://github.com/poole/hyde)進一步修改的[Hydeout](https://github.com/fongandrew/hydeout)，
`Hydeout`除了更新`Hyde`以支援Jekyll 3.x/4.x以外，還額外新增了一些功能，例如已經支援文章的`tag`跟`category`，並且可以非常容易的與`disqus`做整合。除此之外，這個模板還已經附上了很多篇作為範例的文章，展示了各種用法，除了markdown語法外，還包含內嵌youtube影片的寫法，對於這領域的新手來說我覺得挺友善的。

我這邊使用的方式是先從`Hydeout`的GitHub直接clone一份code下來，這時候可以馬上先試一下用Jekyll產生網頁看起來會長怎樣。

#### 試試看用Jekyll來產生網頁
由於我的Jekyll是裝在Linux子系統中，我都是在bash中打指令啟動Jekyll，接著再把瀏覽器打開看產生的結果
輸入以下指令，應該會看到Jekyll產生網頁的log(後面的`--watch`可以在我們編輯文章的時候，只要文章一存檔，重新刷新頁面就可以看到更新後的結果而不用重新生成網頁)
```
bundle exec jekyll serve --watch
```
![jekyll_serve]({{ site.baseurl }}/assets/images/jekyll_serve.png)
從圖上可以看到，server address是`http://127.0.0.1:4000/hydeout/`，

其實Jekyll預設的server address是`http://127.0.0.1:4000/`，

但因為hydeout的`_config.yml`這個檔案中有一個`baseurl`的設定值被寫為`/hydeout`，所以網頁會放在`http://127.0.0.1:4000/hydeout/`

關於config中有哪些選項可以設定，以及選項的功用請參閱[官方文件](https://jekyllrb.com/docs/configuration/options/)

註: 使用Jekyll產生網頁時，我曾經有一次遇過跳出錯誤訊息，印象中是說我某個套件沒裝，但我記得是有裝的，後來用以下的指令就可以用了，如果也有遇到問題可以先試試看，還是不行的話就需要仔細看一下error message了。
```
bundle update
bundle install
bundle exec jekyll serve --watch
```
成功產生網頁後，就可以用瀏覽器打開上面給的server address看看產生後的結果:
![hydeout]({{ site.baseurl }}/assets/images/hydeout.png)
如果有看到這樣的畫面就代表Jekyll跑起來沒什麼問題，就可以準備開始寫自己的部落格囉!

### 開始寫部落格

#### 複製模板
先把前面創好要用來發布的GitHub Pages repository(後稱`blog repository`)也clone下來(由於沒有做過任何修改，這時候只會載到一個空的repository)，

接著把之前載下來的`Hydeout`中的內容除了`_site`資料夾以外全部copy到`blog repository`中。提醒一下，這個步驟，如果有在檔案總管開啟「顯示隱藏項目」的話，記得`.git`資料夾 **不能** copy到`blog repository`。

同時順便修改了一下`.gitignore`這個檔案，額外多忽略了`_site`及`.jekyll-cache`兩個資料夾。

我自己在這時候就先commit一版了，用意是在開始修改`hydeout`前，先留個最原始的版本。

#### 修改Configuration
基於原本的`_config.yml`檔案做了一些修改，在[git log](https://github.com/jeffreyhc/blog/commits/master)其實都可以看到，只列出比較重要的:
- 修改baseurl = `/blog`
- 設定excerpt_separator = `<!--more-->`，將這個關鍵字插在文章中，就可以達到讓讀者按下More才能看到全文的效果，如下圖:
![more_content]({{ site.baseurl }}/assets/images/more_content.png)
- 開啟disqus留言服務
- 設定個人github網址的位址
- 開啟對於[Font Awesome](https://fontawesome.com/)的支援，這個網站有很多小圖示，未來可能會需要用到

#### 新增一篇文章
既然要寫部落格，最重要的當然是要知道怎麼新增文章，這部分有以下幾點需要注意:
1. 文章檔案要放在`_post`資料夾底下
2. 文章檔案的檔名格式為`YEAR-MONTH-DAY-title.md`
3. 每篇文章開頭必須包含[Front Matter](https://jekyllrb.com/docs/front-matter/)，這樣才能夠被Jekyll處理。
4. 文章支援Markdown語法

#### 注意事項
在架設環境時有遇到三個需要注意的問題點:

1. _config.yml中baseurl的值 **必須** 根據GitHub Pages的網址設定，例如我的網址是`https://jeffreyhc.github.io/blog/`，所以baseurl需要被設為`/blog`，不然Jekyll在生成網頁時會有錯誤。<br/>
有設定baseurl:
![set_baseurl]({{ site.baseurl }}/assets/images/set_baseurl.png)
沒設定baseurl:
![not_set_baseurl]({{ site.baseurl }}/assets/images/not_set_baseurl.png)

2. _config.yml中不能有以github為名的變數，不然就會跳出GitHub Pages failed to build your site，如下圖:
![build_fail_by_github_var]({{ site.baseurl }}/assets/images/build_fail_by_github_var.png)

3. 用Jekyll寫文章時如果文章日期設定在未來，那麼使用Jekyll產生出來的網站除非有使用`--future`的參數，不然將看不到該篇文章，
在寫這篇文章時就是因為把文章日期訂在未來，導致Jekyll產生網站後找不到這篇文章，丟到GitHub後又找到了，才發現好像是因為GitHub有使用`--future`參數

### 結語
其實對於Jekyll或是網站設計的部分我自己覺得還是挺陌生的，所以這篇文章很多地方我自己覺得寫的還不夠清楚。

而且有蠻多東西我還在摸索的，研究怎麼樣刪掉不想要的東西或是加入想要的東西，感覺還有蠻多東西可以慢慢玩的。

如果大家看到這篇文章有什麼想討論或是指教的就留言在下面吧XD。