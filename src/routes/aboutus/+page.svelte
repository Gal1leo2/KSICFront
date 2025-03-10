<script lang="ts">
	import { Card } from '$lib/components/ui/card';
	import { Button } from '$lib/components/ui/button';
	import { Separator } from '$lib/components/ui/separator';
	import {
		Search,
		Microscope,
		Dna,
		TestTube,
		Omega,
		Bolt,
		Clock,
		Award,
		Users,
		Globe
	} from 'lucide-svelte';

	const teamMembers = [
		{
			name: 'Asst.Prof.Dr.Pisan Sukwisute',
			role: 'Director',
			description:
				'Pioneering researcher with over 20 years of experience in scientific instrumentation and advanced research methodologies.',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		}
	];

	const milestones = [
		{ year: 2005, event: 'Establishment of the Science Instrument Center', icon: Clock },
		{ year: 2012, event: 'First advanced electron microscopy facility', icon: Microscope },
		{
			year: 2018,
			event: 'Expanded services to support national research initiatives',
			icon: Globe
		},
		{ year: 2022, event: 'Certified ISO 9001:2015 for scientific testing services', icon: Award }
	];
</script>

<!-- Main Layout -->
<div class="flex min-h-screen flex-col bg-slate-50 font-sans">
	<!-- Header (Same as main page) -->
  <header class="bg-white border-b sticky top-0 z-10">
    <div class="container mx-auto px-4 py-3">
      <div class="flex justify-between items-center">
        <!-- Logo (Wait Ploy) -->
        <div class="flex items-center space-x-2">
          <div class="h-10 w-10 rounded-full bg-blue-600 flex items-center justify-center">
            <span class="text-white font-bold text-xl">SC</span>
          </div>
          <h1 class="text-xl font-bold hidden sm:block">
            <span class="text-blue-600">KMITL</span> Science Instrument Center
          </h1>
        </div>
        
        <!-- Navigation -->
        <nav class="hidden md:flex space-x-6">
          <a href="/" class="text-slate-700 hover:text-blue-600 font-medium transition-colors">Services</a>
          <a href="/prices" class="text-slate-700 hover:text-blue-600 font-medium transition-colors">Service Rates</a>
          <a href="/instruments" class="text-slate-700 hover:text-blue-600 font-medium transition-colors">Instruments</a>
          <a href="/aboutus" class="text-slate-700 hover:text-blue-600 font-medium transition-colors">About Us</a>
          <a href="/personnel" class="text-slate-700 hover:text-blue-600 font-medium transition-colors">บุคลากร</a>
        </nav>
        
        <!-- Mobile Navigation Button -->
        <Button variant="ghost" size="icon" class="md:hidden">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="4" x2="20" y1="12" y2="12"/><line x1="4" x2="20" y1="6" y2="6"/><line x1="4" x2="20" y1="18" y2="18"/></svg>
        </Button>
      </div>
    </div>
  </header>

	<main>
		<!-- Hero Section -->
		<section
			class="relative overflow-hidden bg-gradient-to-br from-blue-50 via-indigo-50 to-blue-100 py-20"
		>
			<div class="bg-grid-slate-200 absolute inset-0 opacity-20"></div>
			<div class="container relative z-10 mx-auto px-4 text-center">
				<h2 class="mb-6 text-5xl font-bold tracking-tight text-slate-900">
					เกี่ยวกับ KMITL <span class="text-blue-600">Science Instrument Center</span>
				</h2>
				<p class="mx-auto mb-10 max-w-2xl text-xl leading-relaxed text-slate-700">
          มุ่งเป็นหน่วยงานบริการทดสอบและตรวจวิเคราะห์ที่มีคุณภาพขับเคลื่อนงานวิจัยและนวัตกรรมด้านวิทยาศาสตร์ของประเทศ
				</p>
				<div class="flex justify-center space-x-4">
					<Button class="bg-blue-600 px-6 py-3 text-white hover:bg-blue-700">เครื่องมือของเรา</Button>
					<Button
						variant="outline"
						class="border-blue-600 px-6 py-3 text-blue-600 hover:bg-blue-50"
					>
						ติดต่อเรา
					</Button>
				</div>
			</div>
		</section>

		<!-- Our Mission Section -->


		<!-- Key Milestones -->
		<section class="bg-gradient-to-br from-slate-50 to-blue-50 py-20">
			<div class="container mx-auto px-4">
				<div class="mb-12 text-center">
					<h3 class="mb-2 text-lg font-semibold text-blue-600">ประวัติของเรา</h3>
					<h2 class="mb-4 text-3xl font-bold text-slate-900">เหตุการณ์สำคัญ
          </h2>
					<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
				</div>

				<div class="grid grid-cols-1 gap-8 md:grid-cols-4">
					{#each milestones as milestone, i}
						<Card
							class="rounded-xl border-t-4 p-8 text-center transition-all duration-300 hover:translate-y-[-5px] hover:shadow-xl"
							style="border-top-color: var(--colors-blue-{500 + i * 100});"
						>
							<div
								class="mx-auto mb-6 flex h-16 w-16 items-center justify-center rounded-full bg-blue-100"
							>
								<svelte:component this={milestone.icon} class="h-8 w-8 text-blue-600" />
							</div>
							<div class="mb-3 text-4xl font-bold text-blue-600">{milestone.year}</div>
							<p class="text-slate-700">{milestone.event}</p>
						</Card>
					{/each}
				</div>
			</div>
		</section>

		<!-- Team Members -->
		<section class="bg-white py-20">
			<div class="container mx-auto px-4">
				<div class="mb-12 text-center">
          <h3 class="mb-2 text-lg font-semibold text-blue-600">OUR HEAD  </h3>
					<h2 class="mb-4 text-3xl font-bold text-slate-900">หัวหน้าศูนย์เครื่องมือ</h2>
					<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
					<p class="mx-auto mt-6 max-w-2xl text-slate-600">
						Our team of dedicated scientists and specialists works tirelessly to advance research
						capabilities at KMITL and beyond
					</p>
				</div>

				<div class="grid grid-cols-1 gap-10 md:grid-cols-3 justify-center place-items-center">
					{#each teamMembers as member}
						<Card
							class="center overflow-hidden rounded-xl border-b-4 border-blue-600 shadow-lg transition-all duration-300 hover:shadow-xl"
						>
							<div class="relative">
								<img src={member.image} alt={member.name} class="h-72 w-full object-cover -mt-5" />
								<div
									class="absolute bottom-0 left-0 right-0 h-24 bg-gradient-to-t from-slate-900 to-transparent"
								></div>
							</div>
							<div class="p-8">
								<h3 class="mb-2 text-2xl font-bold text-slate-900">{member.name}</h3>
								<p class="mb-4 flex items-center font-medium text-blue-600">
									<Users class="mr-2 h-4 w-4" />
									{member.role}
								</p>
								<Separator class="mb-4" />
								<p class="text-slate-600">{member.description}</p>
							</div>
						</Card>
					{/each}
				</div>
			</div>
		</section>

		<!-- พันธกิจ (Mission) Section -->

    <!-- วิสัยทัศน์ (Vision) Section -->
<section class="py-20 bg-white">
  <div class="container mx-auto px-4 max-w-5xl">
    <div class="text-center mb-12">
      <h3 class="text-blue-600 font-semibold text-lg mb-2">OUR VISION</h3>
      <h2 class="text-3xl font-bold text-slate-900 mb-4">วิสัยทัศน์</h2>
      <div class="h-1 w-24 bg-blue-600 mx-auto rounded-full"></div>
    </div>
    
    <Card class="p-10 shadow-xl rounded-xl bg-gradient-to-r from-blue-50 to-indigo-50 border-l-4 border-blue-600">
      <p class="text-slate-800 text-xl text-center font-medium leading-relaxed">
        มุ่งเป็นหน่วยงานบริการทดสอบและตรวจวิเคราะห์ที่มีคุณภาพขับเคลื่อนงานวิจัยและนวัตกรรมด้านวิทยาศาสตร์ของประเทศ
      </p>
    </Card>
  </div>
</section>

<!-- พันธกิจ (Mission) Section -->
<section class="py-20 bg-gradient-to-br from-slate-50 to-blue-50">
  <div class="container mx-auto px-4 max-w-5xl">
    <div class="text-center mb-12">
      <h3 class="text-blue-600 font-semibold text-lg mb-2">OUR MISSION</h3>
      <h2 class="text-3xl font-bold text-slate-900 mb-4">พันธกิจ</h2>
      <div class="h-1 w-24 bg-blue-600 mx-auto rounded-full"></div>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
      <Card class="p-8 shadow-lg rounded-xl overflow-hidden relative hover:shadow-xl transition-all duration-300 border-l-4 border-blue-600">
        <div class="absolute top-0 right-0 w-24 h-24 bg-blue-100 rounded-full -mr-12 -mt-12 opacity-50"></div>
        <div class="relative z-10">
          <div class="bg-blue-100 rounded-full h-12 w-12 flex items-center justify-center mb-4">
            <span class="text-blue-600 font-bold text-xl">1</span>
          </div>
          <p class="text-slate-800 leading-relaxed">
            การให้บริการทดสอบทางวิทยาศาสตร์เพื่อพัฒนางานวิจัยและนวัตกรรมอย่างมีคุณภาพ
          </p>
        </div>
      </Card>
      
      <Card class="p-8 shadow-lg rounded-xl overflow-hidden relative hover:shadow-xl transition-all duration-300 border-l-4 border-blue-600">
        <div class="absolute top-0 right-0 w-24 h-24 bg-blue-100 rounded-full -mr-12 -mt-12 opacity-50"></div>
        <div class="relative z-10">
          <div class="bg-blue-100 rounded-full h-12 w-12 flex items-center justify-center mb-4">
            <span class="text-blue-600 font-bold text-xl">2</span>
          </div>
          <p class="text-slate-800 leading-relaxed">
            การถ่ายทอดองค์ความรู้ด้านเครื่องมือวิเคราะห์และการทดสอบทางวิทยาศาสตร์
          </p>
        </div>
      </Card>
      
      <Card class="p-8 shadow-lg rounded-xl overflow-hidden relative hover:shadow-xl transition-all duration-300 border-l-4 border-blue-600">
        <div class="absolute top-0 right-0 w-24 h-24 bg-blue-100 rounded-full -mr-12 -mt-12 opacity-50"></div>
        <div class="relative z-10">
          <div class="bg-blue-100 rounded-full h-12 w-12 flex items-center justify-center mb-4">
            <span class="text-blue-600 font-bold text-xl">3</span>
          </div>
          <p class="text-slate-800 leading-relaxed">
            พัฒนาและขยายผลิตภัณฑ์การให้บริการทดสอบทางวิทยาศาสตร์ให้มีความหลากหลาย
          </p>
        </div>
      </Card>
      
      <Card class="p-8 shadow-lg rounded-xl overflow-hidden relative hover:shadow-xl transition-all duration-300 border-l-4 border-blue-600">
        <div class="absolute top-0 right-0 w-24 h-24 bg-blue-100 rounded-full -mr-12 -mt-12 opacity-50"></div>
        <div class="relative z-10">
          <div class="bg-blue-100 rounded-full h-12 w-12 flex items-center justify-center mb-4">
            <span class="text-blue-600 font-bold text-xl">4</span>
          </div>
          <p class="text-slate-800 leading-relaxed">
            สร้างเครือข่ายและความร่วมมือด้านการทดสอบทางวิทยาศาสตร์กับหน่วยงานภาครัฐและเอกชน
          </p>
        </div>
      </Card>
    </div>
  </div>
</section>

<!-- ค่านิยม (Values) Section -->
<section class="py-20 bg-white">
  <div class="container mx-auto px-4 max-w-5xl">
    <div class="text-center mb-12">
      <h3 class="text-blue-600 font-semibold text-lg mb-2">OUR VALUES</h3>
      <h2 class="text-3xl font-bold text-slate-900 mb-4">ค่านิยม KSIC</h2>
      <div class="h-1 w-24 bg-blue-600 mx-auto rounded-full"></div>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 mt-12">
      <Card class="p-6 shadow-lg rounded-xl hover:shadow-xl transition-all duration-300 hover:translate-y-[-5px] bg-gradient-to-b from-blue-50 to-white border-t-4 border-blue-600">
        <div class="flex flex-col items-center">
          <div class="flex items-center justify-center h-20 w-20 bg-blue-100 rounded-full mb-6">
            <span class="text-4xl font-bold text-blue-600">K</span>
          </div>
          <h3 class="text-xl font-bold mb-4 text-slate-900">Knowledge</h3>
          <p class="text-slate-700 text-center">
            ความรู้ - การให้ความสำคัญกับการเรียนรู้และพัฒนาทักษะ เพื่อสร้างความรู้และประสบการณ์ที่ลึกซึ้ง ซึ่งนำไปสู่การเติบโตทั้งในองค์กรและบุคลากร
          </p>
        </div>
      </Card>
      
      <Card class="p-6 shadow-lg rounded-xl hover:shadow-xl transition-all duration-300 hover:translate-y-[-5px] bg-gradient-to-b from-indigo-50 to-white border-t-4 border-indigo-600">
        <div class="flex flex-col items-center">
          <div class="flex items-center justify-center h-20 w-20 bg-indigo-100 rounded-full mb-6">
            <span class="text-4xl font-bold text-indigo-600">S</span>
          </div>
          <h3 class="text-xl font-bold mb-4 text-slate-900">Service Excellence</h3>
          <p class="text-slate-700 text-center">
            ความเป็นเลิศในการให้บริการ – มุ่งมั่นในการให้บริการที่มีคุณภาพสูงและตอบสนองความต้องการของลูกค้าอย่างมืออาชีพ
          </p>
        </div>
      </Card>
      
      <Card class="p-6 shadow-lg rounded-xl hover:shadow-xl transition-all duration-300 hover:translate-y-[-5px] bg-gradient-to-b from-sky-50 to-white border-t-4 border-sky-600">
        <div class="flex flex-col items-center">
          <div class="flex items-center justify-center h-20 w-20 bg-sky-100 rounded-full mb-6">
            <span class="text-4xl font-bold text-sky-600">I</span>
          </div>
          <h3 class="text-xl font-bold mb-4 text-slate-900">Ignite</h3>
          <p class="text-slate-700 text-center">
            การพัฒนาอย่างต่อเนื่องและพร้อมนำการเปลี่ยนแปลง
          </p>
        </div>
      </Card>
      
      <Card class="p-6 shadow-lg rounded-xl hover:shadow-xl transition-all duration-300 hover:translate-y-[-5px] bg-gradient-to-b from-blue-50 to-white border-t-4 border-blue-800">
        <div class="flex flex-col items-center">
          <div class="flex items-center justify-center h-20 w-20 bg-blue-100 rounded-full mb-6">
            <span class="text-4xl font-bold text-blue-800">C</span>
          </div>
          <h3 class="text-xl font-bold mb-4 text-slate-900">Commitment</h3>
          <p class="text-slate-700 text-center">
            ความมุ่งมั่น – ยึดมั่นในเป้าหมายและภารกิจขององค์กร พร้อมทำงานอย่างเต็มที่เพื่อบรรลุผลสำเร็จ
          </p>
        </div>
      </Card>
    </div>
  </div>
</section>

<!-- วัฒนธรรมองค์กร (Organizational Culture) Section -->
<section class="py-16 bg-gradient-to-r from-blue-600 to-indigo-700 text-white">
  <div class="container mx-auto px-4 max-w-5xl">
    <div class="text-center mb-12">
      <h3 class="text-blue-200 font-semibold text-lg mb-2">OUR CULTURE</h3>
      <h2 class="text-3xl font-bold text-white mb-4">วัฒนธรรมองค์กร</h2>
      <div class="h-1 w-24 bg-white mx-auto rounded-full"></div>
    </div>
    
    <Card class="p-10 bg-white/10 backdrop-blur-sm border border-white/20 rounded-xl shadow-xl">
      <p class="text-white text-xl text-center font-medium leading-relaxed">
        มุ่งมั่นให้บริการด้วยผลการทดสอบที่มีความถูกต้องและน่าเชื่อถือ<br>
        <span class="text-blue-200 italic">(Accuracy and Reliability)</span>
      </p>
    </Card>
  </div>
</section>

		<!-- Contact & Location Section (Same as main page) -->
		<section class="bg-gradient-to-br from-blue-600 to-indigo-700 py-16 text-white">
			<div class="container mx-auto px-4">
				<div class="mx-auto grid max-w-4xl grid-cols-1 gap-12 md:grid-cols-2">
					<div>
						<h2 class="mb-6 text-3xl font-bold">Contact Us</h2>
						<ul class="space-y-4">
							<li class="flex items-start">
								<svg class="mr-3 mt-1 h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"
									><path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
									/></svg
								>
								<div>
									<p class="font-medium">Phone:</p>
									<p>02-329-8400 ถึง 8411 ต่อ 354, 402</p>
									<p>092-463-9886 (Mobile)</p>
								</div>
							</li>
							<li class="flex items-start">
								<svg class="mr-3 mt-1 h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"
									><path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
									/></svg
								>
								<div>
									<p class="font-medium">Email:</p>
									<p>science@kmitl.ac.th</p>
								</div>
							</li>
							<li class="flex items-start">
								<svg class="mr-3 mt-1 h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"
									><path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
									/></svg
								>
								<div>
									<p class="font-medium">Hours:</p>
									<p>Monday - Friday: 8:30 AM - 4:30 PM</p>
								</div>
							</li>
						</ul>
					</div>

					<div>
						<h2 class="mb-6 text-3xl font-bold">Location</h2>
						<p class="mb-4">
							Faculty of Science, King Mongkut's Institute of Technology Ladkrabang
						</p>
						<p class="mb-4">1 Chalong Krung 1 Alley, Lat Krabang, Bangkok 10520</p>

						<div class="mt-6">
							<Button variant="secondary" class="bg-white text-blue-700 hover:bg-blue-50">
								<svg class="mr-2 h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"
									><path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
									/><path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
									/></svg
								>
								View on Map
							</Button>
						</div>
					</div>
				</div>
			</div>
		</section>
	</main>

	<!-- Footer (Same as main page) -->
	<footer class="mt-auto bg-slate-900 py-10 text-slate-300">
		<div class="container mx-auto px-4">
			<div class="mb-8 grid grid-cols-1 gap-8 md:grid-cols-4">
				<div>
					<h3 class="mb-4 text-lg font-bold text-white">KMITL Science Instrument Center</h3>
					<p class="text-sm">
						Providing cutting-edge scientific equipment and services to researchers, academics, and
						industry professionals.
					</p>
				</div>

				<div>
					<h3 class="mb-4 text-lg font-bold text-white">Quick Links</h3>
					<ul class="space-y-2 text-sm">
						<li><a href="/" class="transition-colors hover:text-white">Home</a></li>
						<li>
							<a href="/instruments" class="transition-colors hover:text-white">Equipment Catalog</a
							>
						</li>
						<li><a href="/prices" class="transition-colors hover:text-white">Service Rates</a></li>
						<li>
							<a href="/booking" class="transition-colors hover:text-white">Make a Booking</a>
						</li>
					</ul>
				</div>

				<div>
					<h3 class="mb-4 text-lg font-bold text-white">Resources</h3>
					<ul class="space-y-2 text-sm">
						<li>
							<a href="/manuals" class="transition-colors hover:text-white">Equipment Manuals</a>
						</li>
						<li>
							<a href="/training" class="transition-colors hover:text-white">Training Programs</a>
						</li>
						<li>
							<a href="/research" class="transition-colors hover:text-white"
								>Research Collaborations</a
							>
						</li>
						<li><a href="/faqs" class="transition-colors hover:text-white">FAQs</a></li>
					</ul>
				</div>

				<div>
					<h3 class="mb-4 text-lg font-bold text-white">Connect us</h3>
					<div class="mb-4 flex space-x-4">
						<a href="#" class="text-slate-300 hover:text-white">
							<svg
								xmlns="http://www.w3.org/2000/svg"
								width="24"
								height="24"
								viewBox="0 0 24 24"
								fill="none"
								stroke="currentColor"
								stroke-width="2"
								stroke-linecap="round"
								stroke-linejoin="round"
								><path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z" /></svg
							>
						</a>

						<a href="#" class="text-slate-300 hover:text-white">
							<svg
								xmlns="http://www.w3.org/2000/svg"
								width="24"
								height="24"
								viewBox="0 0 24 24"
								fill="none"
								stroke="currentColor"
								stroke-width="2"
								stroke-linecap="round"
								stroke-linejoin="round"
								><path d="M22 4S21 3 18 3H6C3 3 2 4 2 4l10 8.5z" /><path
									d="m22 20-4-6-6 3.5L6 14l-4 6"
								/><path d="M2 20V4" /><path d="M22 4v16" /></svg
							>
						</a>
					</div>

					<Separator class="mb-6 bg-slate-700" />
					<div class="text-center text-sm">
						<p>© 2025 KMITL Scientific Instrument Center. All Rights Reserved</p>
					</div>
				</div>
			</div>
		</div>
	</footer>
</div>
