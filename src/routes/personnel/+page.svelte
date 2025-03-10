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
    GraduationCap,
    UserCircle,
    Briefcase
	} from 'lucide-svelte';

	// Head of Science Instrument Center
	const headOfCenter = [
		{
			name: 'ผศ.ดร.ธนากร โอสถจันทร์',
			role: 'หัวหน้าศูนย์เครื่องมือวิทยาศาสตร์',
			description:
				'ผู้เชี่ยวชาญด้านเครื่องมือวิเคราะห์ขั้นสูงและการพัฒนาระบบการให้บริการทางวิทยาศาสตร์ที่มีประสบการณ์มากกว่า 15 ปี',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		}
	];

	// Laboratory Advisors
	const labAdvisors = [
		{
			name: 'ศ.ดร.มาลินี ชัยเวชสกุล',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการเคมีวิเคราะห์',
			description: 'ผู้เชี่ยวชาญด้านเคมีวิเคราะห์และเทคนิคการแยกสาร',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รศ.ดร.พิชญา วงศ์สุวรรณ',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการจุลชีววิทยา',
			description: 'ผู้เชี่ยวชาญด้านจุลชีววิทยาและเทคโนโลยีชีวภาพ',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผศ.ดร.กฤษณะ อันชื่น',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการฟิสิกส์',
			description: 'ผู้เชี่ยวชาญด้านฟิสิกส์วัสดุและการวิเคราะห์โครงสร้างระดับนาโน',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รศ.ดร.สมพงษ์ ธรรมถาวร',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการเครื่องมือวิเคราะห์ขั้นสูง',
			description: 'ผู้เชี่ยวชาญด้านเทคนิคการวิเคราะห์ด้วยเครื่องมือขั้นสูง',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผศ.ดร.นภาพร รัตนาภรณ์',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการวัสดุศาสตร์',
			description: 'ผู้เชี่ยวชาญด้านการวิเคราะห์และทดสอบวัสดุ',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ดร.ธนพล วรรณโน',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการสิ่งแวดล้อม',
			description: 'ผู้เชี่ยวชาญด้านการวิเคราะห์คุณภาพสิ่งแวดล้อม',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผศ.ดร.กัลยา ศรีพงษ์',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการชีวเคมี',
			description: 'ผู้เชี่ยวชาญด้านชีวเคมีและเทคโนโลยีชีวภาพระดับโมเลกุล',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รศ.ดร.เกษร จันทร์ศิริ',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการเทคโนโลยีอาหาร',
			description: 'ผู้เชี่ยวชาญด้านการวิเคราะห์คุณภาพและความปลอดภัยอาหาร',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผศ.ดร.วิชัย สุทธิเดช',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการพอลิเมอร์',
			description: 'ผู้เชี่ยวชาญด้านวิทยาศาสตร์และเทคโนโลยีพอลิเมอร์',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ดร.สุชาติ ทองสุข',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการการวิเคราะห์เชิงความร้อน',
			description: 'ผู้เชี่ยวชาญด้านการวิเคราะห์สมบัติทางความร้อนของวัสดุ',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผศ.ดร.สุมนมาลย์ จันทร์เอี่ยม',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการเลเซอร์และแสง',
			description: 'ผู้เชี่ยวชาญด้านเทคโนโลยีเลเซอร์และทัศนศาสตร์',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		}
	];

	// Staff members
	const staffMembers = [
		{
			name: 'นางสาววิภาวดี ศิริรัตน์',
			role: 'นักวิทยาศาสตร์ชำนาญการพิเศษ',
			department: 'ห้องปฏิบัติการเคมีวิเคราะห์',
			description: 'ผู้เชี่ยวชาญการใช้เครื่องมือวิเคราะห์ทางเคมี HPLC, GC, AAS',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'นายธนกร มณีทอง',
			role: 'นักวิทยาศาสตร์ชำนาญการ',
			department: 'ห้องปฏิบัติการกล้องจุลทรรศน์อิเล็กตรอน',
			description: 'ผู้เชี่ยวชาญการใช้กล้องจุลทรรศน์อิเล็กตรอนแบบส่องกราดและแบบส่องผ่าน',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'นางสาวปิยะนุช ทองดี',
			role: 'นักวิทยาศาสตร์',
			department: 'ห้องปฏิบัติการจุลชีววิทยา',
			description: 'ผู้เชี่ยวชาญการวิเคราะห์และเพาะเลี้ยงจุลินทรีย์',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'นายวิชัย สุขสวัสดิ์',
			role: 'นักวิทยาศาสตร์',
			department: 'ห้องปฏิบัติการเครื่องมือวิเคราะห์ขั้นสูง',
			description: 'ผู้เชี่ยวชาญการใช้เครื่องมือ XRD, XRF, FTIR',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'นางสาวจิตรา ใจดี',
			role: 'นักวิทยาศาสตร์',
			department: 'ห้องปฏิบัติการสิ่งแวดล้อม',
			description: 'ผู้เชี่ยวชาญการวิเคราะห์คุณภาพน้ำและอากาศ',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'นายนพดล รักษาชาติ',
			role: 'นักวิทยาศาสตร์',
			department: 'ห้องปฏิบัติการวัสดุศาสตร์',
			description: 'ผู้เชี่ยวชาญการทดสอบสมบัติทางกลของวัสดุ',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'นางสาวอรุณี มณีวงศ์',
			role: 'เจ้าหน้าที่บริหารงานทั่วไป',
			department: 'ฝ่ายบริหารและธุรการ',
			description: 'ดูแลงานสารบรรณ งบประมาณ และการประสานงานทั่วไป',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'นายสมชาย ใจเย็น',
			role: 'เจ้าหน้าที่บริหารงานทั่วไป',
			department: 'ฝ่ายพัสดุและครุภัณฑ์',
			description: 'ดูแลงานจัดซื้อจัดจ้าง ควบคุมครุภัณฑ์ และซ่อมบำรุง',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'นางสาวภัทรา วงศ์สมบูรณ์',
			role: 'เจ้าหน้าที่บริหารงานทั่วไป',
			department: 'ฝ่ายบริการวิชาการ',
			description: 'ดูแลงานประชาสัมพันธ์ ฝึกอบรม และบริการวิชาการ',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'นายสุรชัย นิลประเสริฐ',
			role: 'นักวิทยาศาสตร์',
			department: 'ห้องปฏิบัติการชีวเคมี',
			description: 'ผู้เชี่ยวชาญการวิเคราะห์ทางชีวเคมีและชีวโมเลกุล',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		}
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
          <a href="/personnel" class="text-blue-600 font-medium transition-colors">บุคลากร</a>
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
					บุคลากร <span class="text-blue-600">ศูนย์เครื่องมือวิทยาศาสตร์</span>
				</h2>
				<p class="mx-auto mb-10 max-w-2xl text-xl leading-relaxed text-slate-700">
          ทีมงานผู้เชี่ยวชาญของเราพร้อมให้บริการและสนับสนุนงานวิจัยและการวิเคราะห์ทดสอบทางวิทยาศาสตร์อย่างมีคุณภาพ
				</p>
			</div>
		</section>

		<!-- Head of Science Instrument Center -->
		<section class="bg-white py-20">
			<div class="container mx-auto px-4">
				<div class="mb-12 text-center">
          <h3 class="mb-2 text-lg font-semibold text-blue-600">OUR HEAD</h3>
					<h2 class="mb-4 text-3xl font-bold text-slate-900">หัวหน้าศูนย์เครื่องมือวิทยาศาสตร์</h2>
					<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
					<p class="mx-auto mt-6 max-w-2xl text-slate-600">
						ผู้นำทีมที่มีความรู้ความสามารถและประสบการณ์สูงในการดูแลและพัฒนาศูนย์เครื่องมือวิทยาศาสตร์
					</p>
				</div>

				<div class="flex justify-center">
					{#each headOfCenter as member}
						<Card
							class="overflow-hidden rounded-xl border-b-4 border-blue-600 shadow-lg transition-all duration-300 hover:shadow-xl max-w-lg"
						>
							<div class="relative">
								<img src={member.image} alt={member.name} class="h-72 w-full object-cover" />
								<div
									class="absolute bottom-0 left-0 right-0 h-24 bg-gradient-to-t from-slate-900 to-transparent"
								></div>
							</div>
							<div class="p-8">
								<h3 class="mb-2 text-2xl font-bold text-slate-900">{member.name}</h3>
								<p class="mb-4 flex items-center font-medium text-blue-600">
									<UserCircle class="mr-2 h-4 w-4" />
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

		<!-- Lab Advisors Section -->
		<section class="py-20 bg-gradient-to-r from-slate-50 to-blue-50">
			<div class="container mx-auto px-4">
				<div class="text-center mb-12">
					<h3 class="text-blue-600 font-semibold text-lg mb-2">OUR ADVISORS</h3>
					<h2 class="text-3xl font-bold text-slate-900 mb-4">อาจารย์ที่ปรึกษาห้องปฏิบัติการ</h2>
					<div class="h-1 w-24 bg-blue-600 mx-auto rounded-full"></div>
					<p class="mx-auto mt-6 max-w-2xl text-slate-600">
						คณาจารย์ผู้เชี่ยวชาญที่ให้คำปรึกษาและกำกับดูแลการดำเนินงานของห้องปฏิบัติการต่างๆ
					</p>
				</div>

				<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
					{#each labAdvisors as advisor}
						<Card class="overflow-hidden rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 hover:translate-y-[-5px] border-l-4 border-blue-600">
							<div class="p-6">
								<div class="flex items-center space-x-4 mb-4">
									<div class="h-16 w-16 rounded-full overflow-hidden">
										<img src={advisor.image} alt={advisor.name} class="h-full w-full object-cover" />
									</div>
									<div>
										<h3 class="text-xl font-bold text-slate-900">{advisor.name}</h3>
										<p class="text-blue-600 flex items-center text-sm">
											<GraduationCap class="h-4 w-4 mr-1" />
											{advisor.role}
										</p>
									</div>
								</div>
								<Separator class="my-4" />
								<p class="text-slate-600 text-sm">{advisor.description}</p>
							</div>
						</Card>
					{/each}
				</div>
			</div>
		</section>

		<!-- Staff Section -->
		<section class="py-20 bg-white">
			<div class="container mx-auto px-4">
				<div class="text-center mb-12">
					<h3 class="text-blue-600 font-semibold text-lg mb-2">OUR STAFF</h3>
					<h2 class="text-3xl font-bold text-slate-900 mb-4">นักวิทยาศาสตร์และเจ้าหน้าที่</h2>
					<div class="h-1 w-24 bg-blue-600 mx-auto rounded-full"></div>
					<p class="mx-auto mt-6 max-w-2xl text-slate-600">
						บุคลากรมืออาชีพที่ให้บริการด้านการวิเคราะห์ทดสอบและสนับสนุนการดำเนินงานของศูนย์ฯ
					</p>
				</div>

				<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
					{#each staffMembers as staff}
						<Card class="overflow-hidden rounded-lg shadow hover:shadow-md transition-all duration-300 border border-slate-200 hover:border-blue-200">
							<div class="p-4">
								<div class="flex flex-col items-center text-center mb-3">
									<div class="h-20 w-20 rounded-full overflow-hidden mb-4 border-2 border-blue-100">
										<img src={staff.image} alt={staff.name} class="h-full w-full object-cover" />
									</div>
									<h3 class="text-lg font-bold text-slate-900">{staff.name}</h3>
									<p class="text-blue-600 text-sm font-medium flex items-center">
										<Briefcase class="h-3 w-3 mr-1" />
										{staff.role}
									</p>
									<p class="text-slate-500 text-xs mt-1">{staff.department}</p>
								</div>
								<Separator class="my-3" />
								<p class="text-slate-600 text-xs">{staff.description}</p>
							</div>
						</Card>
					{/each}
				</div>
			</div>
		</section>

		<!-- Organization Chart Section -->
<!-- Organization Chart Section -->
<section class="py-20 bg-gradient-to-r from-blue-50 to-indigo-50">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <h3 class="text-blue-600 font-semibold text-lg mb-2">STRUCTURE</h3>
        <h2 class="text-3xl font-bold text-slate-900 mb-4">โครงสร้างองค์กร</h2>
        <div class="h-1 w-24 bg-blue-600 mx-auto rounded-full"></div>
        <p class="mx-auto mt-6 max-w-2xl text-slate-600">
          แผนผังโครงสร้างการบริหารงานของศูนย์เครื่องมือวิทยาศาสตร์ คณะวิทยาศาสตร์ สถาบันเทคโนโลยีพระจอมเกล้าเจ้าคุณทหารลาดกระบัง
        </p>
      </div>
  
      <div class="bg-white rounded-2xl shadow-lg p-8 max-w-4xl mx-auto">
        <!-- Organization chart tree structure -->
        <div class="flex flex-col items-center">
          <!-- Head of Center -->
          <div class="mb-8">
            <div class="bg-blue-600 text-white rounded-lg p-4 shadow-md text-center">
              <h4 class="font-bold">หัวหน้าศูนย์เครื่องมือวิทยาศาสตร์</h4>
              <p class="text-sm">ผศ.ดร.ธนากร โอสถจันทร์</p>
            </div>
          </div>
  
          <!-- Connecting line -->
          <div class="w-px h-8 bg-slate-300"></div>
  
          <!-- Main divisions - First Level -->
          <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-8 w-full">
            <!-- Academic Services Division -->
            <div class="flex flex-col items-center">
              <div class="bg-blue-500 text-white rounded-lg p-3 shadow-md text-center w-full">
                <h4 class="font-bold">ฝ่ายบริการวิชาการ</h4>
              </div>
            </div>
  
            <!-- Administration Division -->
            <div class="flex flex-col items-center">
              <div class="bg-blue-500 text-white rounded-lg p-3 shadow-md text-center w-full">
                <h4 class="font-bold">ฝ่ายบริหารและธุรการ</h4>
              </div>
            </div>
  
            <!-- Laboratory Management Division -->
            <div class="flex flex-col items-center">
              <div class="bg-blue-500 text-white rounded-lg p-3 shadow-md text-center w-full">
                <h4 class="font-bold">ฝ่ายห้องปฏิบัติการ</h4>
              </div>
            </div>
          </div>
  
          <!-- Second Level Labs - Lab Management Division Expansion -->
          <div class="w-full px-4">
            <h4 class="text-center font-semibold text-slate-700 mb-4">ห้องปฏิบัติการ</h4>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
              <!-- Lab 1 -->
              <div class="bg-blue-100 border border-blue-200 rounded-lg p-3 shadow-sm">
                <div class="flex items-center">
                  <TestTube class="h-5 w-5 text-blue-600 mr-2" />
                  <h5 class="font-medium text-slate-800">ห้องปฏิบัติการเคมีวิเคราะห์</h5>
                </div>
              </div>
  
              <!-- Lab 2 -->
              <div class="bg-blue-100 border border-blue-200 rounded-lg p-3 shadow-sm">
                <div class="flex items-center">
                  <Microscope class="h-5 w-5 text-blue-600 mr-2" />
                  <h5 class="font-medium text-slate-800">ห้องปฏิบัติการจุลชีววิทยา</h5>
                </div>
              </div>
  
              <!-- Lab 3 -->
              <div class="bg-blue-100 border border-blue-200 rounded-lg p-3 shadow-sm">
                <div class="flex items-center">
                  <Omega class="h-5 w-5 text-blue-600 mr-2" />
                  <h5 class="font-medium text-slate-800">ห้องปฏิบัติการฟิสิกส์</h5>
                </div>
              </div>
  
              <!-- Lab 4 -->
              <div class="bg-blue-100 border border-blue-200 rounded-lg p-3 shadow-sm">
                <div class="flex items-center">
                  <Bolt class="h-5 w-5 text-blue-600 mr-2" />
                  <h5 class="font-medium text-slate-800">ห้องปฏิบัติการเครื่องมือวิเคราะห์ขั้นสูง</h5>
                </div>
              </div>
  
              <!-- Lab 5 -->
              <div class="bg-blue-100 border border-blue-200 rounded-lg p-3 shadow-sm">
                <div class="flex items-center">
                  <Dna class="h-5 w-5 text-blue-600 mr-2" />
                  <h5 class="font-medium text-slate-800">ห้องปฏิบัติการชีวเคมี</h5>
                </div>
              </div>
  
              <!-- Lab 6 -->
              <div class="bg-blue-100 border border-blue-200 rounded-lg p-3 shadow-sm">
                <div class="flex items-center">
                  <Globe class="h-5 w-5 text-blue-600 mr-2" />
                  <h5 class="font-medium text-slate-800">ห้องปฏิบัติการสิ่งแวดล้อม</h5>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
  
  <!-- Contact Section -->
  <section class="py-16 bg-slate-900 text-white">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <h3 class="text-blue-400 font-semibold text-lg mb-2">CONTACT US</h3>
        <h2 class="text-3xl font-bold text-white mb-4">ติดต่อศูนย์เครื่องมือวิทยาศาสตร์</h2>
        <div class="h-1 w-24 bg-blue-400 mx-auto rounded-full"></div>
      </div>
  
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-4xl mx-auto">
        <!-- Address -->
        <div class="bg-slate-800 rounded-lg p-6 flex flex-col items-center text-center">
          <div class="bg-blue-500 rounded-full p-3 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-white"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"></path><circle cx="12" cy="10" r="3"></circle></svg>
          </div>
          <h4 class="text-xl font-bold mb-2">ที่อยู่</h4>
          <p class="text-slate-300">คณะวิทยาศาสตร์ สถาบันเทคโนโลยีพระจอมเกล้าเจ้าคุณทหารลาดกระบัง<br> ถนนฉลองกรุง แขวงลาดกระบัง<br> เขตลาดกระบัง กรุงเทพฯ 10520</p>
        </div>
  
        <!-- Phone -->
        <div class="bg-slate-800 rounded-lg p-6 flex flex-col items-center text-center">
          <div class="bg-blue-500 rounded-full p-3 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-white"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
          </div>
          <h4 class="text-xl font-bold mb-2">โทรศัพท์</h4>
          <p class="text-slate-300">02-329-8400 ต่อ 6237-8</p>
          <p class="text-slate-300 mt-2">โทรสาร: 02-329-8410</p>
        </div>
  
        <!-- Email -->
        <div class="bg-slate-800 rounded-lg p-6 flex flex-col items-center text-center">
          <div class="bg-blue-500 rounded-full p-3 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-white"><rect width="20" height="16" x="2" y="4" rx="2"></rect><path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"></path></svg>
          </div>
          <h4 class="text-xl font-bold mb-2">อีเมล</h4>
          <p class="text-slate-300">sciservice@kmitl.ac.th</p>
          <p class="text-slate-300 mt-2">เวลาทำการ: จันทร์-ศุกร์ 8:30-16:30 น.</p>
        </div>
      </div>
    </div>
  </section>
  
  <!-- Footer -->
  <footer class="bg-slate-950 text-slate-400 py-10">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-center">
        <div class="mb-6 md:mb-0">
          <div class="flex items-center space-x-2">
            <div class="h-8 w-8 rounded-full bg-blue-600 flex items-center justify-center">
              <span class="text-white font-bold text-sm">SC</span>
            </div>
            <span class="text-white font-bold">KMITL Science Instrument Center</span>
          </div>
          <p class="mt-2 text-sm">© 2025 คณะวิทยาศาสตร์ สถาบันเทคโนโลยีพระจอมเกล้าเจ้าคุณทหารลาดกระบัง</p>
        </div>
        
        <div class="flex space-x-8">
          <div>
            <h5 class="text-white font-medium mb-3">Links</h5>
            <ul class="space-y-2 text-sm">
              <li><a href="/" class="hover:text-blue-400 transition-colors">Services</a></li>
              <li><a href="/prices" class="hover:text-blue-400 transition-colors">Service Rates</a></li>
              <li><a href="/instruments" class="hover:text-blue-400 transition-colors">Instruments</a></li>
            </ul>
          </div>
          
          <div>
            <h5 class="text-white font-medium mb-3">About</h5>
            <ul class="space-y-2 text-sm">
              <li><a href="/aboutus" class="hover:text-blue-400 transition-colors">About Us</a></li>
              <li><a href="/personnel" class="hover:text-blue-400 transition-colors">Personnel</a></li>
              <li><a href="#" class="hover:text-blue-400 transition-colors">Contact</a></li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </footer>
    </main>
</div>