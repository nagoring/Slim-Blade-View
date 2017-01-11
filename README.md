# Slim-Blade-View

[![Build Status](https://travis-ci.org/rubellum/Slim-Blade-View.svg?branch=master)](https://travis-ci.org/rubellum/Slim-Blade-View)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This is a Slim Framework view helper built on top of the Blade component.

You can use this component to create and render templates in your Slim Framework application.

## Install

Via [Composer](https://getcomposer.org/)

```
$ composer require hiropeke/slim-blade-view
```

Requires Slim Framework 3 and PHP 5.5.0 or newer.

## Usage

```
// Slim Settings
$config = [
    'settings' => [
        'displayErrorDetails' => true, // set to false in production

        // Renderer settings
        'renderer'            => [
            'blade_template_path' => 'path/to/views', // String or array of multiple paths
            'blade_cache_path'    => 'path/to/cache', // Mandatory by default, though could probably turn caching off for development
        ],
    ],
];

// Create Slim app
$app = new \Slim\App($config);

// Fetch DI Container
$container = $app->getContainer();

// Register Blade View helper
$container['view'] = function ($container) {
    return new \Slim\Views\Blade(
        $container['settings']['renderer']['blade_template_path'],
        $container['settings']['renderer']['blade_cache_path']
    );
};

// Define named route
$app->get('/hello/{name}/', function ($request, $response, $args) {
    return $this->view->render($response, 'profile', [
        'name' => $args['name'],
    ]);
})->setName('profile');

// Run app
$app->run();
```

## Testing

```
$ phpunit
```

## License

The MIT License (MIT). Please see [License File](LICENSE) for more information.
