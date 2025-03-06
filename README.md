# Simple Image Viewer

Simple image viewer component for React v19+

This is an in-place replacement fork of the original repository [react-simple-image-viewer](https://github.com/specter256/react-simple-image-viewer).
Apart from support for React version 19, some additional fixed and features have been added.

# Installation

```shell
$ npm install simple-image-viewer-react19
```
or
```shell
$ yarn add simple-image-viewer-react19
```

# Example

```jsx
import React, { useState, useCallback } from 'react';
import { render } from 'react-dom';
import ImageViewer from 'simple-image-viewer-react19';

function App() {
  const [currentImage, setCurrentImage] = useState(0);
  const [isViewerOpen, setIsViewerOpen] = useState(false);
  const images = [
    'https://picsum.photos/1200/800',
    'https://picsum.photos/800/1200',
    'https://picsum.photos/1920/1080',
    'https://picsum.photos/1500/500',
  ];
  const alts = [
    'Random image 1200 by 800',
    'Random image 800 by 1200',
    'Random image 1920 by 1080',
    'Random image 1500 by 500',
  ]

  const openImageViewer = useCallback((index) => {
    setCurrentImage(index);
    setIsViewerOpen(true);
  }, []);

  const closeImageViewer = () => {
    setCurrentImage(0);
    setIsViewerOpen(false);
  };

  return (
    <div>
      {images.map((src, index) => (
        <img
          src={ src }
          onClick={ () => openImageViewer(index) }
          width="300"
          key={ index }
          style={{ margin: '2px' }}
          alt={ alts[index] }
        />
      ))}

      {isViewerOpen && (
        <ImageViewer
          src={ images }
          alt={ alts }
          currentIndex={ currentImage }
          disableScroll={ false }
          closeOnClickOutside={ true }
          closeOnClickInside={ true }
          onClose={ closeImageViewer }
        />
      )}
    </div>
  );
}

render(<App />, document.getElementById('app'));
```
# API

| Property              |  Type         | Description                                                                       |
| :--------------       | :--------     | :-------------------------------------------------------------------------------- |
| src                   | string[]      | Array of image URLs                                                               |
| alt                   | string[]      | Array of alt texts                                                                |
| currentIndex          | number        | Index of image in `src` and `alt` property will be shown when viewer is open      |
| onClose               | function      | Callback which will be called when viewer will closed                             |
| backgroundStyle       | object        | Custom styles for background of modal window                                      |
| disableScroll         | boolean       | Disable scrolling images by mouse wheel                                           |
| closeOnClickOutside   | boolean       | Whether viewer should be closed when clicking outside of image                    |
| closeOnClickInside    | boolean       | Whether viewer should be closed when clicking inside image                        |
| closeComponent        | JSX.Element   | Custom component for the close button                                             |
| leftArrowComponent    | JSX.Element   | Custom component for the left arrow                                               |
| rightArrowComponent   | JSX.Element   | Custom component for the right arrow                                              |


# Shortcuts

| Shortcut        | Description                     |
| :-------------- | :------------------------------ |
| Escape          | Close the viewer                |
| Right Arrow / l | Next image                      |
| Left Arrow / h  | Previous image                  |
| Mouse wheel     | Scrolling previous / next image |


# Forked from original repository

[Github Repository](https://github.com/specter256/react-simple-image-viewer)
