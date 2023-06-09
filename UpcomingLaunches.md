<html>
<head>
  <title>Upcoming Launches</title>
  <link rel="icon" href="RocketLaunchNavigatorIcon.ico" type="image/ico">
  <div>  
    <a href="https://www.rocketlaunchnavigator.com" class="button">Home</a>
    <a href="https://www.rocketlaunchnavigator.com/UpcomingLaunches" class="button">Upcoming Launches</a>
    <a href="https://www.rocketlaunchnavigator.com/PreviousLaunches" class="button">Previous Launches</a>
  <div>
<head>
<body>
  <h1>Upcoming Launches</h1>
  <p>572 Upcoming Launches</p>
<style>
  .button {
    display: inline-block;
    padding: 10px 20px;
    background-color: #337ab7;
    color: #fff;
    text-decoration: none;
    border-radius: 4px;
}

  .button:hover {
      background-color: #23527c;
}
  body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
}

header {
  font-size: 24px;
  text-align: center;
}

p {
  font-size: 16px;
  text-align: center;
}

.launch-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  height: 400px;
}

.launch-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.launch-box {
  width: 400px;
  height: 500px;
  background-color: #310198;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: rgb(255, 255, 255);
}

.launch-image {
  width: 400px; /* Adjust the width as desired */
  height: auto; /* Maintain aspect ratio */
  margin-bottom: 0px;
  margin-top: 30px; /* Adjust the margin-top as desired */
}
  
.rocket-name {
  text-decoration: underline;
}
</style>

<div class="launch-container">
<script>
const apiKey = '2578b44e83f2942913e1e7775ffdb3a9beed808d'; // Replace 'YOUR_API_KEY' with your actual API key
const apiUrl = `https://ll.thespacedevs.com/2.2.0/launch/upcoming/?limit=572&api_key=${apiKey}`;

async function fetchRocketLaunches() {
  try {
    const response = await fetch(apiUrl);
    if (!response.ok) {
      throw new Error('Failed to fetch data from the API');
    }
    const data = await response.json();
    if (data && data.results) {
      const launches = data.results.filter((launch) => launch.status.id !== 3 && launch.status.id !== 4);
      launches.forEach((launch) => {
        const { name, net, pad, rocket, webcast_live, status, net_precision, image } = launch;
        const launchItem = document.createElement('div');
        launchItem.classList.add('launch-item');
        const launchImage = new Image();
        launchImage.src = image; // Replace with actual image URL
        launchImage.alt = 'Launch Image';
        launchImage.classList.add('launch-image');
        const launchBox = document.createElement('div');
        launchBox.classList.add('launch-box');
        launchBox.innerHTML = `
          <h2><span class="rocket-name">${name}</span></h2>
          <p>Rocket: ${rocket.configuration.full_name}</p>
          <p>NET: ${net}</p>
          <p>Status: ${status.abbrev}</p>
          <p>NET Precestion: ${net_precision && net_precision.name}</p> <!-- Add null check for net_precision -->
          <p>Launch Pad: ${pad.name}</p>
          <p>Pad Location: ${pad.location.name}</p>
          <p>Webcast Live: ${webcast_live}</p>
        `;
        launchItem.appendChild(launchImage);
        launchItem.appendChild(launchBox);
        document.querySelector('.launch-container').appendChild(launchItem);
      });
    } else {
      const noDataText = document.createElement('p');
      noDataText.textContent = 'No launch data available.';
      document.body.appendChild(noDataText);
    }
  } catch (error) {
    const errorText = document.createElement('p');
    errorText.textContent = `An error occurred while fetching the data: ${error}`;
    document.body.appendChild(errorText);
  }
}

fetchRocketLaunches();
</script>
</div>

</body>
</html>
