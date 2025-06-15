<script lang="ts">
  const {title, text} = $props();
</script>

<div class="scroll-card">
  <div class="card-content">
    <h2>{title}</h2>
    <p>{text}</p>
  </div>
</div>

<style>
  /* Individual Scroll Card */
  .scroll-card {
    scroll-snap-align: start; /* Ensures the card snaps to the top */
    height: 100vh; /* Each card takes full viewport height */
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2.5rem; /* More generous padding */
    box-sizing: border-box; /* Include padding in height calculation */
  }

  .card-content {
    max-width: 650px; /* Wider content area */
    background: rgba(30, 30, 30, 0.95); /* Darker, more solid background */
    padding: 3rem; /* More internal padding */
    border-radius: 1.5rem; /* More pronounced rounded corners */
    box-shadow: 0 15px 60px rgba(0, 0, 0, 0.7), inset 0 0 15px rgba(102, 255, 255, 0.1); /* Stronger shadow, subtle inner glow */
    text-align: center;
    border: 1px solid rgba(70, 70, 70, 0.6); /* Slightly more prominent border */
    transform: translateY(0); /* Base state for potential animation */
    opacity: 1; /* Base state for potential animation */
    transition: transform 0.5s ease-out, opacity 0.5s ease-out; /* For card reveal effects */
  }

  .card-content h2 {
    font-size: clamp(2rem, 3.5vw, 2.8rem); /* Slightly larger, more imposing headings */
    margin-bottom: 1.5rem;
    color: #66ffff; /* Bright cyan for impact */
    text-shadow: 0 0 10px rgba(102, 255, 255, 0.6), 0 0 20px rgba(102, 255, 255, 0.2); /* Stronger glow */
    letter-spacing: 0.05em; /* Slightly increased letter spacing */
  }

  .card-content p {
    font-size: clamp(1.05rem, 1.6vw, 1.25rem); /* Slightly larger body text */
    color: #c0c0c0; /* Softer gray for readability */
  }

  /* Media Queries for Responsiveness within the card */
  @media (max-width: 768px) {
    .card-content {
      padding: 1.8rem;
    }
    .card-content h2 {
      font-size: 2rem;
    }
    .card-content p {
      font-size: 1.1rem;
    }
  }

  @media (max-width: 480px) {
    .card-content {
      padding: 1.2rem;
      border-radius: 1rem;
    }
    .card-content h2 {
      font-size: 1.7rem;
    }
    .card-content p {
      font-size: 0.95rem;
    }
  }
</style>
