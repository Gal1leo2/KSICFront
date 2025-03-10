<script lang="ts">
	import { onMount } from 'svelte';
	import { Button } from '$lib/components/ui/button';
	import { Input } from '$lib/components/ui/input';
	import { Card } from '$lib/components/ui/card';
	import { Separator } from '$lib/components/ui/separator';
	import { 
		FileText, 
		Beaker, 
		DollarSign, 
		CreditCard, 
		AlertCircle, 
		Clock, 
		CheckCircle,
		CircleSlash,
		Calendar,
		Search,
		ArrowRight,
		Plus,
		ChevronDown,
		Percent
	} from 'lucide-svelte';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';
	import { Accordion, AccordionContent, AccordionItem, AccordionTrigger } from '$lib/components/ui/accordion';
	import { Tabs, TabsContent, TabsList, TabsTrigger } from '$lib/components/ui/tabs';
	
	// Sample service request steps data
	const requestSteps = [
		{
			step: 1,
			title: 'ลงทะเบียนผู้ใช้บริการ',
			description: 'ผู้ใช้บริการต้องลงทะเบียนเป็นสมาชิกเพื่อยืนยันตัวตนในการขอใช้บริการ'
		},
		{
			step: 2,
			title: 'กรอกแบบฟอร์มขอใช้บริการ',
			description: 'ระบุรายละเอียดบริการที่ต้องการและข้อมูลตัวอย่างให้ครบถ้วน'
		},
		{
			step: 3,
			title: 'ส่งตัวอย่างและเอกสาร',
			description: 'นำส่งตัวอย่างพร้อมเอกสารที่เกี่ยวข้องที่ศูนย์เครื่องมือวิทยาศาสตร์'
		},
		{
			step: 4,
			title: 'ชำระค่าบริการ',
			description: 'ชำระค่าบริการตามใบแจ้งหนี้ที่ได้รับหลังจากเจ้าหน้าที่ตรวจสอบเอกสารและตัวอย่าง'
		},
		{
			step: 5,
			title: 'ดำเนินการทดสอบ',
			description: 'เจ้าหน้าที่ดำเนินการทดสอบตามที่ร้องขอ'
		},
		{
			step: 6,
			title: 'รับผลการทดสอบ',
			description: 'รับผลการทดสอบตามระยะเวลาที่กำหนด ทั้งรูปแบบเอกสารหรือไฟล์อิเล็กทรอนิกส์'
		}
	];

	// Sample service rates
	const serviceCategories = [
		{
			id: 'materials',
			name: 'การวิเคราะห์วัสดุ',
			services: [
				{
					name: 'Scanning Electron Microscope (SEM)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 800 },
						{ group: 'บุคลากรภายใน', price: 1200 },
						{ group: 'หน่วยงานภายนอก', price: 2500 },
						{ group: 'เอกชน', price: 3500 }
					]
				},
				{
					name: 'X-Ray Diffraction (XRD)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 600 },
						{ group: 'บุคลากรภายใน', price: 900 },
						{ group: 'หน่วยงานภายนอก', price: 1800 },
						{ group: 'เอกชน', price: 2500 }
					]
				},
				{
					name: 'Transmission Electron Microscope (TEM)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 1500 },
						{ group: 'บุคลากรภายใน', price: 2000 },
						{ group: 'หน่วยงานภายนอก', price: 4000 },
						{ group: 'เอกชน', price: 5500 }
					]
				}
			]
		},
		{
			id: 'chemicals',
			name: 'การวิเคราะห์ทางเคมี',
			services: [
				{
					name: 'High-Performance Liquid Chromatography (HPLC)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 500 },
						{ group: 'บุคลากรภายใน', price: 700 },
						{ group: 'หน่วยงานภายนอก', price: 1500 },
						{ group: 'เอกชน', price: 2200 }
					]
				},
				{
					name: 'Gas Chromatography-Mass Spectrometry (GC-MS)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 900 },
						{ group: 'บุคลากรภายใน', price: 1100 },
						{ group: 'หน่วยงานภายนอก', price: 2000 },
						{ group: 'เอกชน', price: 2800 }
					]
				},
				{
					name: 'Fourier Transform Infrared Spectroscopy (FTIR)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 400 },
						{ group: 'บุคลากรภายใน', price: 600 },
						{ group: 'หน่วยงานภายนอก', price: 1200 },
						{ group: 'เอกชน', price: 1800 }
					]
				}
			]
		},
		{
			id: 'biological',
			name: 'การวิเคราะห์ทางชีววิทยา',
			services: [
				{
					name: 'PCR/RT-PCR',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 700 },
						{ group: 'บุคลากรภายใน', price: 900 },
						{ group: 'หน่วยงานภายนอก', price: 1800 },
						{ group: 'เอกชน', price: 2500 }
					]
				},
				{
					name: 'Flow Cytometry',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 1000 },
						{ group: 'บุคลากรภายใน', price: 1200 },
						{ group: 'หน่วยงานภายนอก', price: 2200 },
						{ group: 'เอกชน', price: 3000 }
					]
				}
			]
		}
	];

	// Sample product categories for testing
	const productCategories = [
		{
			id: 'food',
			name: 'อาหารและเครื่องดื่ม',
			items: [
				'การวิเคราะห์คุณค่าทางโภชนาการ',
				'การตรวจสอบสารปนเปื้อน',
				'การตรวจสอบจุลินทรีย์ในอาหาร',
				'การวิเคราะห์วัตถุกันเสีย',
				'การทดสอบอายุการเก็บรักษา'
			]
		},
		{
			id: 'cosmetics',
			name: 'เครื่องสำอางและผลิตภัณฑ์เพื่อความงาม',
			items: [
				'การวิเคราะห์สารสำคัญ',
				'การทดสอบความคงตัว',
				'การตรวจสอบจุลินทรีย์ปนเปื้อน',
				'การวิเคราะห์โลหะหนัก',
				'การทดสอบประสิทธิภาพผลิตภัณฑ์'
			]
		},
		{
			id: 'pharma',
			name: 'ยาและผลิตภัณฑ์ทางการแพทย์',
			items: [
				'การวิเคราะห์ปริมาณสารสำคัญ',
				'การทดสอบความคงตัว',
				'การตรวจสอบสารปนเปื้อน',
				'การทดสอบการละลาย',
				'การวิเคราะห์สารสลายตัว'
			]
		},
		{
			id: 'environment',
			name: 'ตัวอย่างสิ่งแวดล้อม',
			items: [
				'การวิเคราะห์น้ำเสีย',
				'การตรวจสอบคุณภาพน้ำประปา',
				'การวิเคราะห์ดิน',
				'การตรวจสอบมลพิษทางอากาศ',
				'การวิเคราะห์โลหะหนักในสิ่งแวดล้อม'
			]
		}
	];

	// Sample promotions data
	const promotions = [
		{
			title: 'ส่วนลด 20% สำหรับนักศึกษาบัณฑิตศึกษา',
			description: 'สำหรับนักศึกษาระดับบัณฑิตศึกษาที่ทำวิทยานิพนธ์ รับส่วนลด 20% สำหรับบริการวิเคราะห์ทุกประเภท',
			expiry: '30 เมษายน 2568',
			code: 'GRAD20'
		},
		{
			title: 'แพ็คเกจวิเคราะห์วัสดุ 3 รายการ',
			description: 'รับส่วนลด 15% เมื่อใช้บริการวิเคราะห์วัสดุตั้งแต่ 3 รายการขึ้นไปในครั้งเดียว',
			expiry: '31 พฤษภาคม 2568',
			code: 'MATERIAL3'
		},
		{
			title: 'โปรโมชันสำหรับสมาชิกใหม่',
			description: 'สมาชิกใหม่รับส่วนลด 10% สำหรับการใช้บริการครั้งแรก',
			expiry: '31 ธันวาคม 2568',
			code: 'NEWUSER10'
		}
	];

	// Sample faulty equipment list
	const faultyEquipment = [
		{
			name: 'Scanning Electron Microscope (SEM) รุ่น JSM-7800F',
			status: 'อยู่ระหว่างการซ่อม',
			department: 'ห้องปฏิบัติการวิเคราะห์วัสดุ',
			estimatedRepair: '20 มีนาคม 2568'
		},
		{
			name: 'Atomic Absorption Spectroscopy (AAS)',
			status: 'ปิดซ่อมบำรุงตามแผน',
			department: 'ห้องปฏิบัติการวิเคราะห์โลหะ',
			estimatedRepair: '15 มีนาคม 2568'
		},
		{
			name: 'UV-Visible Spectrophotometer',
			status: 'รอการเปลี่ยนอะไหล่',
			department: 'ห้องปฏิบัติการเคมีวิเคราะห์',
			estimatedRepair: '25 มีนาคม 2568'
		}
	];

	// Tracking sample status
	let trackingId = '';
	let searchResult = null;

	function searchSampleStatus() {
		// Mock sample status search
		if (trackingId) {
			searchResult = {
				id: trackingId,
				status: 'อยู่ระหว่างการทดสอบ',
				receivedDate: '5 มีนาคม 2568',
				estimatedCompletion: '15 มีนาคม 2568',
				progress: 60,
				serviceType: 'การวิเคราะห์ด้วยเครื่อง SEM',
				department: 'ห้องปฏิบัติการวิเคราะห์วัสดุ',
				contactPerson: 'ดร.สมชาย วิทยาศาสตร์',
				contactEmail: 'somchai.w@example.ac.th'
			};
		} else {
			searchResult = null;
		}
	}

	// Payment verification
	let paymentReference = '';
	let paymentResult = null;

	function verifyPayment() {
		// Mock payment verification
		if (paymentReference) {
			paymentResult = {
				reference: paymentReference,
				status: 'ชำระเงินเรียบร้อยแล้ว',
				amount: '3,500 บาท',
				date: '8 มีนาคม 2568',
				service: 'การวิเคราะห์ด้วยเครื่อง SEM',
				receiptNumber: 'REC-20250308-001'
			};
		} else {
			paymentResult = null;
		}
	}
</script>

<div class="relative flex min-h-screen flex-col bg-slate-50 font-sans">
	<!-- Header -->
	<Header />

	<main>
		<!-- Hero banner for Our Services -->
		<section class="relative pb-6 pt-32 bg-gradient-to-br from-blue-700 to-indigo-900">
			<div class="container mx-auto px-4 pb-10">
				<div class="mx-auto max-w-3xl text-center text-white">
					<h1 class="mb-6 text-5xl font-bold">บริการของเรา</h1>
					<div class="mx-auto mb-6 h-1 w-24 bg-amber-500"></div>
					<p class="text-xl opacity-90">
						ศูนย์เครื่องมือวิทยาศาสตร์ให้บริการด้านการวิเคราะห์ทดสอบทางวิทยาศาสตร์โดยทีมงานผู้เชี่ยวชาญ
						พร้อมเครื่องมือที่ทันสมัยและได้มาตรฐานระดับสากล
					</p>
				</div>
			</div>
		</section>

		<!-- Services content with tabs -->
		<section class="bg-white py-10">
			<div class="container mx-auto mb-10 px-4">
				<div class="mx-auto max-w-5xl">
					<Tabs defaultValue="steps" class="w-full">
						<TabsList class="mb-8 w-full justify-start space-x-1 rounded-md bg-slate-100 p-1">
							<TabsTrigger value="steps" class="rounded-sm px-6 py-2.5 text-base">
								ขั้นตอนการติดต่อขอใช้บริการ
							</TabsTrigger>
							<TabsTrigger value="rates" class="rounded-sm px-6 py-2.5 text-base">
								อัตราค่าบริการ
							</TabsTrigger>
							<TabsTrigger value="promotions" class="rounded-sm px-6 py-2.5 text-base">
								โปรโมชัน/ส่วนลด
							</TabsTrigger>
							<TabsTrigger value="payment" class="rounded-sm px-6 py-2.5 text-base">
								แจ้งชำระค่าบริการ
							</TabsTrigger>
							<TabsTrigger value="status" class="rounded-sm px-6 py-2.5 text-base">
								ตรวจสอบสถานะ
							</TabsTrigger>
							<TabsTrigger value="equipment" class="rounded-sm px-6 py-2.5 text-base">
								รายการเครื่องเสีย
							</TabsTrigger>
						</TabsList>

						<!-- 1.1. ขั้นตอนการติดต่อขอใช้บริการ -->
						<TabsContent value="steps" class="mt-0">
							<Card class="overflow-hidden border-none shadow-lg">
								<div class="p-8">
									<h2 class="mb-8 text-3xl font-bold text-slate-900">ขั้นตอนการติดต่อขอใช้บริการ</h2>
									
									<div class="mb-8 rounded-lg bg-blue-50 p-4 text-blue-800">
										<p class="text-lg font-medium">
											การขอใช้บริการศูนย์เครื่องมือวิทยาศาสตร์สามารถดำเนินการได้ทั้งแบบออนไลน์และการติดต่อด้วยตนเอง
											โดยมีขั้นตอนดังนี้
										</p>
									</div>

									<div class="relative mb-14 mt-20 border-l-4 border-blue-500 pl-10">
										{#each requestSteps as step, index}
											<div class="relative mb-16 last:mb-0">
												<div class="absolute -left-14 flex h-10 w-10 items-center justify-center rounded-full bg-blue-600 text-lg font-bold text-white">
													{step.step}
												</div>
												<h3 class="mb-2 text-xl font-bold text-slate-900">{step.title}</h3>
												<p class="text-slate-600">{step.description}</p>
											</div>
										{/each}
									</div>

									<div class="mt-8 rounded-lg bg-amber-50 p-6">
										<h3 class="mb-4 text-xl font-bold text-amber-800">เอกสารที่ต้องเตรียม</h3>
										<ul class="space-y-2 text-amber-800">
											<li class="flex items-start">
												<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-amber-500"></div>
												<span>แบบฟอร์มขอใช้บริการที่กรอกข้อมูลครบถ้วน</span>
											</li>
											<li class="flex items-start">
												<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-amber-500"></div>
												<span>สำเนาบัตรประจำตัวนักศึกษา/บุคลากร หรือบัตรประชาชน (กรณีผู้ใช้บริการภายนอก)</span>
											</li>
											<li class="flex items-start">
												<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-amber-500"></div>
												<span>หนังสือรับรองจากอาจารย์ที่ปรึกษา (กรณีเป็นนักศึกษา)</span>
											</li>
											<li class="flex items-start">
												<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-amber-500"></div>
												<span>เอกสารข้อมูลความปลอดภัย (SDS) ของตัวอย่าง (ถ้ามี)</span>
											</li>
										</ul>
									</div>

									<div class="mt-10 flex flex-col items-center justify-center space-y-4">
										<p class="text-lg font-medium text-slate-800">
											หากมีข้อสงสัยเกี่ยวกับการขอใช้บริการ สามารถติดต่อเจ้าหน้าที่ได้ที่
										</p>
										<div class="flex items-center space-x-4">
											<Button class="bg-blue-600 hover:bg-blue-700">
												ดาวน์โหลดแบบฟอร์ม
											</Button>
											<Button variant="outline" class="border-blue-600 text-blue-600 hover:bg-blue-50">
												ติดต่อเจ้าหน้าที่
											</Button>
										</div>
									</div>
								</div>
							</Card>
						</TabsContent>

						<!-- 1.2. อัตราค่าบริการ -->
						<TabsContent value="rates" class="mt-0">
							<Card class="overflow-hidden border-none shadow-lg">
								<div class="p-8">
									<h2 class="mb-8 text-3xl font-bold text-slate-900">อัตราค่าบริการ</h2>
									
									<Tabs defaultValue="services" class="w-full">
										<TabsList class="mb-8 w-full max-w-md justify-start space-x-1 rounded-md bg-slate-100 p-1">
											<TabsTrigger value="services" class="rounded-sm px-6 py-2.5">
												รายการบริการและทดสอบ
											</TabsTrigger>
											<TabsTrigger value="products" class="rounded-sm px-6 py-2.5">
												กลุ่มผลิตภัณฑ์และตัวอย่าง
											</TabsTrigger>
										</TabsList>

										<!-- 1.2.1. รายการบริการและทดสอบ -->
										<TabsContent value="services" class="mt-0">
											<div class="mb-6 rounded-lg bg-blue-50 p-4 text-blue-800">
												<p>
													อัตราค่าบริการแบ่งตามประเภทผู้ใช้บริการ ดังนี้
												</p>
											</div>

											<div class="space-y-8">
												{#each serviceCategories as category}
													<div>
														<h3 class="mb-4 text-xl font-bold text-slate-900">{category.name}</h3>
														<div class="overflow-x-auto">
															<table class="min-w-full divide-y divide-gray-200 rounded-lg border">
																<thead>
																	<tr class="bg-gray-50">
																		<th class="px-6 py-3 text-left text-sm font-medium text-gray-500">บริการ</th>
																		<th class="px-6 py-3 text-right text-sm font-medium text-gray-500">นักศึกษาภายใน</th>
																		<th class="px-6 py-3 text-right text-sm font-medium text-gray-500">บุคลากรภายใน</th>
																		<th class="px-6 py-3 text-right text-sm font-medium text-gray-500">หน่วยงานภายนอก</th>
																		<th class="px-6 py-3 text-right text-sm font-medium text-gray-500">เอกชน</th>
																	</tr>
																</thead>
																<tbody class="divide-y divide-gray-200 bg-white">
																	{#each category.services as service}
																		<tr class="hover:bg-gray-50">
																			<td class="whitespace-nowrap px-6 py-4 text-sm font-medium text-gray-900">
																				{service.name}
																			</td>
																			{#each service.rates as rate}
																				<td class="whitespace-nowrap px-6 py-4 text-right text-sm text-gray-900">
																					{rate.price.toLocaleString()} บาท
																				</td>
																			{/each}
																		</tr>
																	{/each}
																</tbody>
															</table>
														</div>
													</div>
												{/each}
											</div>

											<div class="mt-8 rounded-lg bg-slate-100 p-6">
												<h3 class="mb-4 text-lg font-medium text-slate-800">หมายเหตุ:</h3>
												<ul class="space-y-2 text-slate-700">
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
														<span>ราคาไม่รวมภาษีมูลค่าเพิ่ม (VAT 7%)</span>
													</li>
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
														<span>กรณีตัวอย่างที่ต้องการเตรียมเป็นพิเศษ มีค่าเตรียมตัวอย่างเพิ่มเติม</span>
													</li>
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
														<span>กรณีเร่งด่วน มีค่าบริการเพิ่ม 50% จากอัตราปกติ</span>
													</li>
												</ul>
											</div>

											<div class="mt-8 text-center">
												<Button class="bg-blue-600 hover:bg-blue-700">
													ดาวน์โหลดเอกสารอัตราค่าบริการฉบับเต็ม
												</Button>
											</div>
										</TabsContent>

										<!-- 1.2.2. กลุ่มผลิตภัณฑ์และตัวอย่าง -->
										<TabsContent value="products" class="mt-0">
											<div class="mb-6 rounded-lg bg-blue-50 p-4 text-blue-800">
												<p>
													ศูนย์เครื่องมือวิทยาศาสตร์ให้บริการวิเคราะห์ทดสอบตัวอย่างหลากหลายประเภท ดังนี้
												</p>
											</div>

											<div class="grid grid-cols-1 gap-6 md:grid-cols-2">
												{#each productCategories as category}
													<Card class="border-none shadow">
														<div class="p-6">
															<h3 class="mb-4 text-xl font-bold text-slate-900">{category.name}</h3>
															<ul class="space-y-2">
																{#each category.items as item}
																	<li class="flex items-start">
																		<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-amber-500"></div>
																		<span class="text-slate-700">{item}</span>
																	</li>
																{/each}
															</ul>
														</div>
													</Card>
												{/each}
											</div>

											<div class="mt-8 rounded-lg bg-slate-100 p-6">
												<h3 class="mb-4 text-lg font-medium text-slate-800">ข้อกำหนดในการส่งตัวอย่าง:</h3>
												<ul class="space-y-2 text-slate-700">
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
														<span>ตัวอย่างต้องบรรจุในภาชนะที่เหมาะสมและปิดสนิท</span>
													</li>
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
														<span>ต้องติดฉลากระบุชื่อตัวอย่างและข้อมูลสำคัญให้ชัดเจน</span>
													</li>
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
                                                        <span>ตัวอย่างต้องส่งมาถึงศูนย์เครื่องมือวิทยาศาสตร์ภายในเวลาทำการ</span>