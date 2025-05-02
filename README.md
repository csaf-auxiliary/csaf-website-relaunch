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
SPDX-FileCopyrightText: <channel-name-and-link>
```

Example:
```
SPDX-License-Identifier: LicenseRef-YouTube-Standard-License
SPDX-FileCopyrightText: FIRST <https://www.youtube.com/channel/UCK3_z6YyWvfqrOuCmrfxsTw>
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

The `/events/` section of the website contains the list of the events,
pages of which are uploaded to the "/community-dats/" and "/workshops/"
folders.
The structure of the `/community-days/` and `/workshops/` website sections
directly matches the structure of these folders.

---

#### Managing Markdown Files

Hugo will automatically organize your event pages when you follow
the [Creating New Event Pages](#creating-new-event-pages) steps.
This keeps everything tidy and makes sure your event lists show up correctly
on the site.

If you ever need to add or update an event file by hand,
please follow these rules:

**File Name**

- Use the year of the event as the file name.

- For example: `2024.md`

**File Location**

- Put each year’s file into the folder for its event type.

- For example, a community days event in 2024 goes here:
  `content/community-days/2024.md`

Here’s what your folders might look like:

```
content
├─events.md
├─community-days/
│   ├── 2024.md
│   └── ...
└─workshops/
    ├── 2024.md
    └── ...
```

---

#### Managing Images

All event images go into the `static/images/events/` folder.
You’ll see two subfolders there already:

- `community-days/`

- `workshops/`

To organize images:

1. **Create a Year Folder**:
   Inside the appropriate event type folder make a new folder
   named for the year.

   * Example: `static/images/events/workshops/2025/`

2. **Add Event Images**:
   Inside the year folder, drop in all images for each individual event.

Here’s how it might look:

```
static/
└── images/
  └── events/
    ├── community-days/
    │ └── 2025/
    │   ├── header.png
    │   └── image1.png
    └── workshops/
      └── 2025/
        ├── header.png
        └── image1.png
```

When inserting images in your Markdown file, **do not**
include `/static` in the file path.

✅ Correct:

```
![Image description](/images/events/workshops/2025/image1.png)
```

🚫 Incorrect:

```
![Image description](/static/images/events/workshops/2025/image1.png)
```

---

#### Creating New Event Pages

You can either start with a ready-to-use template or create a blank page.

- **Using a template** (recommended for easier setup):

  ```
  hugo new <event-type>/<year>.md
  ```

  Available event types: `workshops`, `community-days`.

  Examples:

  ```
  hugo new workshops/2025.md
  hugo new community-days/2025.md
  ```

- **Starting with an empty page:**

  ```
  hugo new --kind=event <event-type>/<year>.md
  ```

  Example:

  ```
  hugo new --kind=event workshops/2025-munich.md
  ```

> **Important:** Use hyphens (`-`) if you need separate words in filenames.

> All event files must use the `.md` file extension.

---

#### License Information

Each Markdown file must begin with a license block.
**Do not remove or move this block.**
It ensures legal compliance and correct attribution.

If needed, update the license details to reflect the actual license
under which your content should be published.

Example:

```markdown
<!--
  SPDX-FileCopyrightText: 2025 OASIS CSAF TC
  SPDX-License-Identifier: LicenseRef-OASIS-CSAF-TC-License
-->
```

---

#### Front Matter Parameters

Each event page begins with technical information called **front matter**.
These help control how the page looks and where it appears.

Example:

```yaml
---
title: 'Workshop 2024'
weight: 1
type: 'event'
draft: true

params:
  event:
    dates: 'December 9-12, 2024'
    location_long: 'Germany, Information Security Hub at Munich Airport (Südallee 1, 85356 München, Germany)'
    location_short: 'München, Germany'
    year: 2024
  render:
    lists:
      display_in_lists: true
      display_on_top: true
    images:
      preview: '/images/events/default/workshop_list.png'
      header: '/images/events/workshops/2024/person-using-the-trackpad.jpg'
---
```

##### Required Settings

Required parameters **must not** be empty.

- **`title`**
  It will be shown at the top of the event page and in event lists.

  - If you generate an event page from a template,
    it will have the event type and the year as a default title.

  - You can write a custom title anytime.

- **`layout`**
  *Please don’t change this!*

  - It’s a technical setting that tells Hugo how to build the page.

- **`draft`**
  Controls whether the event is published on the website.

  - `true` = hidden (not published)

  - `false` = visible (published).

  Set to `false` when the event is ready to go live.

- **`params.event.dates`**
  The event’s date.

  - It will appear on the page and in event lists.

- **`params.event.location_long`**
  The full location name.

  - Shown on the event page.

  - Example: `Information Security Hub at Munich Airport (Südallee 1, 85356 München, Germany)`

- **`params.event.location_short`**
  A shorter location name.

  - Shown in event lists.

  - Example: `'München, Germany'`

---

##### **Optional Settings**

- **`weight`**
  Controls the order of events in lists.

  - Lower numbers appear higher on the list.

  - Default is `1`.

  [More about changing event order](#changing-the-order-of-events-in-lists)

- **`params.render.images.preview`**
  A preview image for the event card shown on the main `/events/` page.

  - If not added, the card will not have an image.

- **`params.render.images.header`**
  The big header background image at the top of the event page.

  - If not added, a blue-black gradient will be used.

- **`params.render.lists.display_in_lists`**
  Should this event appear in the list pages
  (`/events/`, `/workshops/`, `community-days`)?

  - `true` = show in the lists

  - `false` or not set = not shown in the lists

  ⚠️ This does not control whether the page is live —
    it just hides or shows it in the list views.
    To publish or unpublish, use the `draft` setting.

- **`params.render.lists.display_on_top`**
  Do you want the event to appear in a large card
  at the top of the `/events/` page?

  - `true` = featured at the top

  - `false` or not set = shown in the “Previous Events” section

⚠️ This setting only affects how the event is displayed —
not whether it is listed at all.
Use `display_in_lists` (above) to include it in the list.

---

#### Event information visibility

Published events can be visible on the following pages:

- The event page (for Example `/workshops/2024/`)

- List pages `/events/` and `/workshops/` or `/community-days/`
depending on the folder where event file is uploaded.

Page visibility is defined on the top of its .md-file.

To **unpublish** an event or year page (hide it completely), set:

  ```yaml
  draft: true
  ```

This will remove the page from all the list pages and make it not accessible
by its direct URL.

**To hide a link to the event from the lists** without unpublishing its page,
set:

  ```yaml
  params:
    ...
    render:
      lists:
        display_in_lists: true
  ```

This will remove the page from all the list pages,
but it can still be found by its direct URL.

---

#### **How to Feature an Event at the Top of the Events Page**

The `/events/` page has **two sections**:

1. **Highlighted Events** – Big cards shown at the top of the page

2. **Previous Events** – Regular event list shown below

To choose **where** your event appears, adjust this setting
at the top of the event’s `.md` file:

**To Feature the Event at the Top (Highlighted)**

Change `display_on_top` to `true`:

```yaml
---
params:
  render:
    lists:
      display_on_top: true
---
```

This will display the event as a **large card at the top** of the `/events/`
page.

**To Show It in the “Previous events” Section**

Change `display_on_top` to `false`:

```yaml
---
params:
  render:
    lists:
      display_on_top: false
---
```

This will place the event **in the regular list** under "Previous events"
headline.

---

#### Changing the Order of Events in Lists

Events are sorted based on two parameters from the front matter:

- **Year** Newer events appear first.

- **Weight:** Pages with lower numbers appear first.

- **Title:** If Weight is the same (or missing), events
are sorted alphabetically by title.

**Default behavior:**
All events have a default weight of `1`.
This means they are normally sorted by their years and then - by titles.

**To change the order manually:**
Set a different weight at the top of the event page file:

```yaml
---
weight: 2
---
```

- Lower weight → Higher in the list.

- Higher weight → Lower in the list.

- 0 → Below all the other numbers within the same year.

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

This will make the page accessible to users.

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
