<!--
  SPDX-License-Identifier: Apache-2.0

  SPDX-FileCopyrightText: 2025 German Federal Office for Information Security (BSI) <https://www.bsi.bund.de>
  Software-Engineering: 2025 Intevation GmbH <https://intevation.de>

  This file is Free Software under the Apache-2.0 License
  without warranty, see README.md and LICENSES/Apache-2.0.txt for details.
-->

- [Website for csaf.io (beta)](#website-for-csafio-beta)
   * [Deployment](#deployment)
      + [How it Works](#how-it-works)
      + [How to update the website content](#how-to-update-the-website-content)
         - [Add a new tool](#add-a-new-tool)
         - [Update "Specifications" page](#update-specifications-page)
         - [Add a link to a new presentation video](#add-a-link-to-a-new-presentation-video)
      + [Adding a New Event Page](#adding-a-new-event-page)
         - [Folder and Website Sections Structure](#folder-and-website-sections-structure)
         - [Managing Markdown Files](#managing-markdown-files)
         - [Managing Images](#managing-images)
         - [Creating New Event Pages](#creating-new-event-pages)
         - [License Information](#license-information)
         - [Front Matter Parameters](#front-matter-parameters)
         - [Using Shortcodes](#using-shortcodes)
            * [📩 `{{< register-button >}}`](#-register-button-)
            * [🖼️ `{{< text-and-image >}}...{{< /text-and-image >}}`](#-text-and-image-text-and-image-)
            * [🔶 `{{< paragraph-accent >}}...{{< /paragraph-accent >}}`](#-paragraph-accent-paragraph-accent-)
            * [🗓️ `{{< event-timetable >}}...{{< /event-timetable >}}`](#-event-timetable-event-timetable-)
            * [🔗 `{{< internal-link "Header Name" >}}`](#-internal-link-header-name-)
            * [🗺️ `{{< open-street-maps "lat,lon[,zoom]" >}}`](#-open-street-maps-latlonzoom-)
            * [📝 `{{< session-card >}}...{{< /session-card >}}`](#-session-card-session-card-)
         - [Publishing a Page](#publishing-a-page)
         - [Managing Event Lists](#managing-event-lists)
         - [Structure of the `/events/` List Page](#structure-of-the-events-list-page)
         - [Changing the Order of Events in Lists](#changing-the-order-of-events-in-lists)
         - [Controlling What Appears on Event Lists](#controlling-what-appears-on-event-lists)
   * [Development server (with live reload)](#development-server-with-live-reload)
      + [Prerequisites](#prerequisites)
      + [1. Pull the Repository](#1-pull-the-repository)
      + [2. Install Dependencies](#2-install-dependencies)
      + [3. Start the Development Server](#3-start-the-development-server)
   * [Directory structure](#directory-structure)
   * [Project Settings Defined in `hugo.toml`](#project-settings-defined-in-hugotoml)
      + [Markup Settings](#markup-settings)
   * [License](#license)

# Website for csaf.io (beta)

This website provides information and resources
about the Common Security Advisory Framework (CSAF).
It helps organizations create, distribute, and consume
security advisories in a structured, machine-readable format.

Built with Hugo and styled using Bootstrap, the site offers a clean and
accessible way to explore CSAF-related content.

For more details about CSAF,
visit the [OASIS CSAF Technical Committee](https://www.oasis-open.org/committees/csaf/charter.php).

---

## Deployment

The website is built and deployed automatically via GitHub Actions.

### How it Works

- The preferred way to update the website is by opening a **pull request**.
  Once merged into `main`, the changes will be deployed automatically.

- Advanced users with the necessary permissions can push directly to `main`,
  but using pull requests is recommended for review and tracking.

- Deployments can also be triggered manually from the **GitHub Actions** tab.

- The latest version is published at
  [GitHub Pages](https://csaf-auxiliary.github.io/csaf-website-relaunch).

No manual deployment is required. Changes go live once reviewed and merged.

---

### How to update the website content

#### Add a new tool

If you want to add a new CSAF tool,
open [content/tools.md](content/tools.md?plain=1) with the text editor.

Add a section with markdown as content like in this example
(place information about the tool in markdown
between `{{% card %}}` and `{{% /card %}}`):

```markdown
{{% card %}}
### [CSAF Downloader](https://github.com/gocsaf/csaf/blob/main/docs/csaf_downloader.md)
A tool to download CSAF content from a specific domain / CSAF provider.<br>
{{% /card %}}
```

Then open a pull request to the main branch of this repository
as suggested by [Github](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request).

---

#### Update "Specifications" page

If you want to change the text or button on the "Specifications" page,
open the [content/specifications.md](content/specification.md?plain=1) file,
change the HTML there and then open a pull request.

---

#### Add a link to a new presentation video

If you want to add a presentation, there is more work for privacy reasons:

Using a YouTube video cover (a static image with a link)
instead of embedding the video
prevents YouTube from automatically loading tracking scripts, cookies,
and third-party requests when a visitor opens the page.

This ensures that no user data is sent to Google (YouTube's parent company)
until the user explicitly clicks on the link to watch the video.

Follow these steps to **add new presentation**
(in all the steps insert the id of the video instead of the `<video-id>`):

1. Open the [data/presentations.json](data/presentations.json) file,
and insert a new block like this:

```
    ,
    {
        "link": <video-id>
    }
```

2. Make a screenshot of the video or get a custom video cover.
Name the file in the format `<video-id>.jpg`.

3. Add the file to the
   [static/images/youtube_covers/](static/images/youtube_covers/) folder.

4. In the same folder create a file with the name `<video-id>.jpg.license`
   and provide the licensing information in this format:

```
SPDX-License-Identifier: LicenseRef-YouTube-Standard-License
SPDX-FileCopyrightText: Author: <channel-name-and-link>
SPDX-FileCopyrightText: Distributor: YouTube, Inc. <https://www.youtube.com>
Source: https://www.youtube.com/watch?v=<video-id>
```

Replace `<video-id>` and `<channel-name-and-link>` with the actual ones.


5. Insert the licensing information to the
[LICENSE](LICENSE.md#video-thumbnails-attribution) file in this format:

```
### Thumbnail <number-of-the-new-file>
- **Link Source**: [YouTube](https://www.youtube.com/watch?v=<video-id>)
- **License**: <license-type>
- **Author**: [<channel-name>](https://www.youtube.com/channel/<channel-id>)
- **Distributor**: [YouTube, Inc.](https://www.youtube.com)
- **Video ID**: <video-id>
```

replace `<number-of-the-new-file>`, `<<video-id>`, `<license-type>`,
`<channel-name>` and `<channel-id>` with the actual data.

How to define the `<license-type>`:

- If video description contains the label
  "Creative Commons Attribution license (reuse allowed)",
  insert `[CC-BY-3.0](https://creativecommons.org/licenses/by/3.0/)`

- Otherwise insert `[YouTube Content License](https://www.youtube.com/t/terms)`

6. Open a pull request.

---

### Adding a New Event Page

#### Folder and Website Sections Structure

The `/events/` section of the website directly matches the structure
of the [`/content/events/`](/content/events/) folder.

---

#### Managing Markdown Files

To keep everything organized and make sure the event lists display correctly,
group event pages by year.

Example folder structure:

```
content/events/
├── 2024/
│   ├── workshop.md
│   ├── community-days.md
│   └── ...
└── 2025/
    └── ...
```

---

#### Managing Images

Images for event pages should be placed
in the [`/static/images/events/`](/static/images/events/) folder.

- Create a subfolder for each year.
- Inside the year folder, create a separate folder for each event.

Example:

```
static/images/events/2025/workshop/
```

When inserting images in your Markdown file, **do not**
include `/static` in the file path.

✅ Correct:

```
![Image description](/images/events/2025/workshop/filename.png)
```

🚫 Incorrect:

```
![Image description](/static/images/events/2025/workshop/filename.png)
```

---

#### Creating New Event Pages

1. **Check if the year folder already exists.**
   If it does not, create it first by generating the default year page:

   ```
   hugo new --kind=events-index events/<year>/_index.md
   ```

   Example:

   ```
   hugo new --kind=events-index events/2025/_index.md
   ```

2. **Create a new event page.**
   You can either start with a ready-to-use template or create a blank page.

   - **Using a template** (recommended for easier setup):

     ```
     hugo new --kind=<template> events/<year>/<event>.md
     ```

     Available templates: `workshop`, `cdays`.

     Examples:

     ```
     hugo new --kind=workshop events/2025/workshop.md
     hugo new --kind=cdays events/2025/community-days.md
     ```

   - **Starting with an empty page:**

     ```
     hugo new events/<year>/<event>.md
     ```

     Example:

     ```
     hugo new events/2025/workshop-munich.md
     ```

> **Important:** Use hyphens (`-`) to separate words in filenames.
> All event files must use the `.md` file extension.

---

#### License Information

At the top of every Markdown file, the license information is included.
**Do not remove or modify this block.**
Write your event content **below** the license section.

Example:

```markdown
<!--
  SPDX-License-Identifier: Apache-2.0

  SPDX-FileCopyrightText: 2025 German Federal Office for Information Security (BSI) <https://www.bsi.bund.de>

  This file is Free Software under the Apache-2.0 License
  without warranty, see README.md and LICENSES/Apache-2.0.txt for details.
-->
```

---

#### Front Matter Parameters

Each event page begins with technical information called **front matter**.

Example:

```yaml
---
title: 'Workshop 2024'
weight: 1
draft: true

params:
  event:
    dates: 'December 9-12, 2024'
    location: 'Germany, Information Security Hub at Munich Airport (Südallee 1, 85356 München, Germany)'
  render:
    images:
      preview: '/images/events/default/workshop.png'
      header: '/images/events/2024/workshop/person-using-the-trackpad.jpg'
---
```

**Parameter Description**

- **`title`** (required)
  Displayed as the event page title, header, and in event lists.
  Default: filename + year (from folder name).
  You can set a custom title freely.

- **`weight`** (optional)
  Controls the order of events in event lists.
  Lower weight = higher on the list.
  Default: `1`.
  [Learn more about the events order](#changing-the-order-of-events-in-lists).

- **`draft`** (required)
  Defines whether the page is published.
  Default: `true` (not published).
  Set to `false` to publish the page.

- **`params.event.dates` and `params.event.location`** (required)
  Information displayed on the event page.
  For upcoming events, also shown on event cards on the `/events/` page.

- **`params.render.images.preview`** (optional)
  Image shown on event cards.
  If not provided, the card will not have an image.

- **`params.render.images.header`** (optional)
  Header background image on the event page.
  If not provided, a default blue-black gradient will be used.

> **Important:**
> Required parameters **must not** be empty.
> Optional parameters can be deleted if not needed.

---

#### Using Shortcodes

Shortcodes help keep all event pages consistent.
You can add them in your Markdown files as needed.

---

##### 📩 `{{< register-button >}}`

Adds a "Register now" button that links to `mailto:csaf@bsi.bund.de`.

---

##### 🖼️ `{{< text-and-image >}}...{{< /text-and-image >}}`

Displays an image alongside a block of text.

Example:

```markdown
{{< text-and-image >}}
![image](/images/events/<year>/<event-name>/<filename>)

Markdown text.
{{< /text-and-image >}}
```

- On large screens: image appears to the right.
- On small screens: image appears above the text.

---

##### 🔶 `{{< paragraph-accent >}}...{{< /paragraph-accent >}}`

Highlights a block of text with a vertical orange line on the left.

Example:

```markdown
{{< paragraph-accent >}}
Markdown text.
{{< /paragraph-accent >}}
```

---

##### 🗓️ `{{< event-timetable >}}...{{< /event-timetable >}}`

Formats a schedule block with a vertical orange line on the left
and larger text.

Example:

```markdown
{{< event-timetable >}}
**Workshop 1:**

09.12.2024 13:30–18:00 (Part 1)

10.12.2024 08:00–12:30 (Part 2)

(limited to 40 participants)
{{< /event-timetable >}}
```

---

##### 🔗 `{{< internal-link "Header Name" >}}`

Creates a link to a section header within the same page.

Example:

```markdown
{{< internal-link "Welcome & Keynote" >}}
```

Useful for making a table of contents.

---

##### 🗺️ `{{< open-street-maps "lat,lon[,zoom]" >}}`

Embeds an OpenStreetMap with a marker at the given coordinates.

Examples:

```markdown
{{< open-street-maps "48.350442,11.774101" >}}
{{< open-street-maps "48.350442,11.774101,16" >}}
```

- Without zoom: defaults to `14`.
- With zoom: set it manually (e.g., `16`).

---

##### 📝 `{{< session-card >}}...{{< /session-card >}}`

Renders a session description as a styled card.

Example:

```markdown
{{< session-card >}}

### Welcome & Keynote

#### Speaker:

**Abstract:**

**Bio:**

{{< /session-card >}}
```

---

#### Publishing a Page

When the page is ready to go live, set `draft` to `false`
at the top of the file:

```yaml
---
draft: false
---
```

This will make the page accessible to users and automatically add it
to the navigation and event lists.

---

#### Managing Event Lists

Event lists are created automatically from the content
inside the `/content/events/` folder.

#### Structure of the `/events/` List Page

The `/events/` page has two main sections:

1. **Upcoming Events**
   Displays cards for upcoming events.
   These events are defined at the top
   of the `/content/events/_index.md` file:

    ```yaml
    ---
    params:
      events:
        year: <year>
    ---
    ```

2. **Previous Events**
   Displays links to all other published
   (and [not excluded](#controlling-what-appears-on-event-lists))
   event pages.

---

#### Changing the Order of Events in Lists

Events are sorted based on two parameters from the front matter:

- **Weight:** Pages with lower numbers appear first.
- **Title:** If Weight is the same (or missing), events
are sorted alphabetically by title.

**Default behavior:**
All events have a default weight of `1`.
This means they are normally sorted by their titles.

**To change the order manually:**
Set a different weight at the top of the event page file:

```yaml
---
weight: 2
---
```

- Lower weight → Higher in the list.
- Higher weight → Lower in the list.
- 0 → Below all the other numbers.

---

#### Controlling What Appears on Event Lists

By default, all published events are visible on:

- `/events/`
- `/events/<year>/`

**If you want to hide a page from the lists:**

- To **unpublish** an event or year page (hide it completely), set:

    ```yaml
    draft: true
    ```

- To **hide a whole year** from the `/events/` page
(without unpublishing the events):

  1. Open the `_index.md` file for that year
  (`/content/events/<year>/_index.md`).

  2. Add this to the top:

    ```yaml
    ---
    params:
      render:
        exclude: true
    ---
    ```

**Important:**
Events and year pages that are excluded this way will **still be accessible**
via direct URL.

---

## Development server (with live reload)

To run the Hugo development server with live reload, follow these steps:

### Prerequisites

Before starting the development server, ensure you have the following installed:

- **Hugo**: Required for generating the static website from the source code files.

    - Check if Hugo is installedby running `hugo version` in the terminal.

    - [Install Hugo](https://gohugo.io/getting-started/installing/) if necessary.

- **Git**: Required to clone the repository.

    - Check if Git is installed by running ```git --version```
      in the terminal.

    - [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if necessary.

- **Node.js and npm**: Required for managing project dependencies,
  such as the Bootstrap framework used for styling the pages.

    - Check if Node.js and npm are installed by running `node -v` and
      `npm -v` in the terminal.

    - [Install Node.js and npm](https://nodejs.org/) if necessary.

### 1. Pull the Repository

Clone the repository to your local machine using Git:

```bash
git clone https://github.com/csaf-auxiliary/csaf-website-relaunch.git
```

### 2. Install Dependencies

Navigate into the project directory:

```bash
cd your-repository-name
```

Install project dependencies, including the Bootstrap framework:
```bash
npm install
```

### 3. Start the Development Server

```bash
hugo server -D
```

'-D' flag allows to include the draft pages to the build.

The site will be accessible at http://localhost:1313/.

---

## Directory structure

- **assets**: Contains the files that are being pre-processed
  (.scss files compiled into .css)
  and icons that have to be injected into HTML for styling;

- **content/**: Contains content files, most of which have only meta headers;

- **layouts/**: Contains custom templates and layout files for rendering the site;

- **static/**: Stores static assets such as images and SCSS files;

- **hugo.toml**: The configuration file for the Hugo site,
  where site-wide settings are defined;

- **data/**: Holds additional JSON data files
  used by Hugo for dynamic content generation;

- **LICENSE.md**: an overview over the licences of the used components;

- **LICENSES/**: Contains any additional licensing information for dependencies
  or components used;

- **package.json** and **package-lock.json**: Manages Node.js dependencies;

---

## Project Settings Defined in `hugo.toml`

The `hugo.toml` file contains the main configuration settings for the Hugo project.

- **languageCode**: Defines the default language for the website
  (set to American English).

- **title**: The title of the website.

- **disableKinds**: Specifies which kinds of content to disable.
   The page types required for generating list-pages are disabled.

- **baseUrl**: Specifies the root URL of your site,
    which is used as the base for all relative links.

- **canonifyURLs**: When set to true, allows Hugo to add baseUrl
to the relative links.
At this stage is needed to handle base url that is not the site root.

### Markup Settings

Goldmark Parser is the tool that turns written content from the markdown files
into the final format that appears on the website.

For processing the text, the following settings are applied:
**[markup.goldmark.renderer]:**

- **unsafe = true:** It makes it possible to wrap the Markdown content
  in the .md files (specifically, tools.md) with extra HTML for styling.

**[markup.goldmark.extensions]:**

- **table = true:** Allows rendering markdown tables as <table> elements.

**[markup.goldmark.parser]:**

- **autoHeadingID = true:** Automatically generates `id` on every <h1>–<h6>
  (only for content rendered automatically from markdown).

- **autoHeadingIDType = "github":** Generates `id`s as lowercase,
  dash-separated slugs (GitHub style).

---

## License

Originally content from the old csaf.io webpage:
Copyright 2023 OASIS CSAF TC - All Rights Reserved

New files developed for the webpage mechanics and the custom styles are
Copyright 2025 German Federal Office for Information Security (BSI)
([bsi.bund.de](https://www.bsi.bund.de))

Additionally, there are third-party resources in the repository
under various Free Software and non free content licenses.
For more information, see [LICENSE.md](LICENSE.md).

The webpage and repo was constructed 2025-03 by
Intevation GmbH ([intevation.de](https://intevation.de))
