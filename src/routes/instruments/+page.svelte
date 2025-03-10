<script lang="ts">
  import { onMount } from 'svelte';
  import { Button } from "$lib/components/ui/button";
  import { Input } from "$lib/components/ui/input";
  import { Card } from "$lib/components/ui/card";
  import { Badge } from "$lib/components/ui/badge";
  import { Separator } from "$lib/components/ui/separator";
  import { Search, Microscope, Dna, TestTube, Omega, Bolt, FilterIcon, X, CalendarDays, Building, GraduationCap, BookOpen, ChevronRight } from 'lucide-svelte';
  import Header from '$lib/components/Header.svelte';
  import Footer from '$lib/components/Footer.svelte';
  
  let searchQuery: string = "";
  let selectedCategory: string | null = null;
  
  const categories = [
    { icon: Microscope, name: 'Physical and structural characterization', description: 'SEM, XRD, FTIR, AFM, and similar surface/structure analysis equipment' },
    { icon: TestTube, name: 'Applied chemical instrument', description: 'HPLC, GC-MS, DSC, TGA, and other chemical analysis equipment' },
    { icon: Dna, name: 'Biological test', description: 'PCR, flow cytometry, microplate readers, cell analysis systems' },
    { icon: Bolt, name: 'Sample preparation equipment', description: 'Centrifuges, homogenizers, extractors, sample concentrators' },
    { icon: Omega, name: 'General equipment', description: 'Balances, pH meters, water purification, basic lab equipment' }
  ];
  
  const instruments = [
    { 
      name: 'Scanning Electron Microscope', 
      model: 'JEOL JSM-7800F', 
      category: 'Physical and structural characterization',
      availability: 'Available', 
      description: 'High-resolution microscope using electron beams to create detailed surface images with magnification up to 300,000x.',
      image: "/api/placeholder/400/240",
      department: "Surface Analysis Laboratory",
      hourlyCost: 1500,
      bookingAvailable: true 
    },
    { 
      name: 'FTIR Spectrometer', 
      model: 'Bruker Tensor II', 
      category: 'Physical and structural characterization',
      availability: 'Maintenance', 
      description: 'Identifies chemical bonds in molecules by analyzing infrared absorption spectrum. Suitable for organic and inorganic compound analysis.',
      image: "/api/placeholder/400/240",
      department: "Spectroscopy Laboratory",
      hourlyCost: 800,
      bookingAvailable: false,
      maintenanceDate: 'March 25, 2025'
    },
    { 
      name: 'Ultra-High Performance LC', 
      model: 'Agilent 1290 Infinity II', 
      category: 'Applied chemical instrument',
      availability: 'Available', 
      description: 'Advanced liquid chromatography system for separating, identifying, and quantifying components in complex mixtures.',
      image: "/api/placeholder/400/240",
      department: "Chromatography Laboratory",
      hourlyCost: 1200,
      bookingAvailable: true 
    },
    { 
      name: 'PCR Thermal Cycler', 
      model: 'Bio-Rad T100', 
      category: 'Sample preparation equipment',
      availability: 'Available', 
      description: 'Amplifies DNA segments through repeated heating and cooling cycles for genetic analysis.',
      image: "/api/placeholder/400/240",
      department: "Molecular Biology Laboratory",
      hourlyCost: 600,
      bookingAvailable: true 
    },
    { 
      name: 'Microplate Reader', 
      model: 'BioTek Synergy HTX', 
      category: 'Biological test',
      availability: 'Available', 
      description: 'Multi-mode detection system for microplate assays including absorbance, fluorescence, and luminescence measurements.',
      image: "/api/placeholder/400/240",
      department: "Cell Biology Laboratory",
      hourlyCost: 750,
      bookingAvailable: true 
    },
    { 
      name: 'Differential Scanning Calorimeter', 
      model: 'TA Instruments DSC 250', 
      category: 'Applied chemical instrument',
      availability: 'Available', 
      description: 'Measures heat flow changes in samples for thermal analysis of phase transitions and chemical reactions.',
      image: "/api/placeholder/400/240",
      department: "Thermal Analysis Laboratory",
      hourlyCost: 900,
      bookingAvailable: true 
    },
    { 
      name: 'Analytical Balance', 
      model: 'Mettler Toledo XPR', 
      category: 'General equipment',
      availability: 'Available', 
      description: 'High-precision weighing instrument with readability to 0.01mg for accurate sample preparation.',
      image: "/api/placeholder/400/240",
      department: "General Laboratory",
      hourlyCost: 300,
      bookingAvailable: true 
    },
    { 
      name: 'X-Ray Diffractometer', 
      model: 'Rigaku MiniFlex 600', 
      category: 'Physical and structural characterization',
      availability: 'Maintenance', 
      description: 'Determines crystal structures by measuring diffraction patterns of X-rays interacting with crystalline samples.',
      image: "/api/placeholder/400/240",
      department: "X-Ray Laboratory",
      hourlyCost: 1400,
      bookingAvailable: false,
      maintenanceDate: 'March 20, 2025'
    },
    { 
      name: 'GC-MS System', 
      model: 'Agilent 7890B/5977B', 
      category: 'Applied chemical instrument',
      availability: 'Available', 
      description: 'Combined gas chromatography-mass spectrometry system for separation and identification of compounds in complex mixtures.',
      image: "/api/placeholder/400/240",
      department: "Mass Spectrometry Laboratory",
      hourlyCost: 1600,
      bookingAvailable: true 
    },
    { 
      name: 'Confocal Microscope', 
      model: 'Leica SP8', 
      category: 'Biological test',
      availability: 'Available', 
      description: 'High-resolution optical imaging technique that uses point illumination and a spatial pinhole to increase optical resolution and contrast.',
      image: "/api/placeholder/400/240",
      department: "Microscopy Laboratory",
      hourlyCost: 1800,
      bookingAvailable: true 
    },
    { 
      name: 'UV-Vis Spectrophotometer', 
      model: 'Shimadzu UV-2600', 
      category: 'Applied chemical instrument',
      availability: 'Available', 
      description: 'Measures the absorption or reflectance in the ultraviolet-visible spectral region for quantitative determination of different analytes.',
      image: "/api/placeholder/400/240",
      department: "Spectroscopy Laboratory",
      hourlyCost: 500,
      bookingAvailable: true 
    },
    { 
      name: 'Freeze Dryer', 
      model: 'Labconco FreeZone 6', 
      category: 'Sample preparation equipment',
      availability: 'Available', 
      description: 'Removes water from samples by freezing the material and then reducing the pressure to allow the frozen water to sublimate.',
      image: "/api/placeholder/400/240",
      department: "Sample Preparation Laboratory",
      hourlyCost: 700,
      bookingAvailable: true 
    }
  ];
  
  // Featured instruments to highlight
  const featuredInstruments = [
    instruments.find(i => i.name === 'Scanning Electron Microscope'),
    instruments.find(i => i.name === 'GC-MS System'),
    instruments.find(i => i.name === 'Confocal Microscope')
  ];
  
  $: filteredInstruments = instruments.filter(instrument => {
    const matchesSearch = searchQuery === "" || 
      instrument.name.toLowerCase().includes(searchQuery.toLowerCase()) ||
      instrument.model.toLowerCase().includes(searchQuery.toLowerCase()) ||
      instrument.description.toLowerCase().includes(searchQuery.toLowerCase()) ||
      instrument.category.toLowerCase().includes(searchQuery.toLowerCase());
    
    const matchesCategory = selectedCategory === null || 
      instrument.category === selectedCategory;
    
    return matchesSearch && matchesCategory;
  });

  function selectCategory(categoryName: string) {
    selectedCategory = selectedCategory === categoryName ? null : categoryName;
  }

  function clearFilters() {
    selectedCategory = null;
    searchQuery = "";
  }
</script>

<!-- Main Layout -->
<div class="flex min-h-screen flex-col bg-slate-50 font-sans">
<!-- Header -->
<Header />

<main>
  <!-- Hero Section -->
  <section class="relative overflow-hidden bg-gradient-to-br from-blue-700 to-indigo-900 py-16 text-white">
    <!-- Decorative elements -->
    <div class="absolute left-0 top-0 h-full w-full overflow-hidden opacity-10">
      <div class="absolute -left-10 -top-10 h-40 w-40 rounded-full bg-white"></div>
      <div class="absolute -right-20 top-40 h-80 w-80 rounded-full bg-indigo-400"></div>
      <div class="absolute -bottom-20 -left-20 h-60 w-60 rounded-full bg-blue-400"></div>
    </div>

    <div class="container relative z-10 mx-auto px-4">
      <div class="flex flex-col md:flex-row items-center justify-between gap-8">
        <div class="md:max-w-xl">
          <h2 class="mb-4 text-4xl font-bold">เครื่องมือวิทยาศาสตร์</h2>
          <h3 class="mb-6 text-2xl font-semibold">
            ศูนย์เครื่องมือวิทยาศาสตร์ คณะวิทยาศาสตร์ สจล.
          </h3>
          <p class="mb-8 text-xl opacity-90">
            บริการเครื่องมือวิทยาศาสตร์ชั้นสูงสำหรับการวิจัย การเรียนการสอน และการบริการวิชาการ พร้อมให้คำปรึกษาโดยผู้เชี่ยวชาญ
          </p>

          <div class="rounded-lg bg-white/10 p-1 backdrop-blur-sm flex">
            <Input
              type="text"
              bind:value={searchQuery}
              placeholder="ค้นหาเครื่องมือ..."
              class="h-14 rounded-md border-0 bg-white/80 text-slate-900 placeholder:text-slate-500 flex-1"
            />
            <Button class="h-14 rounded-md bg-amber-500 text-white hover:bg-amber-600 ml-1 flex items-center" on:click={() => window.scrollTo({ top: document.getElementById('instrument-list')?.offsetTop - 100, behavior: 'smooth' })}>
              <Search class="mr-2 h-5 w-5" />
              ค้นหา
            </Button>
          </div>
        </div>
        
        <div class="hidden md:block relative">
          <img src="/api/placeholder/450/350" alt="Scientific Instrument" class="rounded-lg shadow-lg relative z-10" />
          <div class="absolute -bottom-4 -right-4 -z-0 h-full w-full rounded-lg bg-gradient-to-br from-blue-500 to-indigo-600"></div>
        </div>
      </div>
    </div>
  </section>

  <!-- Featured Instruments -->
  <section class="py-16 bg-white">
    <div class="container mx-auto px-4">
      <div class="mb-12 text-center">
        <span class="mb-2 inline-block rounded-full bg-blue-100 px-4 py-1 text-sm font-medium text-blue-800">
          FEATURED EQUIPMENT
        </span>
        <h2 class="mb-4 text-3xl font-bold text-slate-900">เครื่องมือแนะนำ</h2>
        <div class="mx-auto mb-6 h-1 w-24 bg-blue-600"></div>
        <p class="mx-auto max-w-3xl text-lg text-slate-600">
          เครื่องมือวิทยาศาสตร์ชั้นสูงที่ได้รับความนิยมและมีประสิทธิภาพสูงสำหรับงานวิจัยและการวิเคราะห์ทดสอบ
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        {#each featuredInstruments as instrument}
          <Card class="overflow-hidden border-none shadow-lg transition-all duration-300 hover:shadow-xl flex flex-col h-full group">
            <div class="relative overflow-hidden">
              <img src={instrument?.image} alt={instrument?.name} class="w-full h-60 object-cover transition-transform duration-500 group-hover:scale-105" />
              <div class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent"></div>
              <div class="absolute bottom-0 left-0 right-0 p-5">
                <Badge class={`${instrument?.availability === 'Available' ? 'bg-green-100 text-green-800' : 'bg-amber-100 text-amber-800'} mb-2`}>
                  {instrument?.availability}
                </Badge>
                <h3 class="text-xl font-bold text-white">{instrument?.name}</h3>
                <p class="text-white/80 text-sm">{instrument?.model}</p>
              </div>
            </div>
            
            <div class="p-6 flex flex-col flex-grow">
              <p class="text-slate-600 mb-4 flex-grow">{instrument?.description}</p>
              <div class="space-y-3 mb-4">
                <div class="flex items-center text-sm text-slate-700">
                  <Building class="h-4 w-4 text-blue-600 mr-2" />
                  <span>{instrument?.department}</span>
                </div>
                <div class="flex items-center text-sm text-slate-700">
                  <svg class="h-4 w-4 text-blue-600 mr-2" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="12" cy="12" r="10" />
                    <path d="M12 6v6l4 2" />
                  </svg>
                  <span>{instrument?.hourlyCost} บาท/ชั่วโมง</span>
                </div>
              </div>
              <Button class="w-full">รายละเอียดเพิ่มเติม</Button>
            </div>
          </Card>
        {/each}
      </div>
      
      <div class="text-center mt-10">
        <Button variant="outline" class="border-blue-600 text-blue-600 hover:bg-blue-50" on:click={() => window.scrollTo({ top: document.getElementById('instrument-list')?.offsetTop - 100, behavior: 'smooth' })}>
          ดูเครื่องมือทั้งหมด
          <ChevronRight class="ml-1 h-4 w-4" />
        </Button>
      </div>
    </div>
  </section>

  <!-- Equipment Categories -->
  <section class="py-16 bg-slate-50">
    <div class="container mx-auto px-4">
      <div class="mb-12 text-center">
        <span class="mb-2 inline-block rounded-full bg-blue-100 px-4 py-1 text-sm font-medium text-blue-800">
          CATEGORIES
        </span>
        <h2 class="mb-4 text-3xl font-bold text-slate-900">ประเภทเครื่องมือวิทยาศาสตร์</h2>
        <div class="mx-auto mb-6 h-1 w-24 bg-blue-600"></div>
        <p class="mx-auto max-w-3xl text-lg text-slate-600">
          เครื่องมือวิทยาศาสตร์ของเราแบ่งออกเป็นหมวดหมู่ตามลักษณะการใช้งานและเทคโนโลยี
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-5 gap-6">
        {#each categories as category}
          <Card 
            class={`p-6 border-t-4 ${selectedCategory === category.name ? 'border-blue-600 bg-blue-50' : 'border-slate-200 hover:border-blue-600 hover:bg-blue-50'} cursor-pointer transition-all duration-300 h-full flex flex-col`}
            on:click={() => selectCategory(category.name)}
          >
            <div class="mb-4 flex h-14 w-14 items-center justify-center rounded-full bg-blue-100 text-blue-600">
              <svelte:component this={category.icon} size={24} />
            </div>
            <h3 class="text-lg font-bold text-slate-900 mb-2">{category.name}</h3>
            <p class="text-sm text-slate-600 flex-grow">{category.description}</p>
          </Card>
        {/each}
      </div>
    </div>
  </section>

  <!-- Instruments List -->
  <section id="instrument-list" class="py-16 bg-white">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-8">
        <div>
          <h2 class="text-3xl font-bold text-slate-900 mb-2">รายการเครื่องมือวิทยาศาสตร์</h2>
          <p class="text-slate-600">
            {filteredInstruments.length} 
            {filteredInstruments.length === 1 ? 'instrument' : 'instruments'} found
            {selectedCategory ? `in ${selectedCategory}` : ''}
          </p>
        </div>
        
        <div class="mt-4 md:mt-0 flex flex-wrap gap-2">
          {#if selectedCategory || searchQuery}
            <Button variant="outline" size="sm" on:click={clearFilters} class="flex items-center">
              <X class="mr-2 h-4 w-4" />
              <span>Clear filters</span>
            </Button>
          {/if}
          
          <div class="relative w-64">
            <div class="relative flex w-full items-center">
              <Input 
                type="text" 
                bind:value={searchQuery} 
                placeholder="Search instruments..." 
                class="pr-10"
              />
              <div class="absolute right-3 text-slate-400">
                <Search class="h-5 w-5" />
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="flex flex-col lg:flex-row gap-8">
        <!-- Category Sidebar -->
        <div class="w-full lg:w-64 order-2 lg:order-1">
          <div class="bg-slate-50 rounded-lg p-6 sticky top-24">
            <div class="flex items-center mb-4">
              <FilterIcon class="w-5 h-5 mr-2 text-blue-600" />
              <h3 class="font-bold text-lg">Filter by Category</h3>
            </div>
            
            <Separator class="my-4" />
            
            <div class="space-y-2">
              {#each categories as category}
                <Button 
                  variant={selectedCategory === category.name ? "default" : "ghost"} 
                  class="w-full justify-start text-left h-auto py-3"
                  on:click={() => selectCategory(category.name)}
                >
                  <svelte:component this={category.icon} class="mr-3 h-4 w-4 flex-shrink-0" />
                  <div class="truncate">{category.name}</div>
                </Button>
              {/each}
            </div>
            
            <Separator class="my-4" />
            
            <div class="bg-blue-50 rounded-lg p-4 border border-blue-100">
              <h4 class="font-medium text-blue-800 mb-2 flex items-center">
                <GraduationCap class="h-4 w-4 mr-2" />
                <span>Need Training?</span>
              </h4>
              <p class="text-blue-700 text-sm mb-3">
                Our expert staff provides comprehensive training on all equipment. Schedule a session before your first use.
              </p>
              <Button variant="outline" size="sm" class="w-full border-blue-300 text-blue-700 hover:bg-blue-100">
                Request Training
              </Button>
            </div>
          </div>
        </div>
        
        <!-- Instruments Grid -->
        <div class="flex-1 order-1 lg:order-2">
          {#if filteredInstruments.length === 0}
            <div class="text-center py-16 bg-slate-50 rounded-lg">
              <div class="text-5xl mb-4">🔍</div>
              <h3 class="text-xl font-bold mb-2">No instruments found</h3>
              <p class="text-slate-500 mb-4">Try adjusting your search or filter criteria</p>
              <Button variant="outline" on:click={clearFilters}>Clear all filters</Button>
            </div>
          {:else}
            <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
              {#each filteredInstruments as instrument}
                <Card class="overflow-hidden h-full flex flex-col hover:shadow-xl transition-all duration-300 border-none">
                  <div class="relative">
                    <img src={instrument.image} alt={instrument.name} class="w-full h-48 object-cover" />
                    <div class="absolute top-0 left-0 right-0 p-4 flex justify-between items-start">
                      <Badge class="bg-blue-100 text-blue-800">{instrument.category}</Badge>
                      <Badge class={`${instrument.availability === 'Available' ? 'bg-green-100 text-green-800' : 'bg-amber-100 text-amber-800'}`}>
                        {instrument.availability}
                      </Badge>
                    </div>
                  </div>
                  <div class="p-5 flex-1 flex flex-col">
                    <div class="mb-3">
                      <h3 class="font-bold text-lg text-slate-900">{instrument.name}</h3>
                      <p class="text-slate-500 text-sm">Model: {instrument.model}</p>
                    </div>
                    <p class="text-slate-600 text-sm mb-4 flex-1">{instrument.description}</p>
                    
                    <div class="space-y-2 mb-4">
                      <div class="flex items-center justify-between text-sm">
                        <div class="flex items-center text-slate-600">
                          <Building class="h-4 w-4 mr-2 text-blue-600" />
                          <span>{instrument.department}</span>
                        </div>
                        <span class="font-medium text-slate-700">{instrument.hourlyCost} บาท/ชม.</span>
                      </div>
                      
                      {#if instrument.availability === 'Maintenance'}
                        <div class="flex items-center text-sm text-amber-700">
                          <CalendarDays class="h-4 w-4 mr-2" />
                          <span>Available after: {instrument.maintenanceDate}</span>
                        </div>
                      {/if}
                    </div>
                    
                    <div class="mt-auto">
                      <Button class="w-full" disabled={!instrument.bookingAvailable}>
                        {instrument.bookingAvailable ? 'จองใช้เครื่องมือ' : 'ไม่สามารถจองได้'}
                      </Button>
                    </div>
                  </div>
                </Card>
              {/each}
            </div>
          {/if}
        </div>
      </div>
    </div>
  </section>

  <!-- Service and Training Section -->
  <section class="py-16 bg-gradient-to-br from-slate-50 to-blue-50">
    <div class="container mx-auto px-4">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
        <div>
          <span class="mb-2 inline-block rounded-full bg-blue-100 px-4 py-1 text-sm font-medium text-blue-800">
            TRAINING
          </span>
          <h2 class="text-3xl font-bold text-slate-900 mb-4">การอบรมการใช้เครื่อง</h2>
          <div class="h-1 w-24 bg-blue-600 mb-6"></div>
          
          <p class="text-slate-700 mb-6">
            ศูนย์เครื่องมือวิทยาศาสตร์จัดอบรมการใช้เครื่องมือโดยผู้เชี่ยวชาญ เพื่อให้ผู้ใช้บริการสามารถใช้เครื่องมือได้อย่างถูกต้องและมีประสิทธิภาพ
          </p>
          
          <div class="bg-white rounded-lg p-6 shadow-md">
            <h3 class="text-lg font-bold text-slate-900 mb-4 flex items-center">
              <BookOpen class="h-5 w-5 mr-2 text-blue-600" />
              <span>รายการอบรมที่กำลังจะมาถึง</span>
            </h3>
            
            <div class="space-y-4">
              <div class="border-l-4 border-blue-600 pl-4 py-1">
                <h4 class="font-medium text-slate-900">การใช้งานเครื่อง SEM เบื้องต้น</h4>
                <p class="text-slate-500 text-sm">20 มีนาคม 2568 | 9:00 - 16:00 น. | ห้องอบรม SC1-205</p>
              </div>
              
              <div class="border-l-4 border-blue-600 pl-4 py-1">
                <h4 class="font-medium text-slate-900">การวิเคราะห์ด้วยเครื่อง HPLC</h4>
                <p class="text-slate-500 text-sm">25 มีนาคม 2568 | 9:00 - 16:00 น. | ห้องอบรม SC1-207</p>
              </div>
              
              <div class="border-l-4 border-blue-600 pl-4 py-1">
                <h4 class="font-medium text-slate-900">การใช้งานเครื่อง XRD และการวิเคราะห์ข้อมูล</h4>
                <p class="text-slate-500 text-sm">30 มีนาคม 2568 | 9:00 - 16:00 น. | ห้องอบรม SC1-205</p>
              </div>
            </div>
            
            <Button class="w-full mt-6">ดูรายการอบรมทั้งหมด</Button>
          </div>
        </div>
        
        <div>
          <span class="mb-2 inline-block rounded-full bg-blue-100 px-4 py-1 text-sm font-medium text-blue-800">
            SERVICE REQUEST
          </span>
          <h2 class="text-3xl font-bold text-slate-900 mb-4">การขอใช้บริการ</h2>
          <div class="h-1 w-24 bg-blue-600 mb-6"></div>
          
          <p class="text-slate-700 mb-6">
            ให้บริการวิเคราะห์ทดสอบตัวอย่างโดยนักวิทยาศาสตร์ผู้เชี่ยวชาญ พร้อมให้คำปรึกษาและแปลผลการวิเคราะห์อย่างละเอียด
          </p>
          
          <Card class="overflow-hidden">
            <div class="bg-gradient-to-r from-blue-600 to-indigo-700 p-6 text-white">
              <h3 class="text-xl font-bold mb-2">ขั้นตอนการขอใช้บริการ</h3>
              <p class="text-white/90">
                กรุณาปฏิบัติตามขั้นตอนต่อไปนี้เพื่อขอใช้บริการวิเคราะห์ทดสอบ
              </p>
            </div>
            
            <div class="p-6">
              <div class="space-y-6">
                <div class="flex">
                  <div class="flex-shrink-0 mr-4">
                    <div class="flex h-10 w-10 items-center justify-center rounded-full bg-blue-100 text-blue-600 text-lg font-bold">
                      1
                    </div>
                  </div>
                  <div>
                    <h4 class="text-lg font-medium text-slate-900 mb-1">ลงทะเบียนผู้ใช้บริการ</h4>
                    <p class="text-slate-600 text-sm">
                      ลงทะเบียนเป็นสมาชิกศูนย์เครื่องมือวิทยาศาสตร์ผ่านระบบออนไลน์หรือติดต่อเจ้าหน้าที่
                    </p>
                  </div>
                </div>
                
                <div class="flex">
                  <div class="flex-shrink-0 mr-4">
                    <div class="flex h-10 w-10 items-center justify-center rounded-full bg-blue-100 text-blue-600 text-lg font-bold">
                      2
                    </div>
                  </div>
                  <div>
                    <h4 class="text-lg font-medium text-slate-900 mb-1">กรอกแบบฟอร์มส่งตัวอย่าง</h4>
                    <p class="text-slate-600 text-sm">
                      กรอกรายละเอียดตัวอย่างและการทดสอบที่ต้องการในแบบฟอร์มให้ครบถ้วน
                    </p>
                  </div>
                </div>
                
                <div class="flex">
                  <div class="flex-shrink-0 mr-4">
                    <div class="flex h-10 w-10 items-center justify-center rounded-full bg-blue-100 text-blue-600 text-lg font-bold">
                      3
                    </div>
                  </div>
                  <div>
                    <h4 class="text-lg font-medium text-slate-900 mb-1">ชำระค่าบริการ</h4>
                    <p class="text-slate-600 text-sm">
                      ชำระค่าบริการตามอัตราที่กำหนดผ่านช่องทางที่ศูนย์ฯ จัดเตรียมไว้
                    </p>
                  </div>
                </div>
                
                <div class="flex">
                  <div class="flex-shrink-0 mr-4">
                    <div class="flex h-10 w-10 items-center justify-center rounded-full bg-blue-100 text-blue-600 text-lg font-bold">
                      4
                    </div>
                  </div>
                  <div>
                    <h4 class="text-lg font-medium text-slate-900 mb-1">รับผลการวิเคราะห์</h4>
                    <p class="text-slate-600 text-sm">
                      รับผลการวิเคราะห์ทางอีเมลหรือมารับที่ศูนย์ฯ ตามระยะเวลาที่กำหนด
                    </p>
                  </div>
                </div>
              </div>
              
              <div class="mt-6 flex space-x-4">
                <Button class="flex-1">ดาวน์โหลดแบบฟอร์ม</Button>
                <Button variant="outline" class="flex-1 border-blue-600 text-blue-600 hover:bg-blue-50">ขอคำปรึกษา</Button>
              </div>
            </div>
          </Card>
        </div>
      </div>
    </div>
  </section>

  <!-- Call to Action -->
  <section class="py-16 bg-white">
    <div class="container mx-auto px-4">
      <div class="bg-gradient-to-r from-blue-600 to-indigo-700 rounded-2xl overflow-hidden shadow-xl">
        <div class="p-8 md:p-12 flex flex-col md:flex-row items-center justify-between gap-8">
          <div class="text-white max-w-2xl">
            <h2 class="text-3xl font-bold mb-4">ต้องการข้อมูลเพิ่มเติม?</h2>
            <p class="text-white/90 text-lg mb-6">
              ติดต่อเจ้าหน้าที่ศูนย์เครื่องมือวิทยาศาสตร์ คณะวิทยาศาสตร์ สจล. เพื่อสอบถามข้อมูลเพิ่มเติมเกี่ยวกับเครื่องมือและบริการของเรา
            </p>
            <div class="flex flex-wrap gap-4">
              <Button class="bg-white text-blue-600 hover:bg-blue-50">ติดต่อเรา</Button>
              <Button variant="outline" class="text-white border-white hover:bg-blue-700/30">ดูอัตราค่าบริการ</Button>
            </div>
          </div>
          
          <div class="flex-shrink-0 w-72 hidden md:block">
            <img src="/api/placeholder/300/200" alt="Scientific Research" class="w-full h-auto rounded-lg shadow-lg" />
          </div>
        </div>
      </div>
    </div>
  </section>
</main>

<!-- Footer -->
<Footer />
</div>