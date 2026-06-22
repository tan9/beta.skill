<!-- .slide: data-background-color="#0d1117" -->
# 培棠.skill

<p class="sub">把一個人，打包成一個檔案</p>

Note:
（這是倒數第二場，調性放輕鬆。）今天很實用 ── 我把我每天怎麼跟 AI 工作，打包成一個你們現在就能 clone 回去用的檔案。哲學的部分，留到最後一場。

---

你們可能看過「同事.skill」──

<p class="sub">把一個同事打包成 AI，好讓他被取代。</p>

Note:
前陣子有點聲量的一個專案，把同事的技能跟個性蒸餾成一個 skill。它整個裹在一層很喪的外皮裡 ── 大模型要害死所有工程師。

---

他們是**被**打包，怕被取代。

<p class="creed">我是自己動手打包，<br>而且老早就想這樣。</p>

Note:
因為「可被取代」從來不是工程師的末日，是工程師的修養。拿一個喪氣的玩具，我想把它講成一個釋懷的故事。

---

## 那要怎麼<br>把一個人打包進檔案？

<p class="sub">先打包「怎麼做」。</p>

Note:
先講能寫成規則的部分 ── 我怎麼想事情、怎麼做決定。

---

<!-- .slide: class="belief" data-background-color="#161b22" -->
## 先問底層，再談方案

<p class="creed">這東西的底層 primitive 是什麼？</p>

Note:
任何問題進來，我不急著找工具、抄設定。先回答一個問題：它的底層是什麼。

---

- 網頁應用 → 一個個 `request / response`
- PKI → 一條 `certificate chain`
- K8s pod → 一個帶 cgroup 的 `Linux process`，沒有魔法
- GitOps → 整座叢集是 git repo 的**純函數**

Note:
握住 primitive，上面那層隨時能重算、能查、能讓 AI 生 ── 因為你手上有一把尺，量得出它有沒有騙你。握不住 primitive 的東西，不要碰，更不要讓 AI 替你決定。

---

## stateless me

<p class="creed">我只記最底層，<br>其他都重算。</p>

Note:
我不是真的沒有狀態 ── 我只留不可再生的那一層，也就是事物的基礎；其他衍生知識全部丟掉，要用再重算。就像 stateless 服務：不存 session，但握著唯一的真實來源，任何 response 都能從「來源 + request」重算出來。

---

## 在限制裡用 AI

<p class="sub">Bedrock 上的 Claude、OA 網路綁死、政府／金融合規。</p>

Note:
這段是你們最缺、別人最少講的。為什麼選 Bedrock 上的 Claude Code 而不是直接打 API；OA 網路綁死下哪些能做、哪些不能；個人帳號拿來做低敏感工作算不算合規。工具半年就過時，但「在限制裡怎麼判斷」放得久。

---

## 一個真實的 agentic 工作流

<p class="sub">把「肉眼比對畫面」這種苦工，丟給機器。</p>

Note:
← 這張先留白：填你自己要 demo／講的真實工作流（例如：UI 升級用序列式 agent + Playwright 截圖自動比對，把人工逐畫面比對的瓶頸交給機器）。我沒在 repo 裡確認到具體版本與細節，所以不替你編 ── 你給我真實案例，我把這張補滿。

---

<p class="creed">AI 是拿來吵架的，<br>不是拿來拜的。</p>

Note:
我最常拿 AI 幹嘛？不是要它給答案，是要它戳破我 ── 用最便宜的方式，在上 production 之前先發現我哪裡錯了。

---

## 我不信它的地方

<p class="sub">它最會一本正經，餵你「看起來對、其實錯」的設定檔。</p>

Note:
在政府金融環境，把生成的東西原封不動信進去，就是事故。所以我只在握得住 primitive 的領域才放它生 ── 那時我才驗得了。它生出來的東西，責任是我的，不是它的。它是 stateless 的，它不負責。

---

<!-- .slide: data-background-color="#000000" -->
<p class="tag">DEMO</p>

<p class="cmd">/beta</p>

<p class="sub">現場跑一段 code review，用我的口氣、我的規範。</p>

Note:
〔現場操作〕打開 Claude Code，輸入 /beta，丟一段 code 進去做 review。讓它用「先問 primitive、宣告式優先、標準優先」的方式念給大家聽。重點不是按鈕，是它的判斷長得像我。（備援：若現場網路／環境出狀況，準備一段預錄的輸出截圖。）

---

而這個 skill，<br>每次結尾都會補一句 ──

<p class="creed">我可能錯了。自己去驗。</p>

<p class="sub">而且我關不掉它。</p>

Note:
這是我這將近 19 年學到、唯一打包得進去的信念。不是免責聲明，是規則。（這裡的「我可能錯了」是 lint 規則版 ── 最後一場那個，是人生姿態版，記得做出高度差。）

---

## 但有三樣，<br>我打包不進去。

<p class="sub">判斷該不該做 · 扛責任 · 為什麼還在乎。</p>

Note:
上面都是「能寫成規則的我」。有三樣寫不進這個檔案：判斷一件事值不值得做、出事誰扛、還有 ── 做了將近 19 年還沒冷掉的那個東西。

---

<!-- .slide: data-background-color="#0d1117" -->
<p class="creed">那三樣，<br>我留到最後一場，親口講。</p>

<p class="small">↳ 不可取代，是一種失敗 · tan9.github.io/standardized-life</p>

Note:
今天先給你們能帶走的「手」。下一場，講為什麼我願意把這一切交出去。── 上一堂我把腦袋開源了；下一堂，講為什麼我願意把它全部交出去。

---

<!-- .slide: data-background-color="#000000" -->
<p class="cmd">git clone … ~/.claude/skills/beta</p>

<p class="sub">拿去用。然後告訴我哪裡像、哪裡不像。</p>

Note:
（收尾，把檔案真的交出去。）repo 在 github.com/tan9/beta.skill，clone 進你的 skills 目錄就能用。不藏私，連我怎麼準備這場分享，都攤給你看。
