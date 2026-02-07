---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date | time.Format "2006-01-02" }}
slug: {{ now.Format "2006-01-02" }}-{{ .Name | urlize }}
type: posts
draft: true
tags:
  - default
---
