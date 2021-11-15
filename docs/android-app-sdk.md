---
title: Overview
date: 2018-09-15 07:42:34
slug: android-app-sdk
---

## Some sub header 1
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Nec tincidunt praesent semper feugiat nibh sed. Scelerisque viverra mauris in aliquam sem fringilla ut morbi. Pellentesque adipiscing commodo elit at imperdiet dui accumsan. Tincidunt lobortis feugiat vivamus at augue eget arcu. Magna eget est lorem ipsum dolor sit amet. Est velit egestas dui id ornare arcu odio. Quam elementum pulvinar etiam non quam lacus. Egestas maecenas pharetra convallis posuere. Pretium quam vulputate dignissim suspendisse in est ante. Cursus vitae congue mauris rhoncus aenean vel elit scelerisque. Elit eget gravida cum sociis natoque penatibus et magnis. Morbi tincidunt ornare massa eget. Egestas fringilla phasellus faucibus scelerisque. Viverra ipsum nunc aliquet bibendum enim facilisis gravida neque.


## Some sub header 2
If you need to use icons somewhere in the theme, you can use any icon from [Feather Icons](https://feathericons.com/) as a component. All that is needed is that you import the icon in the component you want to use it like i do it in the theme switcher component:

```javascript
import { MoonIcon, SunIcon } from 'vue-feather-icons'

export default {
  components: {
    MoonIcon,
    SunIcon
  },
...
```

And then the icon can be used like this:

```html
<sun-icon class="sun" />
```

## 3
To change the theme colors you need to edit the file `src/assets/scss/config/_colors.scss`. When you open the file for the first time it will look like this:

```scss
// Dark theme
$backgroundDark: #18191a;
$sidebarDark: #2a2c2f;
$textDark: #fff;

// Bright theme
$backgroundBright: #fff;
$sidebarBright: #f3f4f5;
$textBright: #2a2c2f;

// Brand
$brandPrimary: #10c186;
```

## 4
Jamdocs uses Source Sans Pro by default. I chose to embed the font in the project to increase page speed. To change the font, you just install another Google Font as a dependency, lets say you want Open Sans:

```bash
yarn add typeface-open-sans
```

Then, on line 7 in `src/main.js` you change the line to:

```javascript
require('typeface-open-sans')
```

Now you can go to line 12 in `src/assets/scss/globals.scss` and change that line to:

```scss
font-family: 'Open Sans', sans-serif;
```

You're done!

## 5

To edit the sidebar, open the file `data/settings.json`. In this file you will find global theme settings as objects and arrays. The sidebar is edit by adding an sections. A section object looks like this:

```json
{
  "section": "Introduction",
  "topics": [
    {
      "title": "Getting started",
      "slug": "getting-started"
    }
  ]
}
```

The section contains a name, in this case "Introduction", and following the name is an array called topics. Each topic resembles a markdown file in `docs` and contains the title you want that file to have in the sidebar, as well as the slug for routing.

For each topic the markdown is scanned for h2 headings, which is added as anchor links right below the topic in the sidebar.