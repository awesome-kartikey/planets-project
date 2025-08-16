# Frequently Asked Questions (FAQ)

**Q1: What is the main goal of this project?**

A: The project aims to identify potentially habitable exoplanets by parsing data from the `kepler_data.csv` file (sourced from the NASA Exoplanet Archive). It filters planets based on confirmation status, stellar flux received, and planetary radius.

**Q2: Where does the `kepler_data.csv` file come from?**

A: The data originates from the NASA Exoplanet Archive ([http://exoplanetarchive.ipac.caltech.edu](http://exoplanetarchive.ipac.caltech.edu)). The specific file provided contains data on Kepler Objects of Interest (KOIs).

**Q3: What specific criteria are used to determine if a planet is "habitable" in this script?**

A: The script `index.js` uses the `isHabitablePlanet` function, which checks for three conditions:
1.  `koi_disposition === 'CONFIRMED'`: The planet's discovery must be confirmed.
2.  `koi_insol > 0.36 && koi_insol < 1.11`: The planet must receive between 36% and 111% of the stellar flux that Earth receives from the Sun. This is a proxy for the "Goldilocks Zone" where liquid water could potentially exist.
3.  `koi_prad < 1.6`: The planet's radius must be less than 1.6 times Earth's radius. This increases the likelihood that the planet is rocky, like Earth, rather than a gas giant.

**Q4: Why does the script use `fs.createReadStream` instead of `fs.readFile`?**

A: `fs.createReadStream` reads the file in chunks rather than loading the entire file into memory at once. This is much more memory-efficient, especially for large files like `kepler_data.csv` might be (or could become with more data). It processes the data piece by piece as it arrives.

**Q5: How does the CSV parsing work?**

A: The project uses the `csv-parse` library. The configuration `{ comment: '#', columns: true }` tells the parser:
*   `comment: '#'` : Ignore lines that start with the `#` character (like the header comment in `kepler_data.csv`).
*   `columns: true`: Treat the first non-commented line as a header row, and parse subsequent rows into JavaScript objects where keys are the header names and values are the corresponding cell data.

**Q6: Can I use a different dataset or update the `kepler_data.csv` file?**

A: Yes, you can replace `kepler_data.csv` with an updated or different file. However, ensure the file format is compatible:
*   It must be a comma-separated values (CSV) file.
*   It must contain the columns used for filtering: `koi_disposition`, `koi_insol`, `koi_prad`, and the column used for output: `kepler_name`.
*   If the column names change, you'll need to update the `isHabitablePlanet` function and the final `map` function in `index.js`.

**Q7: How can I change the criteria for habitability?**

A: Modify the conditions inside the `isHabitablePlanet` function in `index.js`. For example, you could adjust the ranges for `koi_insol` or `koi_prad`, or add checks based on other columns available in the CSV data.

**Q8: What happens if there's an error reading or parsing the file?**

A: The script includes basic error handling using `.on('error', (err) => { ... })`. If an error occurs during file reading or parsing, it will be logged to the console, and the script might terminate or fail to produce complete results, depending on where the error occurs in the stream pipeline.

**Q9: Is this script guaranteed to find *all* habitable planets?**

A: No. "Habitability" is a complex concept. This script uses specific, simplified proxies (stellar flux, radius, confirmation status) based on available data in the CSV. There are many other factors influencing habitability (atmosphere, magnetic field, stellar activity, etc.) not considered here. It identifies planets that meet *these specific criteria*.