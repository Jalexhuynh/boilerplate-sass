# Main file

The main file (usually labelled `main.scss`) should be the only Sass file from the whole code base not to begin with an underscore. This file should not contain anything but `@import` and comments.

## Folder Architecture

### 1. Base
- The `base/` folder holds what we might call the boilerplate code for the project. In there, you might find some typographic rules, universal selector resets, HTML/body selectors, animations, typography, and utilities.

### 2. Abstracts 
- The `abstracts/` folder gathers all Sass tools and helpers used across the project. Every global variable, function, mixin and placeholder should be put in here. 
- The rule of thumb for this folder is that it should not output a single line of CSS when compiled on its own. These are nothing but Sass helpers.

### 3. Components
- The `components/` folder is more focused on widgets. It contains all kind of specific modules like a slider, a loader, a widget, buttons, and basically anything along those lines. There are usually a lot of files in `components/` since the whole site/application should be mostly composed of tiny modules.

### 4. Layout
- The `layout/` folder contains everything that takes part in laying out the site or application. This folder could have stylesheets for the main parts of the site (header, footer, navigation, sidebar…), the grid system or even CSS styles for all the forms.

### 5. Pages
- If you have page-specific styles, it is better to put them in a `pages/` folder, in a file named after the page. For instance, it’s not uncommon to have very specific styles for the home page hence the need for a `_home.scss` file in `pages/`.
*Note — Depending on your deployment process, these files could be called on their own to avoid merging them with the others in the resulting stylesheet. It is really up to you.*

### 6. Themes
- On large sites and applications, it is not unusual to have different themes. There are certainly different ways of dealing with themes but I personally like having them all in a `themes/` folder.

*Note — This is very project-specific and is likely to be non-existent on many projects.*

### 7. Vendors
- Most projects will have a `vendors/` folder containing all the CSS files from external libraries and frameworks – Normalize, Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered, and so on. Putting those aside in the same folder is a good way to say “Hey, this is not from me, not my code, not my responsibility”.

- If you have to override a section of any vendor, I recommend you have an 8th folder called `vendors-extensions/` in which you may have files named exactly after the vendors they overwrite. For instance, `vendors-extensions/_bootstrap.scss` is a file containing all CSS rules intended to re-declare some of Bootstrap’s default CSS. This is to avoid editing the vendor files themselves, which is generally not a good idea.