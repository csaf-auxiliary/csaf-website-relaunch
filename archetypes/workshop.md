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
      preview: '/images/events/default/workshop.png'
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

{{< register-button >}}

{{< text-and-image >}}
![image](/images/events/<year>/<event-name>/<filename>)

Markdown text.
{{< /text-and-image >}}

{{< paragraph-accent >}}
Markdown text.
{{< /paragraph-accent >}}

{{< event-timetable >}}
**Workshop 1:**

09.12.2024 13:30-18:00 (Part 1)

10.12.2024 08:00-12:30 (Part 2)

(limited to 40 participants)
{{< /event-timetable >}}
