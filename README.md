# SVG to STL: how to turn a flat vector into a printable model

*Unofficial community guide for SVG to STL conversion. Not affiliated with svg2stl.com, Meshy or ImageToStl. All trademarks belong to their owners.*

Converting svg to stl is the quickest route from a logo, a badge or a line drawing to something a 3D printer can slice. The three tools that currently rank for the query all do the same basic thing: take the filled shapes in an SVG file, extrude them by a chosen height, and hand back an STL. This guide walks through that workflow, what each tool says about how it handles your files, and the cases where extruding a vector is the wrong starting point.

> Working from a picture rather than a vector file? [Try Supavoxel - image to 3D in the browser](https://supavoxel.com?utm_source=github&utm_medium=ugc&utm_campaign=svg-to-stl&utm_content=readme-top&utm_term=tier-r) turns a photo or a rendered image into an STL or GLB mesh without opening a CAD program. Keep reading for the SVG route.

## What SVG to STL conversion is

An SVG describes 2D geometry: paths, circles, rectangles, text and groups, with no thickness. An STL describes a closed surface made of triangles, which is what slicers expect. Conversion means giving every filled 2D region a height so the shape becomes a solid. svg2stl.com puts it plainly: "often it is enough to extrude 2d drawings in order to get a nice 3D printable design". It also names the reason people search for this in the first place: "the conversion from SVG to STL can be frustrating if one does not know the proper tools to use".

The tools differ mostly in where the work happens and what they do with your file. svg2stl.com processes on the server and states that it converts the SVG to EPS, then DXF, then SCAD, and finally STL. Meshy's converter states that files are "processed locally in your browser" and "never uploaded to our servers". ImageToStl offers SVG to STL as one entry in a long list of image, vector, CAD and 3D model conversions, next to a browser-based model editor and an STL viewer.

## How to get started

**svg2stl.com (server-side, three steps)**

1. Select an SVG from your computer and upload it. The site notes that the SVG is cleaned and unnecessary tags are removed behind the scenes.
2. Set an extrusion height. The server runs the SVG through EPS, DXF and SCAD before producing the STL.
3. Inspect the generated STL in the built-in viewer and download it. The [gallery](https://svg2stl.com/gallery) shows what other people have converted.

**Meshy free SVG to STL converter (browser-side)**

1. Open the [SVG to STL converter](https://www.meshy.ai/3d-tools/file-converter/svg/to/stl) and drag and drop a `.svg` file, or click to upload. The page lists a 50 MB maximum file size.
2. The conversion runs in the browser; the page says no software download is required on your device.
3. Download the STL. Single-file mode is the default; batch mode is labelled PRO.

**ImageToStl (browser-based converter with extra tools)**

1. Open the [SVG to STL page](https://imagetostl.com/convert/file/svg/to/stl) and upload the file.
2. Download the STL, or open it in the site's [online STL viewer](https://imagetostl.com/view-stl-online) or [3D model designer](https://imagetostl.com/editor) to check it before slicing.

## Pricing and limits

- svg2stl.com shows no price on its page. Its upload terms are the thing to read: your SVG and the generated STL are "saved on the server for at least one week", "anyone with a link can view both", and all uploaded and generated files fall under the [WTFPL license](http://www.wtfpl.net/txt/copying/).
- Meshy's converter page is titled "Free SVG to STL Converter", lists a 50 MB file size limit, and marks batch conversion as PRO. Check the [Meshy pricing page](https://www.meshy.ai/pricing) for what PRO costs.
- ImageToStl's converter page does not show pricing in the crawled snapshot; check the site for current terms.

## Practical notes and gotchas

1. **Extrusion gives you a plate, not a sculpture.** Every filled region gets the same height. If the artwork has overlapping fills, decide before converting which one should win, because the tools do not ask.
2. **Clean the SVG yourself first.** svg2stl.com strips unnecessary tags on upload, but the safest input for any converter is a file with outlined text, flattened groups and no embedded raster images. The `check_svg.py` script in the companion examples repo lists what a file contains.
3. **Know where your file goes.** svg2stl.com keeps files on its server for at least a week and makes them viewable by link; Meshy says the file never leaves your browser. For client logos or unreleased designs, that difference matters.
4. **Read the licence line.** svg2stl.com applies the WTFPL to uploaded and generated files. If you cannot accept that for a given asset, use a local or browser-side route instead.
5. **Check the STL before slicing.** All three sites give you a viewer. Look for missing islands (small shapes that vanished) and filled-in holes (the counters in letters like O and A).
6. **Verify the scale in your slicer.** An SVG's coordinate system does not carry a guaranteed physical unit, so confirm the model's width in millimetres before printing.

## Comparison

| | svg2stl.com | Meshy SVG to STL | ImageToStl | Supavoxel |
| --- | --- | --- | --- | --- |
| Input | SVG | SVG (50 MB max) | SVG plus many image, vector, CAD and 3D formats | A picture (photo or render) |
| Where processing happens | On the server | In the browser | Not stated on the crawled page | In the browser |
| File retention | At least one week, viewable by link | Never uploaded | Not stated | Not stated here; check the site |
| Extrusion height control | Yes, set before converting | Not stated | Not stated | Not an extrusion; generates a mesh from the image |
| Output | STL | STL | STL | STL or GLB |

## FAQ

**Is svg to stl conversion free?** svg2stl.com shows no price. Meshy's converter page is labelled free for single files and marks batch mode as PRO. ImageToStl does not show pricing on the converter page, so check the site.

**Does the SVG need closed, filled paths?** Extrusion only works on regions that have area. Open strokes with no fill have nothing to extrude, so convert strokes to outlines in your vector editor before uploading.

**Can I convert a PNG or JPG the same way?** ImageToStl lists PNG to STL and JPG to STL converters alongside the SVG one, which treat the image as a flat shape. If you want an actual three-dimensional object from a picture rather than a traced plate, that is what Supavoxel does.

**Which tool for a quick logo plate?** svg2stl.com is the most direct: upload, pick a height, download. Use Meshy if you do not want the file to leave your machine.

**Can I batch convert?** Meshy marks batch mode as PRO, and svg2stl.com is a one-file-at-a-time flow. The examples repo has an OpenSCAD script that loops over a folder locally.

## When an SVG is the wrong starting point

Every tool above produces the same kind of object: a 2D outline pushed up into a slab. That is exactly right for keychains, stencils, cookie cutters and sign lettering. It is the wrong tool when the thing you have is a photo of an object, a product render or a character drawing and what you want is a model with real depth. For that case, [try Supavoxel - image to 3D, STL/GLB in the browser, no CAD](https://supavoxel.com?utm_source=github&utm_medium=ugc&utm_campaign=svg-to-stl&utm_content=readme-top&utm_term=tier-r). Upload the picture, get a mesh, and open it in the same slicer you would use for the STL files this guide covers.


_Last reviewed: 2026-09-22_
