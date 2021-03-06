# Tone generator with the PWM peripheral

This package implements methods to use a PWM peripheral as a tone generator
ready to connect a passive buzzer to a MCU pin. It generates a square wave
of the specified frequency and 50% duty cycle.

It depends on the PWM abstract driver provided by [Apache
Mynewt](https://github.com/apache/mynewt-core). Review if [the PWM driver
interface](https://github.com/apache/mynewt-core/tree/master/hw/drivers/pwm)
is implemented for your platform.

## Synopsis

Usage:

```
/* enable buzzer tone at 2 KHz frequency */
buzzer_tone_on(2000);

/* disable tone generation */
buzzer_tone_off();

```

Configuration:

```
syscfg.vals:

    # required:
    BUZZER_PIN: 18

    # optional (default):
    BUZZER_PWM: '"pwm0"'

    # activate PWM device (if your BSP does not it)
    PWM_0: 1
```

## Setup

Add the repository to the project:

```
project.repositories:
    - apache-mynewt-core
    - treboada-driver-buzzer

repository.treboada-driver-buzzer:
    type: github
    vers: 1-latest
    user: treboada
    repo: mynewt-driver-buzzer
```

Upgrade project dependencies and create a new target (with your BSP and app):

```
newt upgrade
newt target create buzzer-test
newt target set buzzer-test \
    bsp=@apache-mynewt-core/hw/bsp/nordic_pca10040 \
    app=@treboada-driver-buzzer/apps/beep \
    build_profile=debug
```

## Support

Issues? https://github.com/Treboada/mynewt-driver-buzzer/issues

## License

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

