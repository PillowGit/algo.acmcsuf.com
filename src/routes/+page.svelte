<script lang="ts">

</script>

<div class="page-content">
  <img src="icons/algo-logo.svg" alt="algo-logo"/>
</div>

<style>
  .page-content {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-flow: column nowrap;
  }
  .page-content>img {
    margin-top: 10%;
    width: 20%;
    aspect-ratio: 1 / 1;

    animation: sillylogo 2s infinite linear;
    animation-delay: 1s;
  }
  @keyframes sillylogo {
    0% {
      transform: none;
    }
    40% {
      transform: rotateX(180deg) translateY(-20rem);
    }
    80% {
      transform: rotateX(360deg);
    }
    100% {
      transform: rotateX(360deg) scaleX(-1);
    }
  }
</style>