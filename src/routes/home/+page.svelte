<script lang="ts">
	import { onMount } from 'svelte';
	import { Button } from '$lib/components/ui/button';
	import { Input } from '$lib/components/ui/input';
	import { Card } from '$lib/components/ui/card';
	import { Separator } from '$lib/components/ui/separator';
	import {
		Search,
		FileText,
		Beaker,
		Download,
		CalendarDays,
		ChevronLeft,
		ChevronRight,
		MessageCircle
	} from 'lucide-svelte';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';

	let searchQuery: string = '';
	let currentBannerIndex = 0;
	let showChatBox = false;

	// Banner images for carousel
	const bannerImages = [
		{
			image: '/api/placeholder/1200/500',
			title: 'บริการวิเคราะห์ทดสอบทางวิทยาศาสตร์',
			description: 'วิเคราะห์ตัวอย่างด้วยเครื่องมือวิทยาศาสตร์ขั้นสูง โดยทีมผู้เชี่ยวชาญ'
		},
		{
			image: '/api/placeholder/1200/500',
			title: 'เครื่อง SEM รุ่นใหม่ล่าสุด',
			description: 'เปิดให้บริการเครื่อง Scanning Electron Microscope รุ่นใหม่ล่าสุดแล้ววันนี้'
		},
		{
			image: '/api/placeholder/1200/500',
			title: 'บริการฝึกอบรมการใช้เครื่องมือ',
			description: 'หลักสูตรอบรมการใช้เครื่องมือวิทยาศาสตร์ขั้นสูงสำหรับนักวิจัย'
		},
		{
			image: '/api/placeholder/1200/500',
			title: 'ขยายเวลาให้บริการ',
			description: 'ขยายเวลาให้บริการจนถึง 20.00 น. ทุกวันทำการ ตั้งแต่วันที่ 1 เมษายน เป็นต้นไป'
		},
		{
			image: '/api/placeholder/1200/500',
			title: 'เปิดให้บริการห้องปฏิบัติการใหม่',
			description: 'เปิดให้บริการห้องปฏิบัติการวิเคราะห์ทดสอบอาหารที่ทันสมัยที่สุด'
		},
		{
			image: '/api/placeholder/1200/500',
			title: 'โครงการความร่วมมือกับภาคอุตสาหกรรม',
			description: 'บริการให้คำปรึกษาและวิเคราะห์ทดสอบผลิตภัณฑ์สำหรับภาคอุตสาหกรรม'
		},
		{
			image: '/api/placeholder/1200/500',
			title: 'กิจกรรม Open House 2568',
			description: 'เปิดบ้านให้ผู้สนใจเยี่ยมชมเครื่องมือและห้องปฏิบัติการ วันที่ 15-16 พฤษภาคม 2568'
		},
		{
			image: '/api/placeholder/1200/500',
			title: 'ทุนวิจัยสำหรับนักศึกษา',
			description: 'เปิดรับข้อเสนอโครงการวิจัยสำหรับนักศึกษาระดับบัณฑิตศึกษา'
		}
	];

	// Partnership logos
	const partners = [
		{ name: 'กระทรวงวิทยาศาสตร์และเทคโนโลยี', logo: '/api/placeholder/160/80', url: '#' },
		{ name: 'สวทช.', logo: '/api/placeholder/160/80', url: '#' },
		{ name: 'สำนักงานกองทุนสนับสนุนการวิจัย', logo: '/api/placeholder/160/80', url: '#' },
		{ name: 'ศูนย์นาโนเทคโนโลยีแห่งชาติ', logo: '/api/placeholder/160/80', url: '#' },
		{ name: 'สถาบันวิจัยดาราศาสตร์แห่งชาติ', logo: '/api/placeholder/160/80', url: '#' },
		{ name: 'มหาวิทยาลัยมหิดล', logo: '/api/placeholder/160/80', url: '#' }
	];

	// Our Services data
	const services = [
		{
			title: 'บริการตรวจวิเคราะห์เชิงคุณภาพ',
			description: 'การตรวจสอบคุณภาพของตัวอย่างด้วยเครื่องมือวิทยาศาสตร์ชั้นสูง',
			icon: Beaker,
			items: [
				'การวิเคราะห์โครงสร้างของสาร',
				'การตรวจสอบองค์ประกอบทางเคมี',
				'การวิเคราะห์คุณสมบัติทางกายภาพ'
			]
		},
		{
			title: 'บริการให้คำปรึกษา',
			description: 'ให้คำปรึกษาด้านการวิจัยและการใช้เครื่องมือวิทยาศาสตร์โดยผู้เชี่ยวชาญ',
			icon: FileText,
			items: [
				'การออกแบบการทดลอง',
				'การเลือกใช้เครื่องมือที่เหมาะสม',
				'การแปลผลข้อมูลทางวิทยาศาสตร์'
			]
		},
		{
			title: 'บริการฝึกอบรม',
			description: 'หลักสูตรฝึกอบรมการใช้เครื่องมือวิทยาศาสตร์ขั้นสูงสำหรับนักวิจัยและผู้สนใจ',
			icon: CalendarDays,
			items: [
				'การใช้งานเครื่องมือวิเคราะห์ขั้นสูง',
				'เทคนิคการเตรียมตัวอย่าง',
				'การวิเคราะห์และแปลผลข้อมูล'
			]
		}
	];

	// News data
	const news = [
		{
			title: 'เปิดให้บริการเครื่อง HPLC รุ่นใหม่ล่าสุด',
			date: '5 มีนาคม 2568',
			summary:
				'ศูนย์เครื่องมือวิทยาศาสตร์ คณะวิทยาศาสตร์ สจล. ได้เปิดให้บริการเครื่อง HPLC รุ่นใหม่ล่าสุดแล้ววันนี้',
			image: '/api/placeholder/400/240'
		},
		{
			title: 'การอบรมเชิงปฏิบัติการการใช้เครื่อง SEM',
			date: '15 มีนาคม 2568',
			summary:
				'ขอเชิญนักวิจัยและผู้สนใจเข้าร่วมการอบรมเชิงปฏิบัติการการใช้เครื่อง Scanning Electron Microscope',
			image: '/api/placeholder/400/240'
		},
		{
			title: 'ประกาศปิดปรับปรุงห้องปฏิบัติการชั้น 5',
			date: '20 มีนาคม 2568',
			summary:
				'แจ้งปิดปรับปรุงห้องปฏิบัติการชั้น 5 ระหว่างวันที่ 25-30 มีนาคม 2568 เพื่อปรับปรุงระบบความปลอดภัย',
			image: '/api/placeholder/400/240'
		}
	];

	// Publications data
	const publications = [
		{
			title: 'คู่มือการใช้งานเครื่องมือวิทยาศาสตร์',
			description: 'เอกสารแนะนำการใช้งานเครื่องมือวิทยาศาสตร์ประเภทต่างๆ',
			fileSize: '2.5 MB',
			fileType: 'PDF'
		},
		{
			title: 'ขั้นตอนการขอใช้บริการศูนย์เครื่องมือวิทยาศาสตร์',
			description: 'คู่มือแนะนำขั้นตอนการขอใช้บริการสำหรับบุคลากรและนักวิจัยภายนอก',
			fileSize: '1.8 MB',
			fileType: 'PDF'
		},
		{
			title: 'รายงานประจำปี 2567',
			description: 'รายงานผลการดำเนินงานของศูนย์เครื่องมือวิทยาศาสตร์ประจำปี 2567',
			fileSize: '3.2 MB',
			fileType: 'PDF'
		},
		{
			title: 'ตารางอัตราค่าบริการ',
			description: 'เอกสารแสดงอัตราค่าบริการการใช้เครื่องมือและบริการวิเคราะห์ต่างๆ',
			fileSize: '1.2 MB',
			fileType: 'PDF'
		}
	];

	// Function to advance the banner carousel
	function nextBanner() {
		currentBannerIndex = (currentBannerIndex + 1) % bannerImages.length;
	}

	function prevBanner() {
		currentBannerIndex = (currentBannerIndex - 1 + bannerImages.length) % bannerImages.length;
	}

	// Set up auto-sliding for banner
	onMount(() => {
		const interval = setInterval(() => {
			nextBanner();
		}, 5000); // Change slide every 5 seconds

		return () => clearInterval(interval);
	});

	// Toggle chat box
	function toggleChatBox() {
		showChatBox = !showChatBox;
	}
</script>

<!-- Main Layout -->
<div class="relative flex min-h-screen flex-col bg-slate-50 font-sans">
	<!-- Header with modern navigation -->
	<Header />

	<main>
		<!-- Banner Carousel Section -->
		<section class="relative h-[500px] overflow-hidden">
			{#each bannerImages as banner, index}
				<div
					class="absolute inset-0 transition-opacity duration-1000"
					style="opacity: {index === currentBannerIndex ? '1' : '0'};"
				>
					<img src={banner.image} alt={banner.title} class="h-full w-full object-cover" />
					<div
						class="absolute inset-0 flex flex-col justify-center bg-gradient-to-r from-blue-900/80 to-transparent px-16"
					>
						<div class="max-w-2xl">
							<h2 class="mb-4 text-5xl font-bold text-white">{banner.title}</h2>
							<p class="mb-8 text-xl text-white/90">{banner.description}</p>
							<Button class="bg-amber-500 px-8 py-6 text-white hover:bg-amber-600"
								>รายละเอียดเพิ่มเติม</Button
							>
						</div>
					</div>
				</div>
			{/each}

			<!-- Banner navigation arrows -->
			<button
				class="absolute left-4 top-1/2 -translate-y-1/2 rounded-full bg-black/30 p-3 text-white hover:bg-black/50"
				on:click={prevBanner}
			>
				<ChevronLeft size={24} />
			</button>
			<button
				class="absolute right-4 top-1/2 -translate-y-1/2 rounded-full bg-black/30 p-3 text-white hover:bg-black/50"
				on:click={nextBanner}
			>
				<ChevronRight size={24} />
			</button>

			<!-- Dots navigation -->
			<div class="absolute bottom-6 left-1/2 flex -translate-x-1/2 space-x-2">
				{#each bannerImages as _, index}
					<button
						class="h-3 w-3 rounded-full transition-colors {index === currentBannerIndex
							? 'bg-white'
							: 'bg-white/50'}"
						on:click={() => (currentBannerIndex = index)}
					></button>
				{/each}
			</div>
		</section>

		<!-- Hero Section with Search -->
		<section
			class="relative overflow-hidden bg-gradient-to-br from-blue-700 to-indigo-900 py-16 text-white"
		>
			<!-- Decorative elements -->
			<div class="absolute left-0 top-0 h-full w-full overflow-hidden opacity-10">
				<div class="absolute -left-10 -top-10 h-40 w-40 rounded-full bg-white"></div>
				<div class="absolute -right-20 top-40 h-80 w-80 rounded-full bg-indigo-400"></div>
				<div class="absolute -bottom-20 -left-20 h-60 w-60 rounded-full bg-blue-400"></div>
			</div>

			<div class="container relative z-10 mx-auto px-4 text-center">
				<h2 class="mb-4 text-5xl font-bold">ศูนย์เครื่องมือวิทยาศาสตร์</h2>
				<h3 class="mb-6 text-3xl font-semibold">
					คณะวิทยาศาสตร์ สถาบันเทคโนโลยีพระจอมเกล้าเจ้าคุณทหารลาดกระบัง
				</h3>
				<p class="mx-auto mb-10 max-w-3xl text-xl opacity-90">
          บริการเครื่องมือวิทยาศาสตร์ชั้นสูงและการวิเคราะห์ทดสอบโดยผู้เชี่ยวชาญ เพื่อการวิจัยและพัฒนาที่มีประสิทธิภาพ
				</p>

				<div class="mx-auto max-w-xl">
					<div
						class="flex w-full items-center space-x-2 rounded-lg bg-white/10 p-1 backdrop-blur-sm"
					>
						<Input
							type="text"
							bind:value={searchQuery}
							placeholder="ค้นหาเครื่องมือหรือบริการ..."
							class="h-14 rounded-md border-0 bg-white/80 text-slate-900 placeholder:text-slate-500"
						/>
						<Button class="h-14 rounded-md bg-amber-500 px-8 text-white hover:bg-amber-600">
							<Search class="mr-2 h-5 w-5" />
							ค้นหา
						</Button>
					</div>
				</div>
			</div>
		</section>

		<!-- Our Services Section -->
		<section class="bg-white py-20">
			<div class="container mx-auto px-4">
				<div class="mb-16 text-center">
					<div
						class="mb-4 inline-block rounded-full bg-blue-100 px-3 py-1 text-sm font-medium text-blue-800"
					>
						บริการของเรา
					</div>
					<h2 class="mb-4 text-4xl font-bold text-slate-900">
						บริการที่ครบวงจรเพื่อการวิจัยที่เป็นเลิศ
					</h2>
					<div class="mx-auto mb-6 h-1 w-24 bg-amber-500"></div>
					<p class="mx-auto max-w-3xl text-lg text-slate-600">
						ศูนย์เครื่องมือวิทยาศาสตร์ให้บริการด้านการวิเคราะห์ทดสอบทางวิทยาศาสตร์โดยทีมงานผู้เชี่ยวชาญ
						พร้อมเครื่องมือที่ทันสมัยและได้มาตรฐานระดับสากล
					</p>
				</div>

				<div class="grid grid-cols-1 gap-8 md:grid-cols-3">
					{#each services as service}
						<Card
							class="overflow-hidden border-none shadow-lg transition-all duration-300 hover:shadow-xl"
						>
							<div class="p-8">
								<div
									class="mb-6 flex h-16 w-16 items-center justify-center rounded-lg bg-blue-100 text-blue-600"
								>
									<svelte:component this={service.icon} size={32} />
								</div>
								<h3 class="mb-3 text-xl font-bold text-slate-900">{service.title}</h3>
								<p class="mb-6 text-slate-600">{service.description}</p>
								<ul class="space-y-2">
									{#each service.items as item}
										<li class="flex items-center text-slate-700">
											<div class="mr-3 h-2 w-2 rounded-full bg-amber-500"></div>
											{item}
										</li>
									{/each}
								</ul>
								<div class="mt-8">
									<Button variant="outline" class="border-blue-600 text-blue-600 hover:bg-blue-50"
										>รายละเอียดเพิ่มเติม</Button
									>
								</div>
							</div>
						</Card>
					{/each}
				</div>
			</div>
		</section>

		<!-- Partnership Section -->
		<section class="bg-slate-100 py-16">
			<div class="container mx-auto px-4">
				<div class="mb-12 text-center">
					<div
						class="mb-4 inline-block rounded-full bg-blue-100 px-3 py-1 text-sm font-medium text-blue-800"
					>
						เครือข่ายความร่วมมือ
					</div>
					<h2 class="mb-4 text-4xl font-bold text-slate-900">พันธมิตรทางวิชาการ</h2>
					<div class="mx-auto mb-6 h-1 w-24 bg-amber-500"></div>
					<p class="mx-auto max-w-3xl text-lg text-slate-600">
						ความร่วมมือกับหน่วยงานชั้นนำทั้งภาครัฐและเอกชน เพื่อพัฒนาการวิจัยและบริการทางวิทยาศาสตร์
					</p>
				</div>

				<div class="grid grid-cols-2 gap-8 md:grid-cols-3 lg:grid-cols-6">
					{#each partners as partner}
						<a
							href={partner.url}
							class="flex items-center justify-center rounded-lg bg-white p-4 shadow transition-shadow duration-300 hover:shadow-md"
						>
							<img
								src={partner.logo}
								alt={partner.name}
								class="h-auto max-w-full"
								title={partner.name}
							/>
						</a>
					{/each}
				</div>
			</div>
		</section>

		<!-- News Section -->
		<section class="bg-white py-20">
			<div class="container mx-auto px-4">
				<div class="mb-16 text-center">
					<div
						class="mb-4 inline-block rounded-full bg-blue-100 px-3 py-1 text-sm font-medium text-blue-800"
					>
						ข่าวสาร/ความเคลื่อนไหว
					</div>
					<h2 class="mb-4 text-4xl font-bold text-slate-900">ข่าวสารและกิจกรรมล่าสุด</h2>
					<div class="mx-auto mb-6 h-1 w-24 bg-amber-500"></div>
					<p class="mx-auto max-w-3xl text-lg text-slate-600">
						ติดตามข่าวสารกิจกรรม การอบรม และข้อมูลล่าสุดเกี่ยวกับศูนย์เครื่องมือวิทยาศาสตร์
					</p>
				</div>

				<div class="grid grid-cols-1 gap-8 md:grid-cols-3">
					{#each news as item, index}
						<Card
							class="h-full overflow-hidden border-none shadow-lg transition-all duration-300 hover:shadow-xl"
						>
							<img src={item.image} alt={item.title} class="h-48 w-full object-cover" />
							<div class="p-6">
								<div class="mb-3 flex items-center text-blue-600">
									<CalendarDays class="mr-2 h-4 w-4" />
									<span class="text-sm">{item.date}</span>
								</div>
								<h3 class="mb-3 text-xl font-bold text-slate-900">{item.title}</h3>
								<p class="mb-6 text-slate-600">{item.summary}</p>
								<Button variant="link" class="h-auto p-0 text-blue-600">อ่านเพิ่มเติม →</Button>
							</div>
						</Card>
					{/each}
				</div>

				<div class="mt-12 text-center">
					<Button variant="outline" class="border-blue-600 px-8 text-blue-600 hover:bg-blue-50"
						>ดูข่าวทั้งหมด</Button
					>
				</div>
			</div>
		</section>

		<!-- Publications Section -->
		<section class="bg-slate-50 py-20">
			<div class="container mx-auto px-4">
				<div class="mb-16 text-center">
					<div
						class="mb-4 inline-block rounded-full bg-blue-100 px-3 py-1 text-sm font-medium text-blue-800"
					>
						เอกสารเผยแพร่
					</div>
					<h2 class="mb-4 text-4xl font-bold text-slate-900">เอกสารและสิ่งพิมพ์</h2>
					<div class="mx-auto mb-6 h-1 w-24 bg-amber-500"></div>
					<p class="mx-auto max-w-3xl text-lg text-slate-600">
						คู่มือการใช้งาน เอกสารเผยแพร่ และรายงานต่างๆ ของศูนย์เครื่องมือวิทยาศาสตร์
					</p>
				</div>

				<div class="grid grid-cols-1 gap-6 md:grid-cols-4">
					{#each publications as pub}
						<Card
							class="h-full overflow-hidden border-none bg-white shadow transition-all duration-300 hover:shadow-xl"
						>
							<div class="p-6">
								<div
									class="mb-4 flex h-12 w-12 items-center justify-center rounded bg-amber-100 text-amber-600"
								>
									<Download size={20} />
								</div>
								<h3 class="mb-2 text-lg font-bold text-slate-900">{pub.title}</h3>
								<p class="mb-4 text-sm text-slate-600">{pub.description}</p>
								<div class="mb-4 flex items-center justify-between text-sm text-slate-500">
									<span>{pub.fileType}</span>
									<span>{pub.fileSize}</span>
								</div>
								<Button class="w-full bg-blue-600 hover:bg-blue-700">
									<Download class="mr-2 h-4 w-4" />
									ดาวน์โหลด
								</Button>
							</div>
						</Card>
					{/each}
				</div>

				<div class="mt-12 text-center">
					<Button variant="outline" class="border-blue-600 px-8 text-blue-600 hover:bg-blue-50"
						>ดูเอกสารทั้งหมด</Button
					>
				</div>
			</div>
		</section>

		<!-- Contact & Location Section -->
		<Footer />
	</main>
</div>
