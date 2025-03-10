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
		Globe,
		Building,
		FileText,
		Shield,
		MapPin
	} from 'lucide-svelte';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';

	const teamMembers = [
		{
			name: 'ผศ.ดร. พิศาล ศรีราช',
			role: 'หัวหน้าศูนย์เครื่องมือวิทยาศาสตร์',
			description:
				'ประวัติโดยย่อก็ได้ครับ',
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
	
	// Organizational structure data
	interface DutyItem {
		title: string;
		duties: string[];
	}
	
	interface DirectorItem {
		title: string;
		name: string;
		children: DutyItem[];
	}
	
	interface CenterItem {
		title: string;
		children: DirectorItem[];
	}
	
	interface FacultyItem {
		title: string;
		children: CenterItem[];
	}
	
	// Organizational structure data
	const organizationStructure: FacultyItem[] = [
		{
			title: 'คณะวิทยาศาสตร์',
			children: [
				{
					title: 'ศูนย์เครื่องมือวิทยาศาสตร์',
					children: [
						{
							title: 'หัวหน้าศูนย์เครื่องมือวิทยาศาสตร์',
							name: 'ผศ.ดร. พิศาล ศรีราช',
							children: [
								{
									title: 'ฝ่ายบริหารและจัดการ',
									duties: [
										'งานแผนและประกันคุณภาพ',
										'งานจัดซื้อจัดจ้างและงานพัสดุ',
										'งานการเงินและบัญชี',
										'งานธุรการและสารบรรณ',
										'งานบริหารลูกค้าสัมพันธ์'
									]
								},
								{
									title: 'ฝ่ายบริการเครื่องมือทางวิทยาศาสตร์',
									duties: [
										'เครื่องมือตรวจลักษณะทางกายภาพและโครงสร้าง (Physical and structural characterization)',
										'เครื่องมือทางเคมีประยุกต์ (Applied chemical instrument)',
										'เครื่องมือทดสอบทางชีววิทยา (Biological test)',
										'เครื่องเตรียมตัวอย่าง (Sample preparation equipment)',
										'เครื่องมือพื้นฐาน (General equipment)'
									]
								},
								{
									title: 'ฝ่ายที่ปรึกษา การทดสอบทางวิทยาศาสตร์',
									duties: [
										'งานให้คำปรึกษาวิเคราะห์ทดสอบ',
										'งานออกแบบและตรวจสอบมาตรฐานวิธีทดสอบ'
									]
								}
							]
						}
					]
				}
			]
		}
	];
	
	
	// Strategic plan data
	const strategicPlan = [
		{
			title: 'ยุทธศาสตร์ที่ 1',
			description: 'พัฒนาระบบการให้บริการทดสอบทางวิทยาศาสตร์ตามมาตรฐานระดับสากล',
			objectives: [
				'พัฒนาและปรับปรุงขั้นตอนการให้บริการให้มีประสิทธิภาพ',
				'ขยายขอบข่ายการรับรองตามมาตรฐานสากล ISO/IEC 17025',
				'พัฒนาระบบการให้บริการแบบดิจิทัลเพื่อเพิ่มความสะดวกและรวดเร็ว'
			]
		},
		{
			title: 'ยุทธศาสตร์ที่ 2',
			description: 'ยกระดับศักยภาพบุคลากรและเพิ่มประสิทธิภาพการบริหารจัดการองค์กร',
			objectives: [
				'พัฒนาบุคลากรให้มีความเชี่ยวชาญในการใช้เครื่องมือวิทยาศาสตร์ขั้นสูง',
				'สร้างวัฒนธรรมองค์กรที่เน้นคุณภาพและการบริการที่เป็นเลิศ',
				'พัฒนาระบบบริหารจัดการทรัพยากรอย่างมีประสิทธิภาพ'
			]
		},
		{
			title: 'ยุทธศาสตร์ที่ 3',
			description: 'สร้างเครือข่ายความร่วมมือกับภาคอุตสาหกรรมและหน่วยงานภายนอก',
			objectives: [
				'สร้างความร่วมมือกับภาคอุตสาหกรรมในการพัฒนาโจทย์วิจัยและนวัตกรรม',
				'ขยายเครือข่ายการให้บริการกับหน่วยงานภาครัฐและเอกชน',
				'ส่งเสริมการถ่ายทอดองค์ความรู้และเทคโนโลยีสู่ภาคอุตสาหกรรม'
			]
		}
	];
</script>

<!-- Main Layout -->
<div class="flex min-h-screen flex-col bg-slate-50 font-sans">
	<!-- Header (Same as main page) -->
<Header />

	<main>
		<!-- Hero Section -->
		<section
			class="relative overflow-hidden bg-gradient-to-br from-blue-50 via-indigo-50 to-blue-100 py-24"
		>
			<div class="absolute inset-0 bg-pattern-grid opacity-10"></div>
			<div class="absolute -top-24 -right-24 h-64 w-64 rounded-full bg-blue-300 opacity-20 blur-3xl"></div>
			<div class="absolute -bottom-32 -left-32 h-96 w-96 rounded-full bg-indigo-300 opacity-20 blur-3xl"></div>
			
			<div class="container relative z-10 mx-auto px-4 text-center">
				<span class="mb-2 inline-block rounded-full bg-blue-100 px-4 py-1 text-sm font-medium text-blue-800">KMITL Science Instrument Center</span>
				<h2 class="mb-6 text-5xl font-bold tracking-tight text-slate-900 md:text-6xl">
					เกี่ยวกับเรา <span class="bg-gradient-to-r from-blue-600 to-indigo-600 bg-clip-text text-transparent">ศูนย์เครื่องมือวิทยาศาสตร์</span>
				</h2>
				<p class="mx-auto mb-10 max-w-2xl text-xl leading-relaxed text-slate-700">
          ทีมงานผู้เชี่ยวชาญของเราพร้อมให้บริการและสนับสนุนงานวิจัยและการวิเคราะห์ทดสอบทางวิทยาศาสตร์อย่างมีคุณภาพ
				</p>

			</div>
		</section>

		<!-- Navigation tabs for About Us subpages -->
		<section class="py-8 bg-white border-b">
			<div class="container mx-auto px-4">
				<div class="flex overflow-x-auto pb-2 space-x-6 justify-center">
					<a href="#vision-mission" class="px-4 py-2 text-blue-600 font-medium border-b-2 border-blue-600 whitespace-nowrap">วิสัยทัศน์/พันธกิจ</a>
					<a href="#history" class="px-4 py-2 text-slate-600 hover:text-blue-600 font-medium border-b-2 border-transparent hover:border-blue-600 whitespace-nowrap">ความเป็นมา</a>
					<a href="#structure" class="px-4 py-2 text-slate-600 hover:text-blue-600 font-medium border-b-2 border-transparent hover:border-blue-600 whitespace-nowrap">โครงสร้างองค์กร</a>
					<a href="#strategic-plan" class="px-4 py-2 text-slate-600 hover:text-blue-600 font-medium border-b-2 border-transparent hover:border-blue-600 whitespace-nowrap">แผนยุทธศาสตร์</a>
					<a href="#contact" class="px-4 py-2 text-slate-600 hover:text-blue-600 font-medium border-b-2 border-transparent hover:border-blue-600 whitespace-nowrap">ติดต่อเรา</a>
					<a href="/personnel" class="px-4 py-2 text-slate-600 hover:text-blue-600 font-medium border-b-2 border-transparent hover:border-blue-600 whitespace-nowrap">ผู้บริหารและบุคลากร</a>
					<a href="/privacy-policy" class="px-4 py-2 text-slate-600 hover:text-blue-600 font-medium border-b-2 border-transparent hover:border-blue-600 whitespace-nowrap">นโยบายความเป็นส่วนตัว</a>
				</div>
			</div>
		</section>

    <!-- วิสัยทัศน์ (Vision) Section -->
    <section id="vision-mission" class="py-20 bg-white">
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
	<section id="structure" class="py-20 bg-white">
		<div class="container mx-auto px-4">
			<div class="mb-12 text-center">
				<h3 class="mb-2 text-lg font-semibold text-blue-600">ORGANIZATION</h3>
				<h2 class="mb-4 text-3xl font-bold text-slate-900">โครงสร้างองค์กรและบริหารงาน</h2>
				<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
			</div>

			<div class="mx-auto max-w-5xl">
				<!-- Organizational Chart -->
				<Card class="p-8 shadow-lg rounded-xl mb-12">
					<div class="flex flex-col items-center">
						<!-- Faculty -->
						<div class="relative mb-12 w-full max-w-md">
							<Card class="relative p-6 border-t-4 border-blue-800 shadow-md text-center bg-blue-50">
								<h4 class="text-xl font-bold text-slate-900">คณะวิทยาศาสตร์</h4>
							</Card>
						</div>
						
						<!-- Connect lines -->
						<div class="h-12 w-1 bg-blue-300"></div>
						
						<!-- Science Instrument Center -->
						<div class="relative mb-12 w-full max-w-md">
							<Card class="relative p-6 border-t-4 border-blue-700 shadow-md text-center bg-blue-50">
								<h4 class="text-xl font-bold text-slate-900">ศูนย์เครื่องมือวิทยาศาสตร์</h4>
							</Card>
						</div>

						<!-- Connect lines -->
						<div class="h-12 w-1 bg-blue-300"></div>

						<!-- Director -->
						<div class="relative mb-12 w-full max-w-md">
							<Card class="relative p-6 border-t-4 border-blue-600 shadow-lg text-center">
								<div class="flex flex-col items-center">
									<div class="flex items-center justify-center h-16 w-16 bg-blue-100 rounded-full mb-4">
										<Building class="h-8 w-8 text-blue-600" />
									</div>
									<h4 class="text-xl font-bold text-slate-900">หัวหน้าศูนย์เครื่องมือวิทยาศาสตร์</h4>
									<p class="text-blue-600 font-medium">Asst.Prof.Dr.Pisan Sukwisute</p>
								</div>
							</Card>
						</div>

						<!-- Connect lines -->
						<div class="h-12 w-1 bg-blue-200"></div>

						<!-- Divisions -->
						<div class="grid grid-cols-1 md:grid-cols-3 gap-8 w-full">
							{#each organizationStructure[0].children[0].children[0].children as division}
								<Card class="p-6 border-t-4 border-blue-500 shadow-md relative">
									<div class="h-6 w-1 bg-blue-200 absolute -top-6 left-1/2 transform -translate-x-1/2"></div>
									<div class="flex flex-col items-center">
										<div class="flex items-center justify-center h-12 w-12 bg-blue-100 rounded-full mb-4">
											<Users class="h-6 w-6 text-blue-600" />
										</div>
										<h4 class="text-lg font-bold text-slate-900 mb-4 text-center">{division.title}</h4>
										<ul class="text-slate-700 text-sm">
											{#each division.duties as duty}
												<li class="mb-2 flex items-start">
													<span class="mr-2 mt-1 text-blue-600">•</span>
													<span>{duty}</span>
												</li>
											{/each}
										</ul>
									</div>
								</Card>
							{/each}
						</div>
					</div>
				</Card>

		<!-- Key Milestones / ความเป็นมา -->
		<section id="history" class="bg-gradient-to-br from-slate-50 to-blue-50 py-20">
			<div class="container mx-auto px-4">
				<div class="mb-12 text-center">
					<h3 class="mb-2 text-lg font-semibold text-blue-600">ประวัติของเรา</h3>
					<h2 class="mb-4 text-3xl font-bold text-slate-900">ความเป็นมา</h2>
					<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
					<p class="mx-auto mt-6 max-w-3xl text-slate-700">
						ศูนย์เครื่องมือวิทยาศาสตร์ คณะวิทยาศาสตร์ สถาบันเทคโนโลยีพระจอมเกล้าเจ้าคุณทหารลาดกระบัง 
						ก่อตั้งขึ้นในปี พ.ศ. xxxx เพื่อเป็นศูนย์กลางในการให้บริการเครื่องมือวิทยาศาสตร์
					</p>
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
				
				<div class="mt-16 bg-white p-8 rounded-xl shadow-lg">
					<h3 class="text-2xl font-bold text-slate-900 mb-6">ประวัติความเป็นมาโดยละเอียด</h3>
					<div class="space-y-6 text-slate-700">
						<p>
							ศูนย์เครื่องมือวิทยาศาสตร์ คณะวิทยาศาสตร์ สถาบันเทคโนโลยีพระจอมเกล้าเจ้าคุณทหารลาดกระบัง 
							ได้เริ่มต้นจากการเป็นหน่วยบริการเครื่องมือกลางของคณะวิทยาศาสตร์ โดยมีวัตถุประสงค์เพื่อสนับสนุนการเรียนการสอน
							และการวิจัยของคณาจารย์และนักศึกษาภายในสถาบัน
						</p>
						<p>
							คณะวิทยาศาสตร์เริ่มก่อตั้งขึ้นในปี พ.ศ. 2520 โดยเป็นส่วนหนึ่งของคณะครุศาสตร์อุตสาหกรรม และ วิทยาศาสตร์ ดำเนินการสอนวิชาพื้นฐานทางวิทยาศาสตร์ และ คณิตศาสตร์ ให้กับนักศึกษาระดับปริญญาตรีทุกหลักสูตรในสถาบันฯ


						</p>
						<p>
							สถาบันฯ มีฐานะเป็นหน่วยงานในกำกับของรัฐ ซึ่งไม่เป็นส่วนราชการตามกฎหมายว่าด้วยระเบียบบริหารราชการแผ่นดิน กฎหมายว่าด้วยระเบียบบริหารราชการกระทรวงศึกษาธิการ และกฎหมายว่าด้วยการปรับปรุงกระทรวง ทบวง กรม และไม่เป็นรัฐวิสาหกิจตามกฎหมายว่าด้วยวิธีการงบประมาณ และกฎหมายอื่น ตามพระราชบัญญัติสถาบันเทคโนโลยีพระจอมเกล้าเจ้าคุณทหารลาดกระบัง พ.ศ. 2551


						</p>
						<p>
							จากการขยายภาระหน้าที่ความรับผิดชอบ จึงได้มีพระราชกฤษฎีกาจัดตั้งคณะวิทยาศาสตร์ขึ้น เมื่อวันที่ 8 ธันวาคม 2531 และได้ขยายการผลิตบัณฑิตระดับปริญญาตรีในสาขาอื่นๆ รวมทั้งเปิดรับนักศึกษาระดับปริญญาโทและปริญญาเอกอีกด้วย


						</p>
						<p>
							และในปี พ.ศ. 2565 ศูนย์ฯ ได้รับการรับรองระบบมาตรฐาน ISO 9001:2015 สำหรับการให้บริการทดสอบทางวิทยาศาสตร์ 
							ซึ่งแสดงถึงความมุ่งมั่นในการพัฒนาคุณภาพการให้บริการอย่างต่อเนื่อง เพื่อสร้างความเชื่อมั่นแก่ผู้รับบริการทั้งในและต่างประเทศ
						</p>
					</div>
				</div>
			</div>
		</section>

		<!-- โครงสร้างองค์กรและบริหารงาน (Organizational Structure) -->
		

		<!-- แผนยุทธศาสตร์และนโยบาย (Strategic Plan) -->
		<section id="strategic-plan" class="py-20 bg-gradient-to-br from-slate-50 to-blue-50">
			<div class="container mx-auto px-4">
				<div class="mb-12 text-center">
					<h3 class="mb-2 text-lg font-semibold text-blue-600">STRATEGIC PLAN</h3>
					<h2 class="mb-4 text-3xl font-bold text-slate-900">แผนยุทธศาสตร์และนโยบาย</h2>
					<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
					<p class="mx-auto mt-6 max-w-3xl text-slate-700">
						แผนยุทธศาสตร์ศูนย์เครื่องมือวิทยาศาสตร์ พ.ศ. 2565-2570 มุ่งเน้นการพัฒนาศักยภาพการให้บริการทดสอบทางวิทยาศาสตร์
						เพื่อสนับสนุนงานวิจัยและนวัตกรรมทั้งในระดับสถาบันและระดับประเทศ
					</p>
				</div>

				<div class="mx-auto max-w-5xl space-y-8">
					{#each strategicPlan as strategy, i}
						<Card class="p-8 shadow-lg rounded-xl border-l-4 hover:shadow-xl transition-all duration-300"
						style="border-left-color: var(--colors-blue-{600 - i * 100});">
							<div class="grid grid-cols-1 md:grid-cols-4 gap-4">
								<div class="md:col-span-1">
									<div class="bg-blue-100 rounded-full h-16 w-16 flex items-center justify-center mb-4">
										<span class="text-2xl font-bold text-blue-600">{i + 1}</span>
									</div>
								</div>
								<div class="md:col-span-3">
									<h4 class="text-xl font-bold text-blue-700 mb-2">{strategy.title}</h4>
									<p class="text-slate-800 mb-4 font-medium">{strategy.description}</p>
									<div class="bg-white p-4 rounded-md">
										<h5 class="text-sm font-semibold text-slate-600 mb-2">เป้าประสงค์:</h5>
										<ul class="text-slate-700 space-y-2">
											{#each strategy.objectives as objective}
												<li class="flex items-start">
													<span class="mr-2 mt-1 text-blue-600">•</span>
													<span>{objective}</span>
												</li>
											{/each}
										</ul>
									</div>
								</div>
							</div>
						</Card>
					{/each}
					
					<!-- Download Strategic Plan Button -->
					<div class="text-center mt-12">
						<Button class="bg-blue-600 px-6 py-3 text-white hover:bg-blue-700">
							<FileText class="h-5 w-5 mr-2" />
							ดาวน์โหลดแผนยุทธศาสตร์ฉบับเต็ม (PDF)
						</Button>
					</div>
				</div>
			</div>
		</section>

		<!-- ติดต่อเรา / ข้อเสนอแนะ (Contact & Feedback) -->
		

		<!-- Team Members -->
		<section class="bg-white py-20">
			<div class="container mx-auto px-4">
				<div class="mb-12 text-center">
          <h3 class="mb-2 text-lg font-semibold text-blue-600">OUR HEAD</h3>
					<h2 class="mb-4 text-3xl font-bold text-slate-900">หัวหน้าศูนย์เครื่องมือ</h2>
					<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
					<p class="mx-auto mt-6 max-w-2xl text-slate-600">
						Our team of dedicated scientists and specialists works tirelessly to advance research
						capabilities at KMITL and beyond
					</p>
				</div>
				<div class="flex justify-center">
					<Card class="max-w-sm flex flex-col items-center text-center overflow-hidden rounded-xl border-b-4 border-blue-600 shadow-lg transition-all duration-300 hover:shadow-xl">
					  <div class="relative">
						<img src={teamMembers[0].image} alt={teamMembers[0].name} class="h-72 w-full object-cover -mt-5" />
						<div class="absolute bottom-0 left-0 right-0 h-24 bg-gradient-to-t from-slate-900 to-transparent"></div>
					  </div>
					  <div class="p-8">
						<h3 class="mb-2 text-2xl font-bold text-slate-900">{teamMembers[0].name}</h3>
						<p class="mb-4 flex items-center font-medium text-blue-600">
						  <Users class="mr-2 h-4 w-4" />
						  {teamMembers[0].role}
						</p>
						<Separator class="mb-4" />
						<p class="text-slate-600">{teamMembers[0].description}</p>
					  </div>
					</Card>
				  </div>
				  
				
				<div class="mt-10 text-center">
					<a href="/personnel" class="inline-flex items-center text-blue-600 hover:text-blue-800 font-medium">
						ดูรายชื่อบุคลากรทั้งหมด
						<svg class="h-5 w-5 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
						</svg>
					</a>
				</div>
			</div>
		</section>
		<section id="contact" class="py-20 bg-white">
			<div class="container mx-auto px-4">
				<div class="mb-12 text-center">
					<h3 class="mb-2 text-lg font-semibold text-blue-600">CONTACT US</h3>
					<h2 class="mb-4 text-3xl font-bold text-slate-900">ติดต่อเรา / ข้อเสนอแนะ</h2>
					<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
				</div>

				<div class="mx-auto max-w-6xl">
					<div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
						<!-- Contact Information -->
						<div>
							<Card class="p-8 shadow-lg rounded-xl h-full">
								<h4 class="text-xl font-bold text-slate-900 mb-6 flex items-center">
									<Users class="h-6 w-6 mr-2 text-blue-600" />
									ข้อมูลการติดต่อ
								</h4>
								
								<div class="space-y-6">
									<div class="flex items-start">
										<div class="bg-blue-100 rounded-full h-10 w-10 flex items-center justify-center mr-4 mt-1">
											<Building class="h-5 w-5 text-blue-600" />
										</div>
										<div>
											<h5 class="font-semibold text-slate-900">ที่อยู่:</h5>
											<p class="text-slate-700">
												ศูนย์เครื่องมือวิทยาศาสตร์ คณะวิทยาศาสตร์<br>
												สถาบันเทคโนโลยีพระจอมเกล้าเจ้าคุณทหารลาดกระบัง<br>
												เลขที่ 1 ซอยฉลองกรุง 1 เขตลาดกระบัง กรุงเทพฯ 10520
											</p>
										</div>
									</div>
									
									<div class="flex items-start">
										<div class="bg-blue-100 rounded-full h-10 w-10 flex items-center justify-center mr-4 mt-1">
											<svg class="h-5 w-5 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
											</svg>
										</div>
										<div>
											<h5 class="font-semibold text-slate-900">เบอร์โทรศัพท์:</h5>
											<p class="text-slate-700">
												02-329-8400 ถึง 8411 ต่อ 354, 402<br>
												092-463-9886 (Mobile)
											</p>
										</div>
									</div>
									
									<div class="flex items-start">
										<div class="bg-blue-100 rounded-full h-10 w-10 flex items-center justify-center mr-4 mt-1">
											<svg class="h-5 w-5 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
											</svg>
										</div>
										<div>
											<h5 class="font-semibold text-slate-900">อีเมล:</h5>
											<p class="text-slate-700">science@kmitl.ac.th</p>
										</div>
									</div>
									
									<div class="flex items-start">
										<div class="bg-blue-100 rounded-full h-10 w-10 flex items-center justify-center mr-4 mt-1">
											<svg class="h-5 w-5 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
											</svg>
										</div>
										<div>
											<h5 class="font-semibold text-slate-900">เวลาทำการ:</h5>
											<p class="text-slate-700">
												จันทร์ - ศุกร์: 8:30 - 16:30 น.<br>
												หยุดวันเสาร์-อาทิตย์ และวันหยุดนักขัตฤกษ์
											</p>
										</div>
									</div>
									
									<div class="flex items-start">
										<div class="bg-blue-100 rounded-full h-10 w-10 flex items-center justify-center mr-4 mt-1">
											<svg class="h-5 w-5 text-blue-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
												<path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z" />
											</svg>
										</div>
										<div>
											<h5 class="font-semibold text-slate-900">Facebook:</h5>
											<p class="text-slate-700">
												<a href="#" class="text-blue-600 hover:underline">KMITL Science Instrument Center</a>
											</p>
										</div>
									</div>
								</div>
							</Card>
						</div>
						
						<!-- Map and Feedback Form -->
						<div class="space-y-8">
							<!-- Map -->
							<Card class="p-6 shadow-lg rounded-xl overflow-hidden">
								<h4 class="text-xl font-bold text-slate-900 mb-4 flex items-center">
									<MapPin class="h-6 w-6 mr-2 text-blue-600" />
									แผนที่
								</h4>
								<div class="rounded-lg overflow-hidden h-64 bg-gray-200 relative">
									<!-- This is a placeholder for the actual map. In a real implementation, you would integrate with Google Maps or similar -->
									<div class="absolute inset-0 flex items-center justify-center">
										<p class="text-slate-600">แผนที่จะแสดงตำแหน่งศูนย์เครื่องมือวิทยาศาสตร์ คณะวิทยาศาสตร์ สจล.</p>
									</div>
								</div>
								<div class="mt-4">
									<Button class="bg-blue-600 text-white hover:bg-blue-700 px-4 py-2">
										<MapPin class="h-4 w-4 mr-2" />
										ดูใน Google Maps
									</Button>
								</div>
							</Card>
							
							<!-- Feedback Form -->
							<Card class="p-6 shadow-lg rounded-xl">
								<h4 class="text-xl font-bold text-slate-900 mb-4 flex items-center">
									<svg class="h-6 w-6 mr-2 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 8h10M7 12h4m1 8l-4-4H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-3l-4 4z" />
									</svg>
									ข้อเสนอแนะ / ข้อร้องเรียน
								</h4>
								<form class="space-y-4">
									<div>
										<label for="name" class="block text-sm font-medium text-slate-700 mb-1">ชื่อ-นามสกุล</label>
										<input type="text" id="name" class="w-full p-2 border border-slate-300 rounded-md" />
									</div>
									<div>
										<label for="email" class="block text-sm font-medium text-slate-700 mb-1">อีเมล</label>
										<input type="email" id="email" class="w-full p-2 border border-slate-300 rounded-md" />
									</div>
									<div>
										<label for="feedbackType" class="block text-sm font-medium text-slate-700 mb-1">ประเภท</label>
										<select id="feedbackType" class="w-full p-2 border border-slate-300 rounded-md">
											<option value="suggestion">ข้อเสนอแนะ</option>
											<option value="complaint">ข้อร้องเรียน</option>
											<option value="question">คำถาม</option>
										</select>
									</div>
									<div>
										<label for="message" class="block text-sm font-medium text-slate-700 mb-1">ข้อความ</label>
										<textarea id="message" rows="4" class="w-full p-2 border border-slate-300 rounded-md"></textarea>
									</div>
									<div>
										<Button class="bg-blue-600 text-white hover:bg-blue-700 w-full py-2">ส่งข้อมูล</Button>
									</div>
								</form>
							</Card>
						</div>
					</div>
				</div>
			</div>
		</section>


	</main>
	<Footer />
</div>
