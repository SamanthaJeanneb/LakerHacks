<script lang="ts">
	import { onMount } from 'svelte';
	import { slide } from 'svelte/transition';
	import TeamItem from '$lib/Components/TeamItem.svelte';
	// Sponsors for LakerHacks
	import CSALogo from '$lib/assets/sponsor_images/lh_logo-csa.png';
	import HCIOLogo from '$lib/assets/sponsor_images/lh_logo-hcio.png';
	// TODO: Find out where the actual MajorLeagueHacking logo is!
	import MajorLeagueHackingLogo from '$lib/assets/sponsor_images/lh_logo-MLH.png';
	import MicronLogo from '$lib/assets/sponsor_images/lh_logo-micron.png';
	import SicuraLogo from '$lib/assets/sponsor_images/lh_logo-sicura.png';
	// TODO: Get the EnterProLogo from Joey
	import EnterProLogo from '$lib/assets/sponsor_images/lh_logo-enterpro.png'
	// TODO: Get the HackUpstate Logo from Joey
	import HackUpstateLogo from '$lib/assets/sponsor_images/lh_logo-hackupstate.png'
	import NovelisLogo from '$lib/assets/sponsor_images/lh_logo-novelis.png';
	import PaulAustinLogo from '$lib/assets/sponsor_images/lh_paulaustin.png';
	// TODO: Get the Pure Button logo from Joey
	import PureButtonLogo from '$lib/assets/sponsor_images/lh_logo-purebuttons.png'
	import QualifAiLogo from '$lib/assets/sponsor_images/lh_logo-qualifAI.png';
	import KenwoodConnectLogo from '$lib/assets/sponsor_images/lh_logo-kenwood.png';
	import WonzonesCalzonesLogo from '$lib/assets/sponsor_images/lh_logo-wonzones.png';
	
	// TODO: Get the following Nord Security images
	import NexosAiLogo from '$lib/assets/sponsor_images/lh_logo-nexosai.svg';
	import NordVPNLogo from '$lib/assets/sponsor_images/lh_logo-nordVPN.png';
	import SailyLogo from '$lib/assets/sponsor_images/lh_logo-sailySim.png';
	import incogniLogo from '$lib/assets/sponsor_images/lh_logo-incogni.png';
	import NordPassLogo from '$lib/assets/sponsor_images/lh_logo-nordPass.png';
	import NordProtectLogo from '$lib/assets/sponsor_images/lh_logo-nordprotect.png'
	// Special thanks for LakerHacks


	import Image1 from '$lib/assets/workingImage1.png';
	import Image2 from '$lib/assets/workingImage2.png';

	// Images of directors, etc.
	import JosephImage from '$lib/assets/josephvega.png';
	import RileyImage from '$lib/assets/rileynixon.png';
	import BavushiImage from '$lib/assets/bivushiBasnet.png';
	import theOneTheOnlyTheGallagher from '$lib/assets/jackGallagher.png';
	import ethanMoody from '$lib/assets/ethanMoody.png';
	import JaceDunlap from '$lib/assets/jaceDunlap.png';
	// For responsive navigation
	let isMenuOpen: boolean = false;
	import { browser } from '$app/environment';

	// Countdown timer
	let days = 0;
	let hours = 0;
	let minutes = 0;
	let seconds = 0;
	let countdownInterval: ReturnType<typeof setInterval>;

	function updateCountdown() {
		const targetDate = new Date('2026-04-18T10:00:00-04:00'); // 10:00 AM EDT (updated from April 18)
		const now = new Date();
		const difference = targetDate.getTime() - now.getTime();

		if (difference <= 0) {
			days = hours = minutes = seconds = 0; // clamp at zero
			if (countdownInterval) clearInterval(countdownInterval);
			return;
		}

		days = Math.floor(difference / (1000 * 60 * 60 * 24));
		hours = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
		minutes = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60));
		seconds = Math.floor((difference % (1000 * 60)) / 1000);
	}
	function toggleMenu(): void {
		isMenuOpen = !isMenuOpen;
	}
	onMount(() => {
		if (!browser) return;

		updateCountdown();
		countdownInterval = setInterval(updateCountdown, 1000);

		const handleClickOutside = (event: MouseEvent): void => {
			const target = event.target as HTMLElement;
			// Only close if clicking outside both the nav and the toggle button
			if (
				isMenuOpen &&
				!target.closest('nav') &&
				!target.closest('button[aria-label="Toggle menu"]')
			) {
				toggleMenu();
			}
		};

		document.addEventListener('click', handleClickOutside);

		return () => {
			document.removeEventListener('click', handleClickOutside);
			clearInterval(countdownInterval);
		};
	});


	// FIXME: Change the registrationURL and the discordURL to be consistent across all components.
	const registrationURL: string = 'https://forms.gle/q8KpPixbczVfDdMs9';
	const discordURL = 'https://discord.gg/GJrP3cQt2x';
	const scheduleURL = "https://docs.google.com/document/d/1pBrEOZ6A4_cW2II83rrgYoqRCfr0ZsESkwK_hocAE28/edit?usp=sharing";

	// eslint-disable-next-line no-undef
	const faqItems: FAQItem[] = [
		{
			question: 'What is a hackathon?',
			answer:
				"Hackathons are events where people come together to build innovative projects and compete for prizes. At LakerHacks, you'll have 24 hours to work with your team to create something amazing. It's a great opportunity to learn valuable skills, meet other developers, and build your portfolio. Whether you're a beginner or an experienced programmer, hackathons are perfect for pushing your boundaries.",
			expanded: false
		},
		{
			question: 'Who can participate?',
			answer:
				"Any college student that is 18 or above, who is passionate about technology and innovation can participate! No matter your major or background, if you're excited about building something cool and learning new skills, LakerHacks is for you.",
			expanded: false
		},
		{
			question: "What if I don't have a team?",
			answer:
				"We'll help you find a team. At the beginning of the hackathon, we'll have team formation activities where you can meet other participants and form teams. You can also join our Discord server before the event to connect with potential teammates.",
			expanded: false
		},
		{
			question: "What if I don't have any coding experience?",
			answer:
				"That's exactly why we have mentors and workshops! We'll have experienced developers and industry professionals available throughout the event to help you learn and build. Our beginner-friendly workshops can help you get started. Many successful hackathon participants start with no coding experience - it's all about the willingness to learn and create!",
			expanded: false
		},
		{
			question: "What if I don't have an idea?",
			answer:
				"No problem! We'll announce our exciting theme and tracks during the opening ceremony, which will give you and your team plenty of inspiration.",
			expanded: false
		}
	];

	function handleFAQClick(index: number): void {
		// Close all other FAQs
		faqItems.forEach((item, i) => {
			if (i !== index) {
				item.expanded = false;
			}
		});
		// Toggle the clicked FAQ
		faqItems[index].expanded = !faqItems[index].expanded;
	}
</script>

<svelte:head>
	<title>LakerHacks - SUNY Oswego's Annual Hackathon</title>
	<meta
		name="description"
		content="Join LakerHacks, SUNY Oswego's biggest annual hackathon! A weekend of coding, innovation, and collaboration for students and tech enthusiasts. Build projects, network, and compete for prizes!"
	/>
</svelte:head>

<div class="graphic flex flex-col text-white">
	<!-- Hero Section -->
	<section id="home" class="mx-auto w-full px-4 py-[100px] text-center">
		<div class="mx-auto flex w-full max-w-[1000px] flex-col gap-[60px]">
			<div class="flex flex-col gap-[10px]">
				<!-- Countdown Timer -->
				<!-- FIXME: Change the following countdown timer to have semantic information for the integers. -->
				<div class="flex justify-center gap-1">
					<div
						class="w-[70px] rounded-lg border border-white/10 bg-[#0B111F]/50 px-2 py-1 backdrop-blur-sm"
					>
						<div class="text-lg font-bold text-[#9CC747]">{days}</div>
						<div class="text-[10px] text-white/80">Days</div>
					</div>
					<div
						class="w-[70px] rounded-lg border border-white/10 bg-[#0B111F]/50 px-2 py-1 backdrop-blur-sm"
					>
						<div class="text-lg font-bold text-[#9CC747]">{hours}</div>
						<div class="text-[10px] text-white/80">Hours</div>
					</div>
					<div
						class="w-[70px] rounded-lg border border-white/10 bg-[#0B111F]/50 px-2 py-1 backdrop-blur-sm"
					>
						<div class="text-lg font-bold text-[#9CC747]">{minutes}</div>
						<div class="text-[10px] text-white/80">Minutes</div>
					</div>
					<div
						class="w-[70px] rounded-lg border border-white/10 bg-[#0B111F]/50 px-2 py-1 backdrop-blur-sm"
					>
						<div class="text-lg font-bold text-[#9CC747]">{seconds}</div>
						<div class="text-[10px] text-white/80">Seconds</div>
					</div>
				</div>
				<h1><span class="text-[#FFE34F]">Laker</span><span class="text-[#9CC747]">Hacks</span></h1>
				<p class="text-white/80">April 18th-19th, 2026</p>

				<div class="mx-auto mt-4 flex max-w-[400px] flex-col justify-center gap-[10px]">
					<a
						href={registrationURL}
						target="_blank"
						rel="noopener noreferrer"
						class="rounded-md bg-[#D4563F] px-6 py-2 text-sm font-medium text-white transition-all hover:bg-[#D4563F]/80"
					>
						Register Now
					</a>
					<a
						href={scheduleURL}
						class="rounded-md border border-[#D4563F] bg-[#0B111F] px-6 py-2 text-sm font-medium text-[#D4563F] transition-all hover:bg-[#050a14]"
					>
						View Schedule
					</a>
				</div>
			</div>

			<!-- YouTube video section -->
			<div
				class="video-container relative mx-auto aspect-video w-full max-w-[1000px] overflow-hidden rounded-xl shadow-[0_0_20px_rgba(0,0,0,0.3)]"
			>
				<iframe
					width="100%"
					height="100%"
					src="https://www.youtube.com/embed/pH_abitLy3E?si=zWJQjMpjPSs2WBvn&rel=0&modestbranding=1"
					title="YouTube video player"
					frameborder="0"
					allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
					referrerpolicy="strict-origin-when-cross-origin"
					allowfullscreen
					class="h-full w-full"
				></iframe>
			</div>
		</div>
	</section>

	<!-- About Section -->
	<section id="about" class="mx-auto w-full px-4 py-[100px] text-center">
		<div class="mx-auto flex max-w-[1000px] flex-col gap-[40px]">
			<h2 class="text-[#9CC747]">About</h2>
			<div
				class="flex flex-col rounded-xl border border-white/10 bg-[#0B111F]/50 p-4 backdrop-blur-sm xl:p-8"
			>
				<p class="text-sm font-normal text-white/80 xl:text-[24px]">
					Launching this spring, LakerHacks is SUNY Oswego's student-led annual hackathon—a
					multi-day event where students design, code, and innovate. With hands-on workshops, talks
					from industry professionals, and fun activities, it's the perfect place to learn, create,
					and connect.
				</p>
			</div>
		</div>
	</section>

<section id="sponsors" class="mx-auto w-full px-4 py-[100px] text-center">
        <div class="mx-auto flex max-w-[1000px] flex-col gap-[40px]">
            <h2 class="text-[#9CC747]">Sponsors (descending by sponsor amount)</h2>
            <div class="flex flex-wrap justify-center gap-[40px] p-4 xl:p-8">
                
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{MajorLeagueHackingLogo}" alt="The Major League Hacking Logo." class="max-h-full max-w-full object-contain" />
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{CSALogo}" alt="CSA Logo" class="max-h-full max-w-full object-contain" />
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{MicronLogo}" alt="The Micron Logo, a stylized Micron." class="max-h-full max-w-full object-contain" />
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{SicuraLogo}" alt="The Sicura Logo, a stylized helmet, with the words Sicura emblazoned next to it." class="max-h-full max-w-full object-contain"/>
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{NordVPNLogo}" alt="The NordVPN Logo, a stylized white mountain against a blue backdrop, with the words nordVPN flanking it from the right." class="max-h-full max-w-full object-contain"/>
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{NordPassLogo}" alt="The NordPass Logo, a stylized white mountain against a teal backdrop, with the words NordPass flanking it from the right." class="max-h-full max-w-full object-contain"/>
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{NordProtectLogo}" alt="The NordVPN Logo, a stylized white mountain against a blue backdrop, with the words nordVPN flanking it from the right." class="max-h-full max-w-full object-contain"/>
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{incogniLogo}" alt="The incogni logo, the word incogni with a filled in o." class="max-h-full max-w-full object-contain"/>
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{SailyLogo}" alt="The Saily logo" class="max-h-full max-w-full object-contain" />
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{NexosAiLogo}" alt="The NexosAI logo" class="max-h-full max-w-full object-contain" />
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{EnterProLogo}" alt="The EnterPro Logo, a left bracket, front slash, and right bracket." class="max-h-full max-w-full object-contain"/>
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{HackUpstateLogo}" alt="The HackUpstate logo, with the words HackUpstate in a teal." class="max-h-full max-w-full object-contain"/>
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{NovelisLogo}" alt="The Novelis Logo, just the words Novelis." class="max-h-full max-w-full object-contain">
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{HCIOLogo}" alt="HCIO Logo" class="max-h-full max-w-full object-contain" />
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{PaulAustinLogo}" alt="Paul Austin" class="max-h-full max-w-full object-contain" />
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{PureButtonLogo}" alt="The Pure Buttons Logo, simply saying Pure." class="max-h-full max-w-full object-contain" />
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{QualifAiLogo}" alt="The QualifAiLogo, a stylized brain with a system BUS running through the middle." class="max-h-full max-w-full object-contain" />
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{KenwoodConnectLogo}" alt="The Kenwood Connect logo, a stylized shield to the left, emblazoned with an open book on the top left, a graduation cap on the top right, a torch on the bottom left, and a globe on the bottom right. To the right of the shield are the words Kenwood." class="max-h-full max-w-full object-contain" /> 
                </div>
                <div class="flex h-[120px] w-[250px] items-center justify-center">
                    <img src="{WonzonesCalzonesLogo}" alt="The Wonzones Calzones logo, simply a circle around the words Wonzones Calzones." class="max-h-full max-w-full object-contain" />
                </div>          
            </div>
            <p class="text-white/80">
                Looking to sponsor? Email us at <a
                    href="mailto:lakerhacks@oswego.edu"
                    class="text-[#D4563F] hover:underline">lakerhacks@oswego.edu</a
                > for more details!
            </p>
        </div>
    </section>
	<!-- TODO: Add a "Special Thanks" section for people that we owe, but did not sponsor us directly. -->
	<section>
	<h1 class="font-bold text-center mb-5">Special Thanks to: </h1>
		<p class="font-normal text-center mb-5">The SUNY Oswego Computer Science Department</p>
		<p class="font-normal text-center mb-5">Student Association</p>
		<p class="font-normal text-center mb-5">The SUNY Oswego Computer Science Association</p>
		<p class="font-normal text-center mb-5">The Human-Computer Interaction Organization</p>
		<p class="font-normal text-center mb-5">Collegiate Science and Technology Entry Program</p>
		<p class="font-normal text-center mb-5">Women in Computing</p>
		<p class="font-normal text-center mb-5">National Society of Black Engineers</p>
		<p class="font-normal text-center mb-5">Content Creation Club</p>
		<p class="font-normal text-center mb-5">Students Helping Oz Peers</p>
		<p class="font-normal text-center mb-5">Auxiliary Services</p>
	</section>

	<!-- Schedule/CTA Section -->
	<section id="schedule" class="mx-auto w-full px-4 py-[100px]">
		<div class="mx-auto flex max-w-[1000px] flex-col gap-[60px]">
			<div class="flex flex-col gap-[50px] xl:flex-row-reverse">
				<div class="w-full xl:h-full xl:w-1/2">
					<img
						src={Image1}
						alt="Students collaborating at a hackathon"
						class="h-full w-full rounded-xl object-cover shadow-[0_0_20px_rgba(0,0,0,0.3)]"
					/>
				</div>
				<div class="flex w-full flex-col justify-center gap-8 text-center xl:w-1/2 xl:text-left">
					<div class="flex flex-col gap-4">
						<h2 class="text-center text-[#9CC747] xl:text-left">Why Hack?</h2>
						<p class="text-center text-white/80 xl:text-left">
							Build something great, collaborate with like-minded innovators, and make an impact.
						</p>
					</div>
					<div class="flex justify-center xl:justify-start">
						<a
							href={registrationURL}
							target="_blank"
							rel="noopener noreferrer"
							class="rounded-md bg-[#D4563F] px-6 py-2 text-sm font-medium text-white transition-all hover:bg-[#D4563F]/80"
						>
							Register Now
						</a>
					</div>
				</div>
			</div>

			<div class="flex flex-col gap-[50px] xl:flex-row">
				<div class="w-full xl:h-full xl:w-1/2">
					<img
						src={Image2}
						alt="Students presenting their hackathon project"
						class="h-full w-full rounded-xl object-cover shadow-[0_0_20px_rgba(0,0,0,0.3)]"
					/>
				</div>
				<div class="flex w-full flex-col justify-center gap-8 text-center xl:w-1/2 xl:text-left">
					<div class="flex flex-col gap-4">
						<h2 class="text-center text-[#9CC747] xl:text-left">What to Expect</h2>
						<p class="text-center text-white/80 xl:text-left">
							Solve real challenges, get expert mentorship, and compete for prizes.
						</p>
					</div>
					<div class="flex justify-center xl:justify-start">
						<a
							href={scheduleURL}
							class="rounded-md border border-[#D4563F] bg-[#0B111F] px-6 py-2 text-sm font-medium text-[#D4563F] transition-all hover:bg-[#050a14]"
						>
							View Schedule
						</a>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- FAQ Section -->
	<section id="faq" class="mx-auto w-full px-4 py-[100px] text-center">
		<div class="mx-auto flex max-w-[1000px] flex-col gap-[40px]">
			<h2 class="text-[#9CC747]">FAQ</h2>
			<div class="flex flex-col rounded-xl border border-white/10 bg-[#0B111F]/50 backdrop-blur-sm">
				{#each faqItems as item, index}
					<div class="flex flex-col">
						<button
							class="button-text flex flex-row items-center gap-[10px] p-[12px] text-left transition-all hover:bg-white/5 xl:p-[20px] {index ===
							0
								? 'rounded-t-xl'
								: ''} {index === faqItems.length - 1 ? 'rounded-b-xl' : ''}"
							on:click={() => handleFAQClick(index)}
						>
						<!-- TODO: Make SVG accessible -->
							<svg
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								class={`transition-transform duration-200 ${item.expanded ? 'rotate-45' : ''}`}
								style="width: 20px; height: 20px; flex-shrink: 0;"
							>
								<path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
							</svg>
							<span class="text-base xl:text-lg">{item.question}</span>
						</button>
						{#if item.expanded}
							<div transition:slide={{ duration: 300 }}>
								<p
									class="pt-[0px] pr-[12px] pb-[12px] pl-[40px] text-left text-sm opacity-70 xl:pr-[20px] xl:pb-[20px] xl:pl-[50.28px] xl:text-base"
								>
									{item.answer}
								</p>
							</div>
							{#if index < faqItems.length - 1}
								<div class="mx-[20px] h-[1px] bg-gray-300/20"></div>
							{/if}
						{:else if index < faqItems.length - 1}
							<div class="mx-[20px] h-[1px] bg-gray-300/20"></div>
						{/if}
					</div>
				{/each}
			</div>
		</div>
	</section>

	<!-- Meet Our Team Section -->
	<section id="team" class="mx-auto w-full px-4 py-[100px] text-center">
		<div class="mx-auto flex max-w-[1000px] flex-col gap-[40px]">
			<h2 class="text-[#9CC747]">Meet Our Team</h2>
			<div class="flex w-full flex-wrap justify-center gap-[20px]">
				<TeamItem
					name="Joseph Vega"
					role="Director"
					linkedinUrl="https://www.linkedin.com/in/jvega2/"
					image={JosephImage}
				/>
				<TeamItem
				name="Shrishtika Bajracharya"
				role="Co-director/MLH head of contact"
				linkedinUrl="https://www.linkedin.com/in/shrishtika/"
				/>
			<TeamItem 
				name="Aditya Raj Singh" 
				role="Devpost & Registration Manager" 
				linkedinUrl="https://www.linkedin.com/in/aditya-raj-singh-14689a351/" 
				image="">
			</TeamItem>
			<TeamItem 
				name="Ananta Bhowmick Antik" 
				role="Marketing Coordinator" 
				linkedinUrl="https://www.linkedin.com/in/ananta-bhowmick/" 
				image="">
			</TeamItem>
			<TeamItem 
				name="Bivushi Basnet" 
				role="Logistics Director" 
				linkedinUrl="https://www.linkedin.com/in/bivushi-basnet777/" 
				image="{BavushiImage}">
			</TeamItem>
			<TeamItem 
				name="Ethanael Moody (Me!)" 
				role="Web Developer" 
				linkedinUrl="https://www.linkedin.com/in/ethanael-m-6581b4186/" 
				image="{ethanMoody}">
			</TeamItem>
			<TeamItem 
				name="Jack Gallagher" 
				role="Sponsorship Coordinator" 
				linkedinUrl="https://www.linkedin.com/in/jack-gallagher-/" 
				image="{theOneTheOnlyTheGallagher}">
			</TeamItem>
			<TeamItem
				name="Jace Dunlap"
				role="Art Director"
				linkedinUrl="https://www.linkedin.com/in/jace-dunlap/?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app"
				image="{JaceDunlap}">
			</TeamItem>
			<TeamItem 
				name="Praneeta Pradhan" 
				role="Budget Manager" 
				linkedinUrl="https://www.linkedin.com/in/praneeta-pradhan/" 
				image="">
			</TeamItem>
			<TeamItem 
				name="Riley Nixon" 
				role="Live Event Coordinator" 
				linkedinUrl="" 
				image={RileyImage}>
			</TeamItem>
			<TeamItem
				name="Yashaswi Shrestha"
				role="Sponsorship Coordinator"
				linkedinUrl="https://www.linkedin.com/in/yshresth/"
				image=""/>
			</div>
		</div>
	</section>

	<!-- Discord Section -->
	<section id="discord" class="hidden"></section>

	<!-- CTA Section -->
	<section id="cta" class="mx-auto w-full px-4 py-[100px] text-center">
		<div class="mx-auto flex max-w-[1000px] flex-col gap-[40px]">
			<h2 class="text-[#9CC747]">Ready to Hack?</h2>
			<div class="flex justify-center">
				<a
					href={registrationURL}
					target="_blank"
					rel="noopener noreferrer"
					class="rounded-md bg-[#D4563F] px-6 py-2 text-sm font-medium text-white transition-all hover:bg-[#D4563F]/80"
				>
					Register Now
				</a>
			</div>
		</div>
	</section>
	<!-- MLH logo section -->
</div>

<!-- Footer Section -->
<footer class="w-full border-t border-gray-800 bg-[#0B111F] px-[20px] py-[40px] text-white">
	<div class="mx-auto max-w-[1000px]">
		<div class="mb-[40px] flex flex-col xl:flex-row">
			<div class="mb-[40px] xl:mb-0">
				<h3 class="mb-4 text-lg font-semibold text-[#9CC747]">Quick Links</h3>
				<ul class="space-y-2">
					<li>
						<a href="#about" class="text-white/80 transition-colors hover:text-white">About</a>
					</li>
					<li>
						<a
							href={scheduleURL}
							target="_blank"
							rel="noopener noreferrer"
							class="text-white/80 transition-colors hover:text-white">Schedule</a
						>
					</li>
					<li><a href="#faq" class="text-white/80 transition-colors hover:text-white">FAQ</a></li>
					<li><a href="#team" class="text-white/80 transition-colors hover:text-white">Team</a></li>
					<li>
						<a href="#sponsors" class="text-white/80 transition-colors hover:text-white">Sponsors</a>
					</li>
					<li>
						<a href="https://github.com/MLH/mlh-policies/blob/main/code-of-conduct.md" class="text-white/80 transition-colors hover:text-white">MLH Code of Conduct</a>
					</li>
				</ul>
			</div>
			<div class="mb-[40px] xl:mb-0 xl:ml-[100px]">
				<h3 class="mb-4 text-lg font-semibold text-[#9CC747]">Contact Us</h3>
				<ul class="space-y-2">
					<li>
						<a
							href="mailto:lakerhacks@oswego.edu"
							class="text-white/80 transition-colors hover:text-[#D4563F]"
							>
							lakerhacks@oswego.edu
						</a>
					</li>
				</ul>
			</div>
			<div class="xl:ml-auto">
				<h3 class="mb-4 text-lg font-semibold text-[#9CC747]">Stay Connected</h3>
				<ul class="space-y-2">
					<li>
						<a
							href={discordURL}
							target="_blank"
							rel="noopener noreferrer"
							class="inline-flex items-center gap-2 text-white/80 transition-colors hover:text-[#5865F2]"
						>
							<svg class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24"
								><path
									d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515a.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0a12.64 12.64 0 0 0-.617-1.25a.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 0 0 .031.057a19.9 19.9 0 0 0 5.993 3.03a.078.078 0 0 0 .084-.028a14.09 14.09 0 0 0 1.226-1.994a.076.076 0 0 0-.041-.106a13.107 13.107 0 0 1-1.872-.892a.077.077 0 0 1-.008-.128a10.2 10.2 0 0 0 .372-.292a.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127a12.299 12.299 0 0 1-1.873.892a.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028a19.839 19.839 0 0 0 6.002-3.03a.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419c0-1.333.956-2.419 2.157-2.419c1.21 0 2.176 1.096 2.157 2.42c0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419c0-1.333.955-2.419 2.157-2.419c1.21 0 2.176 1.096 2.157 2.42c0 1.333-.946 2.418-2.157 2.418z"
								/></svg
							>
							Join Discord
						</a>
					</li>
					<li>
						<a
							href="https://www.instagram.com/lakerhacks/"
							target="_blank"
							rel="noopener noreferrer"
							class="inline-flex items-center gap-2 text-white/80 transition-colors hover:text-[#E1306C]"
						>
							<svg class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24"
								><path
									d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"
								/></svg
							>
							Instagram
						</a>
					</li>
				</ul>
			</div>
		</div>
		<div class="border-t border-gray-800 pt-8">
			<p class="text-[14px] text-white/60">&copy; {new Date().getFullYear()} LakerHacks</p>
		</div>
	</div>
</footer>

<style>
	/* Add any additional custom styles here */
	:global(html) {
		scroll-behavior: smooth;
	}

	div.graphic {
		background-image: url('/src/lib/assets/background-graphic.png');
		background-size: auto;
		background-repeat: no-repeat;
		background-position: center top;
		min-height: 100vh;
		overflow-x: hidden;
	}

	.button-text {
		font-size: 24px;
		line-height: 1.5;
		cursor: pointer;
	}

	/* Video container styles */
	.video-container {
		transition: filter 0.5s ease-in-out;
		position: relative;
		width: 100%;
		height: 100%;
	}
</style>
