<script lang="ts">
    import { onMount } from 'svelte';
    import { Button } from "$lib/components/ui/button";
    import { Input } from "$lib/components/ui/input";
    import { Card } from "$lib/components/ui/card";
    import { Separator } from "$lib/components/ui/separator";
    import { Tabs, TabsContent, TabsList, TabsTrigger } from "$lib/components/ui/tabs";
    import { Badge } from "$lib/components/ui/badge";
    import { 
        Calendar, 
        Clock, 
        FileText, 
        Download, 
        ExternalLink, 
        Newspaper, 
        Award, 
        Image, 
        Video, 
        Share, 
        Users,
        Calendar as CalendarIcon,
        Mail,
        MapPin,
        Phone
    } from 'lucide-svelte';
    import Header from '$lib/components/Header.svelte';
    import Footer from '$lib/components/Footer.svelte';
    
    // News items
    const newsItems = [
        {
            title: "เปิดให้บริการเครื่อง FTIR รุ่นใหม่",
            date: "1 มีนาคม 2568",
            summary: "ศูนย์เครื่องมือวิทยาศาสตร์เปิดให้บริการเครื่อง Fourier Transform Infrared Spectrometer (FTIR) รุ่นใหม่ล่าสุด ที่มีประสิทธิภาพสูงและแม่นยำ",
            image: "/api/placeholder/400/250",
            tag: "ข่าวสาร",
            url: "/news/1"
        },
        {
            title: "การอบรมการใช้เครื่อง SEM รุ่นใหม่",
            date: "15 มีนาคม 2568",
            summary: "ขอเชิญนักวิจัยและผู้สนใจเข้าร่วมการอบรมเชิงปฏิบัติการการใช้เครื่อง Scanning Electron Microscope รุ่นใหม่ล่าสุด",
            image: "/api/placeholder/400/250",
            tag: "การฝึกอบรม",
            url: "/news/2"
        },
        {
            title: "โครงการความร่วมมือกับมหาวิทยาลัยโอซาก้า",
            date: "20 มีนาคม 2568",
            summary: "ศูนย์เครื่องมือวิทยาศาสตร์ลงนามความร่วมมือกับมหาวิทยาลัยโอซาก้า ประเทศญี่ปุ่น เพื่อแลกเปลี่ยนความรู้และเทคโนโลยีด้านการวิเคราะห์ทดสอบ",
            image: "/api/placeholder/400/250",
            tag: "ความร่วมมือ",
            url: "/news/3"
        },
        {
            title: "ประกาศปิดปรับปรุงห้องปฏิบัติการวิเคราะห์ทางเคมี",
            date: "22 มีนาคม 2568",
            summary: "แจ้งปิดปรับปรุงห้องปฏิบัติการวิเคราะห์ทางเคมี ระหว่างวันที่ 1-5 เมษายน 2568 เพื่อติดตั้งอุปกรณ์ใหม่",
            image: "/api/placeholder/400/250",
            tag: "ประกาศ",
            url: "/news/4"
        },
        {
            title: "โครงการพัฒนานักวิจัยรุ่นใหม่",
            date: "25 มีนาคม 2568",
            summary: "เปิดรับสมัครนักศึกษาและนักวิจัยรุ่นใหม่เข้าร่วมโครงการอบรมเชิงปฏิบัติการการใช้เครื่องมือวิทยาศาสตร์ขั้นสูง",
            image: "/api/placeholder/400/250",
            tag: "โครงการ",
            url: "/news/5"
        },
        {
            title: "งานประชุมวิชาการนานาชาติ ASEAN Scientific Instruments",
            date: "10 เมษายน 2568",
            summary: "ขอเชิญผู้สนใจเข้าร่วมงานประชุมวิชาการนานาชาติ ASEAN Scientific Instruments Conference 2025 ระหว่างวันที่ 15-17 พฤษภาคม 2568",
            image: "/api/placeholder/400/250",
            tag: "การประชุม",
            url: "/news/6"
        }
    ];
    
    // Announcements
    const announcements = [
        {
            title: "ประกาศรับสมัครงานตำแหน่งนักวิทยาศาสตร์",
            date: "5 มีนาคม 2568",
            summary: "ศูนย์เครื่องมือวิทยาศาสตร์เปิดรับสมัครบุคลากรตำแหน่งนักวิทยาศาสตร์ สาขาเคมีวิเคราะห์",
            deadline: "31 มีนาคม 2568"
        },
        {
            title: "ประกาศปรับปรุงอัตราค่าบริการประจำปี 2568",
            date: "10 มีนาคม 2568",
            summary: "แจ้งปรับปรุงอัตราค่าบริการการใช้เครื่องมือและการวิเคราะห์ทดสอบประจำปี 2568 มีผลตั้งแต่วันที่ 1 เมษายน 2568",
            deadline: "มีผลวันที่ 1 เมษายน 2568"
        },
        {
            title: "ประกาศเปลี่ยนแปลงเวลาทำการช่วงเทศกาลสงกรานต์",
            date: "15 มีนาคม 2568",
            summary: "แจ้งเปลี่ยนแปลงเวลาทำการช่วงเทศกาลสงกรานต์ ระหว่างวันที่ 12-15 เมษายน 2568 ศูนย์ฯ จะปิดให้บริการ",
            deadline: "12-15 เมษายน 2568"
        }
    ];
    
    // Publications
    const publications = [
        {
            title: "วารสารเครื่องมือวิทยาศาสตร์ ฉบับที่ 24",
            date: "มีนาคม 2568",
            description: "วารสารรายไตรมาสที่รวบรวมบทความวิชาการและข่าวสารเกี่ยวกับเทคโนโลยีเครื่องมือวิทยาศาสตร์ล่าสุด",
            fileSize: "5.2 MB",
            fileType: "PDF",
            image: "/api/placeholder/200/300"
        },
        {
            title: "รายงานประจำปี 2567",
            date: "กุมภาพันธ์ 2568",
            description: "รายงานผลการดำเนินงานของศูนย์เครื่องมือวิทยาศาสตร์ประจำปี 2567",
            fileSize: "3.8 MB",
            fileType: "PDF",
            image: "/api/placeholder/200/300"
        },
        {
            title: "คู่มือการใช้งานเครื่องมือวิทยาศาสตร์ฉบับปรับปรุง 2568",
            date: "มกราคม 2568",
            description: "คู่มือแนะนำการใช้งานเครื่องมือวิทยาศาสตร์ประเภทต่างๆ ฉบับปรับปรุงล่าสุด",
            fileSize: "4.5 MB",
            fileType: "PDF",
            image: "/api/placeholder/200/300"
        }
    ];
    
    // Events
    const events = [
        {
            title: "งานเปิดตัวเครื่องมือวิทยาศาสตร์ใหม่",
            date: "27 มีนาคม 2568",
            time: "13:00 - 16:00 น.",
            location: "ห้องประชุมใหญ่ ชั้น 5 คณะวิทยาศาสตร์",
            description: "งานเปิดตัวและสาธิตการใช้งานเครื่องมือวิทยาศาสตร์ใหม่ที่ได้รับการสนับสนุนจากกองทุนพัฒนามหาวิทยาลัย"
        },
        {
            title: "สัมมนาวิชาการ Advanced Imaging Techniques",
            date: "10 เมษายน 2568",
            time: "09:00 - 16:00 น.",
            location: "ห้องสัมมนา 2 อาคารเฉลิมพระเกียรติ",
            description: "สัมมนาวิชาการเกี่ยวกับเทคนิคการถ่ายภาพขั้นสูงสำหรับงานวิจัยทางวิทยาศาสตร์ โดยวิทยากรผู้เชี่ยวชาญจากในและต่างประเทศ"
        },
        {
            title: "การอบรมเชิงปฏิบัติการ GC-MS Analysis",
            date: "25-26 เมษายน 2568",
            time: "09:00 - 16:00 น.",
            location: "ห้องปฏิบัติการวิเคราะห์ขั้นสูง ชั้น 3",
            description: "การอบรมเชิงปฏิบัติการเกี่ยวกับการวิเคราะห์ด้วยเครื่อง GC-MS สำหรับนักวิจัยและนักศึกษาบัณฑิตศึกษา"
        }
    ];
    
    // Media gallery items
    const mediaItems = [
        {
            title: "พิธีลงนามความร่วมมือกับภาคอุตสาหกรรม",
            date: "15 กุมภาพันธ์ 2568",
            type: "image",
            url: "/api/placeholder/400/300"
        },
        {
            title: "งานเปิดตัวห้องปฏิบัติการใหม่",
            date: "10 มกราคม 2568",
            type: "image",
            url: "/api/placeholder/400/300"
        },
        {
            title: "การอบรมการใช้เครื่อง HPLC",
            date: "20 ธันวาคม 2567",
            type: "image",
            url: "/api/placeholder/400/300"
        },
        {
            title: "สัมภาษณ์ผู้อำนวยการศูนย์เครื่องมือวิทยาศาสตร์",
            date: "5 มกราคม 2568",
            type: "video",
            url: "/api/placeholder/400/300",
            thumbnail: "/api/placeholder/400/300"
        },
        {
            title: "วิดีโอแนะนำศูนย์เครื่องมือวิทยาศาสตร์",
            date: "15 ธันวาคม 2567",
            type: "video",
            url: "/api/placeholder/400/300",
            thumbnail: "/api/placeholder/400/300"
        },
        {
            title: "การประชุมวิชาการประจำปี 2567",
            date: "10 พฤศจิกายน 2567",
            type: "image",
            url: "/api/placeholder/400/300"
        }
    ];
    
    // State for active tab
    let activeTab = "news";
    
    // Function to format date (just for display in this example)
    function formatDate(dateStr) {
        return dateStr; // In a real app, you might want to format this
    }
</script>

<div class="min-h-screen bg-slate-50 flex flex-col">
    <!-- Header -->
    <Header />
    
    <main>
        <!-- Hero Section -->
        <section class="relative py-16 md:py-24 bg-gradient-to-br from-blue-700 to-indigo-900 text-white">
            <div class="absolute inset-0 overflow-hidden opacity-10">
                <div class="absolute -left-10 -top-10 h-40 w-40 rounded-full bg-white"></div>
                <div class="absolute -right-20 top-40 h-80 w-80 rounded-full bg-indigo-400"></div>
                <div class="absolute -bottom-20 -left-20 h-60 w-60 rounded-full bg-blue-400"></div>
            </div>
            
            <div class="container mx-auto px-4 relative z-10">
                <div class="text-center max-w-3xl mx-auto">
                    <h1 class="text-5xl font-bold mb-6">ประชาสัมพันธ์</h1>
                    <div class="h-1 w-24 bg-amber-500 mx-auto mb-6"></div>
                    <p class="text-xl opacity-90 mb-8">
                        ติดตามข่าวสาร กิจกรรม ประกาศ และสื่อประชาสัมพันธ์ล่าสุดจากศูนย์เครื่องมือวิทยาศาสตร์
                    </p>
                </div>
            </div>
        </section>
        
        <!-- Main Content with Tabs -->
        <section class="py-12 bg-white">
            <div class="container mx-auto px-4">
                <Tabs value={activeTab} onValueChange={(val) => activeTab = val} class="w-full">
                    <TabsList class="w-full justify-start p-0 bg-transparent mb-8 border-b">
                        <TabsTrigger value="news" class="rounded-none px-6 py-3 data-[state=active]:border-b-2 data-[state=active]:border-blue-600">
                            <Newspaper class="w-5 h-5 mr-2" />
                            ข่าวสาร
                        </TabsTrigger>
                        <TabsTrigger value="announcements" class="rounded-none px-6 py-3 data-[state=active]:border-b-2 data-[state=active]:border-blue-600">
                            <FileText class="w-5 h-5 mr-2" />
                            ประกาศ
                        </TabsTrigger>
                        <TabsTrigger value="events" class="rounded-none px-6 py-3 data-[state=active]:border-b-2 data-[state=active]:border-blue-600">
                            <Calendar class="w-5 h-5 mr-2" />
                            กิจกรรม
                        </TabsTrigger>
                        <TabsTrigger value="publications" class="rounded-none px-6 py-3 data-[state=active]:border-b-2 data-[state=active]:border-blue-600">
                            <Award class="w-5 h-5 mr-2" />
                            สิ่งพิมพ์
                        </TabsTrigger>
                        <TabsTrigger value="media" class="rounded-none px-6 py-3 data-[state=active]:border-b-2 data-[state=active]:border-blue-600">
                            <Image class="w-5 h-5 mr-2" />
                            คลังภาพ/วิดีโอ
                        </TabsTrigger>
                    </TabsList>
                    
                    <!-- News Tab -->
                    <TabsContent value="news" class="mt-0">
                        <div class="mb-8">
                            <h2 class="text-3xl font-bold text-slate-900 mb-2">ข่าวสารล่าสุด</h2>
                            <p class="text-slate-600">
                                ติดตามข่าวสารและความเคลื่อนไหวล่าสุดจากศูนย์เครื่องมือวิทยาศาสตร์
                            </p>
                        </div>
                        
                        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                            {#each newsItems as news}
                                <Card class="overflow-hidden border-none shadow-lg transition-all duration-300 hover:shadow-xl h-full flex flex-col">
                                    <img src={news.image} alt={news.title} class="h-48 w-full object-cover" />
                                    <div class="p-6 flex-1 flex flex-col">
                                        <div class="flex items-center justify-between mb-3">
                                            <div class="flex items-center text-blue-600">
                                                <CalendarIcon class="h-4 w-4 mr-2" />
                                                <span class="text-sm">{news.date}</span>
                                            </div>
                                            <Badge class="bg-blue-100 text-blue-800 hover:bg-blue-100">{news.tag}</Badge>
                                        </div>
                                        <h3 class="text-xl font-bold text-slate-900 mb-3">{news.title}</h3>
                                        <p class="text-slate-600 mb-6 flex-1">{news.summary}</p>
                                        <a href={news.url} class="mt-auto text-blue-600 hover:text-blue-800 font-medium inline-flex items-center">
                                            อ่านเพิ่มเติม
                                            <svg class="ml-1 w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                                            </svg>
                                        </a>
                                    </div>
                                </Card>
                            {/each}
                        </div>
                        
                        <div class="mt-12 text-center">
                            <Button variant="outline" class="border-blue-600 px-8 text-blue-600 hover:bg-blue-50">
                                ดูข่าวทั้งหมด
                            </Button>
                        </div>
                    </TabsContent>
                    
                    <!-- Announcements Tab -->
                    <TabsContent value="announcements" class="mt-0">
                        <div class="mb-8">
                            <h2 class="text-3xl font-bold text-slate-900 mb-2">ประกาศ</h2>
                            <p class="text-slate-600">
                                ประกาศสำคัญและข้อมูลที่ต้องทราบเกี่ยวกับการให้บริการของศูนย์เครื่องมือวิทยาศาสตร์
                            </p>
                        </div>
                        
                        <div class="space-y-6 max-w-4xl">
                            {#each announcements as announcement}
                                <Card class="p-6 border-none shadow-md hover:shadow-lg transition-all duration-300">
                                    <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4">
                                        <div>
                                            <div class="flex items-center text-amber-600 mb-2">
                                                <Clock class="h-4 w-4 mr-2" />
                                                <span class="text-sm">ประกาศเมื่อ: {announcement.date}</span>
                                            </div>
                                            <h3 class="text-xl font-bold text-slate-900 mb-2">{announcement.title}</h3>
                                            <p class="text-slate-600">{announcement.summary}</p>
                                        </div>
                                        <div class="md:text-right">
                                            <div class="text-red-600 font-medium flex items-center md:justify-end">
                                                <Clock class="h-4 w-4 mr-2" />
                                                <span>{announcement.deadline}</span>
                                            </div>
                                            <Button variant="outline" class="mt-2 border-blue-600 text-blue-600 hover:bg-blue-50">
                                                รายละเอียด
                                            </Button>
                                        </div>
                                    </div>
                                </Card>
                            {/each}
                        </div>
                        
                        <div class="mt-12 text-center">
                            <Button variant="outline" class="border-blue-600 px-8 text-blue-600 hover:bg-blue-50">
                                ดูประกาศทั้งหมด
                            </Button>
                        </div>
                    </TabsContent>
                    
                    <!-- Events Tab -->
                    <TabsContent value="events" class="mt-0">
                        <div class="mb-8">
                            <h2 class="text-3xl font-bold text-slate-900 mb-2">กิจกรรม</h2>
                            <p class="text-slate-600">
                                กิจกรรมที่กำลังจะเกิดขึ้นและปฏิทินกิจกรรมของศูนย์เครื่องมือวิทยาศาสตร์
                            </p>
                        </div>
                        
                        <div class="space-y-6 max-w-4xl">
                            {#each events as event}
                                <Card class="overflow-hidden border-none shadow-lg transition-all duration-300 hover:shadow-xl">
                                    <div class="flex flex-col md:flex-row">
                                        <div class="bg-blue-600 text-white p-6 md:w-1/4 flex flex-col items-center justify-center text-center">
                                            <Calendar class="h-10 w-10 mb-2" />
                                            <div class="text-2xl font-bold">{event.date.split(' ')[0]}</div>
                                            <div>{event.date.split(' ').slice(1).join(' ')}</div>
                                            <div class="mt-2 text-sm">{event.time}</div>
                                        </div>
                                        <div class="p-6 md:w-3/4">
                                            <h3 class="text-xl font-bold text-slate-900 mb-2">{event.title}</h3>
                                            <div class="flex items-center text-slate-600 mb-4">
                                                <MapPin class="h-4 w-4 mr-2 text-blue-600" />
                                                <span>{event.location}</span>
                                            </div>
                                            <p class="text-slate-600 mb-4">{event.description}</p>
                                            <div class="flex space-x-4">
                                                <Button>ลงทะเบียน</Button>
                                                <Button variant="outline" class="border-blue-600 text-blue-600 hover:bg-blue-50">
                                                    <Calendar class="h-4 w-4 mr-2" />
                                                    เพิ่มในปฏิทิน
                                                </Button>
                                            </div>
                                        </div>
                                    </div>
                                </Card>
                            {/each}
                        </div>
                        
                        <div class="mt-12 text-center">
                            <Button variant="outline" class="border-blue-600 px-8 text-blue-600 hover:bg-blue-50">
                                ดูกิจกรรมทั้งหมด
                            </Button>
                        </div>
                    </TabsContent>
                    
                    <!-- Publications Tab -->
                    <TabsContent value="publications" class="mt-0">
                        <div class="mb-8">
                            <h2 class="text-3xl font-bold text-slate-900 mb-2">สิ่งพิมพ์และเอกสารเผยแพร่</h2>
                            <p class="text-slate-600">
                                วารสาร รายงาน และเอกสารเผยแพร่ต่างๆ ของศูนย์เครื่องมือวิทยาศาสตร์
                            </p>
                        </div>
                        
                        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                            {#each publications as publication}
                                <Card class="overflow-hidden border-none shadow-lg transition-all duration-300 hover:shadow-xl h-full">
                                    <div class="p-6">
                                        <div class="flex flex-col md:flex-row gap-4 mb-4">
                                            <img src={publication.image} alt={publication.title} class="w-full md:w-24 h-auto object-cover rounded-md" />
                                            <div>
                                                <h3 class="text-lg font-bold text-slate-900 mb-1">{publication.title}</h3>
                                                <div class="flex items-center text-blue-600 text-sm">
                                                    <CalendarIcon class="h-4 w-4 mr-1" />
                                                    <span>{publication.date}</span>
                                                </div>
                                            </div>
                                        </div>
                                        
                                        <p class="text-slate-600 mb-4">{publication.description}</p>
                                        
                                        <div class="flex items-center justify-between mb-4">
                                            <span class="text-sm text-slate-500">{publication.fileType}</span>
                                            <span class="text-sm text-slate-500">{publication.fileSize}</span>
                                        </div>
                                        
                                        <Button class="w-full">
                                            <Download class="h-4 w-4 mr-2" />
                                            ดาวน์โหลด
                                        </Button>
                                    </div>
                                </Card>
                            {/each}
                        </div>
                        
                        <div class="mt-12 text-center">
                            <Button variant="outline" class="border-blue-600 px-8 text-blue-600 hover:bg-blue-50">
                                ดูเอกสารทั้งหมด
                            </Button>
                        </div>
                    </TabsContent>
                    
                    <!-- Media Gallery Tab -->
                    <TabsContent value="media" class="mt-0">
                        <div class="mb-8">
                            <h2 class="text-3xl font-bold text-slate-900 mb-2">คลังภาพและวิดีโอ</h2>
                            <p class="text-slate-600">
                                ภาพถ่ายและวิดีโอจากกิจกรรมต่างๆ ของศูนย์เครื่องมือวิทยาศาสตร์
                            </p>
                        </div>
                        
                        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                            {#each mediaItems as item}
                                <Card class="overflow-hidden border-none shadow-lg transition-all duration-300 hover:shadow-xl">
                                    <div class="relative">
                                        <img 
                                            src={item.type === 'video' ? item.thumbnail : item.url} 
                                            alt={item.title} 
                                            class="w-full h-48 object-cover"
                                        />
                                        {#if item.type === 'video'}
                                            <div class="absolute inset-0 flex items-center justify-center">
                                                <div class="h-16 w-16 rounded-full bg-blue-600/80 flex items-center justify-center">
                                                    <Video class="h-8 w-8 text-white" />
                                                </div>
                                            </div>
                                        {/if}
                                        <div class="absolute top-3 right-3">
                                            <Badge class="bg-white/80 text-slate-800">
                                                {item.type === 'image' ? 'รูปภาพ' : 'วิดีโอ'}
                                            </Badge>
                                        </div>
                                    </div>
                                    <div class="p-4">
                                        <h3 class="text-lg font-medium text-slate-900 mb-2">{item.title}</h3>
                                        <div class="flex items-center justify-between">
                                            <div class="flex items-center text-slate-500 text-sm">
                                                <CalendarIcon class="h-3 w-3 mr-1" />
                                                <span>{item.date}</span>
                                            </div>
                                            <Button variant="ghost" size="sm" class="h-8 px-2">
                                                <Share class="h-4 w-4" />
                                            </Button>
                                        </div>
                                    </div>
                                </Card>
                            {/each}
                        </div>
                        
                        <div class="mt-12 text-center">
                            <Button variant="outline" class="border-blue-600 px-8 text-blue-600 hover:bg-blue-50">
                                ดูคลังสื่อทั้งหมด
                            </Button>
                        </div>
                    </TabsContent>
                </Tabs>
            </div>
        </section>
        
        <!-- Newsletter Subscription -->
        <section class="py-16 bg-gradient-to-r from-blue-50 to-indigo-50">
            <div class="container mx-auto px-4">
                <div class="bg-white rounded-xl shadow-xl p-8 max-w-4xl mx-auto">
                    <div class="flex flex-col md:flex-row md:items-center gap-8">
                        <div class="md:w-2/3">
                            <div class="mb-1 inline-block rounded-full bg-blue-100 px-3 py-1 text-xs font-medium text-blue-600">
                                ข่าวสาร
                            </div>
                            <h2 class="text-2xl font-bold text-slate-900 mb-3">ติดตามข่าวสารจากเรา</h2>
                            <p class="text-slate-600 mb-6">
                                ลงทะเบียนเพื่อรับข่าวสาร ประกาศ และกิจกรรมต่างๆ จากศูนย์เครื่องมือวิทยาศาสตร์โดยตรงผ่านทางอีเมล
                            </p>
                            
                            <div class="flex flex-col sm:flex-row gap-3">
                                <Input type="email" placeholder="อีเมลของคุณ" class="h-12" />
                                <Button class="h-12">สมัครรับข่าวสาร</Button>
                            </div>
                        </div>
                        <div class="md:w-1/3 flex justify-center">
                            <div class="h-40 w-40 rounded-full bg-blue-100 flex items-center justify-center">
                                <Mail class="h-20 w-20 text-blue-500" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- Contact Information -->
        <section class="py-16 bg-slate-900 text-white">
            <div class="container mx-auto px-4">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold mb-4">ติดต่อฝ่ายประชาสัมพันธ์</h2>
                    <div class="h-1 w-24 bg-amber-500 mx-auto mb-6"></div>
                    <p class="max-w-2xl mx-auto text-slate-300">
                        มีข้อสงสัยหรือต้องการข้อมูลเพิ่มเติมเกี่ยวกับข่าวสารและการประชาสัมพันธ์ สามารถติดต่อเราได้ตามช่องทางด้านล่าง
                    </p>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-4xl mx-auto">
                    <!-- Email -->
                    <div class="bg-slate-800 rounded-lg p-6 flex flex-col items-center text-center">
                        <div class="bg-blue-500 rounded-full p-3 mb-4">
                            <Mail class="h-6 w-6 text-white" />
                        </div>
                        <h3 class="text-xl font-bold mb-2">อีเมล</h3>
                        <p class="text-slate-300">pr.scientific@kmitl.ac.th</p>
                        <p class="text-slate-400 mt-2 text-sm">ตอบกลับภายใน 24 ชั่วโมงในวันทำการ</p>
                    </div>
                    
                    <!-- Phone -->
                    <div class="bg-slate-800 rounded-lg p-6 flex flex-col items-center text-center">
                        <div class="bg-blue-500 rounded-full p-3 mb-4">
                            <Phone class="h-6 w-6 text-white" />
                        </div>
                        <h3 class="text-xl font-bold mb-2">โทรศัพท์</h3>
                        <p class="text-slate-300">02-329-8000 ต่อ 3456</p>
                        <p class="text-slate-400 mt-2 text-sm">จันทร์-ศุกร์ 8:30-16:30 น.</p>
                    </div>
                    
                    <!-- Social Media -->
                    <div class="bg-slate-800 rounded-lg p-6 flex flex-col items-center text-center">
                        <div class="bg-blue-500 rounded-full p-3 mb-4">
                            <Users class="h-6 w-6 text-white" />
                        </div>
                        <h3 class="text-xl font-bold mb-2">โซเชียลมีเดีย</h3>
                        <div class="flex space-x-4 mt-2">
                            <a href="#" class="text-slate-300 hover:text-white">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                    <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"/>
                                </svg>
                            </a>
                            <a href="#" class="text-slate-300 hover:text-white">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                    <rect width="20" height="16" x="2" y="4" rx="2"/>
                                    <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/>
                                </svg>
                            </a>
                            <a href="#" class="text-slate-300 hover:text-white">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                    <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/>
                                    <rect width="4" height="12" x="2" y="9"/>
                                    <circle cx="4" cy="4" r="2"/>
                                </svg>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>
    
    <!-- Footer -->
    <Footer />
</div>