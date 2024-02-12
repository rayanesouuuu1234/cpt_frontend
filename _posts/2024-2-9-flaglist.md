<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>List of Flags</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            text-align: center;
            background-image: url('https://imagecache.jpl.nasa.gov/images/edu/images/imagerecords/57000/57723/globe_west_2048-640x350.jpg');
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            background-attachment: fixed;
        }
        h1 {
            margin-top: 20px;
            color: #333;
        }
        #flag-list {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin-top: 20px;
        }
        .flag {
            margin: 10px;
            width: 120px;
            padding: 5px;
            background-color: #fff;
            border-radius: 5px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .flag img {
            width: 100%;
            border-radius: 5px;
        }
        .flag-name {
            margin-top: 5px;
            font-size: 14px;
            color: #666;
        }
    </style>
</head>
<body>
    <h1>List of Flags</h1>
    <div id="flag-list">
        <!-- Flag list will be displayed here -->
    </div>

    <script>
        async function fetchFlagData() {
            try {
                const response = await fetch('https://restcountries.com/v3.1/all');
                const data = await response.json();
                return data;
            } catch (error) {
                console.error('Error fetching flag data:', error);
            }
        }

        async function displayFlagList() {
            const flagData = await fetchFlagData();
            const flags = flagData.map(country => {
                const flagUrl = country.flags.png;
                const countryName = country.name.common;
                return `
                    <div class="flag">
                        <img src="${flagUrl}" alt="${countryName}" title="${countryName}">
                        <div class="flag-name">${countryName}</div>
                    </div>
                `;
            });
            document.getElementById('flag-list').innerHTML = flags.join('');
        }

        displayFlagList();
    </script>
</body>
</html>
