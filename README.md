# faced

faced is a light-weight library to identify faces and it's features such as eyes, nose and mouth. It requires opencv.

## Install

### As a dependency to your project
Just add `"faced": "~1.1",` to your dependencies list in `package.json`.

### Globally
`npm install -g faced`

## Identify your first face

```javascript
var faced = new Faced();
faced.detect('image.jpg', function (faces, image, file) {
  if (!faces) {
    return console.log("No faces found!");
  }

  var face = sface[0];

  console.log(
    "Found a face at %d,%d with dimensions %dx%d",
    face.getX(),
    face.getY(),
    face.getWidth(),
    face.getHeight()
  );

  console.log(
    "What a pretty face, it %s a mouth, it %s a nose, it % a left eye and it %s a right eye!",
    face.getMouth() ? "has" : "does not have",
    face.getNose() ? "has" : "does not have",
    face.getEyeLeft() ? "has" : "does not have",
    face.getEyeRight() ? "has" : "does not have",
  );
});
```

## API

### Faced.detect(path, function, context)

Loads an image from the given `path` and executes `function` upon completion.

The callback function expects a prototype like `function (faces, image, file) { }`, where the first is an array of `Face`, the second is a `Matrix` [object from opencv](https://npmjs.org/package/opencv#readme) and the third is the path of the image.

In case of error the arguments `faces` and `image` will be `undefined`.

### Class `Feature`
 - `Feature.getX()` Returns the upper left corner X position of the face
 - `Feature.getY()` Returns the upper left corner Y position of the face
 - `Feature.getX2()` Returns the lower right corner X position of the face
 - `Feature.getY2()` Returns the lower right conrner Y position of the face
 - `Feature.getWidth()` Returns the width
 - `Feature.getHeight()` Returns the height
 - `Feature.intersect(Feature)` Returns the percentage of shared spaced that the current feature has with the given argument Feature. *Although this is used internally it might be useful for client usage.*

### Class `Face` (extends `Feature`)

All of the following method1s return an instance of `Feture` or `undefined` if it could not detect.

 - `Face.getMouth()`
 - `Face.getNose()`
 - `Face.getEyeLeft()`
 - `Face.getEyeRight()`

Other significant methods

 - `Face.getFeature(name)` Returns a feature by name. Possible names are: `mouth`, `nose`, `eyeLeft` and `eyeRight`.
 - `Face.getFeatures()` Returns an array of `Feature` that the instance has detected.
 - `Face.getFeatureCount()` Returns the number of detected features.

## Examples

```bash
$ node examples/identify.js images/lenna.png
```

Then open `images/lenna.features.png` on your favourite image viewer.

## Information

#### License

faced is licensed under the [MIT license](http://opensource.org/licenses/MIT)

#### Copyright

Copyright (c) 2013, Samuel Gordalina <samuel.gordalina@gmail.com>