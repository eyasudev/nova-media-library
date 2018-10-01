# Laravel Advanced Nova Media Library

This package is designed to be used with the [awesome media library package from Spatie](https://github.com/spatie/laravel-medialibrary). 
It is inspired by the basic [nova media library](hhttps://github.com/jameslkingsley/nova-media-library) which lacks upload
of multiple images and ordering. This package is one of the dependencies, so you can use it beside this package.

## Model media configuration

Let's assume you configured your model to use the media library like following:
```php

public function registerMediaConversions(Media $media = null)
{
    $this->addMediaConversion('thumb')
        ->width(130)
        ->height(130);
}

public function registerMediaCollections()
{
    $this->addMediaCollection('main')->singleFile();
    $this->addMediaCollection('my_multi_collection');
}
```

## Single image upload

![Single image upload](docs/single-image.png)

```php
use Ebess\AdvancedNovaMediaLibrary\Fields\Images;

public function fields(Request $request)
{
    return [
        Images::make('Main image', 'main') // second parameter is the media collection name 
            ->thumbnail('thumb') // conversion used to display the image
            ->rules('required'), // validation rules
    ];
}
```

## Multiple image upload

If you enable the multiple upload ability, you can order the images via drag & drop.

![Multiple image upload](docs/multiple-image.png)

```php
use Ebess\AdvancedNovaMediaLibrary\Fields\Images;

    public function fields(Request $request)
    {
        return [
            Images::make('Images', 'my_multi_collection'), // second parameter is the media collection name
                ->thumbnail('thumb') // conversion used to display the image
                ->multiple() // enable upload of multiple images - also ordering
                ->fullSize() // full size column
                ->rules('required|size:3'), // validation rules for the collection of images
                // validation rules for the collection of images
                ->singleImageRules('dimension:min_width=100'),
        ];
    }
```

## File media management

To manage files just use the [nova media library](hhttps://github.com/jameslkingsley/nova-media-library) fields which
are already required in this package.

