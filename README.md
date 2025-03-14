<!--
  SPDX-License-Identifier: Apache-2.0

  SPDX-FileCopyrightText: 2025 German Federal Office for Information Security (BSI) <https://www.bsi.bund.de>
  Software-Engineering: 2025 Intevation GmbH <https://intevation.de>

  This file is Free Software under the Apache-2.0 License
  without warranty, see README.md and LICENSES/Apache-2.0.txt for details.
-->

# Website for csaf.io (beta)

This website provides information and resources
about the Common Security Advisory Framework (CSAF).
It helps organizations create, distribute, and consume
security advisories in a structured, machine-readable format.

Built with Hugo and styled using Bootstrap, the site offers a clean and
accessible way to explore CSAF-related content.

For more details about CSAF,
visit the [OASIS CSAF Technical Committee](https://www.oasis-open.org/committees/csaf/charter.php).

## Deployment

The website is built and deployed automatically via GitHub Actions.

### How it Works

- The preferred way to update the website is by opening a **pull request**.
  Once merged into `main`, the changes will be deployed automatically.

- Advanced users with the necessary permissions can push directly to `main`,
  but using pull requests is recommended for review and tracking.

- Deployments can also be triggered manually from the **GitHub Actions** tab.

- The latest version is published at
  [GitHub Pages](https://<username>.github.io/<repository_name>).

No manual deployment is required. Changes go live once reviewed and merged.

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

#### Update "Specifications" page

If you want to change the text or button on the "Specifications" page,
open the [content/specifications.md](content/specification.md?plain=1) file,
change the HTML there and then open a pull request.

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


## Project Settings Defined in `hugo.toml`

The `hugo.toml` file contains the main configuration settings for the Hugo project.

- **languageCode**: Defines the default language for the website
  (set to American English).

- **title**: The title of the website.

- **disableKinds**: Specifies which kinds of content to disable.
   The page types required for generating list-pages are disabled.

### Markup Settings

Goldmark Parser is the tool that turns written content from the markdown files
into the final format that appears on the website.

For processing the text,
**[markup.goldmark.renderer] unsafe = true** setting is applied.
It makes it possible to wrap the Markdown content in the .md files
(specifically, tools.md) with extra HTML for styling.

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
