# Todoist OAuth2 Provider for Laravel Socialite

This allows you to use the [SocialiteProvider](https://socialiteproviders.github.io/) package for Laravel with the Todoist API. Only thing worth noting is that Todoist OAuth tokens do not expire, so you don't need to mess with refresh tokens. 

Be sure to add this repo to your Laravel's composer.json file in order to install this:
```
  "repositories":[
    {
      "type": "vcs",
      "url": "https://github.com/brynnb/Todoist"
    }
  ]
```

Then add this to the same composer.json file:
```
  "require": {
    ...//your other entries that are already here
    "socialiteproviders/todoist": "dev-master"
  },
```

When you `composer install` it will be installed in the same `/vendor/socialiteproviders` that the other "official" ones are installed in. 

Be sure to update your `/config/services.php`:
```
    'todoist' => [
        'client_id' => env('TODOIST_KEY'),
        'client_secret' => env('TODOIST_SECRET'),
        'redirect' => env('TODOIST_REDIRECT_URI'),
    ],
```

And also obviously include those three items to your `.env` file.

Finally, update your EventServiceProvider to have an entry similar to something like this:
```
    protected $listen = [
        'SocialiteProviders\Manager\SocialiteWasCalled' => [
            'SocialiteProviders\Todoist\TodoistExtendSocialite@handle'
            //and any others you might have here too
        ]
    ];
```

These are nearly the same steps you'd have installing any provider for SocialiteProviders, so if you have questions click the link above to view their documentation for more examples. 
