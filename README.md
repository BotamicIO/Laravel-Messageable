# Laravel Messageable

[![Build Status](https://img.shields.io/travis/artisanry/Messageable/master.svg?style=flat-square)](https://travis-ci.org/artisanry/Messageable)
[![PHP from Packagist](https://img.shields.io/packagist/php-v/artisanry/messageable.svg?style=flat-square)]()
[![Latest Version](https://img.shields.io/github/release/artisanry/Messageable.svg?style=flat-square)](https://github.com/artisanry/Messageable/releases)
[![License](https://img.shields.io/packagist/l/artisanry/Messageable.svg?style=flat-square)](https://packagist.org/packages/artisanry/Messageable)

## Installation

Require this package, with [Composer](https://getcomposer.org/), in the root directory of your project.

``` bash
$ composer require artisanry/messageable
```

To get started, you'll need to publish the vendor assets and migrate:

```
php artisan vendor:publish --provider="Artisanry\Messagable\MessageableServiceProvider" && php artisan migrate
```

## Usage

## Setup a Model

``` php
<?php

namespace App;

use Artisanry\Messageable\HasMessages;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    use HasMessages;
}
```

## Examples

#### Create a new thread
``` php
Thread::create([
    'subject' => str_random(10),
]);
```

#### Add one message to a thread
``` php
$thread->addMessage([
    'body' => str_random(10),
], $user);
```

#### Add multiple messages to a thread
``` php
$thread->addMessage([
    [
        'data' => ['body' => str_random(10)],
        'creator' => User::find(1),
    ],
    [
        'data' => ['body' => str_random(10)],
        'creator' => User::find(2),
    ],
], $user);
```

#### Add one participant to a thread
``` php
$thread->addParticipant($user);
```

#### Add multiple participants to a thread
``` php
$thread->addParticipants([
    User::find(3), Organization::find(2), Player::find(4)
]);
```

#### Mark a thread as ready by the user
``` php
$thread->markAsRead($user);
```

#### Get all threads
``` php
Thread::getAllLatest()->get();
```

#### Get all threads that a user has participated in
``` php
Thread::forModel($user)->latest('updated_at')->get();
```

#### Get all threads that a user has participated in with new messages
``` php
Thread::forModelWithNewMessages($user)->latest('updated_at')->get();
```

#### Get the creator of a thread
``` php
$thread->creator();
```

#### Get the latest message of a thread
``` php
$thread->getLatestMessage();
```

#### Get an array of participant IDs and Types
``` php
$thread->participantsIdsAndTypes();
```

#### Check if the User Model hasn't read the latest message in the thread yet
``` php
$thread->isUnread($user);
```

#### Check if the User Model participated to the Thread
``` php
$thread->hasParticipant($user);
```

## Testing

``` bash
$ phpunit
```

## Security

If you discover a security vulnerability within this package, please send an e-mail to hello@basecode.sh. All security vulnerabilities will be promptly addressed.

## Credits

This project exists thanks to all the people who [contribute](../../contributors).

## License

Mozilla Public License Version 2.0 ([MPL-2.0](./LICENSE)).
