<script lang="ts">
  import { onMount } from 'svelte';
  import { Button } from "$lib/components/ui/button";
  import { Input } from "$lib/components/ui/input";
  import { Card } from "$lib/components/ui/card";
  import { Separator } from "$lib/components/ui/separator";
  import { Search, Microscope, Dna, TestTube, Omega, Bolt } from 'lucide-svelte';
  
  let searchQuery: string = "";
  
  const categories = [
    { icon: Microscope, name: 'Sample preparation equipment', description: 'PCR, Microscopes, Cell Counters' },
    { icon: Dna, name: 'Biological test', description: 'Centrifuges, Incubators, Balances' },
    { icon: TestTube, name: 'Applied chemical instrument', description: 'Homogenizers, Extractors, Filters' },
    { icon: Bolt, name: 'General equipment', description: 'HPLC, GC, Elemental Analyzers' },
    { icon: Omega, name: 'Physical and structural characterization', description: 'HPLC, GC, Elemental Analyzers' }

  ];
  
  const featuredEquipment = [
    { name: 'Scanning Electron Microscope', model: 'JEOL JSM-7800F', availability: 'Available', image: "/api/placeholder/300/200" },
    { name: 'FTIR Spectrometer', model: 'Bruker Tensor II', availability: 'Maintenance', image: "/api/placeholder/300/200" },
    { name: 'Ultra-High Performance LC', model: 'Agilent 1290 Infinity II', availability: 'Available', image: "/api/placeholder/300/200" }
  ];
</script>

<!-- Main Layout -->
<div class="min-h-screen bg-slate-50 font-sans flex flex-col">
  <!-- Header with modern navigation -->
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
          <a href="/aboutstaff" class="text-slate-700 hover:text-blue-600 font-medium transition-colors">About Us</a>
        </nav>
        
        <!-- Mobile Navigation Button -->
        <Button variant="ghost" size="icon" class="md:hidden">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="4" x2="20" y1="12" y2="12"/><line x1="4" x2="20" y1="6" y2="6"/><line x1="4" x2="20" y1="18" y2="18"/></svg>
        </Button>
      </div>
    </div>
  </header>

  <main>
    <!-- Hero Section with Modern Search -->
    <section class="py-16 bg-gradient-to-br from-blue-50 to-indigo-100">
      <div class="container mx-auto px-4 text-center">
        <h2 class="text-4xl font-bold mb-4 text-slate-900">Scientific Instruments</h2>
        <p class="text-slate-600 mb-8 text-lg max-w-2xl mx-auto">
          Access cutting-edge scientific equipment and expert testing services for your research needs
        </p>
        
        <div class="max-w-md mx-auto">
          <div class="flex w-full items-center space-x-2">
            <Input 
              type="text" 
              bind:value={searchQuery} 
              placeholder="Search for equipment..." 
              class="h-12"
            />
            <Button class="h-12 px-6">
              <Search class="mr-2 h-4 w-4" />
              Search
            </Button>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Equipment Categories with Cards -->
    <section class="py-16 bg-white">
      <div class="container mx-auto px-4">
        <h2 class="text-3xl font-bold mb-2 text-center text-slate-900">Our Equipment Categories</h2>
        <p class="text-slate-600 mb-10 text-center">Browse our comprehensive range of scientific instruments</p>
        
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-6">
          {#each categories as category}
            <Card class="overflow-hidden transition-all hover:shadow-lg hover:scale-105 cursor-pointer">
              <div class="flex flex-col items-center p-6 text-center h-full">
                <div class="h-16 w-16 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 mb-4">
                  <svelte:component this={category.icon} size={28} />
                </div>
                <h3 class="font-bold text-slate-900 mb-2">{category.name}</h3>
                <p class="text-sm text-slate-500">{category.description}</p>
              </div>
            </Card>
          {/each}
        </div>
      </div>
    </section>
    
    <section class="py-16 bg-slate-50">
      <div class="container mx-auto px-4">
        <h2 class="text-3xl font-bold mb-2 text-center text-slate-900">Featured Equipment</h2>
        <p class="text-slate-600 mb-10 text-center">Our most popular and advanced scientific instruments</p>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          {#each featuredEquipment as equipment}
            <Card class="overflow-hidden">
              <img src={equipment.image} alt={equipment.name} class="w-full h-48 object-cover" />
              <div class="p-5">
                <h3 class="font-bold text-lg mb-1">{equipment.name}</h3>
                <p class="text-slate-500 text-sm mb-3">Model: {equipment.model}</p>
                <div class="flex justify-between items-center">
                  <span class={`px-3 py-1 rounded-full text-xs font-medium ${equipment.availability === 'Available' ? 'bg-green-100 text-green-800' : 'bg-amber-100 text-amber-800'}`}>
                    {equipment.availability}
                  </span>
                  <Button variant="outline" size="sm">Details</Button>
                </div>
              </div>
            </Card>
          {/each}
        </div>
      </div>
    </section>
    
    <!-- Services Overview -->
    <section class="py-16 bg-white">
      <div class="container mx-auto px-4">
        <div class="max-w-4xl mx-auto">
          <h2 class="text-3xl font-bold mb-2 text-center text-slate-900">Our Services</h2>
          <p class="text-slate-600 mb-10 text-center">Comprehensive scientific testing and equipment usage services</p>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <Card class="p-6">
              <h3 class="text-xl font-bold mb-4 flex items-center">
                <div class="h-8 w-8 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 mr-3">
                  <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14.5 4h-5L7 7H4a2 2 0 0 0-2 2v9a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2V9a2 2 0 0 0-2-2h-3l-2.5-3z"/><circle cx="12" cy="13" r="3"/></svg>
                </div>
                Equipment Rental
              </h3>
              <ul class="space-y-2 text-slate-600">
                <li class="flex items-center">
                  <svg class="h-5 w-5 text-blue-500 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>
                  Hourly and daily rates available
                </li>
                <li class="flex items-center">
                  <svg class="h-5 w-5 text-blue-500 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>
                  Technical staff assistance included
                </li>
                <li class="flex items-center">
                  <svg class="h-5 w-5 text-blue-500 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>
                  Special rates for academic research
                </li>
              </ul>
            </Card>
            
            <Card class="p-6">
              <h3 class="text-xl font-bold mb-4 flex items-center">
                <div class="h-8 w-8 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 mr-3">
                  <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1-2.5-2.5Z"/><path d="M8 7h6"/><path d="M8 11h8"/><path d="M8 15h5"/></svg>
                </div>
                Testing Services
              </h3>
              <ul class="space-y-2 text-slate-600">
                <li class="flex items-center">
                  <svg class="h-5 w-5 text-blue-500 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>
                  Sample analysis with detailed reports
                </li>
                <li class="flex items-center">
                  <svg class="h-5 w-5 text-blue-500 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>
                  Fast turnaround times available
                </li>
                <li class="flex items-center">
                  <svg class="h-5 w-5 text-blue-500 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>
                  Consultation with scientific experts
                </li>
              </ul>
            </Card>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Contact & Location Section -->
    <section class="py-16 bg-gradient-to-br from-blue-600 to-indigo-700 text-white">
      <div class="container mx-auto px-4">
        <div class="max-w-4xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-12">
          <div>
            <h2 class="text-3xl font-bold mb-6">Contact Us</h2>
            <ul class="space-y-4">
              <li class="flex items-start">
                <svg class="h-6 w-6 mt-1 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/></svg>
                <div>
                  <p class="font-medium">Phone:</p>
                  <p>02-329-8400 ถึง 8411 ต่อ 354, 402</p>
                  <p>092-463-9886 (Mobile)</p>
                </div>
              </li>
              <li class="flex items-start">
                <svg class="h-6 w-6 mt-1 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
                <div>
                  <p class="font-medium">Email:</p>
                  <p>science@kmitl.ac.th</p>
                </div>
              </li>
              <li class="flex items-start">
                <svg class="h-6 w-6 mt-1 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
                <div>
                  <p class="font-medium">Hours:</p>
                  <p>Monday - Friday: 8:30 AM - 4:30 PM</p>
                </div>
              </li>
            </ul>
          </div>
          
          <div>
            <h2 class="text-3xl font-bold mb-6">Location</h2>
            <p class="mb-4">Faculty of Science, King Mongkut's Institute of Technology Ladkrabang</p>
            <p class="mb-4">1 Chalong Krung 1 Alley, Lat Krabang, Bangkok 10520</p>
            
            <div class="mt-6">
              <Button variant="secondary" class="bg-white text-blue-700 hover:bg-blue-50">
                <svg class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/></svg>
                View on Map
              </Button>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>

  <!-- Footer -->
  <footer class="bg-slate-900 text-slate-300 py-10 mt-auto">
    <div class="container mx-auto px-4">
      <div class="grid grid-cols-1 md:grid-cols-4 gap-8 mb-8">
        <div>
          <h3 class="text-white font-bold text-lg mb-4">KMITL Science Instrument Center</h3>
          <p class="text-sm">Providing cutting-edge scientific equipment and services to researchers, academics, and industry professionals since 1982.</p>
        </div>
        
        <div>
          <h3 class="text-white font-bold text-lg mb-4">Quick Links</h3>
          <ul class="space-y-2 text-sm">
            <li><a href="/" class="hover:text-white transition-colors">Home</a></li>
            <li><a href="/instruments" class="hover:text-white transition-colors">Equipment Catalog</a></li>
            <li><a href="/prices" class="hover:text-white transition-colors">Service Rates</a></li>
            <li><a href="/booking" class="hover:text-white transition-colors">Make a Booking</a></li>
          </ul>
        </div>
        
        <div>
          <h3 class="text-white font-bold text-lg mb-4">Resources</h3>
          <ul class="space-y-2 text-sm">
            <li><a href="/manuals" class="hover:text-white transition-colors">Equipment Manuals</a></li>
            <li><a href="/training" class="hover:text-white transition-colors">Training Programs</a></li>
            <li><a href="/research" class="hover:text-white transition-colors">Research Collaborations</a></li>
            <li><a href="/faqs" class="hover:text-white transition-colors">FAQs</a></li>
          </ul>
        </div>
        <!-- wait real website  -->
        <div>
          <h3 class="text-white font-bold text-lg mb-4">Connect us</h3>
          <div class="flex space-x-4 mb-4">
            <a href="#" class="text-slate-300 hover:text-white">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"/></svg>
            </a>

            <a href="#" class="text-slate-300 hover:text-white">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 4S21 3 18 3H6C3 3 2 4 2 4l10 8.5z"/><path d="m22 20-4-6-6 3.5L6 14l-4 6"/><path d="M2 20V4"/><path d="M22 4v16"/></svg>
            </a>

          </div>
      
      <Separator class="mb-6 bg-slate-700" />
      
      <div class="text-center text-sm">
        <p>© 2025 KMITL Scientific Instrument Center. All Rights Reserved</p>
      </div>
    </div>
  </footer>
</div>