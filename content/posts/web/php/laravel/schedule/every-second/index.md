---
title: "laravel schedule run every second"
date: 2025-05-16T17:27:38Z
authors: ["pashamray"]
description: "laravel schedule run every second"
tags: ["php", "laravel", "gist"]
---
```php
<?php

declare(strict_types=1);

namespace App\Console;

class Kernel extends ConsoleKernel
{
    /**
     * Define the application's command schedule.
     */
    protected function schedule(Schedule $schedule): void
    {
        // Run call every second
        $schedule->call(static function (int $seconds) use ($schedule) {
            $dt = Carbon::now();
            $x = 60 / $seconds;

            do {
                app('log')->debug('Run call with params:', ['seconds' => $seconds]);

                $schedule->command(YourCommand::class, ['--force', '--param', 123])->withoutOverlapping(1);

                time_sleep_until((float) $dt->addSeconds($seconds)->timestamp);
            } while ($x-- > 0);
        }, ['seconds' => 1])->everyMinute();
    }
}
```

#### refs
https://laracasts.com/discuss/channels/laravel/how-to-run-scheduling-every-2-sec
