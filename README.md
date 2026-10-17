# Table of Contents

- [1. Git branching cheatsheet](#1-git-branching-cheatsheet)
  - [Useful commands](#useful-commands)
- [1. Merge Strategies](#1-merge-strategies)
  - [A.Fast-forward merge](#afast-forward-merge)
  - [B. Merge commit](#b-merge-commit)
  - [C. Squash merge](#c-squash-merge)
- [1. Timetravel](#1-timetravel)
  - [A. Push ပြီးသား commit ကို undo ပြန်လုပ်ချင်ရင်](#a-push-ပြီးသား-commit-ကို-undo-ပြန်လုပ်ချင်ရင်)
  - [B. Commit ကို ဖြုတ်ချင်ရင်](#b-commit-ကို-ဖြုတ်ချင်ရင်)
- [Cheatsheet for rebase and merge](#cheatsheet-for-rebase-and-merge)
  - [A. dev ကို main ထဲ merge မယ်](#a-dev-ကို-main-ထဲ-merge-မယ်)
  - [B. dev ကို main ပေါ် rebase မယ်](#b-dev-ကို-main-ပေါ်-rebase-မယ်)

---

# 1. Git branching cheatsheet

Git branching ဆိုတာ environment မတူတဲ့ code တွေဖြစ်စေ feature အသစ်ရေးရင်ဖြစ်စေ bug fix တာဖြစ်စေ စသဖြင့် ရှိပြီးသား branch တစ်ခုခုကနေ branch ခွဲလိုက်ခြင်းဖြစ်ပါတယ်

Github မှာတော့ default branch က main ဖြစ်ပါတယ်။

## Useful commands

| Command | |
|---|---|
| `git branch` | local branch များကြည့်ရန် |
| `git branch -a` | Local နဲ့ Remote branch များကြည့်ရန် |
| `git branch dev` | ရောက်နေတဲ့ branch ကနေ branch အသစ်တစ်ခု create လုပ်ရန် ( git status ရိုက်၍ ရောက်နေတဲ့ branch က်ို ကြည့်လို့ရပါတယ်) |
| `git switch dev` | ရှိပြီးသား branch ကို change ချင်တဲ့ အခါ သုံးရန် |
| `git switch -` | အရင်သွားခဲ့တဲ့ branch ကို ပြန်သွားရန် |
| `git branch -m sit` | လက်ရှိ branch ကို (modify) နာမည်ပြောင်းရန် |
| `git branch -d sit` | fully merge ပြီးသား branch ကို ဖျက်ရန် |
| `git branch -D sit` | merge မပြီးလည်း ဖျက်ရန် |
| `git push -u origin dev` | Remote repository က dev branch ကို code push ရန် |

---

# 1. Merge Strategies

## A.Fast-forward merge

ဥပမာ main က dev branch ခွဲထားတယ်

dev branchမှာ commit 2 ခုတ်ိုးပြီး main မှာ မ merge ရသေးတဲ့ အခြေအနေမှာ main branch ကို dev ရဲ့ နောက်ဆုံး commit အထိ mainရဲ့ HEAD ကိုရွှေ့ပေးပါတယ်

```bash
git switch main
git merge —-ff—only dev
```

- merge commit အသစ် create မလုပ်ပါ
- branch နှစ်ခုလုံးက history တွေကွဲနေရင် (diverging branches) ဖြစ်နေရင် command က fail ပါလိမ့်မယ်

## B. Merge commit

```bash
git switch main
git merge dev
```

- dev branch မှာရှိနေတဲ့ commit history ကို main branch ဆီသယ်သွားပါတယ်
- Brach 2 ခုပေါင်းတဲ့အခါ merge commit တစ်ခု auto create လုပ်ပါတယ်
- Branch 2 ခု ဘယ်အချိန်မှာ ပေါင်းခဲ့လဲဆိုတာ commit history မှာတွေ့နိုင်ပါတယ်
- history တွေကွဲနေလို့ fast forward နဲ့ merge မရရင် merge ကိုသုံးလို့ရပါတယ်

## C. Squash merge


```bash
git switch main
git merge —-squash dev
git commit -m "Merge dev to main"
```

- dev မှာရှိတဲ့ changes အားလုံးကို commit တစ်ခုအနေနဲ့ပေါင်းလိုက်ခြင်းဖြစ်ပါတယ်
- dev branch မှာလည်း ဘာ changes မှ မရှိသွားပါဘူး
- main မှာ တော့ ကိုယ်ပေးလိုက်တဲ့ commit message နဲ့ dev က changes တွေရောက်သွားပါလိမ့်မယ်

---

# 1. Timetravel

## A. Push ပြီးသား commit ကို undo ပြန်လုပ်ချင်ရင်


```bash
git log
git revert c3de5f
```

မူလcommit ကို မဖျက်ပဲ c3de5f (commit hash) ကို reverse ပြန်လုပ်တဲ့အခါ သုံးပါတယ်

Code က c3de5f commit မတိုင်ခင် အခြေအနေရောက်သွားပေမဲ့ history တော့ ကျန်နေမှာ ဖြစ်ပါတယ်

## B. Commit ကို ဖြုတ်ချင်ရင်

```bash
git reset —-soft HEAD~1
```

လက်ရှိ branch history က ပြန်ဖြုတ်တာဖြစ်ပါတယ်

working directory မှာတော့ staged အဖြစ်ကျန်ပါတယ်

> Note: HEAD ဆိုတာ working directory ရဲ့နောက်ဆုံး commit
>
> HEAD~1 ဆို လက်ရှိ commit ရဲ့ first parent (ပုံမှန်အားဖြင့် နောက်ဆုံးcommit မတိုင်ခင် commit)

```bash
git reset HEAD~1
```

soft နဲ့ကွာခြားချက်က working directory မှာ unstaged အနေနဲ့ ကျန်ပါတယ်

```bash
git reset —-hard HEAD~1
```

Reset လုပ်လိုက်တဲ့ commit ကိုရောက်သွားပြီး Local changes ပျောက်သွားပါလိမ့်တယ်

---

# Cheatsheet for rebase and merge

2 ခုလုံးက branch တစ်ခုခုက changes တွေက်ို branch တစ်ခုမှာ သွားပေါင်းချင်တဲ့ အချိန်မှာသုံးပါတယ်

## A. dev ကို main ထဲ merge မယ်

**Cmd**

```bash
git fetch —-all
git switch main
git merge dev
```

- branch histories က timely ပုံစံပေါင်းသွားတယ်
- Merge တဲ့ commit တစ်ခု ထပ်ထွက်ပါတယ်
- Branch 2 ခုရဲ့ History တွေကွဲနေတဲ့ အချိန်မျိုးမှာ သုံးလေ့ရှိပါတယ်
- Merge တဲ့အချိန် conflict ဖြစ်နိုင်ပါတယ်

## B. dev ကို main ပေါ် rebase မယ်

```bash
git fetch —-all
git switch dev
git rebase main
```

- main ကို အခြေပြုပြီး dev က commit တွေက်ို ပြန်တင်ပါတယ်
- တင်လိုက် commit တွေက id အသစ်နဲ့ ဝင်သွားပါမယ်
- Merge commit ထပ်မထွက်ပါဘူး
- Conflict ကတော့ replay commit တိုင်းမှာ ဖြစ်နိုင်ပါတယ်