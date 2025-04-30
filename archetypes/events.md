---
title: '{{ replace .Name "-" " " | title }} {{ path.Base .File.Dir }}'
weight: 1
draft: true

params:
  event:
    dates: ''
    location: ''
  render:
    images:
      preview: ''
      header: ''
---
<!--
  SPDX-SnippetCopyrightText: {{ now.Format "2025" }} OASIS CSAF TC
  SPDX-License-Identifier: LicenseRef-OASIS-CSAF-TC-License
-->

`Note:`

`This message is only for editors. Delete this block before publishing the page.`

` To learn how to customize and style an event page, please see the instructions in the README file: `
https://github.com/csaf-auxiliary/csaf-website-relaunch#add-a-page-for-the-event
