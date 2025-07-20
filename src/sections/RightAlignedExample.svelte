<script>
    import * as Highcharts from "highcharts";
    import "highcharts/modules/exporting";
    import { Chart } from "@highcharts/svelte";
    import Scroller from "../lib/Scroller.svelte";
    import ArticleText from "../lib/ArticleText.svelte";

    const chartYears = [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023];
    const dataAsian = [20.0, 20.8, 22.0, 23.5, 24.5, 25.0, 26.5, 27.5, 28.5, 29.0, 29.0, 29.0, 29.0]; // Approx from chart
    const dataBlack = [14.0, 14.5, 15.0, 15.5, 16.0, 17.0, 18.0, 18.5, 19.5, 20.5, 20.5, 20.5, 21.5]; // Approx from chart
    const dataHispanic = [13.0, 13.5, 14.0, 14.5, 15.0, 15.5, 16.0, 16.5, 17.0, 18.0, 19.0, 19.0, 19.6]; // Approx from chart
    const dataWhite = [50.0, 51.5, 52.5, 54.0, 55.0, 57.0, 58.0, 58.5, 60.0, 61.0, 61.5, 61.5, 62.9]; // Approx from chart
    const dataTotal = [34.5, 35.5, 36.5, 38.0, 39.0, 40.0, 41.0, 41.5, 42.0, 42.0, 42.0, 42.0, 42.3]; // Approx from chart

    let options = {
        chart: {
            type: "line",
            animation: false,
        },
        title: {
            text: "Bachelor's Degree or Higher Attainment by Race or Ethnicity (Nationwide, 2011-2023)",
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
            max: 70,
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
                name: "Total",
                data: dataTotal,
                color: '#808080' // A neutral
            },
            {
                name: "Asian",
                data: dataAsian,
                color: '#4CAF50' // Green
            },
            {
                name: "Black",
                data: dataBlack,
                color: '#FF5722' // Orange/Red
            },
            {
                name: "Hispanic",
                data: dataHispanic,
                color: '#9C27B0' // Purple
            },
            {
                name: "White",
                data: dataWhite,
                color: '#3F51B5' // Blue
            }
        ],
    };
</script>

<div>
    <Scroller layout="right">
        {#snippet sticky()}
            <div class="chart-container">
                <Chart {options} highcharts={Highcharts} />
            </div>
            <p class="chart-caption">
                This chart illustrates the percentage of individuals aged 25 and older who have attained a Bachelor's degree or higher, by race and ethnicity, nationwide from 2011 to 2023.
            </p>
        {/snippet}

        {#snippet scrolly()}
            <ArticleText>
                <h3>Bachelor's Degree Attainment</h3>
                <p>
                    Achieving a Bachelor's degree or higher shows more significant disparities across racial and ethnic groups in the U.S. from 2011 to 2023 than for high school degrees.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>Asian and White Populations</h3>
                <p>
                    As of 2023, the White population shows an attainment rate of about {dataWhite[dataWhite.length - 1]}% for a Bachelor's degree or higher and the Asian population consistently maintains the highest attainment rate, around {dataAsian[dataAsian.length - 1]}% in 2023 as well. This indicates high levels of higher education within these races.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>Black and Hispanic Populations</h3>
                <p>
                    In contrast, the Black and Hispanic populations show lower Bachelor's degree attainment rates. In 2023, the rate for the Black population was about {dataBlack[dataBlack.length - 1]}%, while for the Hispanic population it was around {dataHispanic[dataHispanic.length - 1]}%. These rates are less than half of the rates observed for the White and Asian populations as a whole.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>Disparities</h3>
                <p>
                    All groups have had an increase in Bachelor's degree attainment since 2011, but the relative gaps have continued to exist. For example, the Hispanic population's rate grew from about {dataHispanic[0]}% in 2011 to {dataHispanic[dataHispanic.length - 1]}% in 2023. This shows progress, but that we are still far from equity.
                </p>
                <p>
                    Understanding these disparities between races is very important in order to address long-standing inequities in wealth and opportunity. for certain races and ethnicities.
                </p>
            </ArticleText>
        {/snippet}
    </Scroller>
</div>

<style>
    /* Chart container styling - simplified */
    .chart-container {
        width: 100%; /* Make it fill its parent */
        max-width: 600px; /* max width for larger screens */
        height: 400px; /* fixed height for chart */
        margin: 20px auto; /* center the chart */
    }

    /* Chart caption styling */
    .chart-caption {
        font-size: 0.9em;
        color: #555;
        text-align: center;
        margin: 15px 10px;
    }

    /* Basic styling for the sticky content */
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
