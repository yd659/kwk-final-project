<script>
    let { title, subtitle } = $props();
</script>

<div class="title-card">
    <div class="content">
        <h1>{title}</h1>
        <p>{subtitle}</p>
    </div>
</div>

<style>
    .title-card {
        background-color: #000000;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        padding: 2rem;
        box-sizing: border-box;
        font-family: "Georgia", serif;
    }

    .content {
        max-width: 700px;
        background-color: #808080;
        padding: 2rem;
        border: 6px solid #F0F8FF;
        border-radius: 2rem;
        box-shadow: 16px 16px #000000;
    }

    h1 {
        font-size: 3rem;
        margin: 0;
        color: #F0F8FF;
        text-shadow: 1px 1px 0 #000000;
    }

    p {
        font-size: 1.3rem;
        color: #f7f5eb;
        margin-top: 1rem;
    }

    @media (max-width: 600px) {
        h1 {
            font-size: 2.2rem;
        }

        p {
            font-size: 1.1rem;
        }
    }
</style>
