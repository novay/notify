# Laravel Notify

[![Latest Stable Version](https://poser.pugx.org/novay/notify/v/stable)](https://packagist.org/packages/novay/notify)
[![Total Downloads](https://poser.pugx.org/novay/notify/downloads)](https://packagist.org/packages/novay/notify)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

![Notify](https://s3.amazonaws.com/s3.codecourse.com/github/banners/notify.png)

## Install

Using Composer

```
composer require novay/notify
```

Optionally add the service provider and the Facade to `config/app.php`

```php
Novay\Notify\NotifyServiceProvider::class,
```

```php
'Notify' => Novay\Notify\Facades\Notify::class,
```

> Note, there is a notify() function available, so unless you really want to use the Facade, there's no need to include it.

## Usage

### Basic

From your application, call the `flash` method with a message and type.

```php
notify()->flash('Welcome back!', 'success');
```

Within a view, you can now check if a flash message exists and output it.

```php
@if (notify()->ready())
    <div class="alert-box {{ notify()->type() }}">
        {{ notify()->message() }}
    </div>
@endif
```
> Notify is front-end framework agnostic, so you're free to easily implement the output however you choose.

### Options

You can pass additional options to the `flash` method, which are then easily accessible within your view.

```php
notify()->flash('Welcome back!', 'success', [
    'timer' => 3000,
    'text' => 'It\'s really great to see you again',
]);
```

Then, in your view.

```javascript
@if (notify()->ready())
    <script>
        swal({
            title: "{!! notify()->message() !!}",
            text: "{!! notify()->option('text') !!}",
            type: "{{ notify()->type() }}",
            @if (notify()->option('timer'))
                timer: {{ notify()->option('timer') }},
                showConfirmButton: false
            @endif
        });
    </script>
@endif
```

![SweetAlert example](https://s3.amazonaws.com/s3.codecourse.com/github/notify/swal-example.png)

> The above example uses SweetAlert, but the flexibily of Notify means you can easily use it with any JavaScript alert solution.

### License
Laravel Notify is licensed under the MIT license. Enjoy!