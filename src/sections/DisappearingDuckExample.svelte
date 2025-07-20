<script>
    import * as Highcharts from "highcharts";
    import "highcharts/modules/exporting";
    import { Chart } from "@highcharts/svelte";
    import Scroller from "../lib/Scroller.svelte";
    import ArticleText from "../lib/ArticleText.svelte";

    const chartYears = [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023];

    const dataHSAsian =    [89.0, 89.5, 90.0, 91.0, 91.5, 92.0, 93.0, 93.5, 94.0, 95.0, 95.5, 95.5, 95.5]; // Approx
    const dataHSBlack =    [83.5, 84.0, 85.0, 86.0, 86.5, 87.0, 88.0, 88.5, 89.0, 90.0, 90.5, 90.5, 90.6]; // Approx
    const dataHSHispanic = [64.0, 65.0, 66.0, 67.0, 68.0, 69.0, 70.0, 71.0, 72.0, 73.0, 74.0, 74.0, 74.3]; // Approx
    const dataHSWhite =    [91.0, 91.5, 92.0, 92.5, 93.0, 93.5, 94.0, 94.5, 95.0, 95.5, 96.0, 96.0, 96.0]; // Approx
    const dataHSTotal =    [85.0, 85.5, 86.0, 87.0, 87.5, 88.0, 89.0, 89.5, 90.0, 91.0, 91.0, 91.0, 91.3]; // Approx


    let options = {
        chart: {
            type: "line",
            animation: false,
        },
        title: {
            text: "High School Completion or Higher Attainment by Race or Ethnicity (Nationwide, 2011-2023)",
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
            max: 100,
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
                data: dataHSTotal,
                color: '#808080'
            },
            {
                name: "Asian",
                data: dataHSAsian,
                color: '#4CAF50'
            },
            {
                name: "Black",
                data: dataHSBlack,
                color: '#FF5722'
            },
            {
                name: "Hispanic",
                data: dataHSHispanic,
                color: '#9C27B0'
            },
            {
                name: "White",
                data: dataHSWhite,
                color: '#3F51B5'
            }
        ],
    };
</script>

<div>
    <Scroller layout="right"> {#snippet sticky()}
            <div class="chart-container">
                <Chart {options} highcharts={Highcharts} />
            </div>
            <p class="chart-caption">
                This chart shows the percentage of individuals aged 25 and older who have attained a High School diploma or higher, broken down by race and ethnicity, nationwide from 2011 to 2023.
            </p>
        {/snippet}

        {#snippet scrolly()}
            <ArticleText>
                <h3>Foundational Education</h3>
                <p>
                    Examining high school completion rates shows insight into foundational educational attainment across different racial and ethnic groups in the U.S.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>White and Asian Populations</h3>
                <p>
                    The White and Asian populations consistently show the highest rates of high school completion or higher, both being above 90% throughout the period. By 2023, the White population reached about {dataHSWhite[dataHSWhite.length - 1]}% and the Asian population reached {dataHSAsian[dataHSAsian.length - 1]}%.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>Significant Progress for Black and Hispanic Populations</h3>
                <p>
                    While still being behind White and Asian groups in high school degree attainment, the Black and Hispanic populations have made significant progress. The Black population's rate rose to about {dataHSBlack[dataHSBlack.length - 1]}% by 2023, and the Hispanic population's rate increased to about {dataHSHispanic[dataHSHispanic.length - 1]}%.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>Closing the Gaps</h3>
                <p>
                    The consistent increase across all groups shows a positive trend in access to and completion of basic education. Continued efforts are crucial to make sure that these gains become equitable opportunities for all.
                </p>
            </ArticleText>
        {/snippet}
    </Scroller>
</div>

<style>
    /* Chart container styling */
    .chart-container {
        width: 100%;
        max-width: 600px;
        height: 400px;
        margin: 20px auto;
    }

    /* Chart caption styling */
    .chart-caption {
        font-size: 0.9em;
        color: #555;
        text-align: center;
        margin: 15px 10px;
    }

    /* Basic styling for the sticky content with layout="right" */
    :global(.sticky-content) {
        padding: 20px;
        /* When layout is "right", add a left border for visual separation */
        border-left: 1px solid #eee; /* Added for right layout */
        box-shadow: -2px 0 5px rgba(0,0,0,0.05); /* Added for right layout */
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    /* Adjust padding for the scrolly content */
    :global(.scrolly-content) {
        padding: 40px;
    }
</style>
