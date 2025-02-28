<script lang="ts">
    import { onMount } from 'svelte';
    import { Button } from "$lib/components/ui/button";
    import { Card } from "$lib/components/ui/card";
    import { Tabs, TabsContent, TabsList, TabsTrigger } from "$lib/components/ui/tabs";
    import { Badge } from "$lib/components/ui/badge";
    import { Separator } from "$lib/components/ui/separator";
    import { Calendar, Clock, FileText, Info, ChevronLeft, Heart, Share2, Building, Users, BarChart4 } from 'lucide-svelte';
    
    let activeTab = "details";
    
    const relatedInstruments = [
      { name: "HPLC System", category: "Chromatography", image: "/api/placeholder/100/100" },
      { name: "Mass Spectrometer", category: "Spectroscopy", image: "/api/placeholder/100/100" },
      { name: "Thermal Analyzer", category: "Thermal Analysis", image: "/api/placeholder/100/100" }
    ];
    
    const upcomingMaintenance = [
      { date: "March 15, 2025", duration: "2 days" }
    ];
    
    let isFavorite = false;
    const toggleFavorite = () => {
      isFavorite = !isFavorite;
    };
  </script>
  
  <div class="min-h-screen bg-slate-50 flex flex-col">
    <!-- Header -->
    <header class="bg-white border-b sticky top-0 z-10">
      <div class="container mx-auto px-4 py-3">
        <div class="flex justify-between items-center">
          <!-- Logo wait ploy-->
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
  
    <!-- Main Content -->
    <main class="container mx-auto px-4 py-8 flex-grow">
      <!-- Back Link -->
      <a href="/instruments" class="inline-flex items-center text-blue-600 hover:text-blue-800 mb-6">
        <ChevronLeft class="h-4 w-4 mr-1" />
        Back to Instruments
      </a>
      
      <!-- Instrument Details Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <!-- Main Content Area -->
        <div class="lg:col-span-2">
          <Card class="overflow-hidden shadow-lg">
            <!-- Header with status badge -->
            <div class="p-6 pb-0">
              <div class="flex flex-wrap justify-between items-start mb-2">
                <h1 class="text-3xl font-bold text-slate-900">GC-MS (Gas Chromatograph-Mass Spectrometer)</h1>
                <Badge class="bg-green-100 text-green-800 hover:bg-green-100">Available</Badge>
              </div>
              <p class="text-slate-500 mb-4">Agilent 7890B GC and 5977B MS</p>
            </div>
            
            <!-- Instrument Image -->
            <div class="px-6">
              <div class="rounded-lg overflow-hidden bg-slate-100 mb-6">
                <img src="/api/placeholder/800/400" alt="GC-MS Instrument" class="w-full h-auto object-cover" />
              </div>
            </div>
            
            <!-- Action Buttons -->
            <div class="px-6 flex space-x-4 mb-6">
              <Button class="flex-1">Book Instrument</Button>
              <Button variant="outline" class="flex items-center justify-center" on:click={toggleFavorite}>
                <Heart class="h-4 w-4 mr-2" fill={isFavorite ? "currentColor" : "none"} />
                {isFavorite ? 'Saved' : 'Save'}
              </Button>
              <Button variant="outline" class="flex items-center justify-center">
                <Share2 class="h-4 w-4 mr-2" />
                Share
              </Button>
            </div>
            
            <!-- Tabs -->
            <div class="px-6 pb-6">
              <Tabs value={activeTab} onValueChange={(value) => activeTab = value} class="w-full">
                <TabsList class="grid w-full grid-cols-4 mb-6">
                  <TabsTrigger value="details">Details</TabsTrigger>
                  <TabsTrigger value="specifications">Specifications</TabsTrigger>
                  <TabsTrigger value="applications">Applications</TabsTrigger>
                  <TabsTrigger value="documents">Documents</TabsTrigger>
                </TabsList>
                
                <TabsContent value="details" class="bg-white p-6 rounded-lg border">
                  <h2 class="text-xl font-semibold mb-4 text-slate-900">Instrument Details</h2>
                  <p class="text-slate-700 leading-relaxed">
                    The Gas Chromatograph-Mass Spectrometer (GC-MS) is a powerful
                    analytical tool that combines the features of gas chromatography
                    and mass spectrometry. It is used to identify different substances
                    within a test sample and is widely used in forensic science,
                    environmental analysis, and drug detection.
                  </p>
                  
                  <h3 class="text-lg font-semibold mt-6 mb-3 text-slate-900">How It Works</h3>
                  <p class="text-slate-700 leading-relaxed">
                    GC-MS works by separating the chemical mixtures (the GC component) and then identifying 
                    the components at a molecular level (the MS component). The sample solution is injected 
                    into the GC inlet where it is vaporized and swept onto a chromatographic column by an inert carrier gas. 
                    The compounds in the mixture are separated based on their relative interaction with the coating 
                    of the column and the carrier gas. As compounds exit the GC column, they enter the MS where 
                    they are bombarded with electrons, causing them to fragment. These fragments are charged ions 
                    with a certain mass, and the mass spectrometer captures, ionizes, accelerates, deflects, and 
                    detects the ionized molecules. The computer then processes this data and generates results.
                  </p>
                </TabsContent>
                
                <TabsContent value="specifications" class="bg-white p-6 rounded-lg border">
                  <h2 class="text-xl font-semibold mb-4 text-slate-900">Technical Specifications</h2>
                  
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-x-6 gap-y-4">
                    <div>
                      <h3 class="text-lg font-medium mb-2 text-slate-900">Gas Chromatograph</h3>
                      <ul class="space-y-2">
                        <li class="flex items-start">
                          <span class="text-blue-600 font-medium mr-2">•</span>
                          <div>
                            <span class="font-medium">Model:</span> Agilent 7890B GC
                          </div>
                        </li>
                        <li class="flex items-start">
                          <span class="text-blue-600 font-medium mr-2">•</span>
                          <div>
                            <span class="font-medium">Oven Temperature Range:</span> Ambient +4°C to 450°C
                          </div>
                        </li>
                        <li class="flex items-start">
                          <span class="text-blue-600 font-medium mr-2">•</span>
                          <div>
                            <span class="font-medium">Heating Rate:</span> 120°C/min
                          </div>
                        </li>
                        <li class="flex items-start">
                          <span class="text-blue-600 font-medium mr-2">•</span>
                          <div>
                            <span class="font-medium">Autosampler:</span> 150 sample capacity
                          </div>
                        </li>
                      </ul>
                    </div>
                    
                    <div>
                      <h3 class="text-lg font-medium mb-2 text-slate-900">Mass Spectrometer</h3>
                      <ul class="space-y-2">
                        <li class="flex items-start">
                          <span class="text-blue-600 font-medium mr-2">•</span>
                          <div>
                            <span class="font-medium">Model:</span> Agilent 5977B MS
                          </div>
                        </li>
                        <li class="flex items-start">
                          <span class="text-blue-600 font-medium mr-2">•</span>
                          <div>
                            <span class="font-medium">Mass Range:</span> 1-1050 amu
                          </div>
                        </li>
                        <li class="flex items-start">
                          <span class="text-blue-600 font-medium mr-2">•</span>
                          <div>
                            <span class="font-medium">Scan Rate:</span> Up to 20,000 amu/second
                          </div>
                        </li>
                        <li class="flex items-start">
                          <span class="text-blue-600 font-medium mr-2">•</span>
                          <div>
                            <span class="font-medium">Ionization Source:</span> Electron Impact (EI)
                          </div>
                        </li>
                      </ul>
                    </div>
                  </div>
                  
                  <h3 class="text-lg font-medium mt-6 mb-2 text-slate-900">Software</h3>
                  <ul class="space-y-2">
                    <li class="flex items-start">
                      <span class="text-blue-600 font-medium mr-2">•</span>
                      <div>
                        <span class="font-medium">Data System:</span> Agilent MassHunter Workstation
                      </div>
                    </li>
                    <li class="flex items-start">
                      <span class="text-blue-600 font-medium mr-2">•</span>
                      <div>
                        <span class="font-medium">Libraries:</span> NIST, Wiley, and custom libraries
                      </div>
                    </li>
                  </ul>
                </TabsContent>
                
                <TabsContent value="applications" class="bg-white p-6 rounded-lg border">
                  <h2 class="text-xl font-semibold mb-4 text-slate-900">Applications</h2>
                  
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-blue-50 rounded-lg p-4">
                      <div class="flex items-center mb-3">
                        <Building class="h-5 w-5 text-blue-600 mr-2" />
                        <h3 class="font-medium text-lg text-slate-900">Industrial Applications</h3>
                      </div>
                      <ul class="space-y-2 text-slate-700">
                        <li class="flex items-start">
                          <span class="text-blue-600 mr-2">•</span>
                          Petrochemical analysis
                        </li>
                        <li class="flex items-start">
                          <span class="text-blue-600 mr-2">•</span>
                          Fragrance and flavor compound identification
                        </li>
                        <li class="flex items-start">
                          <span class="text-blue-600 mr-2">•</span>
                          Food and beverage quality control
                        </li>
                        <li class="flex items-start">
                          <span class="text-blue-600 mr-2">•</span>
                          Polymer additive analysis
                        </li>
                      </ul>
                    </div>
                    
                    <div class="bg-green-50 rounded-lg p-4">
                      <div class="flex items-center mb-3">
                        <BarChart4 class="h-5 w-5 text-green-600 mr-2" />
                        <h3 class="font-medium text-lg text-slate-900">Environmental Applications</h3>
                      </div>
                      <ul class="space-y-2 text-slate-700">
                        <li class="flex items-start">
                          <span class="text-green-600 mr-2">•</span>
                          Detection of pollutants in water, soil, and air
                        </li>
                        <li class="flex items-start">
                          <span class="text-green-600 mr-2">•</span>
                          Pesticide residue analysis
                        </li>
                        <li class="flex items-start">
                          <span class="text-green-600 mr-2">•</span>
                          Identification of volatile organic compounds (VOCs)
                        </li>
                        <li class="flex items-start">
                          <span class="text-green-600 mr-2">•</span>
                          Analysis of contaminants in groundwater
                        </li>
                      </ul>
                    </div>
                    
                    <div class="bg-purple-50 rounded-lg p-4">
                      <div class="flex items-center mb-3">
                        <Users class="h-5 w-5 text-purple-600 mr-2" />
                        <h3 class="font-medium text-lg text-slate-900">Clinical & Forensic Applications</h3>
                      </div>
                      <ul class="space-y-2 text-slate-700">
                        <li class="flex items-start">
                          <span class="text-purple-600 mr-2">•</span>
                          Drug testing and toxicology screening
                        </li>
                        <li class="flex items-start">
                          <span class="text-purple-600 mr-2">•</span>
                          Forensic analysis of evidence
                        </li>
                        <li class="flex items-start">
                          <span class="text-purple-600 mr-2">•</span>
                          Metabolomics and biomarker discovery
                        </li>
                        <li class="flex items-start">
                          <span class="text-purple-600 mr-2">•</span>
                          Analysis of biological samples
                        </li>
                      </ul>
                    </div>
                    
                    <div class="bg-amber-50 rounded-lg p-4">
                      <div class="flex items-center mb-3">
                        <FileText class="h-5 w-5 text-amber-600 mr-2" />
                        <h3 class="font-medium text-lg text-slate-900">Research Applications</h3>
                      </div>
                      <ul class="space-y-2 text-slate-700">
                        <li class="flex items-start">
                          <span class="text-amber-600 mr-2">•</span>
                          Identification of unknown compounds
                        </li>
                        <li class="flex items-start">
                          <span class="text-amber-600 mr-2">•</span>
                          Structural elucidation of organic molecules
                        </li>
                        <li class="flex items-start">
                          <span class="text-amber-600 mr-2">•</span>
                          Analysis of natural products
                        </li>
                        <li class="flex items-start">
                          <span class="text-amber-600 mr-2">•</span>
                          Method development and validation
                        </li>
                      </ul>
                    </div>
                  </div>
                </TabsContent>
                
                <TabsContent value="documents" class="bg-white p-6 rounded-lg border">
                  <h2 class="text-xl font-semibold mb-4 text-slate-900">Related Documents</h2>
                  
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <a href="#" class="flex items-center p-4 border border-blue-100 rounded-lg bg-blue-50 hover:bg-blue-100 transition-colors">
                      <div class="h-10 w-10 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 mr-3">
                        <FileText size={18} />
                      </div>
                      <div>
                        <p class="font-medium text-slate-900">GC-MS User Manual</p>
                        <p class="text-sm text-slate-500">PDF, 4.2 MB</p>
                      </div>
                    </a>
                    
                    <a href="#" class="flex items-center p-4 border border-blue-100 rounded-lg bg-blue-50 hover:bg-blue-100 transition-colors">
                      <div class="h-10 w-10 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 mr-3">
                        <FileText size={18} />
                      </div>
                      <div>
                        <p class="font-medium text-slate-900">Sample Preparation Guide</p>
                        <p class="text-sm text-slate-500">PDF, 2.8 MB</p>
                      </div>
                    </a>
                    
                    <a href="#" class="flex items-center p-4 border border-blue-100 rounded-lg bg-blue-50 hover:bg-blue-100 transition-colors">
                      <div class="h-10 w-10 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 mr-3">
                        <FileText size={18} />
                      </div>
                      <div>
                        <p class="font-medium text-slate-900">Data Analysis Protocol</p>
                        <p class="text-sm text-slate-500">PDF, 3.5 MB</p>
                      </div>
                    </a>
                    
                    <a href="#" class="flex items-center p-4 border border-blue-100 rounded-lg bg-blue-50 hover:bg-blue-100 transition-colors">
                      <div class="h-10 w-10 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 mr-3">
                        <FileText size={18} />
                      </div>
                      <div>
                        <p class="font-medium text-slate-900">Maintenance Guidelines</p>
                        <p class="text-sm text-slate-500">PDF, 1.7 MB</p>
                      </div>
                    </a>
                  </div>
                  
                  <div class="mt-6 bg-amber-50 border border-amber-100 rounded-lg p-4">
                    <h3 class="font-medium text-amber-800 mb-2">Request Additional Documents</h3>
                    <p class="text-amber-700 text-sm">
                      Additional technical documentation, application notes, and method development guides 
                      are available upon request. Please contact our staff for access.
                    </p>
                  </div>
                </TabsContent>
              </Tabs>
            </div>
          </Card>
          
          <!-- Related Instruments -->
          <div class="mt-8">
            <h2 class="text-xl font-bold text-slate-900 mb-4">Related Instruments</h2>
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
              {#each relatedInstruments as instrument}
                <Card class="overflow-hidden hover:shadow-md transition-shadow">
                  <div class="p-4">
                    <div class="flex items-center space-x-4">
                      <img src={instrument.image} alt={instrument.name} class="w-16 h-16 rounded-md object-cover" />
                      <div>
                        <h3 class="font-medium text-slate-900">{instrument.name}</h3>
                        <p class="text-sm text-slate-500">{instrument.category}</p>
                      </div>
                    </div>
                    <Button variant="outline" class="w-full mt-3 text-sm">View Details</Button>
                  </div>
                </Card>
              {/each}
            </div>
          </div>
        </div>
        
        <!-- Sidebar -->
        <div class="space-y-6">
          <!-- Booking Card -->
          <Card class="shadow-md overflow-hidden">
            <div class="bg-gradient-to-r from-blue-600 to-indigo-700 px-6 py-4">
              <h2 class="text-xl font-bold text-white">Booking Information</h2>
            </div>
            <div class="p-6">
              <div class="flex flex-col space-y-4 mb-4">
                <!-- Status -->
                <div class="flex items-center justify-between">
                  <span class="text-slate-600">Status:</span>
                  <Badge class="bg-green-100 text-green-800">Available</Badge>
                </div>
                
                <!-- Rate -->
                <div class="flex items-center justify-between">
                  <span class="text-slate-600">Hourly Rate:</span>
                  <div>
                    <span class="font-medium">฿2,000</span>
                    <span class="text-sm text-slate-500 ml-1">/ hour</span>
                  </div>
                </div>
                
                <!-- Usage Time -->
                <div class="flex items-center justify-between">
                  <span class="text-slate-600">Session Duration:</span>
                  <span class="font-medium">1-4 hours</span>
                </div>
              </div>
              
              <Separator class="my-4" />
              
              <p class="mb-4 text-slate-700">
                To use this instrument, please register and submit a booking request through our online system.
              </p>
              
              <div class="space-y-3">
                <Button class="w-full">Book Now</Button>
                <Button variant="outline" class="w-full">Request Training</Button>
              </div>
            </div>
          </Card>
          
          <!-- Maintenance Schedule -->
          <Card class="shadow-md">
            <div class="p-6">
              <h2 class="text-xl font-bold text-slate-900 mb-4">Maintenance Schedule</h2>
              
              {#if upcomingMaintenance.length > 0}
                <div class="bg-amber-50 border border-amber-200 rounded-lg p-4 mb-4">
                  <h3 class="font-medium text-amber-800 flex items-center">
                    <Clock class="h-4 w-4 mr-2" />
                    Upcoming Maintenance
                  </h3>
                  {#each upcomingMaintenance as maintenance}
                    <div class="mt-2 text-amber-700">
                      <p><span class="font-medium">Date:</span> {maintenance.date}</p>
                      <p><span class="font-medium">Duration:</span> {maintenance.duration}</p>
                    </div>
                  {/each}
                </div>
              {:else}
                <p class="text-slate-700">No maintenance currently scheduled for this instrument.</p>
              {/if}
              
              <div class="bg-blue-50 border border-blue-200 rounded-lg p-4">
                <h3 class="font-medium text-blue-800 mb-2">Regular Maintenance</h3>
                <p class="text-blue-700 text-sm">
                  This instrument undergoes regular monthly maintenance to ensure optimal performance.
                  Please check the calendar before booking.
                </p>
              </div>
            </div>
          </Card>
          
          <!-- Contact Card -->
          <Card class="shadow-md">
            <div class="p-6">
              <h2 class="text-xl font-bold text-slate-900 mb-4">Contact</h2>
              <p class="mb-4 text-slate-600">For inquiries about this instrument, please contact:</p>
              
              <div class="bg-slate-50 border border-slate-200 rounded-lg p-4">
                <p class="font-medium text-slate-900">Dr. Somchai Vichitsurachai</p>
                <p class="text-slate-600 mt-1">Instrument Specialist - Chromatography</p>
                <Separator class="my-3" />
                <div class="space-y-2 text-slate-700">
                  <p class="flex items-center">
                    <svg class="h-4 w-4 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
                    </svg>
                    somchai.v@kmitl.ac.th
                  </p>
                  <p class="flex items-center">
                    <svg class="h-4 w-4 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/>
                    </svg>
                    +66 2 329 8000 ext. 3456
                  </p>
                </div>
                <Button variant="outline" class="w-full mt-4 text-sm">Send Message</Button>
              </div>
            </div>
          </Card>
        </div>
      </div>
    </main>
    
    <!-- Footer -->
    </div>