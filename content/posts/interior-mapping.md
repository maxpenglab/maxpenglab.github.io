---
title: "假室内渲染效果研发"
date: 2024-10-01
tags: ["渲染", "Shader", "专利"]
cover:
  image: "images/interior/cover.png"
  alt: "假室内渲染效果"
summary: "用 Interior Mapping 技术实现低性能消耗的室内空间感，已获公司专利授权。"
draft: false
---

## 问题背景
场景中大量无法交互的室内空间需要具备空间感，但不能有太多性能消耗。

## 技术方案
- 用 Interior Mapping 方式采样 Cubemap 表达室内空间
- 切线空间采样 + 贴图存储折角，支持非正方体形状的室内
- 打通自制 Cubemap 流程，美术可自由定制

## 效果展示

{{< video src="videos/interior_demo.mp4" >}}

## 落地成果
- 游戏内所有视觉可见室内空间均使用此方案
- 已为公司申请专利