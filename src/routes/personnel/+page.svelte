<script lang="ts">
	import { Card } from '$lib/components/ui/card';
	import { Button } from '$lib/components/ui/button';
	import { Separator } from '$lib/components/ui/separator';
	import {
		GraduationCap,
		UserCircle,
		Briefcase,
		Mail,
		Phone
	} from 'lucide-svelte';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';

	// Head of Science Instrument Center
	const headOfCenter = [
		{
			name: 'ผศ.ดร. พิศาล ศรีราช',
			role: 'หัวหน้าศูนย์เครื่องมือวิทยาศาสตร์',
			description:
				'อาจารย์ประจำภาควิชา.....',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d',
			email: 'pisan.sr@kmitl.ac.th',
			phone: '02-329-8400 ต่อ 354'
		}
	];

	// Laboratory Advisors
	const labAdvisors = [
		{
			name: 'ผู้ช่วยศาสตราจารย์ ดร.ชลลดา  ฤตวิรุฬห์',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครื่องมือวิทยาศาสตร์',
			description: 'เครื่อง  Dynamic Mechanical Analyzer  (DMA) เครื่อง  Differential Scanning Calorimeter  (DSC) เครื่อง  Thermogravimetric  Analyzer  (TGA)',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รองศาสตราจารย์ ดร.ภัทธาวุธ  มนต์วิเศษ',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครื่องมือวิทยาศาสตร์',
			description: 'เครื่อง  Gel Permeation Chromatograph (GPC)',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รองศาสตราจารย์ ดร.เสาวภาคย์  ธีราทรง ',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครื่องมือวิทยาศาสตร์',
			description: 'เครื่อง  Ion Chromatograph (IC) เครื่อง  High Performance Liquid Chromatograph (HPLC)',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผู้ช่วยศาสตราจารย์ ดร.กลิ่นสุคนธ์ สุวรรณรัตน์	',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครื่องมือวิทยาศาสตร์',
			description: 'เครื่อง  Total Organic Carbon Analyzer (TOC)',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รองศาสตราจารย์ ดร.ณวสิทธิ์  โชติแสง',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครื่องมือวิทยาศาสตร์',
			description: 'เครื่อง  Fourier Transform Nuclear Magnetic Resonance Spectrometer 500 MHz(NMR 500 MHz) เครื่อง  Fourier Transform Infrared Spectrometer (FTIR) เครื่อง  UV-VIS Spectrophotometer เครื่อง  Spectrofluorophotometer',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รองศาสตราจารย์พัชนี เจริญยิ่ง',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครื่องมือวิทยาศาสตร์',
			description: 'เครื่อง  Fourier Transform Nuclear Magnetic Resonance Spectrometer 500 MHz(NMR 500 MHz) เครื่อง  Fourier Transform Infrared Spectrometer (FTIR) เครื่อง  UV-VIS Spectrophotometer เครื่อง  Spectrofluorophotometer',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รองศาสตราจารย์ ดร.การุณย์  สาดอ่อน	',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครื่องมือวิทยาศาสตร์',
			description: 'เครื่อง  วิเคราะห์หาปริมาณธาตุคาร์บอน ไฮโดรเจน  ไนโตรเจน ซัลเฟอร์ และออกซิเจน (CHNS/O Analyzer)',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รองศาสตราจารย์ ดร.กิตติศักดิ์  ชูจันทร์	',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครื่องมือวิทยาศาสตร์',
			description: 'เครื่อง  Fourier Transform Nuclear Magnetic Resonance Spectrometer 400 MHz (Solid-NMR 400 MHz)',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผศ.ดร.วิชัย สุทธิเดช',
			role: 'อาจารย์ที่ปรึกษาห้องปฏิบัติการพอลิเมอร์',
			description: 'ผู้เชี่ยวชาญด้านวิทยาศาสตร์และเทคโนโลยีพอลิเมอร์',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผู้ช่วยศาสตราจารย์ ดร.อาจณรงค์  เมธาวีสรรเสริญ	',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครี่องมือวิทยาศาสตร์',
			description: 'เครื่อง  Gas Chromatograph - Mass Spectrometer (GC-MS) เครื่อง  Zetasizer ',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผู้ช่วยศาสตราจารย์ ดร.พิศาล  ศรีราช  ',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครื่องมือวิทยาศาสตร์',
			description: 'เครื่อง  X-Ray Diffractometer (XRD) เครื่อง  X-Ray Fluorescence Spectrometer (XRF) เครื่อง  Contact Angle analyzer (CTA) เครื่อง  Zetasizer',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผู้ช่วยศาสตราจารย์ ดร.ศ.ทิพวรรณ  คล้ายบุญมี	',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครี่องมือวิทยาศาสตร์',
			description: 'เครื่อง  Scanning Electron Microscope (SEM) เครื่อง  Sputtering Coater',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รองศาสตราจารย์ ดร.อาภาภรณ์  สกุลการะเวก	',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบเครี่องมือวิทยาศาสตร์',
			description: 'เครื่อง Hall Characterization System',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รองศาสตราจารย์ ดร.สุพัตรา  โพธิ์เอี่ยม		',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบห้องปฏิบัติการภายในศูนย์เครี่องมือวิทยาศาสตร์',
			description: 'ห้องปฏิบัติการเพาะเลี้ยงเซลล์สัตว์ (Cell Culture Laboratory)',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ผู้ช่วยศาสตราจารย์ ดร.กานต์  วงศาริยะ  		',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบห้องปฏิบัติการภายในศูนย์เครี่องมือวิทยาศาสตร์',
			description: 'ห้องปฏิบัติการจุลชีววิทยาและจุลชีววิทยาระดับโมเลกุล (Microbiological and Molecular Biological Laboratory)',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'รองศาสตราจารย์ ดร.เชิดศักดิ์  มณีรัตนรุ่งโรจน์',
			role: 'ที่ปรึกษากำกับควบคุมและตรวจสอบห้องปฏิบัติการภายในศูนย์เครี่องมือวิทยาศาสตร์',
			description: 'ห้องปฏิบัติการเตรียมตัวอย่างสำหรับงานจุลทรรศน์อิเล็กตรอน (Sample Preparation Laboratory for Electron Microscope)',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},

	];

	// Staff members
	const staffMembers = [
		{
			name: 'ดร.นันทวัน เนียมหอม',
			role: 'นักวิทยาศาสตร์',
			description: 'ควบคุมและดูแลห้องปฏิบัติการจุลชีววิทยาและชีววิทยาระดับโมเลกุล, เครื่องมือวิทยาศาสตร์พื้นฐาน',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'สุดใจ ผุดผาด',
			role: 'นักวิทยาศาสตร์ชำนาญการ',
			description: 'ควบคุมและดูแลเครื่อง GC-MS, TGA, FTIR',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'สัญญา มีสิม',
			role: 'นักวิทยาศาสตร์',
			description: 'ควบคุมดูแลเครื่อง HPLC, IC, Contact Angle',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ศักรินทร์ บุญล้ำ',
			role: 'นักวิทยาศาสตร์',
			description: 'ควบคุมดูแล : TOC, DSC, DMA',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'วาสินี ธรรมสถิต',
			role: 'นักวิทยาศาสตร์',
			description: 'ควบคุมดูแล : SEM, Sputter Coater',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ณัฐพร มานะประดิษฐ์',
			role: 'นักวิทยาศาสตร์',
			description: 'ควบคุมดูแล : ห้องปฏิบัติการเพาะเลี้ยงเซลล์สัตว์, กล้องจุลทรรศน์, เครื่องทำน้ำบริสุทธิ์',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'วีรยุทธ อินบุญมา',
			role: 'เจ้าหน้าที่บริหารงานทั่วไป',
			description: 'ควบคุมดูแล : XRD, XRF, Hall',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ธัญญรัตน์ ชูศรี',
			role: 'เจ้าหน้าที่บริหารงานทั่วไป',
			description: 'ควบคุมดูแล : GPC, CHNS/O, BET',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
		},
		{
			name: 'ธนาภรณ์ มาศวรรณา',
			role: 'เจ้าหน้าที่บริหารงานทั่วไป',
			description: 'ควบคุมดูแล : NMR 400 MHz. และ 500 MHz., UV-VIS Spectrophotometer, Spectrofluorophotometer, Zetasizer',
			image: 'https://firebasestorage.googleapis.com/v0/b/cseventstorage.appspot.com/o/20211110012210N0VjO.jpg?alt=media&token=c749abea-f077-4af2-bc5a-d0c71cba935d'
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
					บุคลากร <span class="bg-gradient-to-r from-blue-600 to-indigo-600 bg-clip-text text-transparent">ศูนย์เครื่องมือวิทยาศาสตร์</span>
				</h2>
				<p class="mx-auto mb-10 max-w-2xl text-xl leading-relaxed text-slate-700">
          ทีมงานผู้เชี่ยวชาญของเราพร้อมให้บริการและสนับสนุนงานวิจัยและการวิเคราะห์ทดสอบทางวิทยาศาสตร์อย่างมีคุณภาพ
				</p>

			</div>
		</section>

		<!-- Head of Science Instrument Center -->
		<section class="bg-white py-24">
			<div class="container mx-auto px-4">
				<div class="mb-16 text-center">
          <span class="mb-2 inline-block rounded-full bg-blue-100 px-4 py-1 text-sm font-medium text-blue-800">OUR HEAD</span>
					<h2 class="mb-4 text-4xl font-bold text-slate-900">หัวหน้าศูนย์เครื่องมือวิทยาศาสตร์</h2>
					<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
					<p class="mx-auto mt-6 max-w-2xl text-slate-600">
						ผู้นำทีมที่มีความรู้ความสามารถและประสบการณ์สูงในการดูแลและพัฒนาศูนย์เครื่องมือวิทยาศาสตร์
					</p>
				</div>

				<div class="flex justify-center">
					{#each headOfCenter as member}
						<div class="relative max-w-3xl overflow-hidden rounded-2xl bg-white shadow-2xl transition-all duration-300 hover:shadow-blue-100">
							<div class="absolute -right-20 -top-20 h-64 w-64 rounded-full bg-blue-100 opacity-50"></div>
							<div class="absolute -bottom-20 -left-20 h-64 w-64 rounded-full bg-indigo-100 opacity-50"></div>
							
							<div class="relative z-10 grid grid-cols-1 overflow-hidden lg:grid-cols-2">
								<div class="order-2 p-10 lg:order-1">
									<h3 class="mb-2 text-3xl font-bold text-slate-900">{member.name}</h3>
									<p class="mb-4 flex items-center text-lg font-medium text-blue-600">
										<UserCircle class="mr-2 h-5 w-5" />
										{member.role}
									</p>
									<Separator class="mb-6" />
									<p class="mb-8 text-lg leading-relaxed text-slate-700">{member.description}</p>
									
									<div class="space-y-3">
										<div class="flex items-center text-slate-600">
											<Mail class="mr-3 h-5 w-5 text-blue-600" />
											<span>{member.email || 'science@kmitl.ac.th'}</span>
										</div>
										<div class="flex items-center text-slate-600">
											<Phone class="mr-3 h-5 w-5 text-blue-600" />
											<span>{member.phone || '02-329-8400 ต่อ 354'}</span>
										</div>
									</div>
								</div>
								
								<div class="order-1 lg:order-2">
									<div class="relative h-full min-h-[350px]">
										<img src={member.image} alt={member.name} class="h-full w-full object-cover object-center" />
										<div class="absolute bottom-0 left-0 right-0 h-1/3 bg-gradient-to-t from-slate-900/70 to-transparent"></div>
									</div>
								</div>
							</div>
						</div>
					{/each}
				</div>
			</div>
		</section>

		<!-- Lab Advisors Section -->
		<section class="relative overflow-hidden py-24">
			<div class="absolute inset-0 bg-gradient-to-br from-slate-50 to-blue-50"></div>
			<div class="absolute -top-64 -right-64 h-96 w-96 rounded-full bg-blue-200 opacity-30 blur-3xl"></div>
			<div class="absolute -bottom-96 -left-32 h-[500px] w-[500px] rounded-full bg-indigo-200 opacity-30 blur-3xl"></div>
			
			<div class="container relative z-10 mx-auto px-4">
				<div class="mb-16 text-center">
					<span class="mb-2 inline-block rounded-full bg-blue-100 px-4 py-1 text-sm font-medium text-blue-800">OUR ADVISORS</span>
					<h2 class="mb-4 text-4xl font-bold text-slate-900">อาจารย์ที่ปรึกษาห้องปฏิบัติการ</h2>
					<div class="mx-auto h-1 w-24 rounded-full bg-blue-600"></div>
					<p class="mx-auto mt-6 max-w-2xl text-slate-600">
						คณาจารย์ผู้เชี่ยวชาญที่ให้คำปรึกษาและกำกับดูแลการดำเนินงานของห้องปฏิบัติการต่างๆ ภายในศูนย์เครื่องมือวิทยาศาสตร์
					</p>
				</div>

				<div class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
					{#each labAdvisors as advisor, i}
						<div class="group h-full">
							<Card class="h-full overflow-hidden rounded-xl border-t-4 border-blue-600 bg-white shadow-lg transition-all duration-300 hover:translate-y-[-5px] hover:shadow-xl">
								<div class="relative p-6">
									<div class="absolute -right-6 -top-6 h-24 w-24 rounded-full bg-gradient-to-br from-blue-100 to-indigo-100 opacity-50 transition-all duration-300 group-hover:opacity-80"></div>
									
									<div class="relative z-10">
										<div class="mb-6 flex">
											<div class="mr-4 h-24 w-24 overflow-hidden rounded-xl border-4 border-white shadow-md">
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
										
										<div class="rounded-lg bg-slate-50 p-4">
											<h4 class="mb-2 text-sm font-semibold text-slate-700">ความเชี่ยวชาญ/รับผิดชอบ:</h4>
											<p class="text-slate-600 text-sm">{advisor.description}</p>
										</div>
									</div>
								</div>
							</Card>
						</div>
					{/each}
				</div>
				
			</div>
		</section>

		<!-- Staff Section -->
		<section class="py-24 bg-white">
			<div class="container mx-auto px-4">
				<div class="text-center mb-16">
					<span class="inline-block bg-blue-100 text-blue-800 text-sm font-medium px-4 py-1 rounded-full mb-2">OUR STAFF</span>
					<h2 class="text-4xl font-bold text-slate-900 mb-4">นักวิทยาศาสตร์และเจ้าหน้าที่</h2>
					<div class="h-1 w-24 bg-blue-600 mx-auto rounded-full"></div>
					<p class="mx-auto mt-6 max-w-2xl text-slate-600">
						บุคลากรมืออาชีพที่ให้บริการด้านการวิเคราะห์ทดสอบและสนับสนุนการดำเนินงานของศูนย์ฯ ด้วยความเชี่ยวชาญเฉพาะทาง
					</p>
				</div>

				<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-3 gap-8">
					{#each staffMembers as staff, i}
						<div class="group">
							<Card class="overflow-hidden rounded-xl shadow-lg transition-all duration-300 hover:translate-y-[-5px] hover:shadow-xl border-b-4 border-blue-600">
								<div class="relative">
									<div class="h-48 overflow-hidden">
										<img src={staff.image} alt={staff.name} class="w-full h-full object-cover object-center transition-transform duration-700 group-hover:scale-110" />
										<div class="absolute inset-0 bg-gradient-to-t from-slate-900/70 via-slate-900/20 to-transparent"></div>
									</div>
									
									<div class="absolute bottom-0 left-0 right-0 p-4 text-white">
										<h3 class="text-xl font-bold">{staff.name}</h3>
										<p class="flex items-center text-blue-200 text-sm">
											<Briefcase class="h-3 w-3 mr-1" />
											{staff.role}
										</p>
									</div>
								</div>
								
								<div class="p-5">
									<div class="bg-blue-50 rounded-lg p-4 mb-2">
										<h4 class="text-sm font-semibold text-slate-700 mb-2">ความรับผิดชอบ:</h4>
										<p class="text-slate-600 text-sm">{staff.description}</p>
									</div>
									
									<div class="mt-4 flex justify-end">
										<button class="text-blue-600 text-sm flex items-center hover:text-blue-800 transition-colors">
											ติดต่อ
											<svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
											</svg>
										</button>
									</div>
								</div>
							</Card>
						</div>
					{/each}
				</div>
			</div>
		</section>



		<!-- Contact Section -->

	</main>

	<!-- Footer -->
	<Footer />
</div>