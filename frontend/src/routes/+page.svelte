<script>
	import { onMount } from 'svelte';
	import Navbar from '../lib/Navbar.svelte';
	import Marquee from 'svelte-fast-marquee';
	function iOS() {
		return (
			navigator.platform.startsWith('iP') ||
			(navigator.platform.startsWith('Mac') && navigator.maxTouchPoints > 4)
		);
	}

	let isIOS;

	onMount(() => {
		isIOS = iOS();
	});

	function requestMotionPermission() {
		if (
			typeof DeviceMotionEvent !== 'undefined' &&
			typeof DeviceMotionEvent.requestPermission === 'function'
		) {
			DeviceMotionEvent.requestPermission()
				.then((permissionState) => {
					if (permissionState === 'granted') {
						isIOS = false;
					} else {
						alert('Permission denied for motion data');
					}
				})
				.catch((error) => {
					console.error('Error requesting motion permission:', error);
				});
		} else {
			alert(
				'DeviceMotionEvent is not supported or permission request is not needed on this device'
			);
		}
	}
</script>

<div class="bg-[url('/grid.apng')] bg-center bg-cover h-[100vh]" style="image-rendering:pixelated">
	<div class="fixed top-0 left-0 w-full p-2 bg-black/50 b">
		<Marquee pauseOnHover={true} className=" w-full">
			<div class="grid grid-cols-3 justify-between w-full font-1 font-semibold">
				<div>
					<p class="text-center font-1">Thank god phones can't get concussed!</p>
				</div>
				<div>
					<p class="text-center font-1">
						Free AppleCare+ for the top of the leaderboard! (terms apply) [you're not getting
						anything]
					</p>
				</div>
				<div>
					<p class="text-center font-1">You need a new phone anyway!</p>
				</div>
			</div>
		</Marquee>
	</div>
	<div class="hero w-full h-[80vh]">
		<div class="hero-content flex-col text-center">
			<!-- <h1 class="font-1 text-5xl font-bold">Chuck that thang!!</h1> -->
            <img src="/logo.apng" alt="" class="h-40">

			<div class="mt-2 flex font-1 flex-col gap-2">
				{#if isIOS}
					<div class="fixed top-0 left-0 z-50 h-screen w-full bg-black opacity-75"></div>

					<div class="absolute z-60 top-[10%] left-0 text-left p-4">
						<p class="font-2 text-xl font-extrabold mb-2 text-center">
							I think your accelerometer's broken. Can I check?
						</p>

						<div class="bg-base-300 p-10 mt-4">
							<p class=" text-center">Please accept our permissions to see our magic.</p>

							<button class="btn btn-primary mx-auto w-full mt-4" onclick={requestMotionPermission}>
								Accept Permissions
							</button>
						</div>
						<p class="text-center mt-2">We wont hack you. I promise🥺</p>
					</div>
				{/if}
                <a class="btn text-lg btn-primary scale-150 my-3" href="/lobby"
					>Head-to-head<svg
						xmlns="http://www.w3.org/2000/svg"
						viewBox="0 0 24 24"
						fill="currentColor"
						class="size-6"
					>
						<path
							fillRule="evenodd"
							d="M1.371 8.143c5.858-5.857 15.356-5.857 21.213 0a.75.75 0 0 1 0 1.061l-.53.53a.75.75 0 0 1-1.06 0c-4.98-4.979-13.053-4.979-18.032 0a.75.75 0 0 1-1.06 0l-.53-.53a.75.75 0 0 1 0-1.06Zm3.182 3.182c4.1-4.1 10.749-4.1 14.85 0a.75.75 0 0 1 0 1.061l-.53.53a.75.75 0 0 1-1.062 0 8.25 8.25 0 0 0-11.667 0 .75.75 0 0 1-1.06 0l-.53-.53a.75.75 0 0 1 0-1.06Zm3.204 3.182a6 6 0 0 1 8.486 0 .75.75 0 0 1 0 1.061l-.53.53a.75.75 0 0 1-1.061 0 3.75 3.75 0 0 0-5.304 0 .75.75 0 0 1-1.06 0l-.53-.53a.75.75 0 0 1 0-1.06Zm3.182 3.182a1.5 1.5 0 0 1 2.122 0 .75.75 0 0 1 0 1.061l-.53.53a.75.75 0 0 1-1.061 0l-.53-.53a.75.75 0 0 1 0-1.06Z"
							clipRule="evenodd"
						/>
					</svg>
				</a>
				<a class="btn text-lg btn-outline scale-150 my-3" href="/local">
					Pass and Play<svg
						xmlns="http://www.w3.org/2000/svg"
						viewBox="0 0 24 24"
						fill="currentColor"
						class="size-6"
					>
						<path d="M10.5 18.75a.75.75 0 0 0 0 1.5h3a.75.75 0 0 0 0-1.5h-3Z" />
						<path
							fillRule="evenodd"
							d="M8.625.75A3.375 3.375 0 0 0 5.25 4.125v15.75a3.375 3.375 0 0 0 3.375 3.375h6.75a3.375 3.375 0 0 0 3.375-3.375V4.125A3.375 3.375 0 0 0 15.375.75h-6.75ZM7.5 4.125C7.5 3.504 8.004 3 8.625 3H9.75v.375c0 .621.504 1.125 1.125 1.125h2.25c.621 0 1.125-.504 1.125-1.125V3h1.125c.621 0 1.125.504 1.125 1.125v15.75c0 .621-.504 1.125-1.125 1.125h-6.75A1.125 1.125 0 0 1 7.5 19.875V4.125Z"
							clipRule="evenodd"
						/>
					</svg>
				</a>
				<p class="text-3xl">or</p>
                <a class="btn text-lg btn-outline scale-150 my-3" href="/local">
					Singleplayer<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0ZM4.501 20.118a7.5 7.5 0 0 1 14.998 0A17.933 17.933 0 0 1 12 21.75c-2.676 0-5.216-.584-7.499-1.632Z" />
                      </svg>                      
				</a>
			</div>
		</div>
	</div>
</div>
