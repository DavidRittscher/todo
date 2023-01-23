<script>
    let isMenuOpen = false;

    function toggleMenu() {
        isMenuOpen = !isMenuOpen;
    }

    let current = 0;
</script>

<div class="navbar">
    <button class="logo"><h1>Welcome</h1></button>
    <nav class:open={isMenuOpen}>
        <ul>
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <li on:click={() => (isMenuOpen = false)}>
                <a
                    class:current={current === 0}
                    on:click={() => (current = 0)}
                    href="/">Home</a
                >
            </li>
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <li on:click={() => (isMenuOpen = false)}>
                <a
                    class:current={current === 1}
                    on:click={() => (current = 1)}
                    href="/about">About</a
                >
            </li>
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <li on:click={() => (isMenuOpen = false)}>
                <a
                    class:current={current === 2}
                    on:click={() => (current = 2)}
                    href="/todo">To-Do App</a
                >
            </li>
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <li on:click={() => (isMenuOpen = false)}>
                <a
                    class:current={current === 3}
                    on:click={() => (current = 3)}
                    href="/contact">Contact</a
                >
            </li>
        </ul>
    </nav>
    <button class="burger" on:click={toggleMenu} class:open={isMenuOpen}>
        <div class="bar-1" />
        <div class="bar-2" />
        <div class="bar-3" />
    </button>
</div>

<style>
    .navbar {
        background-color: var(--dark);
        display: flex;
        justify-content: space-between;
        align-items: center;
        position: relative;
        color: var(--light);
        height: 4rem;
        z-index: 7;
    }
    .logo {
        margin-left: 6vw;
        color:var(--light);
        background-color: transparent;
        border: none;
    }

    @media only screen and (max-width: 767px) {
        nav {
            opacity: 0;
            display: none;
            display: block;
            position: absolute;
            top: 100%;
            left: 100%;
            background-color: var(--dark);
            width: 100%;
            transition: all 300ms ease-in-out;
        }
        nav.open {
            opacity: 1;
            left: 0;
        }
    }
    a {
        transition: text-decoration-color 0.5s 0s ease-in, all 0.5s 0s ease;
    }
    a:visited {
        color: var(--light);
    }
    a:hover {
        text-decoration-color: var(--light);
    }

    ul {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        gap: 5vh;
        margin-top: 2vh;
        margin-bottom: 4vh;
        list-style: none;
        font-size: 1.1rem;
    }
    /* navlink animation */
    li > a {
        display: inline-block;
        transition: all 200ms ease-in-out;
    }
    li > a:hover {
        transform: scale(1.1);
    }
    li > a:active {
        transform: scale(0.9);
    }
    li:last-child {
        background-color: var(--caution);
        padding: 0.4rem 1rem;
        border-radius: 10px;
        font-weight: 500;
    }
    .current {
        position: relative;
    }
    .current::after {
        content: "";
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 2px;
        background-color: var(--caution);
    }
    .burger {
        height: 28px;
        aspect-ratio: 1;
        border: 2px solid var(--light);
        background-color: transparent;
        border-radius: 5px;
        margin-right: 6vw;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .burger > div {
        height: 2px;
        width: 14px;
        background-color: var(--light);
        position: absolute;
        transition: all 300ms ease-in-out;
        color: var(--alert);
    }
    .bar-1 {
        transform: translateY(-5px);
    }

    .bar-3 {
        transform: translateY(5px);
    }
    /* menu icon animation */
    .burger.open .bar-1 {
        transform: rotatez(45deg);
    }
    .burger.open .bar-2 {
        opacity: 0;
    }
    .burger.open .bar-3 {
        transform: rotatez(-45deg);
    }
    @media only screen and (min-width: 768px) {
        .logo {
            margin-left: 3vw;
        }
        .burger {
            display: none;
        }
        nav {
            display: block;
            position: relative;
        }
        ul {
            margin: 0;
            flex-direction: row;
            gap: 2vw;
        }
        li:last-child {
            margin-inline: 2vw;
        }
    }
</style>
