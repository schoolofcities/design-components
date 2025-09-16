
# Design components

Guidelines and building blocks for creating print and web-based maps, charts, info-graphics, data stories / story maps, and dashboards at the School of Cities.

If building a new web-based product, this repo can be duplicated to get started to have base styles (fonts, colours, etc.) and components loaded.

This doc has 3 sections:

1. **Visualization design guidelines**: Overall rules and recommendations for designing individual maps, charts, and related graphics.

2. **Print design guidelines**: Specific details and guidelines for when designing visualizations for *print* or `.pdf`

3. **Web design components**: A slew of Svelte components and workflows for building web-pages that include data visualizations, maps, and related graphics. These can be used as building blocks when starting a new web-based project.

Note that this repository and its design guidelines and components is a *living* project. As we continue to work on projects, we'll update this doc with additional advice, update existing web components as needed, as well as add new components if they have potential in being generalized for use in future work. 


# 1. Visualization design guidelines


### Colours

We use [UofT brand colours](https://brand.utoronto.ca/document/13#/colours/colours) form most graphics.

Then as needed, we often create gradients between these for graphics requiring colour ramps and scales. Can parse out mid-points for if we have binned data (e.g. a choropleth map with 5 bins, use 20% marks along the gradients)

In terms of accessibility...

- Check if graphic is colourblind safe. Many software and tools have filters for this. [This is also a good tool](https://www.color-blindness.com/coblis-color-blindness-simulator/)

- Check [contrast ratios](https://webaim.org/resources/contrastchecker/) of colours anytime text or graphic elements are overlaid onto each other. If there is a low ratio, hard to read, and try to adjust.



### Fonts

Here are the main font families we use:

- Titles: `TradeGothicBold`
- Sans-Serif: `OpenSans` 
- Serif: `SourceSerifPro`

For charts and maps, use `OpenSans` for most labels and text, `TradeGothicBold` for titles and subtitles. 

We use `SourceSerifPro` for body text, paragraphs, etc.

For maps, use italics to label natural features (water, mountains) and non-italic for human features (buildings, neighbourhoods, etc.). 

For maps and charts, try to have a hierarchy of labels, e.g. smaller more faint labels for background layers or reference information, and bolder larger labels for key data points.

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

- Do research, exploration, etc. to see how others have visualized similar data.




# 2. Print design constraints

When designing graphics, charts, and maps for `.pdf` reports or other *print* formats follow the visual guidelines above, but with the following constraints

- For portrait layouts (i.e. most reports that we do)

	- Width: 3.4 inches (half page) or 6.8 inches (full page).

	- Max height: 8.5 inches. Feel free to adjust height to best fit the graphic and limit excess white space (as long as it is less than the max)

- For gridded landscape layouts (e.g. LUC case studies). Design to fit in quarters, half, or full page space.

	- Height: 6.8 inch (full) or 3.4 inch (half)

	- Width: 9.3 inch (full) or 4.65 inch (half)

- CRIs are pretty flexible since the layouts are more custom designed. Can be any size that best fits the graphic, but do not exceed the following

	- Max width: 10 inch

	- Max height: 7.8 inch


- Select fonts that would be the same or pair well with those used in broader report layout design. Fallback to using TradeGothicBold for titles and OpenSans for all other text (e.g. axis labels, legend text, etc.) if layout design isn't set or ready or want something standard to previous SofC work.

- No fonts smaller than 8pt.

- Select colours (from the colour options noted above) that align well with broader layout design if available. 

- Note all data sources used to create the graphic, near the bottom in smaller font is usually best.

- If designing multiple graphics for the same publication or series, use similar visual language across all graphics (e.g. same font type size and colour for city labels, same fonts for data sources, same line width and colours for transit lines, etc.).



# 3. Web design components

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

	- `text` main body text

	- `callout` for callout boxes that are important written context but a bit separate from main flow of text

	- `details` smaller paragraph text for details, e.g. about data, methods, etc.

	- `caption` small text meant to provide captions/author/data sources for individual graphic items (e.g. a photograph, chart, etc.). This is also used by the `Image` components noted below.



### Title components

We have a few options for what a title / top of a page would look like

- `TitleStandard` A simple title with option for adding a subtitle.

- `LogoTop` A simple component for placing a logo at the top the page. Use in conjunction with TitleStandard. 

- `TitleHalfSplit` A 50/50 split title with an image. This splits depending on orientation. e.g. if landscape it splits left-right, if portrait it splits top-bottom. Includes a logo. 

- `TitleHalfSplitVideo` A 50/50 split title with an video. This splits depending on orientation. e.g. if landscape it splits left-right, if portrait it splits top-bottom. Includes a logo.


- `TitleFullPage`, a full page image with an overlay title text.

- `AuthorDate` a simple component with author and date information to load below the title.

Of course we can design new titles, but try to keep the same title and subtitle fonts. Trade Gothic Bold for title and Source Serif Italic for subtitle.



### Images and videos

For loading photographs and other raster images (i.e. no selectable text or other interactivity)

- `ImageSingle` a simple component that lazy loads a raster imag (e.g. `.png`, `.jpg`, etc.) from a URL. Make sure to have a caption and state the source. Can specify the max-width of the image. Note that `.png` is larger file size. Try to use `.jpg` or `.webp`.

- `VideoSingle` a simple component for a video from a URL. Make sure to have a caption and state the source. Can specify the max-width of the image, playback speed, and if want to auto play or have video controls. Generally use `.mp4`.



### Static graphic components

Workflow and component for creating *static* graphics, charts, and maps with selectable text. i.e. for graphics that don't require interactivity, dynamic data, or animation, but have labels that we want users to be able to copy/paste as needed.

- Create graphics in design software (e.g. Illustrator, Inkscape, etc) based on the visual design guidelines noted at the top of this page (e.g. colouring, labelling, etc.). Save as `.svg`

- Graphics should be designed at three specific pixel width sizes: 1080px, 720px, and 360px. If you want a larger graphic, e.g. at 1080px, you must include options for each of the smaller iterations so it can be viewed okay on smaller screens without odd size compression. If you only want to show a smaller graphic, e.g. at 360px wide, do not need to make larger versions.

Rules for all graphics:

- 20px margins for most graphics

- 24px TradeGothicBold black title, typically top-left corner aligned. i.e. 20px from top and 20px from left accounting for the margins.

- 12px OpenSans plain for noting data source(s), typically gray but can adapt as needed, and typically at the bottom of the graphic.

- OpenSans (Normal, Bold, Italic) for all other fonts, adapt based on design needs of the graphic

- If the graphic has a embedded raster, make sure that the raster is at least twice the resolution as the graphic width (e.g. if designing for a 360px wide graphic, the raster layer should be crisp at 720px). This is for mobile view which up-samples pixels.

- To convert to an optimized web view, run `svg-conversion.py` with the design `.svg` as an input. Export to a subfolder in `/static` to then load into the component. This process flattens all non-text layers into a single raster to allow for faster uploading in most cases.

There are two components for loading these graphics.

- `GraphicSingle` loads the output `.svg` depending on screen size (e.g. the 360px wide graphic on smaller screens)

- `GraphicMultiple` loads multiple 360px wide graphics and orders them in a grid depending on screen size

- Note that both of the above incorporate a type of lazy loading



### Custom charts and maps

If the above is limiting, use D3, MapLibre, or whatever other JavaScript libraries to design any custom static, dynamic, interactive, and/or animated maps and visualizations we want. Design each of these in its own component to then load onto a `+page.svelte`.

Some tips:

- Try to have Svelte do most of the DOM work if needed, rather than things like `d3.select`. Check out this [post](https://v4.connorrothschild.com/post/svelte-and-d3) for details.

- Make sure to load in `global-styles.css` for style, font, etc. consistency across all content.

- 20px margins for most graphics.

- 24px TradeGothicBold black title, typically top-left corner aligned. Try to align with body paragraph text where possible

- 12px OpenSans plain for data source, typically gray but can adapt as needed, typically at the bottom of the graphic.

- Make sure to test on multiple screen sizes and browsers.

- Make sure we are not loading too much data to the browser, especially on initial load. `5mb` soft limit, `10mb` hard limit for all data loaded on entire web-page for initial load.



### Scrollytelling

- `ScrollyImage` - scrollytelling component that has frames of fading in/out background (an image) and foreground scrolling text or other html content if needed (e.g. other photos). Can adjust left-center-right position of both foreground and background, as well as sizes (widths and heights) of these two pieces.



### Footnotes

Tooling for footnotes and an associated reference list on a page. 

- `fns = []` an array set in the `<script>` of your `+page.svelte` with each reference text

- `Footnote` for an individual footnote with an index to this array

- `Footnotes` generates the reference list

- `footnoteUtils.js` functions to run the above :)


### Password

`Password` protects a page. For hiding in-development content.



### Other text components to potentially create

- Quotation big

- Quotation small

- Big number

- Video options in titles

- Video option for scrolly-telling

- Lists (ordered and unordered)