# JmikolaImagineBundle

This bundle provides a RelativeResize filter for [Imagine][] and a corresponding
loader for use with [AvalancheImagineBundle][]. It also provides a loader for
the basic Resize filter.

## Installation

### Submodule Creation

Add JmikolaImagineBundle to your `vendor/` directory:

``` bash
$ git submodule add https://github.com/jmikola/JmikolaImagineBundle.git vendor/bundles/Jmikola/ImagineBundle
```

### Class Autoloading

Register the "Jmikola" namespace prefix in your project's `autoload.php`:

``` php
# app/autoload.php

$loader->registerNamespaces(array(
    'Jmikola' => __DIR__'/../vendor/bundles',
));
```

### Application Kernel

Add JmikolaImagineBundle to the `registerBundles()` method of your application
kernel.

``` php
# app/AppKernel.php

public function registerBundles()
{
    $bundles[] = new Jmikola\ImagineBundle\JmikolaImagineBundle();
}
```

## Configuration

There are no configuration options. Symfony2 will load the bundle's dependency
injection extension automatically.

Tagged filter loaders will be picked up by AvalancheImagineBundle's compiler
pass and made available for use in its configuration.

## Filters

### Resize

The `resize` filter may be used to simply change the width and height of an
image irrespective of its proportions.

Consider the following configuration example, which defines two filters to alter
an image to an exact screen resolution:

``` yaml
avalanche_imagine:
    filters:
        cga:
            type:    resize
            options: { size: [320, 200] }
        wuxga:
            type:    resize
            options: { size: [1920, 1200] }
```

### RelativeResize

The `relative_resize` filter may be used to `heighten`, `widen`, `increase` or
`scale` an image with respect to its existing dimensions. These options directly
correspond to methods on Imagine's `BoxInterface`.

Given an input image sized 50x40 (width, height), consider the following
annotated configuration examples:

``` yaml
avalanche_imagine:
    filters:
        heighten:
            type:    relative_resize
            options: { heighten: 60 } # Transforms 50x40 to 75x60
        widen:
            type:    relative_resize
            options: { widen: 32 }    # Transforms 50x40 to 40x32
        increase:
            type:    relative_resize
            options: { increase: 10 } # Transforms 50x40 to 60x50
        scale:
            type:    relative_resize
            options: { scale: 2.5 }   # Transforms 50x40 to 125x100
```

If you prefer using Imagine without a filter configuration, the `RelativeResize`
class may be used directly.

  [Imagine]: https://github.com/avalanche123/Imagine
  [AvalancheImagineBundle]: https://github.com/avalanche123/AvalancheImagineBundle
