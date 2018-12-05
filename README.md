<a href="https://luehangs.site/lue_hang/projects/react-native-image-layout"><img src="https://luehangs.site/images/react-native-image-layout-main.jpg" alt="react-native-image-layout"/></a>

> An easy and simple to use React Native component to render a custom masonry layout for remote images and displayed on a custom interactive image viewer. Includes animations and support for both iOS and Android. Free and made possible along with costly maintenance and updates by [Lue Hang](https://www.facebook.com/lue.hang) (the author).

<a href="https://luehangs.site"><img src="https://luehangs.site/images/lh-blog-strip.jpg" alt="LH BLOG"/></a>

![react-native-image-layout](https://www.luehangs.site/videos/react-native-image-layout-demo.gif)

Learn more about React Native with project examples along with Cyber Security and Ethical Hacking at [LH BLOG](https://www.luehangs.site).

Built with [`react-native-gallery-swiper`](https://npmjs.com/package/react-native-gallery-swiper).

## Index

- [Install](#install)
- [Usage Example](#usage-example)
- [API](#api)
- [Props](#props)
- [Scroll State and Events](#scroll-state-and-events)
- [Example Project](#example-project)
- [Author](#author)
- [Contribute](#contribute)
- [License](#license)

## Install

Type in the following to the command line to install the dependency.

```bash
$ npm install --save react-native-image-layout
```

or

```bash
$ yarn add react-native-image-layout
```

## Usage Example

Add an ``import`` to the top of the file.  At minimal, declare the ``ImageLayout`` component in the ``render()`` method providing an array of data for the ``images`` prop.

```javascript
import ImageLayout from "react-native-image-layout";

//...
render() {
    return (
        <ImageLayout
            images={[
                { uri: "https://luehangs.site/pic-chat-app-images/animals-avian-beach-760984.jpg" },
                { uri: "https://luehangs.site/pic-chat-app-images/beautiful-blond-blonde-hair-478544.jpg",
                    // Version *2.0.0 update (or greater versions):
                    // Optional: Does not require an id for each
                    // image object, but is for best practices and
                    // can be better for performance with the API.
                    id: "blpccx4cn" },
                { uri: "https://luehangs.site/pic-chat-app-images/beautiful-beautiful-women-beauty-40901.jpg",
                    // Optional: Adding a dimensions field with
                    // the actual width and height for REMOTE IMAGES
                    // will help improve performance.
                    dimensions: { width: 1080, height: 1920 }
                },
                { uri: "https://luehangs.site/pic-chat-app-images/beautiful-blond-fishnet-stockings-48134.jpg" },
                { uri: "https://luehangs.site/pic-chat-app-images/beautiful-beautiful-woman-beauty-9763.jpg" },
                { uri: "https://luehangs.site/pic-chat-app-images/attractive-balance-beautiful-186263.jpg" },
            ]}
        />
    );
}
//...
```

To select, callback and manipulate an image...

```javascript
import ImageLayout from "react-native-image-layout";
//...

//...
_renderPageHeader = (image, index, onClose) => {
    // Individual image object data.
    console.log(image);
    return (
        <View>
            {/*
                onClose params (third params) is a function
                that will close the react-native-gallery-swiper.

                Swiping up and down animations for closing the
                gallery is only compatible with iOS at
                the moment.  It will be compatible with
                Android in future releases.
            */}
            <TouchableWithoutFeedback onPress={() => {onClose();}}>
                <Image
                    source={backIcon}
                    style={{marginLeft: 10, height: 30, width: 30}}
                />
            </TouchableWithoutFeedback>
            <Text>{image.filename}</Text>
        </View>
    );
}

render() {
    return (
        <ImageLayout
            renderPageHeader={this._renderPageHeader}
            images={[
                { uri: "https://luehangs.site/pic-chat-app-images/beautiful-blond-fishnet-stockings-48134.jpg" },
                { uri: "https://luehangs.site/pic-chat-app-images/beautiful-beautiful-woman-beauty-9763.jpg" },
                { uri: "https://luehangs.site/pic-chat-app-images/attractive-balance-beautiful-186263.jpg" },
            ]}
        />
    );
}
//...
```

<a href="https://luehangs.site"><img src="https://luehangs.site/images/lh-blog-strip.jpg" alt="LH BLOG"/></a>

## API

``<ImageLayout />`` component accepts the following props...

### Props

> Version *2.0.0 update (or greater versions):  Props changes that may not be compatible with lower versions.

| Props                         | Description                                                                                                                                                                                    | Type              | Default |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|---------|
| `images`                      | An array of objects.  `uri` is a required field. EX. `[{uri: "https://luehangs.site/pic-chat-app-images/beautiful-blond-fishnet-stockings-48134.jpg"}, {uri: "https://luehangs.site/pic-chat-app-images/beautiful-blond-blonde-hair-478544.jpg"}]` | `Array` | Required |
| `columns`                     | Desired number of columns. | `number` | 2 |
| `spacing`                     | Gutter size of the column. The spacing is a multiplier of 1% of the available view. | `number` | 1 |
| `initialColToRender`          | How many columns to render in the initial batch. | `number` | 2 |
| `initialNumInColsToRender`    | How many items to render in each column in the initial batch. | `number` | 2 |
| `sorted`                      | Whether to sort the masonry data according to their index position or allow to fill in as soon as the `uri` is ready. | `Boolean` | false |
| `imageContainerStyle`         | The styles object which is added to the Image component. | `Object` | {} |
| `renderIndividualMasonryHeader` | Custom function that is executed **ABOVE** each individual masonry image.  First param is the individual data and second param is the index.  This function must return a React Component. | `Function` | |
| `renderIndividualMasonryFooter` | Custom function that is executed **BELOW** each individual masonry image.  First param is the individual data and second param is the index.  This function must return a React Component. | `Function` | |
| `masonryFlatListColProps`       | Props to be passed to the underlying `FlatList` masonry.  See [`FlatList` props...](https://facebook.github.io/react-native/docs/flatlist#props) | `Object` | {} |
| `imagePageComponent`          | Custom function to render the images for gallery.  First param is the image props and second param is the dimensions. | `Function` | `<Image/>` component |
| `errorPageComponent`          | Custom function to render the page of an image in gallery that couldn't be displayed. | `Function` | `<View/>` with stylized error |
| `renderPageHeader`            | Custom function to render gallery page header and must return a React Component.  First param is the individual data and second param is the index.  Third param is the onClose function to close gallery pages and return to the masonry layout. | `Function` | |
| `renderPageFooter`            | Custom function to render gallery page footer and must return a React Component.  First param is the individual data and second param is the index.  Third param is the onClose function to close gallery pages and return to the masonry layout. | `Function` | |
| `pagesFlatListProps`          | Props to be passed to the underlying `FlatList` gallery.  See [`FlatList` props...](https://facebook.github.io/react-native/docs/flatlist) | `Object` | {windowSize: 3} |
| `pageMargin`                  | Blank space to show between images in gallery. | `number` | 0 |
| `onPageSelected`              | Fired with the index of page that has been selected in gallery. | `Function` | |
| `onPageScrollStateChanged`    | Called when page scrolling state has changed in gallery.  See [scroll state and events...](#scroll-state-and-events) | `Function` | |
| `onPageScroll`                | Scroll event for page gallery.  See [scroll state and events...](#scroll-state-and-events) | `Function` | |
| `pageScrollViewStyle`         | Custom style for the `FlatList` component for gallery. | `Object` | {} |
| `onPageSingleTapConfirmed`    | Fired after a single tap on page in gallery. | `Function` | |
| `onPageLongPress`             | Fired after a long press on page in gallery. | `Function` | |

<a href="https://luehangs.site"><img src="https://luehangs.site/images/lh-blog-strip.jpg" alt="LH BLOG"/></a>

## Scroll State and Events for Gallery

Built with [`react-native-gallery-swiper`](https://npmjs.com/package/react-native-gallery-swiper).

* `onPageScroll` : (event) => {}. 

  The event object carries the following data: 

  * `position`:  index of first page from the left that is currently visible.
  * `offset`: value from range [0,1) describing stage between page transitions.
  * `fraction`: means that (1 - x) fraction of the page at "position" index is visible, and x fraction of the next page is visible.

* `onPageScrollStateChanged` : (state) => {}.

  Called when the page scrolling state has changed. The page scrolling state can be in 3 states:

  * `'idle'`: there is no interaction with the page scroller happening at the time.
  * `'dragging'`: there is currently an interaction with the page scroller.
  * `'settling'`: there was an interaction with the page scroller, and the page scroller is now finishing its closing or opening animation.

## Example Project

Perform steps 1-2 to run locally:

1. [Clone the Repo](#1-clone-the-repo)
2. [Install and Run](#2-install-and-run)

### 1. Clone the Repo

**Clone** `react-native-image-layout` locally. In a terminal, run:

```bash
$ git clone https://github.com/Luehang/react-native-image-layout.git react-native-image-layout
```

### 2. Install and Run

```bash
$ cd react-native-image-layout/example/
```

#### iOS - Mac - Install & Run

	1. check out the code
	2. npm install
	3. npm run ios

#### Android - Mac - Install & Run

	1. check out the code
	2. npm install
	3. emulator running in separate terminal
	4. npm run android

<a href="https://luehangs.site"><img src="https://luehangs.site/images/lh-blog-strip.jpg" alt="LH BLOG"/></a>

## Author

<a href="https://www.facebook.com/lue.hang">
<img src="https://www.luehangs.site/images/lue-hang2018-circle-150px.png"/>
</a>

Free and made possible along with costly maintenance and updates by [Lue Hang](https://www.facebook.com/lue.hang) (the author).

## Contribute

[Pull requests](https://github.com/Luehang/react-native-image-layout/pulls) are welcomed.

### Beginners

Not sure where to start, or a beginner? Take a look at the [issues page](https://github.com/Luehang/react-native-image-layout/issues).

### Contributors

Contributors will be posted here.

## License

MIT © [Lue Hang](https://luehangs.site), as found in the LICENSE file.
