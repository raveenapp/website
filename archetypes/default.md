---
title: "{{ replace .Name "-" " " | title }}"
draft: true
date: {{ .Date | time.Format "2006-01-02" }}
---
