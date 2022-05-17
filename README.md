# GoodWeatherFinder

GoodWeatherFinder allows a user to find good weather for many locations.

The National Weather Service (weather.gov) API provides weather data for one location at a time. Receiving data for hundreds or thousands of locations would take far too long, and would overly tax NWS's servers.

GoodWeatherFinder requests this data at regular time intervals and places this data in its own database. This allow for quick searching on multiple locations and control over how often the servers are taxed.

<hr>

## Development Process

This is a personal project for Nathan Smith.

To follow along with the development process, check out the [development docs](docs/development).

<hr>

## Why?

Why this? Well, a few reasons...
- I have been an avid hiker and backpacker in the Colorado mountains for years.  For those who know the area, mountain weather can be turn on you at a moment's notice. It can be no fun at all to be stuck above treeline when there's lightning or hail storm.
- Before each trip, I would try to find the best weather conditions for various peaks, considering how far I wanted to drive from home.  This would include many steps:
	1. Visit [14ers.com](http://www.14ers.com) to view the map of all peaks in Colorado above 13,000 and 14,000 feet

## Backend
- **Java** compiler version 1.8
- **JPA** version 2.2 *(GoodWeatherJPA)*
- **Gradle** version 7.4.2
- **Hibernate** version 5.4.32 Final
- **MySQL Connector** version 8.0.27
- **JUnit5** Version 5.8.2

<hr>

## Tools
- Spring Tool Suite 4
- Atom
- Git
- MySQL Workbench
