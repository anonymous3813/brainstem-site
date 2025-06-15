<script>
    export let error;
    export let status;
</script>

<style>
    .error-container {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background: linear-gradient(135deg, #232526 0%, #414345 100%);
        color: #fff;
        font-family: 'Segoe UI', 'Roboto', Arial, sans-serif;
        text-align: center;
        padding: 2rem;
    }
    .status {
        font-size: 6rem;
        font-weight: bold;
        margin-bottom: 0.5rem;
        color: #ff6b6b;
        text-shadow: 2px 2px 8px #2228;
    }
    .message {
        font-size: 1.5rem;
        margin-bottom: 2rem;
        max-width: 600px;
    }
    .home-link {
        display: inline-block;
        margin-top: 1rem;
        padding: 0.75rem 2rem;
        background: #ff6b6b;
        color: #fff;
        border-radius: 2rem;
        text-decoration: none;
        font-weight: 600;
        transition: background 0.2s;
    }
    .home-link:hover {
        background: #ff3b3b;
    }
</style>

<div class="error-container">
    <div class="status">{status || 500}</div>
    <div class="message">
        {error?.message || 'Something went wrong. Please try again later.'}
    </div>
    <a class="home-link" href="/">Go back home</a>
</div>