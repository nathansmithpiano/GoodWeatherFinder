# GoodWeatherFinder

GoodWeatherFinder allows a user to find good weather for many locations.

The National Weather Service (weather.gov) API provides weather data for one location at a time. Receiving data for hundreds or thousands of locations would take far too long, and would overly tax NWS's servers.

GoodWeatherFinder requests this data at regular time intervals and places this data in its own database. This allow for quick searching on multiple locations and control over how often the servers are taxed.

<hr>

Each **Location** consists of:

<hr>


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
