> ⚠️ The functionality described in this README will be available with **v1.0.0**<br/>**This is a WIP!** API and features may change

# React Media Components

**React Media Components** is a library with the goal to provide easy to use, portable and fast media components for your React app.

## Key features

- 🌄 **Image component** to render images in a picture tag with all the required formats and sizes.

_**Coming soon**_

- 🎬 _**Video component** to render videos with a video tag using next gen formats and different resolutions._
- 🔊 _**Audio component** to render audio files in an audio tag using next gen formats and different sound qualities._

## Installation

```bash
npm install react-media-components
# or
yarn add react-media-components
```

## Usage

To use the image component you can simply import it and use it inside your components return statement. You can use `sizes` and `formats` props to render the image in the formats and sizes you need. You can also apply any known [img attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attributes) you want, like for example the `alt` or `style` attribute.

```jsx
import { Image } from "react-media-components";

const YourComponent = () => {
  return (
    // v1.0.0 (sizes, formats and quality are set via config file)
    <Image src="/path/to/image.png" />
  );
};
```

The example from above renders the following HTML:

```html
<picture>
  <source media="(min-width:1024px)" srcset="image-1200.avif" type="image/avif" />
  <source media="(min-width:1024px)" srcset="image-1200.webp" type="image/webp" />

  <source media="(min-width:768px)" srcset="image-1024.avif" type="image/avif" />
  <source media="(min-width:768px)" srcset="image-1024.webp" type="image/webp" />

  <source media="(min-width:414px)" srcset="image-768.avif" type="image/avif" />
  <source media="(min-width:414px)" srcset="image-768.webp" type="image/webp" />

  <source srcset="image-414.avif" type="image/avif" />
  <img src="image-414.webp" alt="foobar" />
</picture>
```

## Config
### Default config

Out of the box the default configurations from the code block below are applied. 

<!-- You can also overwrite the configs directly on the component using the [custom props](#props). -->

```json
{
  "image": {
    "sizes": {
      "0": "414", // screens from 0px to 414px will have image of 414px
      "414": "768", // screens from 414px to 768px will have image of 768px
      "768": "1024", // screens from 768px to 1024px will have image of 1024px
      "1024": "1200", // screens from 1024px to 1200px will have image of 1200px
      "1200": "1920" // screens from 1200px to ∞px will have image of 1920px
    },
    "formats": ["AVIF", "WebP"],
    "quality": 70
  }
}
```

### Custom config

We use [`cosmiconfig`](https://github.com/davidtheclark/cosmiconfig) to fetch your custom config. 
This means you can add your custom config by adding a `rmcrc` property in your `package.json` or by creating a `rmcrc.json` file in your project root directory. 
Other config file types/names are also possible as described in the `cosmiconfig` readme.

### Options

| Key             | Type                                                         | Default                                                                       | Description                                                                                                                                                                                                                                                                                                                                                  |
| --------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `image.sizes`   | `{ string: string }`                                         | `{ "0": "414", "414": "768", "768": "1024", "1024": "1200", "1200": "1920" }` | The breakpoints and the associated image widths. The **key is the breakpoint** and the **value is the image width**. The images are loaded in the specified image width as soon as the specified breakpoint is reached. For example the following config `{ "980": "900" }` will render **900px** wide images for screens that are **980px** wide or bigger. |
| `image.formats` | `["APNG", "AVIF", "GIF", "JPEG", "PNG", "WebP", "SRC_TYPE"]` | `["AVIF", "Webp"]`                                                            | The [image file types](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Image_types) your images will be rendered in. To use the original file type you provided in the `src` attribute you can use `SRC_TYPE`.                                                                                                                                    |
| `image.quality` | `number`                                                     | `70`                                                                          | The quality your images will be rendered in. With `70`% you save a lot of data without any noticable quality differences. If you don't want to compress your images at all you can set the value to `100`%.                                                                                                                                                  |

<!-- // "deviceSizes": [414, 768, 1024, 1200],
// "imageSizes": [414, 768, 1024, 1200], -->
<!-- | `image.deviceSizes` | `[number]`                                                   | `[414, 768, 1024, 1200]` | This goes hand in hand with `image.imageSizes`. Those are the breakpoints to switch to the next bigger image. the image size itself is defined in the `image.imageSizes` array. For example a `414px` wide image is used for devices between `0px` and `414px`. Or a `768px` wide image for devices between `414px` and `768px`. And so on. Check out this [visual example](https://www.w3schools.com/TAGS/tryit.asp?filename=tryhtml5_picture) if you're feeling confused. | -->
<!-- | `image.imageSizes`  | `[number]`                                                   | `[414, 768, 1024, 1200]` | This goes hand in hand with `image.deviceSizes`. Breakpoints used to render the different image sizes. For example a `414px` wide image is used for devices between `0px` and `414px`. Or a `768px` wide image for devices between `414px` and `768px`. And so on. Check out this [visual example](https://www.w3schools.com/TAGS/tryit.asp?filename=tryhtml5_picture) if you're feeling confused. | -->
<!-- | `image.maxSize`     | `number`                                                     | `1920`                   | The absolute max width your images should be rendered in. If you have a 100% wide image on your website it will be perfect until `1920px` after that it gets stretched and might become blurry.                                                                                                                                                   | -->

## Props

You can apply any known [img attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attributes).

<!-- To customize (e.g. the sizes) of a single image you can overwrite the global configs by applying the props as described in the table below. -->

| Attributes | Type     | Default | Description                        |
| ---------- | -------- | ------- | ---------------------------------- |
| src        | `string` | `null`  | The path to your image.            |
|            |          |         | _More custom props coming soon..._ |

<!-- | formats    | `Array<ImageType>` | `["AVIF", "WebP", src format]` | The formats your image will be rendered in | -->
<!-- | sizes      | `Array<number>`    | `[375, 768, 1024]`             | The sizes your image will render in        | -->

## Contributors

Big thanks to all our contributors who made this projcect possible.

[![](https://github.com/faessler.png?size=50)](https://github.com/faessler)
[![](https://github.com/sirtobey.png?size=50)](https://github.com/sirtobey)
[![](https://github.com/wityan.png?size=50)](https://github.com/wityan)
