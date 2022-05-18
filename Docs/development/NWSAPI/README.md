[Up](../) | [Next](Endpoints)
<hr>

## National Weather Service (Weather.gov) API

### Importing Data
This is an overview of how NWS API JSON will translate to entities in the database.
Each **location** shares a 1:1 mapping with a **point** in the NWS API.  From this point, many other entities will be created, or more commonly, updated.
The structure below does not show properties for each individual entity.  Rather, it shows each entity or collection of entities that will be created, or more commonly, updated.

<details open><summary><b>location</b></summary>
	<blockquote>
		<details open><summary>location.<b>point</b> <i>(single entity)</i></summary>
			<blockquote>
				<p>i.e. https://api.weather.gov/points/39.1177,-106.4453</p>
				<details open><summary>location.point.<b>geometry</b> <i>(single entity)</i></summary>
					<blockquote>
						<details open><summary>location.point.geometry.<b>coordinate</b> <i>(single entity)</i></summary>
						</details>
					</blockquote>
				</details>
				<details open><summary>location.point.properties.<b>forecastOffice</b> <i>(single entity)</i></summary>
					<blockquote>
						<p>i.e. https://api.weather.gov/offices/PUB</p>
						<details open><summary>location.point.properties.forecastOffice.<b>counties</b> <i>(many IRI's, multiple entities)</summary>
							<blockquote>
								<p>i.e. https://api.weather.gov/zones/county/COC003</p>
							</blockquote>
						</details>
						<details open><summary>location.point.properties.forecastOffice.<b>forecastZones</b> <i>(many IRI's, multiple entities)</summary>
							<blockquote>
								<p>i.e. https://api.weather.gov/zones/forecast/COZ058</p>
							</blockquote>
						</details>
						<details open><summary>location.point.properties.forecastOffice.<b>fireZones</b> <i>(many IRI's, multiple entities)</summary>
							<blockquote>
								<p>i.e. https://api.weather.gov/zones/fire/COZ220</p>
							</blockquote>
						</details>
						<details open><summary>location.point.properties.forecastOffice.<b>observationStations</b> <i>(many IRI's, multiple entities)</summary>
							<blockquote>
								<p>i.e. https://api.weather.gov/stations/K04V</p>
							</blockquote>
						</details>
					</blockquote>
				</details>
				<details open><summary>location.point.properties.<b>forecast & forecastHourly</b> <i>(2 IRI's, multiple entities)</i></summary>
					<blockquote>
						<p>i.e. https://api.weather.gov/gridpoints/PUB/33,107/forecast</p>
						<p>i.e. https://api.weather.gov/gridpoints/PUB/33,107/forecast/hourly</p>
						<details open><summary>location.point.properties.forecast.<b>periods</b> <i>(multiple entities)</i></summary>
						</details>
					</blockquote>
				</details>
				<details open><summary>location.point.properties.<b>forecastGridData</b> <i>(IRI, single entity)</i></summary>
					<blockquote>
						<p>i.e. https://api.weather.gov/gridpoints/PUB/33,107</p>
						<p>for many of these data points, one shared entity could be used.</p>
						<p>i.e. each has a "uom" and a collection of "validTime"/"value" pairs</p>
						<details open><summary>location.point.properties.forecastGridData.<b>geometry</b> <i>(single entity)</i></summary>
							<blockquote>
								<details open><summary>location.point.properties.forecastGridData.geometry.<b>coordinates</b> <i>(multiple entities)</i></summary>
								</details>
							</blockquote>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>forecastOffice</b> <i>(URI, single entity)</i></summary>
							<blockquote>
								<p>i.e. https://api.weather.gov/offices/PUB</p>
							</blockquote>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>temperatures</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>dewpoints</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>relativeHumidities</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>apparentTemperatures</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>windChills</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>skyCovers</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>windDirections</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>windSpeeds</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>windGusts</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>weathers</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>hazards</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>probabilityOfPrecipitations</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>quantitativePrecipitations</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>iceAccumulations</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>snowfallAmounts</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>snowLevels</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>ceilingHeights</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>visibilities</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>transportWindSpeeds</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>transportWindDirections</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>mixingHeights</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>hainesIndexes</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>lightningActivityLevels</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>twentyFootWindSpeeds</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>twentyFootWindDirections</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>waveHeights</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>wavePeriods</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>waveDirections</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>primarySwellHeights</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>primarySwellDirections</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>secondarySwellHeights</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>secondarySwellDirections</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>wavePeriod2s</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>windWaveHeights</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>dispersionIndexs</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>pressures</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>probabilityOfTropicalStormWinds</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>probabilityOfHurricaneWinds</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>potentialOf15mphWinds</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>potentialOf25mphWinds</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>potentialOf35mphWinds</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>potentialOf45mphWinds</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>potentialOf20mphWindGusts</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>potentialOf30mphWindGusts</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>potentialOf40mphWindGusts</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>potentialOf50mphWindGusts</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>potentialOf60mphWindGusts</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>grasslandFireDangerIndexes</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>probabilityOfThunders</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>davisStabilityIndexs</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>atmosphericDispersionIndexs</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>lowVisibilityOccurrenceRiskIndexes</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>stabilities</b> <i>(multiple entities)</i></summary>
						</details>
						<details open><summary>location.point.properties.forecastGridData.<b>redFlagThreatIndexes</b> <i>(multiple entities)</i></summary>
						</details>
					</blockquote>
				</details>
				<details open><summary>location.point.properties.<b>observationStations</b> <i>(IRI, single entity)</i></summary>
					<blockquote>
						<p> i.e. https://api.weather.gov/gridpoints/PUB/33,107/stations</p>
						<p>This IRI contains the JSON for all observationStations, as well as a list of those URI's.<br>
						Rather than creating a unique entity as the unique IRI would imply, point will store a collection.</p>
					</blockquote>
				</details>
				<details open><summary>location.point.properties.<b>relativeLocation</b> <i>(single entity)</i></summary>
					<blockquote>
						<details open><summary>location.point.properties.relativeLocation.<b>geometry</b> <i>(single entity)</i></summary>
							<blockquote>
								<details open><summary>location.point.properties.relativeLocation.geometry.<b>coordinate</b> <i>(single entity)</i></summary>
								</details>
							</blockquote>
						</details>
					</blockquote>
				</details>
				<details open><summary>location.point.properties.<b>forecastZone</b> <i>(IRI, single entity)</i></summary>
					<blockquote>
						<p>i.e. https://api.weather.gov/zones/forecast/COZ060</p>
						<details open><summary>location.point.properties.forecastZone.<b>geometry</b> <i>(single entity)</i></summary>
							<blockquote>
								<details open><summary>location.point.properties.forecastZone.geometry.<b>coordinates</b> <i>(multiple entities)</i></summary>
								</details>
							</blockquote>
						</details>
						<details open><summary>location.point.properties.forecastZone.<b>forecastOffices</b> <i>(many IRI's, multiple entities)</i></summary>
							<blockquote>
								<p>i.e. https://api.weather.gov/offices/PUB</p>
							</blockquote>
						</details>
						<details open><summary>location.point.properties.forecastZone.<b>observationStations</b> <i>(many IRI's, multiple entities)</i></summary>
							<blockquote>
								<p>i.e. https://api.weather.gov/stations/KASE</p>
							</blockquote>
						</details>
					</blockquote>
				</details>
				<details open><summary>location.point.properties.<b>county</b> <i>(IRI, single entity)</i></summary>
					<blockquote>
						<p>i.e. https://api.weather.gov/zones/county/COC065</p>
						<details open><summary>location.point.properties.county.<b>forecastOffices</b> <i>(many IRI's, multiple entities)</i></summary>
							<blockquote>
								<p>i.e. https://api.weather.gov/offices/PUB</p>
							</blockquote>
						</details>
						<details open><summary>location.point.properties.county.<b>observationStations</b> <i>(many IRI's, multiple entities)</i></summary>
							<blockquote>
								<p>no example at this time </p>
							</blockquote>
						</details>
					</blockquote>
				</details>
				<details open><summary>location.point.properties.<b>fireWeatherZone</b> <i>(IRI, single entity)</i></summary>
					<blockquote>
						<details open><summary>location.point.properties.fireWeatherZone.<b>geometry</b> <i>(single entity)</i></summary>
							<blockquote>
								<details open><summary>location.point.properties.fireWeatherZone.geometry.<b>coordinates</b> <i>(multiple entities)</i></summary>
								</details>
							</blockquote>
							<details open><summary>location.point.properties.forecastZone.<b>forecastOffices</b> <i>(many IRI's, multiple entities)</i></summary>
								<p></p>
							</details>
							<details open><summary>location.point.properties.forecastZone.<b>observationStations</b> <i>(many IRI's, multiple entities)</i></summary>
							</details>
						</details>
					</blockquote>
				</details>
			</blockquote>
		</details>
	</blockquote>
</details>
<hr>

#### TEMPLATE
<details open><summary></summary>
	<blockquote>
	</blockquote>
</details>
<hr>

### [Endpoints](Endpoints/README.md)

From [Weather.gov's Documentation](https://www.weather.gov/documentation/services-web-api):
>## Overview
>The National Weather Service (NWS) API allows developers access to critical forecasts, alerts, and observations, along with other weather data. The API was designed with a cache-friendly approach that expires content based upon the information life cycle. The API is based upon of JSON-LD to promote machine data discovery.
>
>The API is located at: https://api.weather.gov
>
>Operational issues should be reported to nco.ops@noaa.gov.
>
>General use questions can be asked on the [API github site](https://weather-gov.github.io/api/).
>
>### Pricing
>All of the information presented via the API is intended to be open data, free to use for any purpose. As a public service of the United States Government, we do not charge any fees for the usage of this service, although there are reasonable rate limits in place to prevent abuse and help ensure that everyone has access. The rate limit is not public information, but allows a generous amount for typical use. If the rate limit is execeed a request will return with an error, and may be retried after the limit clears (typically within 5 seconds). Proxies are more likely to reach the limit, whereas requests directly from clients are not likely.
>
>### Content Negotiation
>The new API will use headers to modify the version and format of the response. Every request, either by browser or application, sends header information every time you visit any website. For example, a commonly used header called "UserAgent" tells a website what type of device you are using so it can tailor the best experience for you. No private information is shared in a header, and this is a standard practice for all government and private sites. Developers can override these headers for specific purposes (see the "API Specifications" tab for more information). You can get full details by visiting the header field definitions page at the [World Wide Web Consortium](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) site.
>
>### Authentication
>A User Agent is required to identify your application. This string can be anything, and the more unique to your application the less likely it will be affected by a security event. If you include contact information (website or email), we can contact you if your string is associated to a security event. This will be replaced with an API key in the future.
>
>```User-Agent: (myweatherapp.com, contact@myweatherapp.com)```
>
>## Examples of using the API
>The API uses linked data to allow applications to discover content. Similar to a web site that provides HTML links to help users navigate to each page, linked data helps applications navigate to each endpoint. You may also review the OPEN API specification on the "Specification" tab on this page, or directly using the specification endpoint (that is also used to create the tab presentation): https://api.weather.gov/openapi.json.
>
>### How do I get the forecast?
>Forecasts are divided into 2.5km grids. Each NWS office is responsible for a section of the grid. The API endpoint for the forecast at a specific grid is:
>
>```https://api.weather.gov/gridpoints/{office}/{grid X},{grid Y}/forecast```
>
>For example: https://api.weather.gov/gridpoints/TOP/31,80/forecast
>
> If you do not know the grid that correlates to your location, you can use the /points endpoint to retrieve the exact grid endpoint by coordinates:
>
>```https://api.weather.gov/points/{latitude},{longitude}```
>
>For example: https://api.weather.gov/points/39.7456,-97.0892
>
>This will return the grid endpoint in the "forecast" property. Applications may cache the grid for a location to improve latency and reduce the additional lookup request. This endpoint also tells the application where to find information for issuing office, observation stations, and zones.
>
>### How do I get alerts?
>The API has a robust selection of filters for alerts. A common request is all active alerts for a state:
>
>```https://api.weather.gov/alerts/active?area={state}```
>
>For example: https://api.weather.gov/alerts/active?area=KS
>
>The /alerts/active endpoint redirects internally to the root /alerts endpoint with the "active=true" parameter. Please review the "Specification" tab for all the filter options. For more detailed information on how the Weather Service geolocates alerts, please review [our guide](https://www.weather.gov/documentation/services-web-api#:~:text=alerts%2C%20please%20review-,our%C2%A0guide,-.%C2%A0).
>
>## Known issues
> - Radar station information (/radar endpoints) performance is unreliable.
> - The zones endpoint has a constraint on the number of zones able to be returned at once. Requesting many zones will result in an error.
> - The gridpoints endpoint returns a 500 error. Retrying the request generally returns valid data.
> - Observations are not being sorted in chronological order.
> - The API is returning gridpoints that are off by 1,1. This causes forecasts for AFG, AJK, CAE, DLH, HNX, LIX, LWX, MAF, MFR, MLB, MRX, MTR to fall outside the bounding box of the grid.
> - The gridpoints/forecast and gridpoints/forecast/hourly endpoints do not work for WFO AFC (site id AER and ALU on the gridpoints endpoint).
>
>*Updated 5/10/2022*
>
>### Upstream Issues/Changes
>The following issues are related to upstream sources of the API, and are not an API bug.
>
> - Delayed observations
>   - Observations may be delayed up to 20 minutes from MADIS, the upstream source.
>
>*Updated 1/26/2022*
