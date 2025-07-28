
# Design components

Guidelines and building blocks for creating print and web-based maps, charts, infographics, data stories / story maps, and dashboards at the School of Cities.

If building a new web-based product, this repo can be duplicated to get started.



## Visualization design guidelines


### Colours

We use [UofT brand colours](https://brand.utoronto.ca/document/13#/colours/colours) form most graphics.

Then as needed we often create gradients between these for graphics requiring colour ramps and scales

In terms of accessibility...

- Check if graphic is colourblind safe. Many software and tools have filters for this. [This is also a good tool](https://www.color-blindness.com/coblis-color-blindness-simulator/)

- Check [contrast ratios](https://webaim.org/resources/contrastchecker/) of colours anytime text or graphic elements are overlaid onto each other. Low ratio, hard to read.



### Fonts

Here are the main font families we use:

- Titles: `TradeGothicBold`
- Sans-Serif: `OpenSans` 
- Serif: `SourceSerifPro`

For charts and maps, use `OpenSans` for most labels and text, and `TradeGothicBold` for titles and subtitles

For maps, use italics to label natural features (water, mountains) and non-italic for human features (buildings, neighbourhoods, etc.). 

Have a hierarchy of labels, e.g. smaller more faint labels for background layers or reference information, and bolder larger labels for key data points.

Make sure to check contrast ratios of label colours compared to their background colours.



### General design reference

Check out these two urban data storytelling textbook chapters for guidelines, tips and tricks, etc.

- [Data visualization](https://schoolofcities.github.io/urban-data-storytelling/urban-data-visualization/data-visualization/data-visualization.html)

- [Maps and visualizing spatial data](https://schoolofcities.github.io/urban-data-storytelling/urban-data-visualization/maps-and-spatial-data-visualization/maps-and-spatial-data-visualization.html)

Key things to consider

- Less is more. Omit needless ink. Reduce clutter. Focus on the data and its story.

- When designing, start with fewer set of colours, classifications, number of fonts, etc. then add more options if need more.

- Have any text on graphics be clear and concise.

- Think about visual hierarchy. Key data points and labels in the foreground as bolder, more prominent colours and larger font-sizes. Background is more muted, faded, for visual reference.

- Think about the visual balance of the graphic. Try to reduce white space.

- Do research, searching, etc. to see how others have visualized similar data.



## Print design constraints

When designing graphics, charts, and maps for `.pdf` reports or other *print* formats follow the visual guidelines above, but with the following constraints

- Width: 3.5 inches (half page) or 7 inches (full page).

- Max height: 8.5 inches. Feel free to adjust height to best fit the graphic and limit excess white space.

- Select fonts that would be the same or pair well with those used in broader report layout design. Fallback to using TradeGothicBold for titles and OpenSans for all other text (e.g. axis labels, legend text, etc.) if layout design isn't set or ready.

- No fonts smaller than 8pt.

- Select colours (from the colour options noted above) that align well with broader layout design if available. 

- Note all data sources used to create the graphic, near the bottom in smaller font is usually best.

- If designing multiple graphics for the same publication or series, use similar visual language across all graphics (e.g. same font type size and colour for city labels, same line width and colours for transit lines, etc.).



## Web design components

The following outlines the components / building blocks for building web-based visualizations, maps, data stories / story maps, dashboards, etc.

(The following requires base knowledge of HTML, CSS, and JavaScript).

We build data stories and interactive tools using Svelte (5.0.0) and SvelteKit (2.22.0). Both have good tutorials on their websites to get started if you haven't used them before. You'll also need `node` and `npm`

This repository is a very simple svelte project that you can copy to start a new project. To start building locally...

```
git clone https://github.com/schoolofcities/design-components
cd design-components
npm install
npm run dev
```

For any large datasets used for analysis (25mb and up), do not upload to GitHub, place in a `local_data` folder, which is noted in `.gitignore`

These are the following layout and design components included can be incorporated into other projects. Start with these to achieve consistency across projects.




### Global styles

`global-styles.css` is the main stylesheet. It ...

- Loads core fonts and colours.

- Provides overall `<body>` and `<main>` settings.

- Includes styling for `<p> <h1> <h2> <h3> <h4> <a> <i> <em> <b> <strong>`.

- Includes the following div classes for text blocks

- - `text` main body text

- - `callout` for callout boxes that are important written context but a bit separate from main flow of text

- - `details` smaller text for details, data, methods



### Title components

We have a couple title options:

- `TitleStandard` A simple title text with option for adding a subtitle.

- `LogoTop` A simple component for placing a logo at the top the page. Use in conjunction with TitleStandard. 

- `TitleHalfSplit` A 50/50 split title with an image. This splits depending on orientation. e.g. if landscape it splits left-right, if portrait it splits top-bottom. Includes a logo. TODO add video option

- `TitleFullPage`, a full page image with an overaly title text. TODO add video option

- `AuthorDate` a simple component with author and date information to load below the title.

Of course we can design new titles, but try to keep the same title and subtitle fonts. Trade Gothic Bold for title and Source Serif Italic for subtitle.



### Images

For loading photographs and other raster images (i.e. no selectable text or other interactivity)

- `SimpleImage` a simple component that lazy loads a raster imag (e.g. `.png`, `.jpg`, etc.) from a URL. Make sure to have a caption and state the source. Can specify the max-width of the image.

- Note that `.png` is larger file size. Try to use `.jpg` or `.webp`.



### Static graphic components

Workflow and component for creating *static* graphics, charts, and maps with selectable text. i.e. for graphics that don't require interactivity or animation, but have labels that we want users to be able to copy/paste as needed.

- Create graphics in design software (e.g. Illustrator, Inkscape, etc) based on the visual design guidelines noted at the top of this page (e.g. colouring, labelling, etc.). Save as `.svg`

- Graphics designed at three specific pixel width sizes: 1080px, 720px, and 360px. If you want a larger graphic, e.g. at 1080, you must include options for each of the smaller iterations so it can be viewed okay on smaller screens without odd size compression.

- 20px margins for most graphics

- 24px TradeGothicBold black title, typically top-left corner aligned.

- 12px OpenSans plain for noting data source(s), typically gray but can adapt as needed, and typically at the bottom of the graphic.

- OpenSans (Normal, Bold, Italic) for all other fonts, adapt as needed based on design needs of the graphic

- If your graphic has a embedded raster, make sure that the raster is at least twice the resolution as the graphic width (e.g. if designing for a 360px wide graphic, the raster layer should be crisp at 720px). This is for mobile view.

- To convert, run `svg-conversion.py` with the design `.svg` as an input. Export to a subfolder in `/static` to then load into the component. This process flattens all non-text layers into a single raster to allow for faster uploading in most cases.

- `GraphicSingle` loads the output `.svg` depending on screen size (e.g. the 360px wide graphic on smaller screens)

- `GraphicMultiple` loads multiple 360px wide graphics and orders them in a grid depending on screen size

- Both of the above incorporate a type of lazy loading



### Custom charts and maps

If the above is limiting, use D3, MapLibre, or whatever other JavaScript libraries to design any custom static, interactive, and/or animated maps and visualizations we want.

Some tips:

- Try to have svelte do most of the DOM work if needed, rather than things like `d3.select`. Check out this [post](https://v4.connorrothschild.com/post/svelte-and-d3) for details.

- Make sure to load in `global-styles.css` for style / font consistency across all content.

- 20px margins for most graphics.

- 24px TradeGothicBold black title, typically top-left corner aligned. Align with body paragraph text.

- 12px OpenSans plain for data source, typically gray but can adapt as needed, typically at the bottom of the graphic.

- Make sure to test on multiple screen sizes and browsers.

- Make sure we are not loading too much data to the browser, especially on initial load. `5mb` soft limit, `10mb` hard limit for all data loaded on entire web-page for initial load.



### Scrollytelling

- Copy over Scott's component to start



### Footnotes

Tooling for footnotes and an associated reference list on a page. 

- `fns = []` an array set in the `<script>` of your `+page.svelte` with each reference text

- `Footnote` for an individual footnote with an index to this array

- `Footnotes` generates the reference list

- `footnoteUtils.js` functions to run the above :)

To do! add a hover function, like Wikipedia


### Password

`Password` protects a page. For hiding in-development content.



### Other text components to create

- Quotation big

- Quotation small

- Big number

- Password