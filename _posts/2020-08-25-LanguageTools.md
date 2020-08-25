---
layout: post
title: Language Tools
author: Mizuha Ki
date: 2020-08-25
categories:
- tools
- spell
- grammar
tags:
- tool
- spell
- grammar
- blog
---

## Introduction 
- A language tool for TexSutdio.

## Software Address
[TexStudio](http://texstudio.sourceforge.net/)
[Java](https://www.oracle.com/java/technologies/javase-downloads.html)
[English Dictionary](https://extensions.libreoffice.org/extensions/english-dictionaries)
[Language Tools](https://blog.csdn.net/yinqingwang/article/details/54583541)


## Environment
-- Java install
java -version
javac -version

-- LanguageTools install
java -jar languagetool.jar
click 'Text Checking' -> options -> General, select server port: 8081
check: http://localhost:8081/v2/check?language=en&text=you+is+girl

-- TexStudio
http://localhost:8081
java
..\languagetool.jar

