<script>
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";
    import "$lib/styles/styles.scss";
    import Navbar from "$lib/components/Navbar.svelte";
</script>

<Navbar />
<!-- <Header /> -->

<main>
    <slot />
</main>

<Footer />

<style>
    @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@500&display=swap");
    :global(*) {
        font-family: "Poppins", sans-serif;
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        text-decoration: none;
        
    }
    :global(:root) {
        --alert: #e03616;
        --caution: #f3a712;
        --confirm: #08A045;
        --light: #f5f5f5;
        --dark: #343333;
    }
    :global(body) {
        background: var(--light);
        color: var(--dark);
        max-width: 100%;
        overflow-x: hidden;
        height: 100%;
    }
    :global(html) {
        max-width: 100%;
        overflow-x: hidden;
        height: 100%;
    }
    :global(.title){
            display: flexbox;
            font-weight: bold;
            text-shadow: 0.125rem 0.125rem 0.313rem rgba(99, 99, 99, 0.75);
            text-align: center;
            margin: auto;
            padding-bottom: 50px;
            margin-top: 50px;
            color: var(--dark)

    }
   
</style>
