<script lang="ts">							
	import { Card } from '$lib/components/ui/card';
	import { Button } from '$lib/components/ui/button';
	import { Input } from '$lib/components/ui/input';
	import { Separator } from '$lib/components/ui/separator';
	import { Badge } from '$lib/components/ui/badge';
	import { Tabs, TabsContent, TabsList, TabsTrigger } from '$lib/components/ui/tabs';
	import { Accordion, AccordionContent, AccordionItem, AccordionTrigger } from '$lib/components/ui/accordion';
	import {
		Search,
		FileText,
		Beaker,
		DollarSign,
		CreditCard,
		AlertCircle,
		Clock,
		CheckCircle,
		CircleSlash,
		Calendar,
		ArrowRight,
		Plus,
		ChevronDown,
		Percent,
		BellRing,
		Calendar as CalendarIcon,
		CreditCard as CreditCardIcon,
		Download,
		InfoIcon,
		PhoneCall,
		Mail,
		Microscope,
		BookOpen,
		ChevronRight
	} from 'lucide-svelte';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';

	// Sample service request steps data
	const requestSteps = [
		{
			step: 1,
			title: 'ลงทะเบียนผู้ใช้บริการ',
			description: 'ผู้ใช้บริการต้องลงทะเบียนเป็นสมาชิกเพื่อยืนยันตัวตนในการขอใช้บริการ',
			icon: 'user'
		},
		{
			step: 2,
			title: 'กรอกแบบฟอร์มขอใช้บริการ',
			description: 'ระบุรายละเอียดบริการที่ต้องการและข้อมูลตัวอย่างให้ครบถ้วน',
			icon: 'form'
		},
		{
			step: 3,
			title: 'ส่งตัวอย่างและเอกสาร',
			description: 'นำส่งตัวอย่างพร้อมเอกสารที่เกี่ยวข้องที่ศูนย์เครื่องมือวิทยาศาสตร์',
			icon: 'sample'
		},
		{
			step: 4,
			title: 'ชำระค่าบริการ',
			description: 'ชำระค่าบริการตามใบแจ้งหนี้ที่ได้รับหลังจากเจ้าหน้าที่ตรวจสอบเอกสารและตัวอย่าง',
			icon: 'payment'
		},
		{
			step: 5,
			title: 'ดำเนินการทดสอบ',
			description: 'เจ้าหน้าที่ดำเนินการทดสอบตามที่ร้องขอ',
			icon: 'testing'
		},
		{
			step: 6,
			title: 'รับผลการทดสอบ',
			description: 'รับผลการทดสอบตามระยะเวลาที่กำหนด ทั้งรูปแบบเอกสารหรือไฟล์อิเล็กทรอนิกส์',
			icon: 'result'
		}
	];

	// Sample service rates
	const serviceCategories = [
		{
			id: 'physical',
			name: 'เครื่องมือตรวจลักษณะทางกายภาพและโครงสร้าง',
			icon: Microscope,
			description: 'บริการวิเคราะห์โครงสร้างและคุณสมบัติทางกายภาพของวัสดุด้วยเครื่องมือที่ทันสมัยและแม่นยำสูง',
			services: [
				{
					name: 'Contact Angle Analyzer',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 600 },
						{ group: 'บุคลากรภายใน', price: 900 },
						{ group: 'หน่วยงานภายนอก', price: 1800 },
						{ group: 'เอกชน', price: 2500 }
					]
				},
				{
					name: 'X-ray Diffractometer (XRD)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 800 },
						{ group: 'บุคลากรภายใน', price: 1100 },
						{ group: 'หน่วยงานภายนอก', price: 2200 },
						{ group: 'เอกชน', price: 3000 }
					]
				},
				{
					name: 'Scanning Electron Microscope (SEM)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 1200 },
						{ group: 'บุคลากรภายใน', price: 1600 },
						{ group: 'หน่วยงานภายนอก', price: 3500 },
						{ group: 'เอกชน', price: 4500 }
					]
				}
			]
		},
		{
			id: 'chemical',
			name: 'เครื่องมือทางเคมีประยุกต์',
			icon: Search,
			description: 'บริการวิเคราะห์องค์ประกอบและคุณสมบัติทางเคมีด้วยเครื่องมือมาตรฐานสากล ให้ผลการวิเคราะห์ที่แม่นยำและน่าเชื่อถือ',
			services: [
				{
					name: 'Dynamic Mechanical Analyzer',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 700 },
						{ group: 'บุคลากรภายใน', price: 1000 },
						{ group: 'หน่วยงานภายนอก', price: 2000 },
						{ group: 'เอกชน', price: 2800 }
					]
				},
				{
					name: 'Fourier Transform Infrared Spectrometer (FTIR)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 500 },
						{ group: 'บุคลากรภายใน', price: 800 },
						{ group: 'หน่วยงานภายนอก', price: 1600 },
						{ group: 'เอกชน', price: 2200 }
					]
				},
				{
					name: 'Gas Chromatography-Mass Spectrometry (GC-MS)',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 900 },
						{ group: 'บุคลากรภายใน', price: 1200 },
						{ group: 'หน่วยงานภายนอก', price: 2400 },
						{ group: 'เอกชน', price: 3200 }
					]
				}
			]
		},
		{
			id: 'biological',
			name: 'เครื่องมือทดสอบทางชีววิทยา',
			icon: Search,
			description: 'บริการวิเคราะห์ตัวอย่างทางชีววิทยาและจุลชีววิทยาโดยผู้เชี่ยวชาญ พร้อมเครื่องมือทดสอบที่มีประสิทธิภาพสูง',
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
				},
				{
					name: 'Cell Culture Analysis',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 800 },
						{ group: 'บุคลากรภายใน', price: 1100 },
						{ group: 'หน่วยงานภายนอก', price: 2000 },
						{ group: 'เอกชน', price: 2800 }
					]
				}
			]
		},
		{
			id: 'sample-prep',
			name: 'เครื่องเตรียมตัวอย่าง',
			icon: Beaker,
			description: 'บริการเตรียมตัวอย่างสำหรับการทดสอบและวิเคราะห์ด้วยเครื่องมือเฉพาะทางที่ทันสมัย',
			services: [
				{
					name: 'Sputtering Coater',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 400 },
						{ group: 'บุคลากรภายใน', price: 600 },
						{ group: 'หน่วยงานภายนอก', price: 1200 },
						{ group: 'เอกชน', price: 1800 }
					]
				},
				{
					name: 'Ultramicrotome',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 500 },
						{ group: 'บุคลากรภายใน', price: 700 },
						{ group: 'หน่วยงานภายนอก', price: 1400 },
						{ group: 'เอกชน', price: 2000 }
					]
				},
				{
					name: 'Freeze Dryer',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 600 },
						{ group: 'บุคลากรภายใน', price: 800 },
						{ group: 'หน่วยงานภายนอก', price: 1600 },
						{ group: 'เอกชน', price: 2200 }
					]
				}
			]
		},
		{
			id: 'general',
			name: 'เครื่องมือพื้นฐาน',
			icon: Search,
			description: 'บริการเครื่องมือพื้นฐานสำหรับการวิเคราะห์ทดสอบทั่วไป สำหรับงานวิจัยและการศึกษา',
			services: [
				{
					name: 'UV-VIS Spectrophotometer',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 300 },
						{ group: 'บุคลากรภายใน', price: 500 },
						{ group: 'หน่วยงานภายนอก', price: 1000 },
						{ group: 'เอกชน', price: 1500 }
					]
				},
				{
					name: 'Digital Microscope',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 200 },
						{ group: 'บุคลากรภายใน', price: 400 },
						{ group: 'หน่วยงานภายนอก', price: 800 },
						{ group: 'เอกชน', price: 1200 }
					]
				},
				{
					name: 'pH Meter and Conductivity Meter',
					rates: [
						{ group: 'นักศึกษาภายใน', price: 100 },
						{ group: 'บุคลากรภายใน', price: 200 },
						{ group: 'หน่วยงานภายนอก', price: 400 },
						{ group: 'เอกชน', price: 600 }
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
			code: 'GRAD20',
			color: 'blue'
		},
		{
			title: 'แพ็คเกจวิเคราะห์วัสดุ 3 รายการ',
			description: 'รับส่วนลด 15% เมื่อใช้บริการวิเคราะห์วัสดุตั้งแต่ 3 รายการขึ้นไปในครั้งเดียว',
			expiry: '31 พฤษภาคม 2568',
			code: 'MATERIAL3',
			color: 'indigo'
		},
		{
			title: 'โปรโมชันสำหรับสมาชิกใหม่',
			description: 'สมาชิกใหม่รับส่วนลด 10% สำหรับการใช้บริการครั้งแรก',
			expiry: '31 ธันวาคม 2568',
			code: 'NEWUSER10',
			color: 'amber'
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
	let searchResult: any = null;

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
	let paymentResult: any = null;

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
	
	// Function to get icon for steps
	function getStepIcon(iconName: string) {
		switch(iconName) {
			case 'user': return '<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" /></svg>';
			case 'form': return '<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" /></svg>';
			case 'sample': return '<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z" /></svg>';
			case 'payment': return '<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" /></svg>';
			case 'testing': return '<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z" /></svg>';
			case 'result': return '<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" /></svg>';
			default: return '<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>';
		}
	}
</script>

<!-- Main Layout -->
<div class="relative flex min-h-screen flex-col bg-slate-50 font-sans">
	<!-- Header -->
	<Header />

	<main>
		<!-- Hero banner -->
		<section class="relative overflow-hidden bg-gradient-to-br from-blue-700 to-indigo-900 py-24">
			<div class="absolute inset-0 bg-pattern-grid opacity-10"></div>
			<div class="absolute -top-24 -right-24 h-64 w-64 rounded-full bg-blue-500 opacity-20 blur-3xl"></div>
			<div class="absolute -bottom-32 -left-32 h-96 w-96 rounded-full bg-indigo-500 opacity-20 blur-3xl"></div>
			
			<div class="container relative z-10 mx-auto px-4 text-center">
				<span class="mb-2 inline-block rounded-full bg-blue-900/30 px-4 py-1 text-sm font-medium text-blue-100">KMITL Science Instrument Center</span>
				<h1 class="mb-6 text-5xl font-bold tracking-tight text-white md:text-6xl">
					บริการของเรา <span class="bg-gradient-to-r from-amber-400 to-amber-300 bg-clip-text text-transparent">ศูนย์เครื่องมือวิทยาศาสตร์</span>
				</h1>
				<div class="mx-auto mb-6 h-1 w-24 bg-amber-500"></div>
				<p class="mx-auto mb-10 max-w-3xl text-xl leading-relaxed text-blue-100">
					ศูนย์เครื่องมือวิทยาศาสตร์ให้บริการด้านการวิเคราะห์ทดสอบทางวิทยาศาสตร์โดยทีมงานผู้เชี่ยวชาญ
					พร้อมเครื่องมือที่ทันสมัยและได้มาตรฐานระดับสากล
				</p>
				
				<!-- Quick access buttons -->
				<div class="mt-10 grid grid-cols-1 gap-4 md:grid-cols-3">
					<Button class="bg-amber-500 px-6 py-4 text-white hover:bg-amber-600 shadow-lg group">
						<span class="mr-2">
							<FileText class="h-5 w-5 transition-transform duration-300 group-hover:scale-110" />
						</span>
						<span>ดาวน์โหลดแบบฟอร์มขอใช้บริการ</span>
					</Button>
					<Button class="bg-white px-6 py-4 text-blue-800 hover:bg-blue-50 shadow-lg group">
						<span class="mr-2">
							<DollarSign class="h-5 w-5 transition-transform duration-300 group-hover:scale-110" />
						</span>
						<span>ดูอัตราค่าบริการ</span>
					</Button>
					<Button class="bg-blue-600 px-6 py-4 text-white hover:bg-blue-700 shadow-lg group">
						<span class="mr-2">
							<Search class="h-5 w-5 transition-transform duration-300 group-hover:scale-110" />
						</span>
						<span>ตรวจสอบสถานะตัวอย่าง</span>
					</Button>
				</div>
			</div>
		</section>

		<!-- Services cards section -->
		<section class="py-16 bg-white">
			<div class="container mx-auto px-4">
				<div class="text-center mb-12">
					<h2 class="text-3xl font-bold text-slate-900 mb-4">บริการวิเคราะห์ทดสอบของเรา</h2>
					<div class="h-1 w-24 bg-blue-600 mx-auto rounded-full mb-6"></div>
					<p class="text-slate-600 max-w-3xl mx-auto">
						ศูนย์เครื่องมือวิทยาศาสตร์ให้บริการวิเคราะห์ทดสอบที่หลากหลาย ครอบคลุมการใช้งานทั้งด้านการวิจัย การศึกษา และการพัฒนาผลิตภัณฑ์
					</p>
				</div>
				
				<div class="grid grid-cols-1 md:grid-cols-3 gap-8">
					{#each serviceCategories as category}
						<div class="group">
							<Card class="h-full overflow-hidden rounded-xl border-t-4 border-blue-600 bg-white shadow-lg transition-all duration-300 hover:translate-y-[-5px] hover:shadow-xl">
								<div class="p-6">
									<div class="flex items-center mb-4">
										<div class="bg-blue-100 p-3 rounded-xl mr-4">
											<svelte:component this={category.icon} class="h-8 w-8 text-blue-600" />
										</div>
										<h3 class="text-xl font-bold text-slate-900">{category.name}</h3>
									</div>
									
									<p class="text-slate-600 mb-6">{category.description}</p>
									
									<Separator class="my-4" />
									
									<ul class="mb-6 space-y-2">
										{#each category.services as service, i}
											{#if i < 3}
												<li class="flex items-center text-slate-700">
													<div class="mr-2 h-1.5 w-1.5 rounded-full bg-blue-500"></div>
													<span>{service.name}</span>
												</li>
											{/if}
										{/each}
										{#if category.services.length > 3}
											<li class="text-blue-600 font-medium text-sm">+ {category.services.length - 3} บริการเพิ่มเติม</li>
										{/if}
									</ul>
									
									<div class="mt-auto pt-4">
										<Button class="w-full bg-blue-600 hover:bg-blue-700 group-hover:shadow-md">
											<span>ดูรายละเอียดและอัตราค่าบริการ</span>
											<ChevronRight class="ml-2 h-4 w-4" />
										</Button>
									</div>
								</div>
							</Card>
						</div>
					{/each}
				</div>
			</div>
		</section>

		<!-- Services content with tabs -->
		<section class="bg-slate-50 py-16">
			<div class="container mx-auto px-4">
				<div class="mx-auto max-w-6xl">
					<Tabs defaultValue="steps" class="w-full">
						<div class="mb-10 flex justify-center overflow-x-auto">
							<TabsList class="bg-white p-1 rounded-full shadow-md border">
								<TabsTrigger value="steps" class="rounded-full px-5 py-2.5 text-base whitespace-nowrap data-[state=active]:bg-blue-600 data-[state=active]:text-white">
									<Clock class="mr-2 h-4 w-4 inline" />
									ขั้นตอนการขอใช้บริการ
								</TabsTrigger>
								<TabsTrigger value="rates" class="rounded-full px-5 py-2.5 text-base whitespace-nowrap data-[state=active]:bg-blue-600 data-[state=active]:text-white">
									<DollarSign class="mr-2 h-4 w-4 inline" />
									อัตราค่าบริการ
								</TabsTrigger>
								<TabsTrigger value="promotions" class="rounded-full px-5 py-2.5 text-base whitespace-nowrap data-[state=active]:bg-blue-600 data-[state=active]:text-white">
									<Percent class="mr-2 h-4 w-4 inline" />
									โปรโมชัน/ส่วนลด
								</TabsTrigger>
								<TabsTrigger value="payment" class="rounded-full px-5 py-2.5 text-base whitespace-nowrap data-[state=active]:bg-blue-600 data-[state=active]:text-white">
									<CreditCard class="mr-2 h-4 w-4 inline" />
									<CreditCard class="mr-2 h-4 w-4 inline" />
									แจ้งชำระค่าบริการ
								</TabsTrigger>
								<TabsTrigger value="status" class="rounded-full px-5 py-2.5 text-base whitespace-nowrap data-[state=active]:bg-blue-600 data-[state=active]:text-white">
									<Search class="mr-2 h-4 w-4 inline" />
									ตรวจสอบสถานะ
								</TabsTrigger>
								<TabsTrigger value="equipment" class="rounded-full px-5 py-2.5 text-base whitespace-nowrap data-[state=active]:bg-blue-600 data-[state=active]:text-white">
									<AlertCircle class="mr-2 h-4 w-4 inline" />
									รายการเครื่องเสีย
								</TabsTrigger>
							</TabsList>
						</div>

						<!-- 1.1. ขั้นตอนการติดต่อขอใช้บริการ -->
						<TabsContent value="steps" class="mt-0">
							<Card class="overflow-hidden border-none shadow-xl rounded-xl">
								<div class="relative overflow-hidden">
									<div class="absolute -right-32 -top-32 h-64 w-64 rounded-full bg-blue-100 opacity-50"></div>
									<div class="absolute -left-32 -bottom-32 h-64 w-64 rounded-full bg-indigo-100 opacity-50"></div>
									
									<div class="relative p-8 md:p-10">
										<div class="flex flex-col md:flex-row md:items-center mb-8">
											<div class="mb-6 md:mb-0 md:mr-8">
												<h2 class="text-3xl font-bold text-slate-900 mb-3">ขั้นตอนการติดต่อขอใช้บริการ</h2>
												<p class="text-slate-600">การขอใช้บริการศูนย์เครื่องมือวิทยาศาสตร์สามารถดำเนินการได้ทั้งแบบออนไลน์และการติดต่อด้วยตนเอง</p>
											</div>
											<div class="flex-shrink-0">
												<div class="flex space-x-3">
													<Button class="bg-blue-600 hover:bg-blue-700 flex items-center">
														<Download class="mr-2 h-4 w-4" />
														ดาวน์โหลดแบบฟอร์ม
													</Button>
													<Button variant="outline" class="border-blue-600 text-blue-600 hover:bg-blue-50 flex items-center">
														<PhoneCall class="mr-2 h-4 w-4" />
														ติดต่อเจ้าหน้าที่
													</Button>
												</div>
											</div>
										</div>
										
										<div class="bg-gradient-to-r from-blue-50 to-indigo-50 p-6 rounded-xl mb-10">
											<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
												{#each requestSteps.slice(0, 3) as step}
													<Card class="bg-white border-none shadow-md hover:shadow-lg transition-all duration-300 overflow-hidden">
														<div class="p-5">
															<div class="flex items-center mb-4">
																<div class="flex-shrink-0 h-10 w-10 rounded-full bg-blue-600 flex items-center justify-center text-white font-bold mr-4">
																	{step.step}
																</div>
																<h3 class="text-lg font-bold text-slate-900">{step.title}</h3>
															</div>
															<p class="text-slate-600">{step.description}</p>
														</div>
													</Card>
												{/each}
											</div>
										</div>
										
										<div class="bg-gradient-to-r from-indigo-50 to-purple-50 p-6 rounded-xl mb-10">
											<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
												{#each requestSteps.slice(3) as step}
													<Card class="bg-white border-none shadow-md hover:shadow-lg transition-all duration-300 overflow-hidden">
														<div class="p-5">
															<div class="flex items-center mb-4">
																<div class="flex-shrink-0 h-10 w-10 rounded-full bg-indigo-600 flex items-center justify-center text-white font-bold mr-4">
																	{step.step}
																</div>
																<h3 class="text-lg font-bold text-slate-900">{step.title}</h3>
															</div>
															<p class="text-slate-600">{step.description}</p>
														</div>
													</Card>
												{/each}
											</div>
										</div>

										<div class="rounded-xl bg-amber-50 p-6 border border-amber-200">
											<div class="flex items-start mb-4">
												<div class="flex-shrink-0 mr-4">
													<div class="h-10 w-10 bg-amber-100 rounded-full flex items-center justify-center">
														<InfoIcon class="h-5 w-5 text-amber-700" />
													</div>
												</div>
												<div>
													<h3 class="text-xl font-bold text-amber-800 mb-2">เอกสารที่ต้องเตรียม</h3>
													<p class="text-amber-700 mb-4">โปรดเตรียมเอกสารต่อไปนี้ให้พร้อมเพื่อความรวดเร็วในการดำเนินการ</p>
												</div>
											</div>
											
											<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
												<ul class="space-y-3">
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-amber-500"></div>
														<span class="text-amber-800">แบบฟอร์มขอใช้บริการที่กรอกข้อมูลครบถ้วน</span>
													</li>
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-amber-500"></div>
														<span class="text-amber-800">สำเนาบัตรประจำตัวนักศึกษา/บุคลากร หรือบัตรประชาชน (กรณีผู้ใช้บริการภายนอก)</span>
													</li>
												</ul>
												<ul class="space-y-3">
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-amber-500"></div>
														<span class="text-amber-800">หนังสือรับรองจากอาจารย์ที่ปรึกษา (กรณีเป็นนักศึกษา)</span>
													</li>
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-amber-500"></div>
														<span class="text-amber-800">เอกสารข้อมูลความปลอดภัย (SDS) ของตัวอย่าง (ถ้ามี)</span>
													</li>
												</ul>
											</div>
										</div>
									</div>
								</div>
							</Card>
						</TabsContent>

						<!-- 1.2. อัตราค่าบริการ -->
						<TabsContent value="rates" class="mt-0">
							<Card class="overflow-hidden border-none shadow-xl rounded-xl">
								<div class="relative overflow-hidden">
									<div class="absolute -right-32 -top-32 h-64 w-64 rounded-full bg-blue-100 opacity-50"></div>
									<div class="absolute -left-32 -bottom-32 h-64 w-64 rounded-full bg-indigo-100 opacity-50"></div>
									
									<div class="relative p-8 md:p-10">
										<div class="flex flex-col md:flex-row md:items-end justify-between mb-8">
											<div>
												<h2 class="text-3xl font-bold text-slate-900 mb-3">อัตราค่าบริการ</h2>
												<p class="text-slate-600 max-w-2xl">
													อัตราค่าบริการแบ่งตามประเภทผู้ใช้บริการ โดยมีอัตราพิเศษสำหรับนักศึกษาและบุคลากรภายในสถาบัน
												</p>
											</div>
											<div class="mt-4 md:mt-0">
												<Button class="bg-blue-600 hover:bg-blue-700 flex items-center">
													<Download class="mr-2 h-4 w-4" />
													ดาวน์โหลดรายการค่าบริการทั้งหมด
												</Button>
											</div>
										</div>
										
										<div class="mb-8">
											<Tabs defaultValue="materials" class="w-full">
												<div class="mb-6 overflow-x-auto">
													<TabsList class="inline-flex rounded-full bg-slate-100 p-1 mb-2">
														{#each serviceCategories as category}
															<TabsTrigger value={category.id} class="rounded-full px-4 py-2 whitespace-nowrap data-[state=active]:bg-blue-600 data-[state=active]:text-white">
																<svelte:component this={category.icon} class="mr-2 h-4 w-4 inline" />
																{category.name}
															</TabsTrigger>
														{/each}
													</TabsList>
												</div>
												
												{#each serviceCategories as category}
													<TabsContent value={category.id} class="mt-0">
														<Card class="p-6 bg-gradient-to-r from-blue-50 to-indigo-50 border-none shadow-md rounded-xl mb-6">
															<h3 class="text-xl font-bold text-slate-900 mb-2">{category.name}</h3>
															<p class="text-slate-600 mb-0">{category.description}</p>
														</Card>
														
														<div class="overflow-x-auto rounded-xl shadow-md">
															<table class="min-w-full divide-y divide-gray-200 rounded-xl border">
																<thead>
																	<tr class="bg-gradient-to-r from-blue-600 to-indigo-700">
																		<th class="px-6 py-4 text-left text-sm font-semibold text-white">บริการ</th>
																		<th class="px-6 py-4 text-right text-sm font-semibold text-white">นักศึกษาภายใน</th>
																		<th class="px-6 py-4 text-right text-sm font-semibold text-white">บุคลากรภายใน</th>
																		<th class="px-6 py-4 text-right text-sm font-semibold text-white">หน่วยงานภายนอก</th>
																		<th class="px-6 py-4 text-right text-sm font-semibold text-white">เอกชน</th>
																	</tr>
																</thead>
																<tbody class="divide-y divide-gray-200 bg-white">
																	{#each category.services as service, i}
																		<tr class="{i % 2 === 0 ? 'bg-white' : 'bg-slate-50'} hover:bg-blue-50 transition-colors">
																			<td class="whitespace-nowrap px-6 py-4 text-sm font-medium text-gray-900">
																				{service.name}
																			</td>
																			{#each service.rates as rate}
																				<td class="whitespace-nowrap px-6 py-4 text-right text-sm font-medium">
																					{#if rate.group === 'นักศึกษาภายใน'}
																						<span class="text-blue-700">{rate.price.toLocaleString()} บาท</span>
																					{:else if rate.group === 'บุคลากรภายใน'}
																						<span class="text-indigo-700">{rate.price.toLocaleString()} บาท</span>
																					{:else if rate.group === 'หน่วยงานภายนอก'}
																						<span class="text-purple-700">{rate.price.toLocaleString()} บาท</span>
																					{:else}
																						<span class="text-slate-700">{rate.price.toLocaleString()} บาท</span>
																					{/if}
																				</td>
																			{/each}
																		</tr>
																	{/each}
																</tbody>
															</table>
														</div>
													</TabsContent>
												{/each}
											</Tabs>
										</div>
										
										<div class="rounded-xl bg-slate-100 p-6">
											<div class="flex mb-4">
												<div class="h-10 w-10 bg-slate-200 rounded-full flex items-center justify-center mr-4">
													<InfoIcon class="h-5 w-5 text-slate-700" />
												</div>
												<h3 class="text-xl font-bold text-slate-800">หมายเหตุ</h3>
											</div>
											
											<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
												<ul class="space-y-2 text-slate-700">
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
														<span>ราคาไม่รวมภาษีมูลค่าเพิ่ม (VAT 7%)</span>
													</li>
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
														<span>กรณีตัวอย่างที่ต้องการเตรียมเป็นพิเศษ มีค่าเตรียมตัวอย่างเพิ่มเติม</span>
													</li>
												</ul>
												<ul class="space-y-2 text-slate-700">
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
														<span>กรณีเร่งด่วน มีค่าบริการเพิ่ม 50% จากอัตราปกติ</span>
													</li>
													<li class="flex items-start">
														<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-slate-500"></div>
														<span>อัตราค่าบริการอาจมีการเปลี่ยนแปลงตามความเหมาะสม</span>
													</li>
												</ul>
											</div>
										</div>
									</div>
								</div>
							</Card>
						</TabsContent>
						
						<!-- 1.3. โปรโมชัน/ส่วนลด -->
						<TabsContent value="promotions" class="mt-0">
							<Card class="overflow-hidden border-none shadow-xl rounded-xl">
								<div class="relative overflow-hidden">
									<div class="absolute -right-32 -top-32 h-64 w-64 rounded-full bg-blue-100 opacity-50"></div>
									<div class="absolute -left-32 -bottom-32 h-64 w-64 rounded-full bg-indigo-100 opacity-50"></div>
									
									<div class="relative p-8 md:p-10">
										<div class="flex items-center mb-8">
											<div class="h-12 w-12 bg-amber-100 rounded-full flex items-center justify-center mr-4">
												<Percent class="h-6 w-6 text-amber-600" />
											</div>
											<div>
												<h2 class="text-3xl font-bold text-slate-900 mb-1">โปรโมชันและส่วนลดพิเศษ</h2>
												<p class="text-slate-600">สิทธิพิเศษสำหรับผู้ใช้บริการของศูนย์เครื่องมือวิทยาศาสตร์</p>
											</div>
										</div>
										
										<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-10">
											{#each promotions as promo, i}
												<Card class="overflow-hidden border-none shadow-lg rounded-xl h-full hover:shadow-xl transition-all duration-300 hover:translate-y-[-5px]">
													<div class="bg-gradient-to-r {promo.color === 'blue' ? 'from-blue-600 to-blue-700' : promo.color === 'indigo' ? 'from-indigo-600 to-indigo-700' : 'from-amber-600 to-amber-700'} p-4 text-white">
														<h3 class="text-xl font-bold mb-2">{promo.title}</h3>
														<Badge class="bg-white/20">{promo.code}</Badge>
													</div>
													<div class="p-6">
														<p class="text-slate-600 mb-6">{promo.description}</p>
														<div class="flex items-center justify-between mt-auto">
															<div class="flex items-center text-sm text-slate-500">
																<Calendar class="mr-2 h-4 w-4" />
																<span>หมดเขต: {promo.expiry}</span>
															</div>
															<Button variant="outline" class="border-blue-600 text-blue-600 hover:bg-blue-50">
																ใช้โปรโมชัน
															</Button>
														</div>
													</div>
												</Card>
											{/each}
										</div>
										
										<div class="bg-blue-50 rounded-xl p-6 border border-blue-200">
											<h3 class="text-xl font-bold text-blue-900 mb-4">เงื่อนไขการใช้โปรโมชัน</h3>
											<ul class="space-y-2 text-blue-800">
												<li class="flex items-start">
													<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-blue-500"></div>
													<span>ส่วนลดใช้ได้เฉพาะบริการตามที่ระบุเท่านั้น</span>
												</li>
												<li class="flex items-start">
													<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-blue-500"></div>
													<span>โปรดแจ้งรหัสส่วนลดในขั้นตอนการลงทะเบียนขอใช้บริการ</span>
												</li>
												<li class="flex items-start">
													<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-blue-500"></div>
													<span>ไม่สามารถใช้ร่วมกับโปรโมชันอื่นได้</span>
												</li>
												<li class="flex items-start">
													<div class="mr-3 mt-1.5 h-2 w-2 rounded-full bg-blue-500"></div>
													<span>ศูนย์ฯ ขอสงวนสิทธิ์ในการเปลี่ยนแปลงเงื่อนไขโดยไม่แจ้งให้ทราบล่วงหน้า</span>
												</li>
											</ul>
										</div>
									</div>
								</div>
							</Card>
						</TabsContent>
						
						<!-- 1.4. แจ้งชำระค่าบริการ -->
						<TabsContent value="payment" class="mt-0">
							<Card class="overflow-hidden border-none shadow-xl rounded-xl">
								<div class="relative overflow-hidden">
									<div class="absolute -right-32 -top-32 h-64 w-64 rounded-full bg-blue-100 opacity-50"></div>
									<div class="absolute -left-32 -bottom-32 h-64 w-64 rounded-full bg-indigo-100 opacity-50"></div>
									
									<div class="relative p-8 md:p-10">
										<div class="flex items-center mb-8">
											<div class="h-12 w-12 bg-blue-100 rounded-full flex items-center justify-center mr-4">
												<CreditCard class="h-6 w-6 text-blue-600" />
											</div>
											<div>
												<h2 class="text-3xl font-bold text-slate-900 mb-1">แจ้งชำระค่าบริการ</h2>
												<p class="text-slate-600">แจ้งการชำระเงินและตรวจสอบสถานะการชำระเงิน</p>
											</div>
										</div>
										
										<div class="grid grid-cols-1 lg:grid-cols-2 gap-10">
											<!-- Check payment status -->
											<div>
												<h3 class="text-xl font-bold text-slate-900 mb-4">ตรวจสอบสถานะการชำระเงิน</h3>
												<Card class="p-6 border border-slate-200">
													<div class="space-y-4">
														<div>
															<label for="paymentRef" class="text-sm font-medium text-slate-700 mb-1 block">
																เลขอ้างอิงการชำระเงิน
															</label>
															<Input 
																id="paymentRef" 
																bind:value={paymentReference} 
																placeholder="ระบุเลขอ้างอิงการชำระเงิน"
																class="border-slate-300"
															/>
														</div>
														<Button 
															class="w-full bg-blue-600 hover:bg-blue-700" 
															on:click={verifyPayment}
														>
															ตรวจสอบสถานะ
														</Button>
													</div>
													
													{#if paymentResult}
														<div class="mt-6 p-4 rounded-lg bg-blue-50 border border-blue-200">
															<div class="flex items-center mb-3">
																<CheckCircle class="h-5 w-5 text-green-600 mr-2" />
																<h4 class="font-bold text-slate-900">{paymentResult.status}</h4>
															</div>
															<div class="space-y-2 text-sm">
																<div class="flex justify-between">
																	<span class="text-slate-600">เลขอ้างอิง:</span>
																	<span class="font-medium text-slate-900">{paymentResult.reference}</span>
																</div>
																<div class="flex justify-between">
																	<span class="text-slate-600">จำนวนเงิน:</span>
																	<span class="font-medium text-slate-900">{paymentResult.amount}</span>
																</div>
																<div class="flex justify-between">
																	<span class="text-slate-600">วันที่ชำระ:</span>
																	<span class="font-medium text-slate-900">{paymentResult.date}</span>
																</div>
																<div class="flex justify-between">
																	<span class="text-slate-600">รายการ:</span>
																	<span class="font-medium text-slate-900">{paymentResult.service}</span>
																</div>
																<div class="flex justify-between">
																	<span class="text-slate-600">เลขที่ใบเสร็จ:</span>
																	<span class="font-medium text-slate-900">{paymentResult.receiptNumber}</span>
																</div>
															</div>
														</div>
													{/if}
												</Card>
											</div>
											
											<!-- Payment instructions -->
											<div>
												<h3 class="text-xl font-bold text-slate-900 mb-4">วิธีการชำระเงิน</h3>
												<Card class="p-6 border border-slate-200">
													<Accordion type="single" collapsible>
														<AccordionItem value="transfer">
															<AccordionTrigger class="text-lg font-medium py-3">
																<div class="flex items-center">
																	<CreditCardIcon class="mr-3 h-5 w-5 text-blue-600" />
																	โอนเงินผ่านบัญชีธนาคาร
																</div>
															</AccordionTrigger>
															<AccordionContent>
																<div class="space-y-4 py-2">
																	<div class="rounded-lg bg-slate-50 p-4">
																		<p class="font-medium text-slate-900 mb-2">บัญชีธนาคารกรุงไทย สาขาลาดกระบัง</p>
																		<p class="text-slate-700">ชื่อบัญชี: สถาบันเทคโนโลยีพระจอมเกล้าเจ้าคุณทหารลาดกระบัง</p>
																		<p class="text-slate-700">เลขที่บัญชี: 693-0-12345-6</p>
																	</div>
																	<div class="text-slate-600 text-sm">
																		<p class="mb-2">หลังจากชำระเงินเรียบร้อยแล้ว กรุณาส่งหลักฐานการชำระเงินพร้อมระบุชื่อผู้ใช้บริการและรหัสการทดสอบมาที่อีเมล: payment@scienceinstrument.kmitl.ac.th</p>
																	</div>
																</div>
															</AccordionContent>
														</AccordionItem>
														
														<AccordionItem value="counter">
															<AccordionTrigger class="text-lg font-medium py-3">
																<div class="flex items-center">
																	<CalendarIcon class="mr-3 h-5 w-5 text-blue-600" />
																	ชำระเงินที่เคาน์เตอร์
																</div>
															</AccordionTrigger>
															<AccordionContent>
																<div class="space-y-4 py-2">
																	<div class="text-slate-600">
																		<p class="mb-2">ท่านสามารถชำระเงินได้ที่เคาน์เตอร์การเงิน ศูนย์เครื่องมือวิทยาศาสตร์ ชั้น 1 อาคารคณะวิทยาศาสตร์</p>
																		<p class="mb-2"><span class="font-medium">เวลาทำการ:</span> จันทร์-ศุกร์ 8:30-15:30 น. (พักเที่ยง 12:00-13:00 น.)</p>
																		<p>ยกเว้นวันหยุดนักขัตฤกษ์และวันหยุดตามประกาศของสถาบัน</p>
																	</div>
																</div>
															</AccordionContent>
														</AccordionItem>
														
														<AccordionItem value="invoice">
															<AccordionTrigger class="text-lg font-medium py-3">
																<div class="flex items-center">
																	<FileText class="mr-3 h-5 w-5 text-blue-600" />
																	ชำระเงินตามใบแจ้งหนี้
																</div>
															</AccordionTrigger>
															<AccordionContent>
																<div class="space-y-4 py-2">
																	<div class="text-slate-600">
																		<p class="mb-2">สำหรับหน่วยงานราชการหรือบริษัทที่ต้องการชำระเงินตามใบแจ้งหนี้ สามารถแจ้งความประสงค์ได้ที่เจ้าหน้าที่</p>
																		<p>โดยจะได้รับใบแจ้งหนี้ภายใน 3 วันทำการหลังจากส่งตัวอย่างและเอกสารครบถ
																			<p>โดยจะได้รับใบแจ้งหนี้ภายใน 3 วันทำการหลังจากส่งตัวอย่างและเอกสารครบถ้วน</p>
																		</div>
																	</div>
																</AccordionContent>
															</AccordionItem>
														</Accordion>
														
														<div class="mt-6 bg-amber-50 p-4 rounded-lg border border-amber-200">
															<div class="flex">
																<div class="flex-shrink-0">
																	<AlertCircle class="h-5 w-5 text-amber-600" />
																</div>
																<div class="ml-3">
																	<h4 class="text-sm font-medium text-amber-800">หมายเหตุ</h4>
																	<div class="mt-2 text-sm text-amber-700">
																		<p>กรุณาชำระเงินภายใน 7 วันหลังจากได้รับการยืนยันค่าบริการ หากพ้นกำหนดอาจมีการยกเลิกคำขอใช้บริการ</p>
																	</div>
																</div>
															</div>
														</div>
													</Card>
												</div>
											</div>
										</div>
									</div>
								</Card>
							</TabsContent>
							
							<!-- 1.5. ตรวจสอบสถานะ -->
							<TabsContent value="status" class="mt-0">
								<Card class="overflow-hidden border-none shadow-xl rounded-xl">
									<div class="relative overflow-hidden">
										<div class="absolute -right-32 -top-32 h-64 w-64 rounded-full bg-blue-100 opacity-50"></div>
										<div class="absolute -left-32 -bottom-32 h-64 w-64 rounded-full bg-indigo-100 opacity-50"></div>
										
										<div class="relative p-8 md:p-10">
											<div class="flex items-center mb-8">
												<div class="h-12 w-12 bg-blue-100 rounded-full flex items-center justify-center mr-4">
													<Search class="h-6 w-6 text-blue-600" />
												</div>
												<div>
													<h2 class="text-3xl font-bold text-slate-900 mb-1">ตรวจสอบสถานะตัวอย่าง</h2>
													<p class="text-slate-600">ติดตามสถานะการทดสอบของตัวอย่างที่ส่งวิเคราะห์</p>
												</div>
											</div>
											
											<div class="bg-gradient-to-r from-blue-50 to-indigo-50 p-6 rounded-xl mb-10">
												<div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
													<div>
														<h3 class="text-xl font-bold text-slate-900 mb-4">ค้นหาสถานะตัวอย่าง</h3>
														<div class="bg-white p-6 rounded-lg shadow-md">
															<div class="space-y-4">
																<div>
																	<label for="trackingId" class="text-sm font-medium text-slate-700 mb-1 block">
																		รหัสติดตามตัวอย่าง
																	</label>
																	<Input 
																		id="trackingId" 
																		bind:value={trackingId} 
																		placeholder="ระบุรหัสติดตามตัวอย่าง"
																		class="border-slate-300"
																	/>
																	<p class="mt-1 text-xs text-slate-500">รหัสติดตาม 10 หลักที่ได้รับหลังจากส่งตัวอย่าง</p>
																</div>
																<Button 
																	class="w-full bg-blue-600 hover:bg-blue-700" 
																	on:click={searchSampleStatus}
																>
																	ค้นหาสถานะ
																</Button>
															</div>
														</div>
														
														{#if !searchResult}
															<div class="mt-6 p-4 bg-blue-50 rounded-lg text-blue-700 text-center">
																<p>กรุณาระบุรหัสติดตามเพื่อตรวจสอบสถานะตัวอย่าง</p>
															</div>
														{/if}
													</div>
													
													{#if searchResult}
														<div>
															<h3 class="text-xl font-bold text-slate-900 mb-4">ผลการค้นหา</h3>
															<div class="bg-white p-6 rounded-lg shadow-md">
																<div class="mb-4">
																	<Badge class="bg-blue-600">{searchResult.status}</Badge>
																	<div class="mt-2 flex justify-between">
																		<span class="text-slate-600">รหัสตัวอย่าง:</span>
																		<span class="font-medium text-slate-900">{searchResult.id}</span>
																	</div>
																</div>
																
																<div class="mb-6">
																	<div class="mb-2 flex justify-between text-sm">
																		<span class="text-slate-600">ความคืบหน้า:</span>
																		<span class="font-medium text-blue-600">{searchResult.progress}%</span>
																	</div>
																	<div class="h-2 w-full bg-slate-200 rounded-full overflow-hidden">
																		<div class="h-full bg-blue-600 rounded-full" style="width: {searchResult.progress}%"></div>
																	</div>
																</div>
																
																<div class="space-y-2 text-sm mb-6">
																	<div class="flex justify-between">
																		<span class="text-slate-600">ประเภทบริการ:</span>
																		<span class="font-medium text-slate-900">{searchResult.serviceType}</span>
																	</div>
																	<div class="flex justify-between">
																		<span class="text-slate-600">หน่วยงานรับผิดชอบ:</span>
																		<span class="font-medium text-slate-900">{searchResult.department}</span>
																	</div>
																	<div class="flex justify-between">
																		<span class="text-slate-600">วันที่รับตัวอย่าง:</span>
																		<span class="font-medium text-slate-900">{searchResult.receivedDate}</span>
																	</div>
																	<div class="flex justify-between">
																		<span class="text-slate-600">คาดว่าจะแล้วเสร็จ:</span>
																		<span class="font-medium text-slate-900">{searchResult.estimatedCompletion}</span>
																	</div>
																</div>
																
																<div class="p-4 bg-blue-50 rounded-lg">
																	<h4 class="font-medium text-blue-800 mb-2">ผู้ประสานงาน</h4>
																	<div class="space-y-1 text-sm">
																		<div class="flex items-center">
																			<UserCircle class="h-4 w-4 text-blue-600 mr-2" />
																			<span class="text-blue-800">{searchResult.contactPerson}</span>
																		</div>
																		<div class="flex items-center">
																			<Mail class="h-4 w-4 text-blue-600 mr-2" />
																			<span class="text-blue-800">{searchResult.contactEmail}</span>
																		</div>
																	</div>
																</div>
															</div>
														</div>
													{/if}
												</div>
											</div>
											
											<div class="bg-white p-6 rounded-xl border border-slate-200 shadow-md">
												<h3 class="text-xl font-bold text-slate-900 mb-4">สถานะการทดสอบและความหมาย</h3>
												<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
													<div class="p-4 rounded-lg bg-yellow-50 border border-yellow-200">
														<div class="flex items-center mb-2">
															<div class="h-8 w-8 bg-yellow-100 rounded-full flex items-center justify-center mr-3">
																<Clock class="h-4 w-4 text-yellow-600" />
															</div>
															<h4 class="font-bold text-yellow-800">รอดำเนินการ</h4>
														</div>
														<p class="text-sm text-yellow-700">ตัวอย่างได้รับการลงทะเบียนแล้ว แต่ยังอยู่ในคิวรอการทดสอบ</p>
													</div>
													
													<div class="p-4 rounded-lg bg-blue-50 border border-blue-200">
														<div class="flex items-center mb-2">
															<div class="h-8 w-8 bg-blue-100 rounded-full flex items-center justify-center mr-3">
																<Beaker class="h-4 w-4 text-blue-600" />
															</div>
															<h4 class="font-bold text-blue-800">อยู่ระหว่างการทดสอบ</h4>
														</div>
														<p class="text-sm text-blue-700">เจ้าหน้าที่กำลังดำเนินการทดสอบตัวอย่างของท่าน</p>
													</div>
													
													<div class="p-4 rounded-lg bg-green-50 border border-green-200">
														<div class="flex items-center mb-2">
															<div class="h-8 w-8 bg-green-100 rounded-full flex items-center justify-center mr-3">
																<CheckCircle class="h-4 w-4 text-green-600" />
															</div>
															<h4 class="font-bold text-green-800">เสร็จสมบูรณ์</h4>
														</div>
														<p class="text-sm text-green-700">การทดสอบเสร็จสมบูรณ์ และผลการทดสอบพร้อมให้รับแล้ว</p>
													</div>
													
													<div class="p-4 rounded-lg bg-purple-50 border border-purple-200">
														<div class="flex items-center mb-2">
															<div class="h-8 w-8 bg-purple-100 rounded-full flex items-center justify-center mr-3">
																<FileText class="h-4 w-4 text-purple-600" />
															</div>
															<h4 class="font-bold text-purple-800">รายงานผลแล้ว</h4>
														</div>
														<p class="text-sm text-purple-700">รายงานผลการทดสอบได้ส่งให้แก่ผู้ขอใช้บริการแล้ว</p>
													</div>
													
													<div class="p-4 rounded-lg bg-amber-50 border border-amber-200">
														<div class="flex items-center mb-2">
															<div class="h-8 w-8 bg-amber-100 rounded-full flex items-center justify-center mr-3">
																<AlertCircle class="h-4 w-4 text-amber-600" />
															</div>
															<h4 class="font-bold text-amber-800">รอข้อมูลเพิ่มเติม</h4>
														</div>
														<p class="text-sm text-amber-700">ต้องการข้อมูลหรือตัวอย่างเพิ่มเติมจากผู้ขอใช้บริการ</p>
													</div>
													
													<div class="p-4 rounded-lg bg-red-50 border border-red-200">
														<div class="flex items-center mb-2">
															<div class="h-8 w-8 bg-red-100 rounded-full flex items-center justify-center mr-3">
																<CircleSlash class="h-4 w-4 text-red-600" />
															</div>
															<h4 class="font-bold text-red-800">ยกเลิก</h4>
														</div>
														<p class="text-sm text-red-700">การทดสอบถูกยกเลิกตามคำขอหรือไม่สามารถดำเนินการได้</p>
													</div>
												</div>
											</div>
										</div>
									</div>
								</Card>
							</TabsContent>
							
							<!-- 1.6. รายการเครื่องเสีย -->
							<TabsContent value="equipment" class="mt-0">
								<Card class="overflow-hidden border-none shadow-xl rounded-xl">
									<div class="relative overflow-hidden">
										<div class="absolute -right-32 -top-32 h-64 w-64 rounded-full bg-blue-100 opacity-50"></div>
										<div class="absolute -left-32 -bottom-32 h-64 w-64 rounded-full bg-indigo-100 opacity-50"></div>
										
										<div class="relative p-8 md:p-10">
											<div class="flex items-center mb-8">
												<div class="h-12 w-12 bg-red-100 rounded-full flex items-center justify-center mr-4">
													<AlertCircle class="h-6 w-6 text-red-600" />
												</div>
												<div>
													<h2 class="text-3xl font-bold text-slate-900 mb-1">รายการเครื่องมือที่อยู่ระหว่างซ่อมบำรุง</h2>
													<p class="text-slate-600">รายการเครื่องมือวิทยาศาสตร์ที่ไม่สามารถให้บริการได้ชั่วคราว</p>
												</div>
											</div>
											
											<div class="mb-10 overflow-hidden rounded-xl border border-red-200 bg-white shadow-md">
												<div class="bg-gradient-to-r from-red-600 to-red-700 p-4 text-white">
													<div class="flex items-center space-x-2">
														<AlertCircle class="h-5 w-5" />
														<h3 class="text-lg font-bold">รายการเครื่องที่ไม่สามารถให้บริการได้ชั่วคราว</h3>
													</div>
													<p class="mt-1 text-sm opacity-90">ข้อมูล ณ วันที่ 10 มีนาคม 2568</p>
												</div>
												
												<div class="divide-y divide-gray-200">
													{#each faultyEquipment as equipment, i}
														<div class="p-5 hover:bg-red-50 transition-colors">
															<div class="flex items-start">
																<div class="flex-shrink-0 pt-1">
																	<div class="bg-red-100 rounded-full h-7 w-7 flex items-center justify-center">
																		<span class="text-red-700 font-bold">{i + 1}</span>
																	</div>
																</div>
																<div class="ml-4 flex-1">
																	<div class="flex flex-col md:flex-row md:items-center md:justify-between">
																		<div>
																			<h4 class="text-lg font-medium text-slate-900">{equipment.name}</h4>
																			<p class="text-sm text-slate-600 mt-1">
																				{equipment.department}
																			</p>
																		</div>
																		<div class="mt-2 md:mt-0">
																			<Badge class="bg-amber-100 text-amber-800 hover:bg-amber-200">
																				{equipment.status}
																			</Badge>
																		</div>
																	</div>
																	<div class="mt-3 flex items-center text-sm text-slate-500">
																		<Calendar class="mr-2 h-4 w-4" />
																		<span>คาดว่าจะซ่อมเสร็จ: {equipment.estimatedRepair}</span>
																	</div>
																</div>
															</div>
														</div>
													{/each}
												</div>
											</div>
											
											<div class="bg-blue-50 p-6 rounded-xl border border-blue-200">
												<div class="flex mb-4">
													<div class="h-10 w-10 bg-blue-100 rounded-full flex items-center justify-center mr-4">
														<BellRing class="h-5 w-5 text-blue-600" />
													</div>
													<h3 class="text-xl font-bold text-blue-800">บริการแจ้งเตือน</h3>
												</div>
												
												<p class="text-blue-700 mb-4">ท่านสามารถลงทะเบียนรับการแจ้งเตือนเมื่อเครื่องมือที่ท่านต้องการใช้บริการกลับมาใช้งานได้ตามปกติ</p>
												
												<div class="mt-4 grid grid-cols-1 md:grid-cols-2 gap-4">
													<div>
														<Input 
															placeholder="อีเมลของท่าน" 
															class="border-blue-300 bg-white placeholder:text-slate-400"
														/>
													</div>
													<Button class="bg-blue-600 hover:bg-blue-700">
														<BellRing class="mr-2 h-4 w-4" />
														ลงทะเบียนรับการแจ้งเตือน
													</Button>
												</div>
											</div>
										</div>
									</div>
								</Card>
							</TabsContent>
						</Tabs>
					</div>
				</div>
			</section>
			
			<!-- Call to action section -->
			
		</main>
		
		<!-- Footer -->
		<Footer />
		</div>	