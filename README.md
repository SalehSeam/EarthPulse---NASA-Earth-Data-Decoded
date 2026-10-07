# 🌍 EarthPulse — NASA Earth Data, Decoded.

> Explore environmental trends using real NASA Earth data, statistical analysis, and clear visual insights.

**Team:** NovaCore  
**Members:** Abu Saleh Seam · Miftahul Jannat

**NASA Space Apps Challenge 2026:**  
**Be An Earth System Trend Detective!**

---

## 🌎 What is EarthPulse?

**EarthPulse** is an interactive web application that helps people understand environmental changes over time using real data from **NASA POWER (Prediction Of Worldwide Energy Resources)**.

Instead of requiring users to download, clean, or manually analyze environmental datasets, EarthPulse automatically retrieves NASA data for a selected location and time period.

It then:

1. Retrieves the data from NASA POWER
2. Validates the data
3. Detects a possible trend
4. Measures the magnitude of change
5. Tests whether the trend is statistically significant
6. Explains the result in simple language

EarthPulse focuses on four important questions:

> **What is changing?**  
> **Where is it changing?**  
> **How much is it changing?**  
> **Is the change statistically significant?**

---

## 🎯 The Problem

NASA provides a huge amount of Earth and environmental data.

However, raw time-series data can be difficult for ordinary users to understand.

A line on a graph may appear to increase or decrease, but visual appearance alone does not prove that a statistically meaningful trend exists.

People need a simpler way to move from:

**Raw Earth Data**

↓

**Statistical Analysis**

↓

**Understandable Environmental Insight**

EarthPulse was created to make this process easier.

---

## 💡 Our Solution

EarthPulse allows a user to select:

- **Where** — a location on Earth
- **What** — an environmental variable
- **When** — a time period

The application then automatically retrieves the corresponding NASA POWER data and performs the analysis.

### The user does NOT need to:

- Upload environmental datasets
- Manually calculate trends
- Clean the NASA data
- Enter environmental measurements
- Perform statistical calculations

EarthPulse handles these steps automatically.

---

# 🛰️ NASA Data Source

EarthPulse uses:

**NASA POWER — Prediction Of Worldwide Energy Resources**

NASA POWER provides publicly accessible environmental and meteorological data.

### Current Variable

**T2M — Temperature at 2 Meters**

- Unit: °C
- Source: NASA POWER
- Data frequency retrieved: Monthly
- Analysis: Annual mean values
- Historical coverage: beginning in 1981

### NASA POWER

https://power.larc.nasa.gov/

### API

EarthPulse retrieves data from the NASA POWER Monthly Point API.

Example request structure:

```text
https://power.larc.nasa.gov/api/temporal/monthly/point
?parameters=T2M
&community=RE
&latitude=LATITUDE
&longitude=LONGITUDE
&start=START_YEAR
&end=END_YEAR
&format=JSON
```

No NASA API key is required.

Data is retrieved live by the browser and is not stored on an application server.

---

# ✨ Key Features

## 🌍 Interactive Location Selection

Users can select a location using:

- Preset locations
- Latitude and longitude inputs
- An interactive world map

The selected location is shared across the application so that:

**Location → Coordinates → NASA Request → Analysis → Results → Chart**

remain synchronized.

---

## 🛰️ Live NASA Data

EarthPulse retrieves real data from NASA POWER rather than using fabricated or demonstration datasets.

If NASA POWER is unavailable, the application reports the error instead of replacing the result with fake data.

---

## 📊 Trend Analysis

EarthPulse calculates:

- Trend direction
- Sen's slope
- Total change
- Starting value
- Ending value
- p-value
- Statistical significance
- Analysis period

---

## 🧪 Mann-Kendall Test

EarthPulse uses the **Mann-Kendall test** to evaluate whether the time series contains evidence of a monotonic trend.

The test uses:

- Two-sided significance testing
- Tie correction
- Normal approximation
- α = 0.05

### Interpretation

```text
p < 0.05
→ Statistically significant trend

p ≥ 0.05
→ No statistically significant trend detected
```

A statistically significant trend does **not** mean that EarthPulse has identified the cause of the change.

---

## 📐 Sen's Slope

EarthPulse uses **Sen's slope** to estimate the magnitude of the trend.

The result is reported as:

```text
Change per year
```

The application also estimates total change over the selected period using the calculated slope and the time span.

---

# 🔬 Methodology

EarthPulse follows this process:

### 1. Select a location

The user selects a preset location, enters coordinates, or clicks on the interactive map.

### 2. Request NASA data

EarthPulse sends the selected coordinates and time period to NASA POWER.

### 3. Validate the data

The application checks the returned data and identifies missing or invalid values.

NASA POWER fill values such as `-999` are treated as missing data rather than real measurements.

### 4. Prepare annual observations

NASA's monthly temperature data is used to calculate or retrieve the annual mean for each year in the selected period.

### 5. Check data sufficiency

EarthPulse does not calculate a trend when the available data is insufficient.

The current implementation requires:

- At least 10 valid years
- No more than 20% missing data

### 6. Test for a trend

The Mann-Kendall test evaluates whether a statistically significant monotonic trend exists.

### 7. Measure the trend

Sen's slope estimates the magnitude of change per year.

### 8. Explain the result

The result is displayed through:

- Statistical values
- Interactive charts
- Data-quality information
- Plain-language explanations

---

# 🧠 What Comes From NASA vs. What We Calculate

This distinction is important.

### NASA provides:

- Environmental data
- Temperature observations
- Historical time-series information

### EarthPulse calculates:

- Annual analysis
- Missing-data checks
- Mann-Kendall test
- p-value interpretation
- Sen's slope
- Total change estimate
- Trend explanation

EarthPulse does **not** claim that NASA itself performs these statistical calculations for this application.

---

# 📈 Results Dashboard

After analysis, EarthPulse provides a result dashboard containing:

- Trend status
- Location
- Coordinates
- Environmental variable
- Time period
- Total change
- Trend slope
- Starting value
- Ending value
- p-value
- Significance threshold
- Data frequency

The application also provides an interactive chart showing the NASA observations and calculated trend.

---

# 📋 Data Quality

EarthPulse reports the quality of the retrieved dataset, including:

- Number of observations
- Missing years
- Missing percentage
- Data source
- Retrieval time
- API status

This helps users understand whether the analysis is based on a complete or incomplete time series.

---

# 💬 Plain-Language Explanation

Statistical results can be difficult to understand.

EarthPulse converts the calculated result into a simple explanation.

For example:

> **"No statistically significant trend was detected."**

This means the observed changes in the selected period were not strong or consistent enough, at the selected significance level, to conclude that a statistically significant monotonic trend exists.

The explanation is generated from fixed application logic and statistical results.

**It is not an AI-generated scientific conclusion.**

---

# 🔐 Security & Privacy

EarthPulse is designed as a lightweight client-side application.

### Privacy

- No user account required
- No database
- No backend application server
- No analytics or tracking
- No browser geolocation request
- No environmental dataset upload required
- No user environmental data stored on a server

### Security

The application includes:

- Input validation
- Coordinate validation
- Year-range validation
- Variable allowlisting
- Safe DOM handling
- Request throttling
- In-memory caching
- API error handling
- Deployment security headers

Deployment configurations include security headers such as:

- Content-Security-Policy
- Strict-Transport-Security
- X-Content-Type-Options
- Referrer-Policy
- Permissions-Policy
- Frame protection

The application does not require or store API secrets.

---

# 🛡️ Error Handling

EarthPulse is designed to fail safely when external data cannot be retrieved.

The application handles situations such as:

- Invalid coordinates
- Invalid year ranges
- Invalid variables
- HTTP 400 errors
- HTTP 404 errors
- HTTP 422 errors
- HTTP 429 rate limits
- Server errors
- Network failures
- Request timeouts
- Empty responses
- Malformed responses
- Missing values
- Insufficient data

EarthPulse does **not** substitute fabricated data when NASA data is unavailable.

---

# ♿ Accessibility & Usability

The interface includes:

- Responsive layout
- Keyboard focus styles
- Reduced-motion support
- Accessible chart descriptions
- Clear text labels
- Trend information that is not communicated by colour alone

The goal is to make the scientific information understandable without relying only on visual interpretation.

---

# 🛠️ Technology

EarthPulse is built as a lightweight web application using:

- HTML
- CSS
- JavaScript
- NASA POWER API
- Leaflet
- Interactive SVG charting
- Static web deployment

---

# 🚀 Running Locally

No build system or package installation is required.

Clone the repository:

```bash
git clone https://github.com/SalehSeam/earthpulse.git
```

Enter the project directory:

```bash
cd earthpulse
```

Start a local HTTP server:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

An internet connection is required because EarthPulse retrieves NASA data and map resources online.

---

# 🔑 Environment Variables

EarthPulse does not require environment variables or API keys.

NASA POWER can be accessed without an API key.

An `.env.example` file may be included only for documentation purposes.

**Never commit real secrets to the repository.**

---

# ☁️ Deployment

EarthPulse is designed for static deployment.

## Netlify

The project can be deployed by:

- Connecting the GitHub repository, or
- Uploading the project folder

No build command is required.

Publish directory:

```text
.
```

Deployment security configuration can be provided through:

```text
netlify.toml
```

---

## Vercel

Import the GitHub repository as a static project.

No build step is required.

Deployment configuration can be provided through:

```text
vercel.json
```

---

## GitHub Pages

EarthPulse can also run on GitHub Pages.

However, GitHub Pages does not provide the same custom HTTP security-header configuration available through platforms such as Netlify or Vercel.

---

# ⚠️ Limitations

EarthPulse has several important limitations.

### Statistical limitations

Annual means may contain autocorrelation, which can affect Mann-Kendall significance.

Therefore, the current implementation should be treated as an exploratory trend-analysis tool rather than a complete climate attribution system.

### NASA POWER data

NASA POWER combines satellite observations and model-based reanalysis products.

It should not be interpreted as the same thing as a single physical weather-station record.

A selected coordinate represents data associated with the underlying grid rather than an exact physical measurement at that precise point.

### Causation

A statistically significant trend does not identify what caused the trend.

EarthPulse describes observed data and does not claim causal explanations.

### Current variable support

The current version focuses on:

**T2M — Temperature at 2 Meters**

Additional environmental variables may be added in future versions.

### Internet dependency

NASA data and map tiles require an internet connection.

If NASA POWER is unavailable, EarthPulse cannot perform a live analysis.

---

# 🔮 Future Improvements

Potential future improvements include:

- Additional NASA POWER variables
- Precipitation analysis
- Humidity analysis
- Wind analysis
- Solar radiation analysis
- Two-location comparison
- Seasonal analysis
- Improved autocorrelation handling
- Server-side caching
- Additional statistical methods
- Optional AI-assisted explanations kept separate from the scientific calculations

These are future possibilities and are **not represented as current features**.

---

# 👥 Team NovaCore

## Abu Saleh Seam

**Developer · Project Lead**

## Miftahul Jannat

**Developer · Team Member**

---

# 🏆 NASA Space Apps Challenge 2026

**Challenge:**

> Be An Earth System Trend Detective!

**Project:**

> EarthPulse — NASA Earth Data, Decoded.

**Team:**

> NovaCore

---

# 📚 Credits

### NASA Data

**NASA POWER — Prediction Of Worldwide Energy Resources**

NASA Langley Research Center

https://power.larc.nasa.gov/

### Interactive Maps

**Leaflet**

https://leafletjs.com/

Map tiles provided by Esri.

---

# 📄 License

This project is released under the **MIT License**.

See the `LICENSE` file for details.

---

## 🌍 EarthPulse

**Real NASA data.  
Statistical analysis.  
Clearer Earth insights.**

Built by **NovaCore** for the **NASA Space Apps Challenge 2026**.
