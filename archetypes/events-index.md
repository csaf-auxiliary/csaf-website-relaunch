---
title: 'Events {{ path.Base .File.Dir }}'
weight: 1
draft: true

params:
  events:
    year: {{ path.Base .File.Dir }}
  render:
    exclude: false
---
<!--
  SPDX-SnippetCopyrightText: {{ now.Format "2025" }} OASIS CSAF TC
  SPDX-License-Identifier: LicenseRef-OASIS-CSAF-TC-License
-->
