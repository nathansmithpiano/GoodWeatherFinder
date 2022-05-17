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

Well, I'm glad you asked...

I have been an avid hiker and backpacker in the Colorado mountains for years.  For those who know the area, mountain weather can be turn on you at a moment's notice. It can be no fun at all to be stuck above treeline when there's lightning or hail storm.

Before each trip, I would try to find the best weather conditions for various peaks, considering how far I wanted to drive from home.  This would include many steps:
1. Visit [14ers.com](http://www.14ers.com) to view the map of all peaks in Colorado above 13,000 and 14,000 feet.
2. Click on each peak and visit the associated weather.gov page to see forecast information.
3. Do this for many locations - not just the one peak - as I want to see if nearby peaks show similar forecasts and/or if certain areas are predicted to have better conditions.
4. Briefly look at the main forecast page (i.e. [Mt. Elbert](https://forecast.weather.gov/MapClick.php?lat=39.117770000000064&lon=-106.44529999999997#)) and if it's not immediately discouraging, click on [Hourly Weather Forecast](https://forecast.weather.gov/MapClick.php?lat=39.1178&lon=-106.4453&unit=0&lg=english&FcstType=graphical).
5. Change the options (namely, include Lightning Activity Level) and submit to refresh the page.
6. Consider the information here, then repeat the process for all the many locations I've opened.
7. Do the same for another area or group of peaks to see if the weather is any better.
8. When necessary, continue my search to more areas further away, or decide to change to another day or another activity.

As you can imagine, this process is time consuming and I've wondered for years why there isn't a better solution.  I imagine many fellow peak baggers do something like this, but by no means is this type of search limited to peak bagging. What about climbing? Mountain biking? Fishing? Camping? Going to the beach? Going to the lake? While other areas might not have such temperamental weather, I could also imagine people deciding where to go for the weekend or for a longer trip.

Weather can make or break an experience, so why not have a way to choose your activity based on the weather, instead of the other way around?

## Is that the only reason?

You guessed it. I do have other motivations. I began this project while attending [Skill Distillery](https://skilldistillery.com)'s Full Stack with Java bootcamp.  Shoutout to the excellent instructors there and fellow SD32 cohort members.

During this program, we were developing RESTful applications through a Java JPA / Spring REST backend and an Angular frontend. While this project would be outside the scope of any weekend or even the midterm or final projects, I wanted a side project as an extra challenge during the bootcamp, and for something to continue working on after graduation. Ideally, I hoped this would be something desirable for potential employers, as I would begin hunting for my first full-time position in June of 2022.

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
