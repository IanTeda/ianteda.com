---
# [Front Matter Formats](https://gohugo.io/content-management/front-matter/)
title: "Why Personal Ledger Is Keyboard First"
description: "Why Personal Ledger is designed to be driven from the keyboard, and why the mouse still works when you want it."
keywords:
- "personal ledger"
- "keyboard navigation"
- "personal finance"
- "user experience"
date: 2026-11-03
publishDate: 2026-11-03
lastmod: 2026-11-03
slug: personal-ledger-keyboard-first
tags:
- "Money"
- "Personal Ledger"
- "Rust"
draft: false
# Template specific - Minimo Theme
toc: true
# cover:
#   image: TODO.png
#   caption: "TODO"
#   alt: "TODO"
#   style: full
---
In my experience, data management and navigation are a big part of working in a financial app: importing transactions, updating and categorising them, and ticking them off against a bank statement. It is repetitive work, and every time your hand leaves the keyboard to find the mouse, it gets a little slower and a little more tedious.

When I started building [Personal Ledger]({{< ref "/blogs/2026-10-28-introducing-personal-ledger" >}}), I really wanted the keyboard to be the main way you get around. I like being able to do everything right from the keys, so I made sure you could do that here. The status line has little keyboard navigation tips if you need them, but you can always grab the mouse if that's easier. I know people won't use Personal Ledger every day, and sometimes you come back after a break. It still needs to feel easy and make sense, no matter how long it's been. If it's simple to get around, that's what matters.

## Speed

It's mostly about speed. When you enter a transaction, you pick the date, payee, category, and amount, then save. If you use the mouse, you reach and click for every step, then go back to the keyboard to type. With the keyboard, you type, hit Tab, type again, and press Enter. It only saves a second or two each time, but after a month of transactions, or a long session catching up, it really adds up.

Keyboard shortcuts get easier the more you use them. At first you're hunting for buttons, but after a week you know where they are. With the keyboard, once a shortcut is in your fingers, you barely have to think about it. The app gets faster as you get used to it.

{{< keyboard-mockup caption="A mockup of moving around the desktop app without a mouse. Keys shown are illustrative." >}}

## Flow

Speed isn't the only thing. Switching back and forth between the keyboard and mouse breaks your focus. When I'm working through a bank statement line by line, I want to stay in that rhythm. Next line, check it, mark it, keep going. Every time you grab the mouse, you lose a little bit of that flow, and that's when mistakes start to show up.

If I stay on the keyboard, I keep my eyes on the numbers instead of looking for where the mouse pointer went.

## One way of working across apps

Personal Ledger comes in two flavors, desktop and terminal. The terminal app is all about the keyboard, so if you learn shortcuts there, they work in the desktop app too. Navigation, selection, and common actions all work the same way, so you only have to learn things once.

<!-- TODO: add a short table of the core keybindings once they are settled, e.g.
| Action | Key |
|---|---|
| Move between sections | ... |
| New transaction | ... |
| Search / filter | ... |
| Save | ... |
-->

## The mouse still works

That doesn't mean the mouse is an afterthought. In the desktop app, you can click, scroll, and select just like you'd expect. Sometimes the mouse is just better, like when you're looking at a chart, scrolling through a long report, or exploring a screen you haven't seen before. And some people just like using the mouse, and that's totally fine.

I'm not trying to force anyone to work a certain way. I want the fast option to be there for me and for people who want it, and for both ways to get you to the same place. You can start out using the mouse, and if you notice you keep doing the same thing, you might try a shortcut. It's all about what works for you.

## Discoverability

The tricky thing about a keyboard-first design is that shortcuts are hidden. A button is obvious, but a key binding isn't. So Personal Ledger makes shortcuts easy to find. You'll see them right next to the actions they trigger, and a help view shows what's available on whatever screen you're on. <!-- TODO: confirm how this is surfaced in each client (help key, command palette, status bar hints). -->

## Wrapping up

Making the keyboard the main way to get around might sound small, but it really changes how the app feels day to day. If you have to do a lot of repetitive data entry, this is what makes the difference between a tedious chore and something that works without getting in your way.

If you have opinions on keybindings, or think I've got this backwards, the code is on [GitHub](https://github.com/IanTeda/Personal-Ledger).
