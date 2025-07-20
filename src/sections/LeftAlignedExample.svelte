<script>
    import * as Highcharts from "highcharts";
    import "highcharts/modules/exporting";
    import { Chart } from "@highcharts/svelte";
    import Scroller from "../lib/Scroller.svelte";
    import ArticleText from "../lib/ArticleText.svelte";

    const chartYears = [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023];
    const dataFemaleAsian =    [21.5, 22.5, 24.0, 25.0, 26.5, 27.0, 28.5, 29.5, 30.5, 31.0, 31.0, 31.0, 31.4]; // Approx
    const dataFemaleBlack =    [15.5, 16.0, 16.5, 17.0, 18.0, 19.0, 20.0, 20.5, 21.5, 22.5, 22.5, 22.5, 23.3]; // Approx
    const dataFemaleHispanic = [14.0, 14.5, 15.0, 15.5, 16.0, 16.5, 17.0, 17.5, 18.0, 19.0, 20.0, 20.0, 20.4]; // Approx
    const dataFemaleWhite =    [55.0, 56.5, 57.5, 59.0, 60.0, 62.0, 63.0, 63.5, 65.0, 66.0, 66.5, 66.5, 67.9]; // Approx
    const dataFemaleTotal =    [36.0, 37.0, 38.0, 39.5, 40.5, 41.5, 42.5, 43.0, 44.0, 44.0, 44.0, 44.0, 44.8]; // Approx

    let options = {
        chart: {
            type: "line", // Changed to line chart
            animation: false,
            // Removed specific background/border styles for simplicity as per previous discussion
            // backgroundColor: "#e3ff00",
            // borderColor: "#007052",
            // borderWidth: 5,
            // borderRadius: 20,
        },
        title: {
            text: "Bachelor's Degree or Higher Attainment for Females by Race or Ethnicity (Nationwide, 2011-2023)",
            align: 'left',
            style: {
                fontSize: '16px'
            }
        },
        credits: {
            enabled: true,
            text: "Data Source: BWDC",
            href: "https://blackwealthdata.org/explore/education",
            position: {
                align: 'right',
                x: -10,
                y: -5
            },
            style: {
                fontSize: '9px'
            }
        },
        xAxis: {
            categories: chartYears,
            title: {
                text: "Year"
            }
        },
        yAxis: {
            title: {
                text: "Attainment Rate (%)"
            },
            min: 0,
            max: 70, // Max for y-axis to fit the data
            labels: {
                format: '{value}%'
            }
        },
        tooltip: {
            valueSuffix: '%',
            shared: true,
            crosshairs: true
        },
        plotOptions: {
            series: {
                marker: {
                    enabled: false
                },
                lineWidth: 2
            }
        },
        series: [
            {
                name: "Total (Female)",
                data: dataFemaleTotal,
                color: '#808080'
            },
            {
                name: "Asian (Female)",
                data: dataFemaleAsian,
                color: '#4CAF50'
            },
            {
                name: "Black (Female)",
                data: dataFemaleBlack,
                color: '#FF5722'
            },
            {
                name: "Hispanic (Female)",
                data: dataFemaleHispanic,
                color: '#9C27B0'
            },
            {
                name: "White (Female)",
                data: dataFemaleWhite,
                color: '#3F51B5'
            }
        ],
    };

    // Removed the toggle logic as it's not needed for static data display
    // let chart;
    // let thirdSeriesVisible = false;
    // function toggleThirdSeries() { ... }
</script>

<div>
    <Scroller layout="left">
        {#snippet sticky()}
            <div class="chart-container">
                <Chart {options} highcharts={Highcharts} />
            </div>
            <p class="chart-caption">
                This chart displays Bachelor's degree attainment rates specifically for females, broken down by race and ethnicity, from 2011 to 2023.
            </p>
        {/snippet}

        {#snippet scrolly()}
            <ArticleText>
                <h3>Focusing on Females: Attainment Trends</h3>
                <p>
                    Analyzing Bachelor's degree attainment rates for females reveals distinct patterns within racial and ethnic groups, reflecting unique educational journeys and challenges.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>White and Asian Females Lead in Higher Education</h3>
                <p>
                    Similar to the overall population, **White females** consistently show high rates of Bachelor's degree attainment, reaching approximately **{dataFemaleWhite[dataFemaleWhite.length - 1]}%** by 2023. **Asian females** maintain the highest rates, peaking around **{dataFemaleAsian[dataFemaleAsian.length - 1]}%** in the same period.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>Gaps Persist for Black and Hispanic Females</h3>
                <p>
                    Despite progress, significant disparities remain for **Black** and **Hispanic females**. In 2023, Bachelor's attainment rates were around **{dataFemaleBlack[dataFemaleBlack.length - 1]}%** for Black females and **{dataFemaleHispanic[dataFemaleHispanic.length - 1]}%** for Hispanic females. These figures underscore ongoing equity challenges in higher education access and completion for these groups.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>Implications for Wealth Equity</h3>
                <p>
                    Educational attainment is a critical factor in long-term economic mobility and wealth accumulation. The persistent gaps in Bachelor's degree attainment for Black and Hispanic females highlight a key area where systemic efforts are needed to foster greater racial wealth equity.
                </p>
            </ArticleText>
        {/snippet}
    </Scroller>
</div>

<style>
    /* Chart container styling - simplified */
    .chart-container {
        width: 100%; /* Make it fill its parent */
        max-width: 600px; /* Optional: Set a max width for larger screens */
        height: 400px; /* Keep fixed height for chart */
        margin: 20px auto; /* Center the chart */
        /* Removed border, box-shadow, padding for simplicity. Add back if desired. */
    }

    /* Chart caption styling */
    .chart-caption {
        font-size: 0.9em;
        color: #555;
        text-align: center;
        margin: 15px 10px;
    }

    /* Basic styling for the sticky content with layout="left" */
    :global(.sticky-content) {
        padding: 20px;
        /* Removed background-color, border, box-shadow. Add back if desired. */
        display: flex;
        flex-direction: column;
        justify-content: center; /* Vertically center content */
        align-items: center; /* Horizontally center content */
    }

    /* Adjust padding for the scrolly content */
    :global(.scrolly-content) {
        padding: 40px;
    }
</style>