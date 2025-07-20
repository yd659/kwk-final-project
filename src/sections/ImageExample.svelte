<script>
    import * as Highcharts from "highcharts";
    import "highcharts/modules/exporting";
    import { Chart } from "@highcharts/svelte";
    import Scroller from "../lib/Scroller.svelte";
    import ArticleText from "../lib/ArticleText.svelte";

    const chartYears = [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023];
    const dataMaleAsian = [19.0, 19.5, 20.0, 21.5, 22.0, 22.5, 24.0, 24.5, 25.5, 26.0, 26.0, 26.0, 26.2]; // Approx
    const dataMaleBlack = [12.5, 13.0, 13.5, 14.0, 14.5, 15.0, 16.0, 16.5, 17.0, 18.0, 18.0, 18.0, 19.6]; // Approx
    const dataMaleHispanic = [12.0, 12.5, 13.0, 13.5, 14.0, 14.5, 15.0, 15.5, 16.0, 17.0, 18.0, 18.0, 19.6]; // Approx
    const dataMaleWhite = [53.0, 54.5, 55.5, 57.0, 58.0, 59.5, 60.5, 61.0, 62.0, 63.0, 63.5, 63.5, 65.1]; // Approx
    const dataMaleTotal = [33.0, 34.0, 35.0, 36.5, 37.5, 38.5, 39.5, 40.0, 41.0, 41.0, 41.0, 41.0, 41.0]; // Approx

    let options = {
        chart: {
            type: "line",
            animation: false,
        },
        title: {
            text: "Bachelor's Degree or Higher Attainment for Males by Race or Ethnicity (Nationwide, 2011-2023)",
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
                name: "Total (Male)",
                data: dataMaleTotal,
                color: '#808080'
            },
            {
                name: "Asian (Male)",
                data: dataMaleAsian,
                color: '#4CAF50'
            },
            {
                name: "Black (Male)",
                data: dataMaleBlack,
                color: '#FF5722'
            },
            {
                name: "Hispanic (Male)",
                data: dataMaleHispanic,
                color: '#9C27B0'
            },
            {
                name: "White (Male)",
                data: dataMaleWhite,
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
                This chart shows Bachelor's degree attainment rates specifically for males, broken up by race and ethnicity, from 2011 to 2023.
            </p>
        {/snippet}

        {#snippet scrolly()}
            <ArticleText>
                <h3>Focusing on males</h3>
                <p>
                    Looking at Bachelor's degree attainment rates among males shows distinct trends between various races and ethnicities.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>White Males</h3>
                <p>
                    The White male population consistently shows the highest Bachelor's degree attainment rates, reaching about {dataMaleWhite[dataMaleWhite.length - 1]}% by 2023. This shows a trend of higher education completion within this demographic.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>Black and Hispanic Males</h3>
                <p>
                    Similar to the overall population and female trends, Black and Hispanic males face significant disparities in Bachelor's degree attainment. In 2023, the rate for Black males was around {dataMaleBlack[dataMaleBlack.length - 1]}%, and for Hispanic males, it was about {dataMaleHispanic[dataMaleHispanic.length - 1]}%. These rates are a lot lower than those for White males.
                </p>
            </ArticleText>

            <ArticleText>
                <h3>Understanding Disparities</h3>
                <p>
                    When comparing male and female degree attainment rates, it is clear that while overall trends for some groups may be similar, the extent of disparities can vary. Understanding these intersectional differences by both race and sex is very important for developing targeted solutions for educational equity.
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

    /* Basic styling for the sticky content with layout="right" (or "left") */
    :global(.sticky-content) {
        padding: 20px;
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