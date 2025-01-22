<script>
  import dayjs from 'dayjs';
  import utc from 'dayjs/plugin/utc';
  dayjs.extend(utc);
  let name, weatherData, date;
  let desc, temp, feelsLike, humid, wind, clouds, icon, cityName;
  let show = false;
  const apiKey = '4d8fb5b93d4af21d66a2948710284366';
  async function click() {
    const geo =
      'http://api.openweathermap.org/geo/1.0/direct?q=' +
      name +
      '&appid=' +
      apiKey;
    await fetch(geo)
      .then((response) => response.json())
      .then((data) => {
        get(data[0].lat, data[0].lon);
      });
  }
  async function get(lat, lon) {
    const url =
      'https://api.openweathermap.org/data/2.5/weather?lat=' +
      lat +
      '&lon=' +
      lon +
      '&appid=' +
      apiKey +
      '&units=imperial';
    fetch(url)
      .then((response) => response.json())
      .then((data) => {
        weatherData = data;
        temp = Math.round(weatherData.main.temp) + '°F';
        feelsLike =
          'Feels like ' + Math.round(weatherData.main.feels_like) + '°F';
        humid = weatherData.main.humidity + '% humidity';
        desc = weatherData.weather[0].description;
        icon =
          'https://openweathermap.org/img/wn/' +
          weatherData.weather[0].icon +
          '@2x.png';
        wind = Math.round(weatherData.wind.speed) + ' mph wind';
        clouds = weatherData.clouds.all + '% cloudy';
        cityName = weatherData.name + ', ' + weatherData.sys.country;
        date = dayjs(weatherData.dt * 1000, 'x')
          .utc()
          .add(weatherData.timezone, 's')
          .format('MMMM D, HH:mm');
        show = true;
      });
  }
</script>

<main>
  <div class="text-bold mx-auto space-y-4 bg-sky-200 px-2 text-center text-3xl">
    <h1 class="text-5xl">William's cool weather app</h1>
    <h3>
      Input the city name, state code (only for the US) and country code divided
      by comma. Please use ISO 3166 country codes.
    </h3>
    <h3>Ex: New York, NY, US (or just New York)</h3>
    <input bind:value={name} placeholder="Enter name here!" class="p-2" /><br />
    <button class="border-2 border-solid border-black p-4" onclick={click}
      >Submit</button
    >
    <div class="flex flex-col bg-white p-4">
      {#if show}
        <h3 class="pt-2">{date}</h3>
      {/if}
      <h1 class="bold text-5xl">{cityName}</h1>
      <div class="flex flex-row items-center justify-center text-4xl">
        {#if show}
          <img class="w-20" src={icon} alt="i like elana" />
        {/if}
        <h2>{temp}</h2>
      </div>
      <h3>{feelsLike}</h3>
      <h3>{desc}</h3>
      <h3>{humid}</h3>
      <h3>{wind}</h3>
      <h3>{clouds}</h3>
    </div>
  </div>
</main>
