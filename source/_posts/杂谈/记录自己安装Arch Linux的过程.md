---
title: 记录自己安装Arch Linux的过程
date: '2022-10-15 00:00:01'
tags: 
- 系统安装
categories:
- Linux
toc: true
---

太香了，本想着那么多基于Linux内核的系统都差不多，所以一直都没装Arch Linux。有一次看到一个我比较喜欢的科技Up主配置Vscode，对于Windows而言采用的WSL2，WSL2使用的是Arch Linux。那个时候我才发现原来WSL2还可以装Arch Linux，于是我第一次装Arch Linux就在WSL2里安装的......后来经常需要在Linux环境下完成项目，WSL2满足不了我了，所以就安装了Arch Linux。
<!--more-->

## 1. 下载ArchLinux镜像

首先是要下载镜像，官网就有。一般来说要装在x86_64架构的机器上，但Arm架构的似乎也有社区版本的镜像，但估计稳定性不是很好，所以我就没有试了：https://archlinux.org/download/

## 2. 制作启动盘

制作启动盘的软件有很多，但首先确保要有至少4~8GB的的U盘。我们要利用制作启动盘的软件来生成关于要安装的系统的引导文件，以便本机在启动的时候能扫到U盘的引导。

在Windows平台上，可以用Rufus制作启动盘，虽然看起来界面简陋，但是实际上很好用很稳定：

![image-20221207022201066](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20221207022201066.png)

打开Rufus，引导文件类型选择你下载的镜像，目标系统类型一定要是UEFI（不然装不了），然后生成启动盘就可以了。

