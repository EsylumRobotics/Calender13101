 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Unified Planetary Calendar</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f9;
      color: #333;
      margin: 20px;
    }
    h1 {
      text-align: center;
      font-size: 2.5em;
    }
    .calendar-section {
      max-width: 800px;
      margin: 30px auto;
    }
    .month {
      background: #fff;
      border-radius: 8px;
      padding: 15px;
      margin-bottom: 20px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    .today-highlight {
      border-left: 4px solid #5b5fcf;
      background-color: #f0f0ff;
    }
    .month-name {
      font-size: 1.6em;
      color: #5b5fcf;
    }
    .season-marker {
      font-size: 0.8em;
      background: #e0e0ff;
      border-radius: 10px;
      padding: 2px 8px;
      margin-left: 10px;
    }
    .month-description {
      margin-top: 10px;
      color: #555;
      line-height: 1.4;
    }
  </style>
</head>
<body>

  <h1>Unified Planetary Calendar</h1>
  <div class="calendar-section"></div>

  <script>
    const calendarData = [
      { name: "Equinox Prime", description: "Beginning of the planetary year at the March Equinox. A time of balance and unity.", seasonMarker: "Equinox" },
      { name: "Floris", description: "Symbolizes growth, beauty, and potential across ecosystems." },
      { name: "Heliora", description: "Represents solar illumination and increasing energy." },
      { name: "Solstice Prime", description: "A month of solar extremes and turning points.", seasonMarker: "Solstice" },
      { name: "Zenithia", description: "Named for the solar zenith, a time of culmination and peak." },
      { name: "Therma", description: "Signifies intensity, heat, and dynamic natural forces." },
      { name: "Harmonia", description: "Reflects planetary transition and preparation for balance." },
      { name: "Equinox Alter", description: "Marks the second planetary equinox. A time of equal light and reflection.", seasonMarker: "Equinox" },
      { name: "Metanoia", description: "Focuses on transformation and reflection." },
      { name: "Declina", description: "Honors the changing solar arc as the solstice nears." },
      { name: "Solstice Alter", description: "Celebrates the second solstice, signifying extremes and contrast.", seasonMarker: "Solstice" },
      { name: "Nadir", description: "Denotes depth, stillness, and solar transition." },
      { name: "Aurora", description: "Represents awakening and light's return toward the equinox." }
    ];

    function getCurrentPlanetaryDate() {
      const today = new Date();
      today.setHours(12, 0, 0, 0);
      const year = today.getFullYear();

      // Approximate base start date: March 20 of current year
      const baseDate = new Date(year, 2, 20); // March 20
      const daysElapsed = Math.floor((today - baseDate) / (1000 * 60 * 60 * 24));

      let monthIndex = Math.floor(daysElapsed / 28);
      let dayInMonth = (daysElapsed % 28) + 1;

      if (monthIndex < 0) {
        monthIndex = 12;
        dayInMonth = 28 + (daysElapsed % 28);
      }
      if (monthIndex >= calendarData.length) {
        monthIndex %= calendarData.length;
      }

      return { monthIndex, dayInMonth };
    }

    function renderCalendar() {
      const container = document.querySelector('.calendar-section');
      const today = getCurrentPlanetaryDate();

      calendarData.forEach((month, i) => {
        const div = document.createElement('div');
        div.classList.add('month');
        if (i === today.monthIndex) div.classList.add('today-highlight');

        const title = document.createElement('div');
        title.classList.add('month-name');
        title.textContent = month.name;

        if (month.seasonMarker) {
          const marker = document.createElement('span');
          marker.classList.add('season-marker');
          marker.textContent = month.seasonMarker;
          title.appendChild(marker);
        }

        const desc = document.createElement('div');
        desc.classList.add('month-description');
        desc.textContent = month.description;

        div.appendChild(title);
        div.appendChild(desc);
        container.appendChild(div);
      });
    }

    document.addEventListener('DOMContentLoaded', renderCalendar);
  </script>
</body>
</html>
