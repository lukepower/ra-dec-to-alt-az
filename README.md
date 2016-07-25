RA/Dec to Alt/Az PHP Class
================

> This repository is a fork of [Tom Gillespy's RA/Dec to Alt/Az repository](https://github.com/tomgillespy), with the sole purpose of making the class `composer` installable. Some code refactoring was done, most importantly the class has been put into its own namespace.

This class converts celestial coordinates, along with the time, latitude and longditude to a altitude and azimuth for a telescope mount or camera.

##Installation

```bash
composer install leonboot/ra-dec-to-alt-az
```

##Usage

```php
require 'vendor/autoload.php';

use Radec\Calculator as radec;

$radec = new radec(radec::decimaldegrees(latitude), radec::decimaldegrees(longditude));

$radec->setradec(radec::decimaldegrees(right_ascention), radec::decimaldegrees(declination));

$time = strtotime('now');

$azimuth = $radec->getAZ($time);
$altitude = $radec->getALT($time);
```
##Other Functions

####Radec\Calculator::daysbeforeJ2000($timestamp)

This gives the number of days between $timestamp and the J2000 epoch. [Wikipedia Article](http://en.wikipedia.org/wiki/Epoch_(astronomy)#Julian_years_and_J2000)

####Radec\Calculator::getdecimalUT($timestamp)

This gives the universitl time in decimal form. All calculations in this are performed using decimals from degrees, minutes and seconds and the time equivalent (hours, minuites and seconds).

####Radec\Calculator::fractionalday($timestamp)

This just divides the UT by 24 to get the fraction of a day.

####Radec\Calculator::getLST($timestamp)

This calculated Local Sidereal time for the latitude and longditude set in the constructor. The approximation is within 0.3 seconds of time for dates within 100 years of J2000.

####Radec\Calculator::getHA($timestamp)

Gets the current hour angle - the current angle of the observers location relative to the celestial sphere.

####Radec\Calculator::getALT($timestamp)

Returns the altitude of the specificed target at this time at a location.

####Radec\Calculator::getAZ($timestamp)

Returns the azimuth of the specified target at this time at a location.
