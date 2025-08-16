# Awesome Kepler Habitable Planets Finder

This project analyzes data from the NASA Exoplanet Archive (specifically, a subset of Kepler Object of Interest data) to identify potentially habitable exoplanets based on predefined criteria.

## Description

The script reads the `kepler_data.csv` file, parses its contents, and applies filters to identify planets that are:

1.  **Confirmed:** Their status (`koi_disposition`) is 'CONFIRMED'.
2.  **In the Habitable Zone:** Receive stellar flux (`koi_insol`) between 0.36 and 1.11 times Earth's flux.
3.  **Likely Rocky:** Have a planetary radius (`koi_prad`) less than 1.6 times Earth's radius.

The names of the planets meeting these criteria are printed to the console, along with the total count found.

## Features

- Parses CSV data efficiently using Node.js streams.
- Filters exoplanets based on habitability criteria (disposition, stellar flux, radius).
- Outputs the names and count of potentially habitable planets found.
- Uses the robust `csv-parse` library for reliable CSV handling.

## Tech Stack

- **Runtime:** Node.js
- **Libraries:**
  - `csv-parse`: For parsing the CSV data file.
  - `fs` (Node.js built-in): For reading the file system.

## Setup Instructions

1.  **Clone the repository:**

    ```bash
    git clone <your-repository-url>
    cd planets-project
    ```

2.  **Install dependencies:**
    Requires Node.js and npm (or yarn) to be installed.
    ```bash
    npm install
    ```
    or
    ```bash
    yarn install
    ```

## Usage

To run the script and find habitable planets:

```bash
npm start
```

or directly using Node:

```bash
node index.js
```

The script will process the `kepler_data.csv` file and print the results to your console.
