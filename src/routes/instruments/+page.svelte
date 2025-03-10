<script lang="ts">
    import { onMount } from 'svelte';
    import { Button } from "$lib/components/ui/button";
    import { Input } from "$lib/components/ui/input";
    import { Card } from "$lib/components/ui/card";
    import { Separator } from "$lib/components/ui/separator";
    import { Search, Microscope, Dna, TestTube, Omega, Bolt, FilterIcon, X, Menu } from 'lucide-svelte';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';
    
    let searchQuery: string = "";
    let selectedCategory: string | null = null;
    let mobileMenuOpen: boolean = false;
    
    const categories = [
      { icon: Microscope, name: 'Sample preparation equipment', description: 'PCR, Microscopes, Cell Counters' },
      { icon: Dna, name: 'Biological test', description: 'Centrifuges, Incubators, Balances' },
      { icon: TestTube, name: 'Applied chemical instrument', description: 'Homogenizers, Extractors, Filters' },
      { icon: Bolt, name: 'General equipment', description: 'HPLC, GC, Elemental Analyzers' },
      { icon: Omega, name: 'Physical and structural characterization', description: 'HPLC, GC, Elemental Analyzers' }
    ];
    
    const instruments = [
      { 
        name: 'Scanning Electron Microscope', 
        model: 'JEOL JSM-7800F', 
        category: 'Physical and structural characterization',
        availability: 'Available', 
        description: 'High-resolution microscope using electron beams to create detailed surface images with magnification up to 300,000x.',
        image: "/api/placeholder/300/200" 
      },
      { 
        name: 'FTIR Spectrometer', 
        model: 'Bruker Tensor II', 
        category: 'Physical and structural characterization',
        availability: 'Maintenance', 
        description: 'Identifies chemical bonds in molecules by analyzing infrared absorption spectrum. Suitable for organic and inorganic compound analysis.',
        image: "/api/placeholder/300/200" 
      },
      { 
        name: 'Ultra-High Performance LC', 
        model: 'Agilent 1290 Infinity II', 
        category: 'Applied chemical instrument',
        availability: 'Available', 
        description: 'Advanced liquid chromatography system for separating, identifying, and quantifying components in complex mixtures.',
        image: "/api/placeholder/300/200" 
      },
      { 
        name: 'PCR Thermal Cycler', 
        model: 'Bio-Rad T100', 
        category: 'Sample preparation equipment',
        availability: 'Available', 
        description: 'Amplifies DNA segments through repeated heating and cooling cycles for genetic analysis.',
        image: "/api/placeholder/300/200" 
      },
      { 
        name: 'Microplate Reader', 
        model: 'BioTek Synergy HTX', 
        category: 'Biological test',
        availability: 'Available', 
        description: 'Multi-mode detection system for microplate assays including absorbance, fluorescence, and luminescence measurements.',
        image: "/api/placeholder/300/200" 
      },
      { 
        name: 'Differential Scanning Calorimeter', 
        model: 'TA Instruments DSC 250', 
        category: 'Applied chemical instrument',
        availability: 'Available', 
        description: 'Measures heat flow changes in samples for thermal analysis of phase transitions and chemical reactions.',
        image: "/api/placeholder/300/200" 
      },
      { 
        name: 'Analytical Balance', 
        model: 'Mettler Toledo XPR', 
        category: 'General equipment',
        availability: 'Available', 
        description: 'High-precision weighing instrument with readability to 0.01mg for accurate sample preparation.',
        image: "/api/placeholder/300/200" 
      },
      { 
        name: 'X-Ray Diffractometer', 
        model: 'Rigaku MiniFlex 600', 
        category: 'Physical and structural characterization',
        availability: 'Maintenance', 
        description: 'Determines crystal structures by measuring diffraction patterns of X-rays interacting with crystalline samples.',
        image: "/api/placeholder/300/200" 
      }
    ];
    
    $: filteredInstruments = instruments.filter(instrument => {
      const matchesSearch = searchQuery === "" || 
        instrument.name.toLowerCase().includes(searchQuery.toLowerCase()) ||
        instrument.model.toLowerCase().includes(searchQuery.toLowerCase()) ||
        instrument.description.toLowerCase().includes(searchQuery.toLowerCase());
      
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
    
    function toggleMobileMenu() {
      mobileMenuOpen = !mobileMenuOpen;
    }
  </script>
  
  <!-- Main Layout -->
  <div class="min-h-screen bg-slate-50 font-sans flex flex-col">
    <!-- Header with modern navigation -->
    <Header />
  
    <main>
      <!-- Page Title & Search -->
      <section class="py-8 md:py-12 bg-gradient-to-br from-blue-50 to-indigo-100">
        <div class="container mx-auto px-4">
          <h2 class="text-2xl md:text-3xl font-bold mb-3 text-slate-900">Scientific Instruments</h2>
          <p class="text-slate-600 mb-6 max-w-3xl">
            Browse our comprehensive collection of scientific instruments available for researchers, academics, and industry professionals.
          </p>
          
          <div class="flex flex-col sm:flex-row gap-4 items-start">
            <div class="relative w-full sm:w-64">
              <div class="relative flex w-full items-center">
                <Input 
                  type="text" 
                  bind:value={searchQuery} 
                  placeholder="Search instruments..." 
                  class="pr-10 h-12"
                />
                <div class="absolute right-3 text-slate-400">
                  <Search class="h-5 w-5" />
                </div>
              </div>
            </div>
            
            {#if selectedCategory !== null || searchQuery !== ""}
              <Button variant="outline" size="sm" on:click={clearFilters} class="flex items-center px-3">
                <X class="mr-2 h-4 w-4" />
                <span>Clear filters</span>
              </Button>
            {/if}
          </div>
        </div>
      </section>
      
      <!-- Main Content with Filters and Instruments -->
      <section class="py-8 md:py-12 bg-white">
        <div class="container mx-auto px-4">
          <!-- Mobile Category Filter Chips -->
          <div class="lg:hidden mb-6 overflow-x-auto pb-2">
            <div class="flex space-x-2">
              {#each categories as category}
                <Button 
                  variant={selectedCategory === category.name ? "default" : "outline"} 
                  size="sm"
                  class="whitespace-nowrap"
                  on:click={() => selectCategory(category.name)}
                >
                  <svelte:component this={category.icon} class="mr-2 h-4 w-4" />
                  <span>{category.name}</span>
                </Button>
              {/each}
            </div>
          </div>
          
          <div class="flex flex-col lg:flex-row gap-6 md:gap-8">
            <!-- Desktop Category Sidebar -->
            <div class="hidden lg:block w-64 flex-shrink-0">
              <div class="bg-slate-50 rounded-lg p-5 sticky top-24">
                <div class="flex items-center mb-4">
                  <FilterIcon class="w-5 h-5 mr-2 text-blue-600" />
                  <h3 class="font-bold text-lg">Categories</h3>
                </div>
                
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
              </div>
            </div>
            
            <!-- Instruments Grid -->
            <div class="flex-1">
              <!-- Results count -->
              <div class="mb-4">
                <p class="text-slate-500">
                  {filteredInstruments.length} 
                  {filteredInstruments.length === 1 ? 'instrument' : 'instruments'} found
                  {selectedCategory ? `in ${selectedCategory}` : ''}
                </p>
              </div>
              
              {#if filteredInstruments.length === 0}
                <div class="text-center py-16 bg-slate-50 rounded-lg">
                  <div class="text-5xl mb-4">🔍</div>
                  <h3 class="text-xl font-bold mb-2">No instruments found</h3>
                  <p class="text-slate-500 mb-4">Try adjusting your search or filter criteria</p>
                  <Button variant="outline" on:click={clearFilters}>Clear all filters</Button>
                </div>
              {:else}
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-2 xl:grid-cols-3 gap-6">
                  {#each filteredInstruments as instrument}
                    <Card class="overflow-hidden h-full flex flex-col hover:shadow-md transition-shadow">
                      <div class="relative">
                        <img src={instrument.image} alt={instrument.name} class="w-full h-48 object-cover" />
                        <div class="absolute top-3 right-3">
                          <span class={`px-3 py-1 rounded-full text-xs font-medium ${instrument.availability === 'Available' ? 'bg-green-100 text-green-800' : 'bg-amber-100 text-amber-800'}`}>
                            {instrument.availability}
                          </span>
                        </div>
                      </div>
                      <div class="p-5 flex-1 flex flex-col">
                        <div class="mb-2">
                          <div class="text-xs text-blue-600 font-medium mb-1">{instrument.category}</div>
                          <h3 class="font-bold text-lg mb-1">{instrument.name}</h3>
                          <p class="text-slate-500 text-sm">Model: {instrument.model}</p>
                        </div>
                        <p class="text-slate-600 text-sm mb-4 flex-1">{instrument.description}</p>
                        <div class="mt-auto">
                          <Button class="w-full">View Details</Button>
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
      
      <!-- Request Service Section -->

    </main>
  
    <!-- Footer -->
    <Footer />
  </div>