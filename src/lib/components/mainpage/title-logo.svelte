<title>ACM Algo at CSUF</title>
<div class="top-section">
	<h1 class="top-section-text title-text">
		Make shit <span style="color: var(--algo-purple);"><b>happen.</b></span>
	</h1>
	<img src="/icons/algo-logo.svg" alt="algo logo" class="top-section-icon" />
</div>

<style>
	.top-section {
		width: 80%;
		display: flex;
		align-items: center;
	}
	.top-section-text {
		text-align: center;
		width: 50%;
	}
	.top-section-icon {
		width: 50%;
		aspect-ratio: 1 / 1;
		animation: 1.75s linear 0s infinite normal slight-wiggle;
	}
	.title-text {
		font-size: 3rem;
	}
	@media only screen and (max-width: 600px) {
		.title-text {
			font-size: 1rem;
		}
	}
	@keyframes slight-wiggle {
		0% {
			transform: rotate(0);
		}
		25% {
			transform: rotate(-2deg);
		}
		50% {
			transform: rotate(0);
		}
		75% {
			transform: rotate(2deg);
		}
		100% {
			transform: rotate(0);
		}
	}
</style>
