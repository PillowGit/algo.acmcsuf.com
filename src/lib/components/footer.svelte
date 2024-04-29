<div class="footer-container">
    <div class="footer-bg"></div>
    <div class="footer-content">
        <h3>Made with 💜 by <a href="https://pillo.dev" target="_blank" style="color: var(--algo-purple);">Pillow</a>. Powered by SvelteKit.</h3>
    </div>
</div>

<style>
    .footer-bg {
        z-index: 13;
        width: 100%;
        height: 0.5vh;
        background: linear-gradient(90deg, rgba(109,98,214,1) 0%, rgba(95,82,209,1) 50%, rgba(65,50,221,1) 100%);
    }
    .footer-container {
        display: flex;
        flex-direction: column;
        align-items: center;

        position: relative;
        z-index: 14;

        min-height: 10vh;
        width: 100%;

        background-color: var(--bg-color);
    }
    .footer-content {
        width: 70%;
        margin-top: 3vh;
    }
    .footer-content h3 {
        text-align: center;
        font-size: 1.2rem;
    }
    @media only screen and (max-width: 600px) {
        .footer-content {
            width: 100%;
        }
        .footer-content h3 {
            font-size: 0.8rem;
        }
    }
</style>